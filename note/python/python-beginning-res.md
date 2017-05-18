      # python res note #

## Syntax and semantics ##

### Indentation ###
空格缩进取代大括号，代码显得非常简洁，代码的层级关系通过空格缩进来体现。

### naming conventions ###
命名约定：

- 类名第一个字母大写，其他标识符第一个字符全部小写
- 以一个_开始的为私有变量
- 以两个_开始为强私有变量
- 以两个_结尾的为系统特定名字

### Reserved Words ###
保留字：
**and exec not as finally or assert for pass break from print class global raise continue if return def import try del in while elif is with else lambda yield except**

### quotation ###

python接收单引号，双引号，三引号，都是用来表示字符串
   
	word = 'word'
	sentence = "This is a sentence."
	paragraph = """This is a paragraph"""

### comments ###

注释：暂时只有单行注释，可以单独注释或者注释在末尾
    
    #first comment
	x = 'hello'  #second comment

### input ###

跟C中类似

    import sys

	x = input("input the file name\n")
	print(x)

	file = open(x, 'w')
	print(file)

输入文件路径后，得到的运行结果为
    
	input the file name
	d:\\testg.gz
	d:\\testg.gz
	<_io.TextIOWrapper name='d:\\\\testg.gz' mode='w' encoding='cp936'>

### suite ###

suite:块，在class，def，if，while等后面，以关键字开始，：结尾标志一个块
    
    if 0 == '0':
    	print("is true")
	else : #end with ：
    	print("is false")

### standard data type ###

#### Numers ####

Numbers分为支持三种数据格式数据：

	- int类型（signed integers） *10,-786,080*
	- float(floating point real values) *11.10 32.3+e18*
	- complex(complex numbers)  *3.14j*

#### String ####

string操作类型有如下 

    str = 'Hello World!'

	print (str)          # 整个字符串
	print (str[0])       # 返回字符串的第1个元素
	print (str[2:4])     # 返回字符串的第3个到第4个元素
	print (str[2:])      # 返回字符串的第3个到最后的元素
	print (str * 2)      # Prints string two times
	print (str + "TEST") # Prints concatenated string


#### List ####

list类似于c语言的数组，但是list元素可以是不同类型的，list操作跟string操作基本一致

list的基本操作如下

    list = [ 'abcd', 786 , 2.23, 'john', 70.2 ]
	tinylist = [123, 'john']

	print (list)          # Prints complete list
	print (list[0])       # Prints first element of the list
	print (list[1:3])     # Prints elements starting from 2nd till 3rd 
	print (list[2:])      # Prints elements starting from 3rd element
	print (tinylist * 2)  # Prints list two times
	print (list + tinylist) # Prints concatenated lists

#### tuple ####

元组除了使用语法跟list不一样外，还有个重要特性只读，不能修改，可以看做是只读的list。

tuple的基本操作如下：

    tuple = ( 'abcd', 786 , 2.23, 'john', 70.2  )
	tinytuple = (123, 'john')

	print (tuple)           # Prints complete tuple
	print (tuple[0])        # Prints first element of the tuple
	print (tuple[1:3])      # Prints elements starting from 2nd till 3rd 
	print (tuple[2:])       # Prints elements starting from 3rd element
	print (tinytuple * 2)   # Prints tuple two times
	print (tuple + tinytuple) # Prints concatenated tuple

#### dictionary ####

字典类型的跟map的key/value键值对比较一致，

dictionary的基本操作：

    dict = {}
	dict['one'] = "This is one"
	dict[2]     = "This is two"

	tinydict = {'name': 'john','code':6734, 'dept': 'sales'}


	print (dict['one'])       # Prints value for 'one' key
	print (dict[2])           # Prints value for 2 key
	print (tinydict)          # Prints complete dictionary
	print (tinydict.keys())   # Prints all the keys
	print (tinydict.values()) # Prints all the values

### data type conversion ###

类型转换，python的类型转换很简单，直接用类型作为方法名，传参即可。

#### int（x [, base]） ####

    x = int("123")
	print(x)

#### float ####

	x = float("123")
	print(x)

#### complex(real [,image])

	x = complex(2,3)
	print(x)
    实部为2，虚部为3的复数

#### ####

## operators ##

操作符分为：

1. 