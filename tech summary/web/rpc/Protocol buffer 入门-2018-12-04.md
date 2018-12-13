## 一、Protocol buffers简述

### 特点

Protocol buffers are a language-neutral, platform-neutral extensible mechanism for serializing structured data.

- 语言中立，平台中立
- 序列化结构化数据

### protocol核心学习点

- protocol buffer 语法[https://developers.google.com/protocol-buffers/docs/proto](https://developers.google.com/protocol-buffers/docs/proto "protocol buffer语法")
- proto3语法[https://developers.google.com/protocol-buffers/docs/proto3](https://developers.google.com/protocol-buffers/docs/proto3 "proto3语法")
- buffer如何进行序列化以及反序列化[https://developers.google.com/protocol-buffers/docs/encoding](https://developers.google.com/protocol-buffers/docs/encoding "protocol buffer encode")

### 优势

- simpler（简单）
- smaller（文件小）
- faster（序列化与反序列化速度快）
- 支持多种语言，相对于xml更易于程序处理

主要是由于采用protocol方式生成的binary format文件相比于xml格式的更小，序列化，反序列化，网络传输过程中有更大优势。

### 历史演变主要解决的问题

- 协议不同版本的字段变换时带来的兼容性问题
- 协议能够带来了更好的自描述，能够被不同语言处理

### 演变历程

- 自动产生序列化与反序列化代码-》**如何使用？**
- 利用protocol buffer自描述能力，用于大数据存储-》**如何存储，效率问题如何？**
- 能够使用编译器能够自动生成服务端stub程序-》**如何生成？**

## 二、Proto3 buffer语法格式

暂时跳过proto2的语法格式

### 2.1 Defining A Message Type

如何在proto文件中定义一个消息类型？

    syntax = "proto3"

	message request {
		string name = 1；
		string age=2；
		int32 page_numer = 3；
		int32 result_per_page = 4;
	}

proto messge主要有field types, field name以及field number构成。

其中field number **【1-15】区间占用One Byte，【16-2047】占用两个bytes**，所以在message中fields个数不多的情况，尽量使用1-15之内的数值。

field number允许的值范围为【1-2的29次方-1（536870911）】，其中【19000-19999】为保留数值。

**Adding Comments**

proto use c/c++ style comments, //for line comments, /*...*/for block comment

**Reserved Fields**

	message ReservedTest{
		reserved 2, 6, 10 to max;
		reserved "name", "age";
	}

**Note:**不能在同一行混用field name与number，必须分开保留。

### 2.2 编译proto文件

对于一个初学者来说，刚开始肯定会拿到一个proto文件，拿到此文件后如何下手？大致步骤如下：

1. 安装编译环境，protocol buffer compiler能够根据不同的客户端语言，生成对应的代码,规则如下
	
	For C++, the compiler generates a .h and .cc file from each .proto, with a class for each message type described in your file.<br/>
	For Java, the compiler generates a .java file with a class for each message type, as well as a special Builder classes for creating message class instances.<br/>
	Python is a little different – the Python compiler generates a module with a static descriptor of each message type in your .proto, which is then used with a metaclass to create the necessary Python data access class at runtime.<br/>
	For Go, the compiler generates a .pb.go file with a type for each message type in your file.<br/>
	For Ruby, the compiler generates a .rb file with a Ruby module containing your message types.<br/>
	For Objective-C, the compiler generates a pbobjc.h and pbobjc.m file from each .proto, with a class for each message type described in your file.<br/>
	For C#, the compiler generates a .cs file from each .proto, with a class for each message type described in your file.<br/>
	For Dart, the compiler generates a .pb.dart file with a class for each message type in your file

2. 运行编译指令

### 2.3 Scalar Value Types

描述protocol文件的field types如何与其他不同语言的数据类型进行一一映射。

具体映射关系参考[protocol数据类型映射表](https://developers.google.com/protocol-buffers/docs/proto3#scalar "protocol数据类型映射表")

protocol中定义的数据类型:

**double，float，int32，int64，uint32, uint64, sint32, sint64, fixed32, fixed64, sfixed32, sfixed64, bool, string, bytes**

对于不同数据类型，不同操作数据类型，在数据序列化与反序列化的时候，会对不同数据类型进行一定的优化。

### 2.4 Default values

在message被反序列化的时候，如果缺少特定field的描述，反序列化时就会设置对应的默认值，规则如下：

- For strings, the default value is the empty string.—空字符串
- For bytes, the default value is empty bytes.—空字节
- For bools, the default value is false.-错
- For numeric types, the default value is zero.-0
- For enums, **the default value is the first defined enum value, which must be 0**.-联合第一个值必须为0
- For message fields, the field is not set. Its exact value is language-dependent. See the generated code guide for details.

### 2.5 Enumerations

联合是protocol中相对复杂的type，例如

	message request {
		string name = 1;
		int age = 2;
		enum Sex {
			MALE = 0;
			FEMALE = 1;
			OTHER = 2
		}
		Sex gender = 3;
	}


在protocol中对enum的第一个元素作了特别的规定，必须为值为0，主要是为了解决enum的默认值问题以及兼容proto2协议。

**联合字段别名**

示例：

	message request {
		string name = 1;
		int age = 2;
		enum Sex {
			option allow_alias = true;
			MALE = 0;
			FEMALE = 1;
			MAN = 1；
			OTHER = 2
		}
		Sex gender = 3;
	}

允许联合字段别名在Java或者C语言中比较少见，protocol默认也不允许开启联合别名，如果要开启必须通过手动打开配置选项

### 2.6 Using Other Message Types

protocol文件之间如何相互引用已经定义好的Message？如何通过Message嵌套引用形成消息结构层次？

示例：

	message Response {
		int http_code = 1;
		string ret_msg = 2;
		repeated Device data = 3;
	}

	message Result {
		string device_uuid = 1;
		string device_name = 2;
		float longitude = 3;
		float latitude = 4;
	}

一般来说，在实际的代码开发过程中，尽量将Message颗粒度进行拆分，便于在项目中相互调用。

**importing definitions**

protocol也支持导入其他proto文件，通过proto文件导入方式，能够通过合并导入proto文件形成新的proto文件，可以对不通版本，用户暴露不一样的proto文件。

### 2.7 Unknown Fields

