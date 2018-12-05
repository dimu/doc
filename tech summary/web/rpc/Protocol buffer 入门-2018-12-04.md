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