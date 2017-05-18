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