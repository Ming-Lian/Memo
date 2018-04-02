<a name="content">目录</a>

[python入门笔记](#title)
- [python基础语法](#basic-grammer)
	- [python保留字](#basic-reserved-word)
	- [注释](#basic-annotation)
	- [行与缩进](#basic-indentation)
	- [字符串(String)](#basic-string)
	- [等待用户输入](#basic-get-input)
	- [多个语句构成代码组](#basic-code-group)
	- [Print 输出](#basic-print)
	- [import 与 from...import](#basic-import)
- [基本数据类型](#type-of-data)
	- [多个变量赋值](#assignment-for-multivariable)
	- [Number（数字）](#number)
	- [String（字符串）](#string)
	- [List（列表）](#list)
	- [Tuple（元组）](#tuple)
	- [Set（集合）](#set)
	- [Dictionary（字典）](#dictionary)
- [运算符](#operator)
	- [算术运算符](#arithmetic-operators)
	- [位运算符](#bit-operators)
	- [逻辑运算符](#logistic-operators)
	- [成员运算符](#memeber-operators)
	- [身份运算符](#id-operators)
- [数字(Number)](#number-detail)
- [字符串](#string-detail)
	- [字符串格式化](#str-format)
	- [三引号](#triple-quotes)
	- [字符串内建函数](#str-function-inbuild)
- [列表](#list-detail)
	- [Python列表函数&方法](#list-function)
- [元组](#tuple-detail)
- [字典](#dictionary-detail)
	- [删除字典元素](#dictionary-delect-element)
	- [字典键的特性](#dictionary-character)
	- [内置函数与方法](#dictionary-function-inbuild)
	- [遍历技巧](#dictionary-traverse)
- [条件控制](#conditional-control)
- [循环语句](#loop)
	- [while循环](#while)
	- [for循环](#for)
	- [循环通用部分](#loop-general)
- [迭代器与生成器](#iteration-generator)
- [函数](#function)
	- [参数传递](#parameter-transmission)
	- [参数](#parameter)
	- [匿名函数](#lambda)
	- [变量作用域](#variable-scope)
	- [用global 和 nonlocal改变变量作用域](#change-variable-scope)
- [数据结构](#data-structure)
	- [将列表当做堆栈使用](#list-stack)
	- [将列表当作队列使用](#list-queue)
	- [列表推导式](#list-formula)
	- [遍历技巧](#traverse-skill)
- [模块](#module)
	- [导入模块](#import-module)
	- [深入模块](#understand-module)
	- [包](#package)
- [输入和输出](#input-output)
	- [格式化输出](#format-output)
		- [str()](#format-output-str)
		- [repr()](#format-output-repr)
		- [rjust()](#format-output-rjust)
		- [format()](#format-output-format)
	- [读取键盘输入](#get-input)
	- [文件读写](#file-rw)
		- [文件对象的方法](#file-method)
			- [read()](#file-method-read)
			- [readline()](#file-method-readline)
			- [readlines()](#file-method-readlines)
			- [迭代文件对象读取每行](#file-method-iterate-read)
			- [write()](#file-method-write)
			- [tell()](#file-method-tell)
			- [seek()](#file-method-seek)
			- [close()](#file-method-close)
	- [pickle 模块](#pickle-module)
- [OS 文件/目录方法](#os-file-path-method)
	- [os.access()](#os-access)
	- [os.chdir()](#os-chdir)
	- [os.chmod()](#os-chmod)
	- [os.chown()](#os-chown)
- [错误和异常](#error)
	- [异常处理](#deal-with-error)
	- [抛出异常](#raise-error)
	- [用户自定义异常](#customized-error)
- [面向对象](#object-oriented)
	- [类定义](#object-define)
	- [类对象操作](#object-operate)
	- [类的方法](#object-method)
	- [类的继承](#object-inherit)
	- [类属性与方法](#object-attrs-method)




<h1 name="title">python入门笔记</h1>

<p align="center"><img src=./picture/Beginning-python-logo.png width=800 /></p>

<a name="basic-grammer"><h3>python基础语法 [<sup>目录</sup>](#content)</h3></a>

<a name="basic-reserved-word"><h4>python保留字 [<sup>目录</sup>](#content)</h4></a>

保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字： 

```
>>>import keyword
>>>keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 
'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

<a name="basic-annotation"><h4>注释 [<sup>目录</sup>](#content)</h4></a>

多行注释可以用多个 # 号，还有 ''' 和 """：

```
#!/usr/bin/python3
# 第一个注释
# 第二个注释
'''
第三注释
第四注释
'''
"""
第五注释
第六注释
"""
print ("Hello, Python!") 
```

<a name="basic-indentation"><h4>行与缩进 [<sup>目录</sup>](#content)</h4></a>


python最具特色的就是使用缩进来表示代码块，不需要使用大括号 {} 。
 
缩进的空格数是可变的，但是同一个代码块的语句必须包含相同的缩进空格数

```
if True:
    print ("True")
else:
    print ("False")
```

<a name="basic-string"><h4>字符串(String) [<sup>目录</sup>](#content)</h4></a>

- 反斜杠可以用来转义，使用r可以让反斜杠不发生转义。。 如 r"this is a line with \n" 则\n会显示，并不是换行。
- 字符串可以用 + 运算符连接在一起，用 * 运算符重复。
- Python 中的字符串有两种索引方式，从左往右以 0 开始，从右往左以 -1 开始。
- 没有单独的字符类型，一个字符就是长度为 1 的字符串。
- 字符串的截取的语法格式如下：变量\[头下标:尾下标\]

字符串操作实例：

```
print(str)                 # 输出字符串
print(str[0:-1])           # 输出第一个到倒数第二个的所有字符
print(str[0])              # 输出字符串第一个字符
print(str[2:5])            # 输出从第三个开始到第五个的字符
print(str[2:])             # 输出从第三个开始的后的所有字符
print(str * 2)             # 输出字符串两次
print(str + '你好')        # 连接字符串
```

<a name="basic-get-input"><h4>等待用户输入 [<sup>目录</sup>](#content)</h4></a>

```
input("\n\n按下 enter 键后退出。")
```

<a name="code-group"><h4>多个语句构成代码组 [<sup>目录</sup>](#content)</h4></a>

缩进相同的一组语句构成一个代码块，我们称之代码组。

像if、while、def和class这样的复合语句，首行以关键字开始，以冒号( : )结束，该行之后的一行或多行代码构成代码组。

我们将首行及后面的代码组称为一个子句(clause)。

例如：

```
if expression : 
   suite
elif expression : 
   suite 
else : 
   suite
```

<a name="basic-print"><h4>Print 输出 [<sup>目录</sup>](#content)</h4></a>

print 默认输出是换行的，如果要实现不换行需要在变量末尾加上 end=""：

```
print( x, end=" " )
```

<a name="basic-import"><h4>import 与 from...import [<sup>目录</sup>](#content)</h4></a>

在 python 用 import 或者 from...import 来导入相应的模块。
> 将整个模块(somemodule)导入，格式为： `import somemodule`
>
> 从某个模块中导入某个函数,格式为： `from somemodule import somefunction`
>
> 从某个模块中导入多个函数,格式为： `from somemodule import firstfunc, secondfunc, thirdfunc`
>
> 将某个模块中的全部函数导入，格式为： `from somemodule import *`

<a name="type-of-data"><h3>Python3 基本数据类型 [<sup>目录</sup>](#content)</h3></a>

<a name="assignment-for-multivariable"><h4>多个变量赋值 [<sup>目录</sup>](#content)</h4></a>

Python允许你同时为多个变量赋值。例如：

```
a = b = c = 1
```

以上实例，创建一个整型对象，值为1，三个变量被分配到相同的内存空间上。 

您也可以为多个对象指定多个变量。例如：

```
a, b, c = 1, 2, "runoob"
```

以上实例，两个整型对象 1 和 2 的分配给变量 a 和 b，字符串对象 "runoob" 分配给变量 c。

<a name="number"><h4>Number（数字） [<sup>目录</sup>](#content)</h4></a>

Python3 支持 int、float、bool、complex（复数）。 

内置的 type() 函数可以用来查询变量所指的对象类型

此外还可以用 isinstance 来判断

isinstance 和 type 的区别在于：

- type()不会认为子类是一种父类类型。

- isinstance()会认为子类是一种父类类型。

<a name="string"><h4>String（字符串） [<sup>目录</sup>](#content)</h4></a>

字符串的截取的语法格式如下：

```
变量[头下标:尾下标]
```

索引值以 0 为开始值，-1 为从末尾的开始位置。

加号 (+) 是字符串的连接符， 星号 (\*) 表示复制当前字符串，紧跟的数字为复制的次数。

Python 使用反斜杠(\)转义特殊字符，如果你不想让反斜杠发生转义，可以在字符串前面添加一个 r，表示原始字符串

**与 C 字符串不同的是，Python 字符串不能被改变。向一个索引位置赋值，比如word[0] = 'm'会导致错误。**

<a name="list"><h4>List（列表） [<sup>目录</sup>](#content)</h4></a>


列表可以完成大多数集合类的数据结构实现。列表中元素的类型可以不相同，它支持数字，字符串甚至可以包含列表（所谓嵌套）。

列表是写在方括号(**[]**)之间、用逗号分隔开的元素列表。

```
list = [ 'abcd', 786 , 2.23, 'runoob', 70.2 ]
```

与Python字符串不一样的是，列表中的元素是可以改变的：

<a name="tuple"><h4>Tuple（元组） [<sup>目录</sup>](#content)</h4></a>

元组（tuple）与列表类似，不同之处在于元组的元素不能修改。元组写在小括号(())里，元素之间用逗号隔开。

```
tuple = ( 'abcd', 786 , 2.23, 'runoob', 70.2  )
tup3 = "a", "b", "c", "d";
```

可以把字符串看作一种特殊的元组

构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

```
tup1 = ()    # 空元组
tup2 = (20,) # 一个元素，需要在元素后添加逗号
```

<a name="set"><h4>Set（集合） [<sup>目录</sup>](#content)</h4></a>

定义：集合（set）是一个无序不重复元素的序列。

基本功能：进行成员关系测试和删除重复元素。

创建方法：可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。 

```
parame = {value01,value02,...}
或者
set(value)
```

操作实例：


```python
student = {'Tom', 'Jim', 'Mary', 'Tom', 'Jack', 'Rose'}

# 成员测试
if('Rose' in student) :
    print('Rose 在集合中')
else :
    print('Rose 不在集合中')
    
# 集合运算
a = set('abracadabra')
b = set('alacazam')
 
print(a)
 
print(a - b)     # a和b的差集
 
print(a | b)     # a和b的并集
 
print(a & b)     # a和b的交集
 
print(a ^ b)     # a和b中不同时存在的元素
```

    Rose 在集合中
    {'r', 'd', 'c', 'b', 'a'}
    {'r', 'b', 'd'}
    {'r', 'd', 'z', 'c', 'm', 'b', 'l', 'a'}
    {'a', 'c'}
    {'r', 'd', 'b', 'l', 'z', 'm'}
    
<a name="dictionary"><h4>Dictionary（字典） [<sup>目录</sup>](#content)</h4></a>

类似于perl中的hash变量，由键(key)和键值(value)组成键值对构成

创建方法：
> - 先用`dict = {}`创建空字典，然后对字典赋值：`dict['one'] = "1 - 菜鸟教程"`
> - 创建同时初始化：`tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}`
> - 用`dict()`函数构造：
> > - 形式一：`dict([('Runoob', 1), ('Google', 2), ('Taobao', 3)])`
> > - 形式二：`dict(Runoob=1, Google=2, Taobao=3)`

<a name="operator"><h3>Python3 运算符 [<sup>目录</sup>](#content)</h3></a>

<a name="arithmetic-operators"><h4>算术运算符 [<sup>目录</sup>](#content)</h4></a>

|	运算符	|	描述	|	实例	|
|:---|:---|:---|
|	+	|	加 - 两个对象相加	|	a + b 输出结果 31	|
|	-	|	减 - 得到负数或是一个数减去另一个数	|	a - b 输出结果 -11	|
|	*	|	乘 - 两个数相乘或是返回一个被重复若干次的字符串	|	a * b 输出结果 210	|
|	/	|	除 - x 除以 y	|	b / a 输出结果 2.1	|
|	%	|	取模 - 返回除法的余数	|	b % a 输出结果 1	|
|	**	|	幂 - 返回x的y次幂	|	a**b 为10的21次方	|
|	//	|	取整除 - 返回商的整数部分	|	9//2 输出结果 4 , 9.0//2.0 输出结果 4.0	|


<a name="bit-operators"><h4>位运算符 [<sup>目录</sup>](#content)</h4></a>

|	运算符	|	描述	|	实例	|
|:---|:---|:---|
|	&	|	按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0	|	(a & b) 输出结果 12 ，二进制解释： 0000 1100	|
|	\|	|	按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。	|	(a \| b) 输出结果 61 ，二进制解释： 0011 1101	|
|	^	|	按位异或运算符：当两对应的二进位相异时，结果为1	|	(a ^ b) 输出结果 49 ，二进制解释： 0011 0001	|
|	~	|	按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1。~x 类似于 -x-1	|	(~a ) 输出结果 -61 ，二进制解释： 1100 0011， 在一个有符号二进制数的补码形式。	|
|	<<	|	左移动运算符：运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。	|	a << 2 输出结果 240 ，二进制解释： 1111 0000	|
|	>>	|	右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数	|	a >> 2 输出结果 15 ，二进制解释： 0000 1111	|

<a name="logistic-operators"><h4>逻辑运算符 [<sup>目录</sup>](#content)</h4></a>

- and
- or
- not

<a name="memeber-operators"><h4>成员运算符 [<sup>目录</sup>](#content)</h4></a>

- in
- not in

<a name="id-operators"><h4>身份运算符 [<sup>目录</sup>](#content)</h4></a>

- is
- not is

is 与 == 区别：is 用于判断两个变量引用对象是否为同一个， == 用于判断引用变量的值是否相等。


<a name="number-detail"><h3>Python3 数字(Number) [<sup>目录</sup>](#content)</h3></a>

在交互模式中，最后被输出的表达式结果被赋值给变量 _ 。

```
>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)
113.06
```

<a name="string-detail"><h3>Python3 字符串 [<sup>目录</sup>](#content)</h3></a>

<a name="str-format"><h4>字符串格式化 [<sup>目录</sup>](#content)</h4></a>

Python 支持格式化字符串的输出，字符串格式化使用与 C 中 sprintf 函数一样的语法。

```
print ("我叫 %s 今年 %d 岁!" % ('小明', 10))
```

字符串格式化符号

|符号|描述|
|:---|:---|
|	%c	|	 格式化字符及其ASCII码	|
|	      %s 	|	 格式化字符串	|
|	      %d 	|	 格式化整数	|
|	      %u	|	 格式化无符号整型	|
|	      %o	|	 格式化无符号八进制数	|
|	      %x	|	 格式化无符号十六进制数	|
|	      %X	|	 格式化无符号十六进制数（大写）	|
|	      %f	|	 格式化浮点数字，可指定小数点后的精度	|
|	      %e	|	 用科学计数法格式化浮点数	|
|	      %E	|	 作用同%e，用科学计数法格式化浮点数	|
|	      %g	|	 %f和%e的简写	|
|	      %G	|	 %f 和 %E 的简写	|
|	      %p	|	 用十六进制数格式化变量的地址	|

格式化操作符辅助指令

|	符号	|	功能	|
|:---|:---|
|	*	|	定义宽度或者小数点精度	|
|	-	|	用做左对齐	|
|	+	|	在正数前面显示加号( + )	|
|	<sp>	|	在正数前面显示空格	|
|	#	|	在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X')	|
|	0	|	显示的数字前面填充'0'而不是默认的空格	|
|	%	|	'%%'输出一个单一的'%'	|
|	(var)	|	映射变量(字典参数)	|
|	m.n.	|	m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)	|

<a name="triple-quotes"><h4>三引号 [<sup>目录</sup>](#content)</h4></a>

三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符

```
para_str = """这是一个多行字符串的实例
多行字符串可以使用制表符
TAB ( \t )。
也可以使用换行符 [ \n ]。
"""
print (para_str)
```

输出结果

```
这是一个多行字符串的实例
多行字符串可以使用制表符
TAB (    )。
也可以使用换行符 [ 
 ]。
 ```
 
 三引号让程序员从引号和特殊字符串的泥潭里面解脱出来，自始至终保持一小块字符串的格式是所谓的WYSIWYG（**所见即所得**）格式的。
 
<a name="str-function-inbuild"><h4>字符串内建函数 [<sup>目录</sup>](#content)</h4></a>

|序号|	方法及描述	|
|:---|:---|
|	1	|	capitalize()	|
|	` `	|	将字符串的第一个字符转换为大写	|
|	2	|	center(width, fillchar)	|
|	` `	|	返回一个指定的宽度 width 居中的字符串，fillchar 为填充的字符，默认为空格。	|
|	3	|	count(str, beg= 0,end=len(string))	|
|	` `	|	返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数	|
|	4	|	bytes.decode(encoding="utf-8", errors="strict")	|
|	` `	|	Python3 中没有 decode 方法，但我们可以使用 bytes 对象的 decode() 方法来解码给定的 bytes 对象，这个 bytes 对象可以由 str.encode() 来编码返回。	|
|	5	|	encode(encoding='UTF-8',errors='strict')	|
|	` `	|	以 encoding 指定的编码格式编码字符串，如果出错默认报一个ValueError 的异常，除非 errors 指定的是'ignore'或者'replace'	|
|	6	|	endswith(suffix, beg=0, end=len(string))	|
|	` `	|	检查字符串是否以 obj 结束，如果beg 或者 end 指定则检查指定的范围内是否以 obj 结束，如果是，返回 True,否则返回 False.	|
|	7	|	expandtabs(tabsize=8)	|
|	` `	|	把字符串 string 中的 tab 符号转为空格，tab 符号默认的空格数是 8 。	|
|	8	|	find(str, beg=0 end=len(string))	|
|	` `	|	检测 str 是否包含在字符串中，如果指定范围 beg 和 end ，则检查是否包含在指定范围内，如果包含返回开始的索引值，否则返回-1	|
|	9	|	index(str, beg=0, end=len(string))	|
|	` `	|	跟find()方法一样，只不过如果str不在字符串中会报一个异常.	|
|	10	|	isalnum()	|
|	` `	|	如果字符串至少有一个字符并且所有字符都是字母或数字则返 回 True,否则返回 False	|
|	11	|	isalpha()	|
|	` `	|	如果字符串至少有一个字符并且所有字符都是字母则返回 True, 否则返回 False	|
|	12	|	isdigit()	|
|	` `	|	如果字符串只包含数字则返回 True 否则返回 False..	|
|	13	|	islower()	|
|	` `	|	如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False	|
|	14	|	isnumeric()	|
|	` `	|	如果字符串中只包含数字字符，则返回 True，否则返回 False	|
|	15	|	isspace()	|
|	` `	|	如果字符串中只包含空白，则返回 True，否则返回 False.	|
|	16	|	istitle()	|
|	` `	|	如果字符串是标题化的(见 title())则返回 True，否则返回 False	|
|	17	|	isupper()	|
|	` `	|	如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False	|
|	18	|	join(seq)	|
|	` `	|	以指定字符串作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串	|
|	19	|	len(string)	|
|	` `	|	返回字符串长度	|
|	20	|	ljust(width[, fillchar])	|
|	` `	|	返回一个原字符串左对齐,并使用 fillchar 填充至长度 width 的新字符串，fillchar 默认为空格。	|
|	21	|	lower()	|
|	` `	|	转换字符串中所有大写字符为小写.	|
|	22	|	lstrip()	|
|	` `	|	截掉字符串左边的空格或指定字符。	|
|	23	|	maketrans()	|
|	` `	|	创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。	|
|	24	|	max(str)	|
|	` `	|	返回字符串 str 中最大的字母。	|
|	25	|	min(str)	|
|	` `	|	返回字符串 str 中最小的字母。	|
|	26	|	replace(old, new [, max])	|
|	` `	|	把 将字符串中的 str1 替换成 str2,如果 max 指定，则替换不超过 max 次。	|
|	27	|	rfind(str, beg=0,end=len(string))	|
|	` `	|	类似于 find()函数，不过是从右边开始查找.	|
|	28	|	rindex( str, beg=0, end=len(string))	|
|	` `	|	类似于 index()，不过是从右边开始.	|
|	29	|	rjust(width,[, fillchar])	|
|	` `	|	返回一个原字符串右对齐,并使用fillchar(默认空格）填充至长度 width 的新字符串	|
|	30	|	rstrip()	|
|	` `	|	删除字符串字符串末尾的空格.	|
|	31	|	split(str="", num=string.count(str))	|
|	` `	|	num=string.count(str)) 以 str 为分隔符截取字符串，如果 num 有指定值，则num指定分割次数。	|
|	32	|	splitlines([keepends])	|
|	` `	|	按照行('\r', '\r\n', \n')分隔，返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如果为 True，则保留换行符。	|
|	33	|	startswith(str, beg=0,end=len(string))	|
|	` `	|	检查字符串是否是以 obj 开头，是则返回 True，否则返回 False。如果beg 和 end 指定值，则在指定范围内检查。	|
|	34	|	strip([chars])	|
|	` `	|	在字符串上执行 lstrip()和 rstrip()	|
|	35	|	swapcase()	|
|	` `	|	将字符串中大写转换为小写，小写转换为大写	|
|	36	|	title()	|
|	` `	|	返回"标题化"的字符串,就是说所有单词都是以大写开始，其余字母均为小写(见 istitle())	|
|	37	|	translate(table, deletechars="")	|
|	` `	|	根据 str 给出的表(包含 256 个字符)转换 string 的字符, 要过滤掉的字符放到 deletechars 参数中	|
|	38	|	upper()	|
|	` `	|	转换字符串中的小写字母为大写	|
|	39	|	zfill (width)	|
|	` `	|	返回长度为 width 的字符串，原字符串右对齐，前面填充0	|
|	40	|	isdecimal()	|
|	` `	|	检查字符串是否只包含十进制字符，如果是返回 true，否则返回 false。	|

<a name="list-detail"><h3>Python3 列表 [<sup>目录</sup>](#content)</h3></a>

<a name="list-function"><h4>Python列表函数&方法 [<sup>目录</sup>](#content)</h4></a>

函数

|	序号	|	函数	|
|:---|:---|
|	1	|	len(list)	|
|	` `	|	列表元素个数	|
|	2	|	max(list)	|
|	` `	|	返回列表元素最大值	|
|	3	|	min(list)	|
|	` `	|	返回列表元素最小值	|
|	4	|	list(seq)	|
|	` `	|	将元组转换为列表	|

方法:

|	序号	|	方法	|
|:---|:---|
|	1	|	list.append(obj)	|
|	` `	|	在列表末尾添加新的对象	|
|	2	|	list.count(obj)	|
|	` `	|	统计某个元素在列表中出现的次数	|
|	3	|	list.extend(seq)	|
|	` `	|	在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）	|
|	4	|	list.index(obj)	|
|	` `	|	从列表中找出某个值第一个匹配项的索引位置	|
|	5	|	list.insert(index, obj)	|
|	` `	|	将对象插入列表	|
|	6	|	list.pop(obj=list[-1])	|
|	` `	|	移除列表中的一个元素（默认最后一个元素），并且返回该元素的值	|
|	7	|	list.remove(obj)	|
|	` `	|	移除列表中某个值的第一个匹配项	|
|	8	|	list.reverse()	|
|	` `	|	反向列表中元素	|
|	9	|	list.sort([func])	|
|	` `	|	对原列表进行排序	|
|	10	|	list.clear()	|
|	` `	|	清空列表	|
|	11	|	list.copy()	|
|	` `	|	复制列表	|

copy()和直接=赋值的区别：

```
a=[0,1,2,3,4,5]
b=a
c=a.copy()

del a[1]  
'''
   各变量值为：
   a=[0, 2, 3, 4, 5]
   b=[0, 2, 3, 4, 5]
   c=[0, 1, 2, 3, 4, 5]
'''
```

可以看出，使用=直接赋值，是引用赋值，更改一个，另一个同样会变, 例子中的a,b改变两次都影响到了对方

copy() 则顾名思义，复制一个副本，原值和新复制的变量互不影响

<a name="tuple-detail"><h3>Python3 元组 [<sup>目录</sup>](#content)</h3></a>

元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可。

元组中只包含一个元素时，需要在元素后面添加逗号，否则括号会被当作运算符使用。

元组中的元素值是不允许修改的，但我们可以对元组进行连接组合。

元组中的元素值是不允许删除的，但我们可以使用del语句来删除整个元组。

<a name="dictionary-detail"><h3>Python3 字典 [<sup>目录</sup>](#content)</h3></a>

```
d = {key1 : value1, key2 : value2 }
```

字典的每个键值(key=>value)对用冒号(:)分割，每个对之间用逗号(,)分割，整个字典包括在花括号({})中

<a name="dictionary-delect-element"><h4>删除字典元素 [<sup>目录</sup>](#content)</h4></a>

```
del dict['Name'] # 删除键 'Name'
dict.clear()     # 清空字典
del dict         # 删除字典
```

<a name="dictionary-character"><h4>字典键的特性 [<sup>目录</sup>](#content)</h4></a>

1）不允许同一个键出现两次。创建时如果同一个键被赋值两次，后一个值会被记住

2）键必须不可变，所以可以用数字，字符串或元组充当，而用列表就不行

<a name="dictionary-function-inbuild"><h4>内置函数与方法 [<sup>目录</sup>](#content)</h4></a>

内置函数

|序号	|函数|描述|
|:---|:---|:---|
|1|	len(dict)|计算字典元素个数，即键的总数。|
|2|str(dict)|输出字典，以可打印的字符串表示。|
|3|type(variable)|返回输入的变量类型，如果变量是字典就返回字典类型。|

内置方法：

|序号|函数|描述|
|:---|:---|:---|
|1|radiansdict.clear()|删除字典内所有元素	|
|2|radiansdict.copy()|返回一个字典的浅复制	|
|3|radiansdict.fromkeys()|创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值|
|4|radiansdict.get(key, default=None)|返回指定键的值，如果值不在字典中返回default值|
|5|key in dict|如果键在字典dict里返回true，否则返回false|
|6|radiansdict.items()|以列表返回可遍历的(键, 值) 元组数组|
|7|radiansdict.keys()|以列表返回一个字典所有的键|
|8|radiansdict.setdefault(key, default=None)|和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default|
|9|radiansdict.update(dict2)|把字典dict2的键/值对更新到dict里|
|10|radiansdict.values()|以列表返回字典中的所有值	|
|11|pop(key[,default])|删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。|
|12|popitem()|随机返回并删除字典中的一对键和值(一般删除末尾对)。|

<a name="dictionary-traverse"><h4>遍历技巧 [<sup>目录</sup>](#content)</h4></a>

在字典中遍历时，关键字和对应的值可以使用 items() 方法同时解读出来： 

```
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...

# 输出
## gallahad the pure
## robin the brave
```


<a name="conditional-control"><h3>Python3 条件控制 [<sup>目录</sup>](#content)</h3></a>

if语句的一般形式

```

if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

<a name="loop"><h3>Python3 循环语句 [<sup>目录</sup>](#content)</h3></a>

<a name="while"><h4>while循环 [<sup>目录</sup>](#content)</h4></a>

while语句的一般形式：

```
while 判断条件：
	语句
```

在Python中没有do .. while循环。

你可以使用 CTRL+C 来退出当前的无限循环。

while 循环使用 else 语句：在 while … else 在条件语句为 false 时执行 else 的语句块

如果你的while循环体中只有一条语句，你可以将该语句与while写在同一行中， 如下所示：

```
while (flag): print ('欢迎访问菜鸟教程!')
```

<a name="for"><h4>for循环 [<sup>目录</sup>](#content)</h4></a>

for循环可以遍历任何序列的项目，如一个列表或者一个字符串。

for循环的一般格式如下：

```
for <variable> in <sequence>:
	<statements>
else:
	<statements>
```

在for循环体中使用 break 语句，可以跳出当前循环体：

```
sites = ["Baidu", "Google","Runoob","Taobao"]
for site in sites:
	if site == "Runoob":
		print("菜鸟教程!")
		break
	print("循环数据 " + site)
else:
	print("没有循环数据!")
```

如果你需要遍历数字序列，可以使用内置range()函数。它会生成数列。可以使range以指定数字开始并指定不同的增量(甚至可以是负数，有时这也叫做'步长')

可以结合range()和len()函数以遍历一个序列的索引

```
>>> a = ['Google', 'Baidu', 'Runoob', 'Taobao', 'QQ']
>>> for i in range(len(a)):
		print(i, a[i])
```

<a name="loop-general"><h4>循环通用部分 [<sup>目录</sup>](#content)</h4></a>

> break 语句可以跳出 for 和 while 的循环体
>
> continue语句被用来告诉Python跳过当前循环块中的剩余语句，然后继续进行下一轮循环。

循环语句可以有 else 子句，它在穷尽列表(以for循环)或条件变为 false (以while循环)导致循环终止时被执行,但循环被break终止时不执行。

pass是空语句，是为了保持程序结构的完整性。pass 不做任何事情，一般用做占位语句。


<a name="iteration-generator"><h3>迭代器与生成器 [<sup>目录</sup>](#content)</h3></a>

- 迭代器

迭代器是一个可以记住遍历的位置的对象。

迭代器有两个基本的方法：iter() 和 next()。

- 生成器

在 Python 中，使用了 yield 的函数被称为生成器（generator）。

跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。

在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行 next() 方法时从当前位置继续运行。

调用一个生成器函数，返回的是一个迭代器对象。

```
import sys
 
def fibonacci(n): # 生成器函数 - 斐波那契
	a, b, counter = 0, 1, 0
	while True:
		if (counter > n): 
			return
		yield a
		a, b = b, a + b
		counter += 1
f = fibonacci(10) # f 是一个迭代器，由生成器返回生成
 
while True:
	try:
		print (next(f), end=" ")
	except StopIteration:
		sys.exit()
```

<a name="function"><h3>函数 [<sup>目录</sup>](#content)</h3></a>

Python 定义函数使用 def 关键字，一般格式如下：

```
def 函数名（参数列表）:
	函数体
```

默认情况下，参数值和参数名称是按函数声明中定义的的顺序匹配起来的。

<a name="parameter-transmission"><h4>参数传递 [<sup>目录</sup>](#content)</h4></a>

**可更改(mutable)与不可更改(immutable)对象**

在 python 中，strings, tuples, 和 numbers 是不可更改的对象，而 list,dict 等则是可以修改的对象。

> - 不可变类型：变量赋值 a=5 后再赋值 a=10，这里实际是新生成一个 int 值对象 10，再让 a 指向它，而 5 被丢弃，不是改变a的值，相当于新生成了a。
> 
> - 可变类型：变量赋值 la=[1,2,3,4] 后再赋值 la[2]=5 则是将 list la 的第三个元素值更改，本身la没有动，只是其内部的一部分值被修改了。

**python 函数的参数传递：**

> - 不可变类型：类似 c++ 的值传递，如 整数、字符串、元组。如fun（a），传递的只是a的值，没有影响a对象本身。比如在 fun（a）内部修改 a 的值，只是修改另一个复制的对象，不会影响 a 本身。

> - 可变类型：类似 c++ 的引用传递，如 列表，字典。如 fun（la），则是将 la 真正的传过去，修改后fun外部的la也会受影响
    
python 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。

- 传不可变对象实例

```
def ChangeInt( a ):
	a = 10

b = 2
ChangeInt(b)
print( b ) # 结果是 2
```

- 传可变对象实例

```
def changeme( mylist ):
	"修改传入的列表"
	mylist.append([1,2,3,4]);
	print ("函数内取值: ", mylist)
	return
 
# 调用changeme函数
mylist = [10,20,30];
changeme( mylist );
print ("函数外取值: ", mylist)

# 输出结果：
## 函数内取值:  [10, 20, 30, [1, 2, 3, 4]]
## 函数外取值:  [10, 20, 30, [1, 2, 3, 4]]
```

<a name="parameter"><h4>参数 [<sup>目录</sup>](#content)</h4></a>

- **必需参数**

必需参数须以正确的顺序传入函数。调用时的数量必须和声明时的一样。

- **关键字参数**

使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。

```
printme( str = "菜鸟教程");
```

- **默认参数**

调用函数时，如果没有传递参数，则会使用默认参数。

- **不定长参数**

你可能需要一个函数能处理比当初声明时更多的参数。这些参数叫做不定长参数，和上述2种参数不同，声明时不会命名。

基本语法如下：

```
def functionname([formal_args,] *var_args_tuple ):
	"函数_文档字符串"
	function_suite
	return [expression]
```

加了星号（*）的变量名会存放所有未命名的变量参数。如果在函数调用时没有指定参数，它就是一个空元组。

```
def printinfo( arg1, *vartuple ):
	"打印任何传入的参数"
	print ("输出: ")
	print (arg1)
	for var in vartuple:
		print (var)
	return;
 
# 调用printinfo 函数
printinfo( 10 );
printinfo( 70, 60, 50 );

# 输出结果
## 输出:
## 10
## 输出:
## 70
## 60
## 50
```

<a name="lambda"><h4>匿名函数 [<sup>目录</sup>](#content)</h4></a>

python 使用 lambda 来创建匿名函数。

lambda 函数的语法只包含一个语句，如下：

```
# func 为之后调用该函数时的函数名
func = lambda [arg1 [,arg2,.....argn]]:expression
```

所谓匿名，意即不再使用 def 语句这样标准的形式定义一个函数。

> - lambda 只是一个表达式，函数体比 def 简单很多。
> - lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
> - lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
> - 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

<a name="variable-scope"><h4>变量作用域 [<sup>目录</sup>](#content)</h4></a>

Python的作用域一共有4种，分别是：

> - L （Local） 局部作用域
> - E （Enclosing） 闭包函数外的函数中
> - G （Global） 全局作用域
> - B （Built-in） 内建作用域

```
x = int(2.9)  # 内建作用域
 
g_count = 0  # 全局作用域

def outer():
	o_count = 1  # 闭包函数外的函数中
	def inner():
		i_count = 2  # 局部作用域
```

以 L –> E –> G –>B 的规则查找，即：在局部找不到，便会去局部外的局部找（例如闭包），再找不到就会去全局找，再者去内建中找。

Python 中只有模块（module），类（class）以及函数（def、lambda）才会引入新的作用域，其它的代码块（如 if/elif/else/、try/except、for/while等）是不会引入新的作用域的，也就是说这些语句内定义的变量，外部也可以访问，如下代码：

```
# 实例中 msg 变量定义在 if 语句块中，但外部还是可以访问的

>>> if True:
...  msg = 'I am from Runoob'
... 
>>> msg
'I am from Runoob'
>>> 
```

<a name="change-variable-scope"><h4>用 global 和 nonlocal 改变变量作用域 [<sup>目录</sup>](#content)</h4></a>

当内部作用域想修改外部作用域的变量时，就要用到global和nonlocal关键字了。

- global：内部作用域想修改全局变量时使用

- nonlocal：内部作用域想修改嵌套作用域（enclosing 作用域，外层非全局作用域）中的变量则需要 nonlocal 关键字

<a name="data-structure"><h3>数据结构 [<sup>目录</sup>](#content)</h3></a>

<a name="list-stack"><h4>将列表当做堆栈使用 [<sup>目录</sup>](#content)</h4></a>

堆栈的特点：**后进先出**

- append() 方法可以把一个元素添加到堆栈顶
- pop() 方法可以把一个元素从堆栈顶释放出来

<a name="list-queue"><h4>将列表当做队列使用 [<sup>目录</sup>](#content)</h4></a>

队列的特点：**先进先出**

也可以把列表当做队列用，只是在队列里第一加入的元素，第一个取出来；但是拿列表用作这样的目的效率不高。在列表的最后添加或者弹出元素速度快，然而在列表里插入或者从头部弹出速度却不快（因为所有其他的元素都得一个一个地移动）。 

<a name="list-formula"><h4>列表推导式 [<sup>目录</sup>](#content)</h4></a>

列表推导式提供了从序列创建列表的简单途径。

```
>>> vec = [2, 4, 6]
>>> [3*x for x in vec]
[6, 12, 18]
```

通常应用程序将一些操作应用于某个序列的每个元素，用其获得的结果作为生成新列表的元素，或者根据确定的判定条件创建子序列。

用 if 子句作为过滤器：

```
>>> vec = [2, 4, 6]
>>> [3*x for x in vec if x > 3]
[12, 18]
>>> [3*x for x in vec if x < 2]
[]
```

<a name="traverse-skill"><h4>遍历技巧 [<sup>目录</sup>](#content)</h4></a>

- 字典遍历

在字典中遍历时，关键字和对应的值可以使用 items() 方法同时解读出来

- 列表遍历

在列表中遍历时，索引位置和对应值可以使用 enumerate() 函数同时得到：

```
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
...
0 tic
1 tac
2 toe
```

同时遍历两个或更多的序列，可以使用 zip() 组合： 

```
>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> for q, a in zip(questions, answers):
...     print('What is your {0}?  It is {1}.'.format(q, a))
...
What is your name?  It is lancelot.
What is your quest?  It is the holy grail.
What is your favorite color?  It is blue.
```



<a name="module"><h3>模块 [<sup>目录</sup>](#content)</h3></a>


模块是一个包含所有你定义的函数和变量的文件，其后缀名是.py。模块可以被别的程序引入，以使用该模块中的函数等功能。

<a name="import-module"><h4>导入模块 [<sup>目录</sup>](#content)</h4></a>

想使用 Python 源文件，只需在另一个源文件里执行 import 语句，语法如下：

```
import module1[, module2[,... moduleN]
```
或
```
# 模块内（函数，变量的）名称导入到当前操作模块
from modname import func1,func2
```

Python的模块搜索路径，被存储在sys模块中的path变量，搜索路径是由一系列目录名组成的，Python解释器会依次从这些目录中去寻找所引入的模块。 

```
>>> import sys
>>> sys.path
['', '/usr/lib/python3.4', '/usr/lib/python3.4/plat-x86_64-linux-gnu', '/usr/lib/python3.4/lib-dynload', '/usr/local/lib/python3.4/dist-packages', '/usr/lib/python3/dist-packages']
>>> 
```

sys.path 输出是一个列表，其中第一项是空串''，代表当前目录，也是搜索的第一个目录。所以**在当前目录下存在与要引入模块同名的文件，就会把要引入的模块屏蔽掉**。 

我们可以在脚本中修改sys.path来引入一些不在搜索路径中的模块。

import一个模块后使用模块中的函数的方法为：`模块名.函数名()`（modname.itemname）


每个模块有各自独立的符号表，在模块内部为所有的函数当作全局符号表来使用

<a name="understand-module"><h4>深入模块 [<sup>目录</sup>](#content)</h4></a>

- **模块之间变量的相互独立性**：每个模块有各自独立的符号表，在模块内部为所有的函数当作全局符号表来使用

- **模块是可以导入其他模块的**

- **\_\_name\_\_属性**

一个模块被另一个程序第一次引入时，其主程序将运行。如果我们想在模块被引入时，模块中的某一程序块不执行，我们可以用\_\_name\_\_属性来使该程序块仅在该模块自身运行时执行。

```
#!/usr/bin/python3
# Filename: using_name.py

if __name__ == '__main__':
   print('程序自身在运行')
else:
   print('我来自另一模块')
```
运行结果：
```
$ python using_name.py
程序自身在运行

$ python
>>> import using_name
我来自另一模块
>>>
```

每个模块都有一个\_\_name\_\_属性，当其值是 '\_\_main\_\_' 时，表明该模块自身在运行，否则是被引入。

- **内置的函数 dir() 可以找到模块内定义的所有名称**，以一个字符串列表的形式返回

```
>>> import fibo
>>> dir(fibo)
['__name__', 'fib', 'fib2']
```

如果没有给定参数，那么 dir() 函数会罗列出当前定义的所有名称

- **标准模块**

Python 本身带着一些标准的模块库。有些模块直接被构建在解析器里，这些虽然不是一些语言内置的功能，但是他却能很高效的使用，甚至是系统级调用也没问题。

有一个特别的模块 sys ，它内置在每一个 Python 解析器中。变量 sys.ps1 和 sys.ps2 定义了主提示符和副提示符所对应的字符串: 

```
>>> import sys
>>> sys.ps1
'>>> '
>>> sys.ps2
'... '
>>> sys.ps1 = 'C> '
C> print('Yuck!')
Yuck!
C>
```

<a name="package"><h4>包 [<sup>目录</sup>](#content)</h4></a>

简单来说，包就是多个实现相关功能的模块的组合。

一种可能的包结构（在分层的文件系统中）: 

```
sound/                          顶层包
      __init__.py               初始化 sound 包
      formats/                  文件格式转换子包
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  声音效果子包
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  filters 子包
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

目录只有包含一个叫做 \_\_init\_\_.py 的文件才会被认作是一个包，主要是为了避免一些滥俗的名字（比如叫做 string）不小心的影响搜索路径中的有效模块。即 \_\_init\_\_.py 文件是必须的。

<a name="input-output"><h3>输入和输出 [<sup>目录</sup>](#content)</h3></a>

<a name="format-output"><h4>格式化输出 [<sup>目录</sup>](#content)</h4></a>

<a name="format-output-str"><li>str()： 函数返回一个用户易读的表达形式。</li></a>

<a name="format-output-repr"><li>repr()： 产生一个解释器易读的表达形式</li></a>

repr() 函数可以转义字符串中的特殊字符

```
... hello = 'hello, runoob\n'
>>> hellos = repr(hello)
>>> print(hellos)
'hello, runoob\n'
```

repr() 的参数可以是 Python 的任何对象

```
>>> repr((x, y, ('Google', 'Runoob')))
"(32.5, 40000, ('Google', 'Runoob'))"
```

<a name="format-output-rjust"><li>rjust()：字符串对象的 rjust() 方法, 它可以将字符串靠右, 并在左边填充空格。</li></a>

还有类似的方法, 如 ljust() 和 center()。

另一个方法 zfill(), 它会在数字的左边填充 0

<a name="format-output-format"><li>str.format()</li></a> 

```
>>> print('{}网址： "{}!"'.format('菜鸟教程', 'www.runoob.com'))
菜鸟教程网址： "www.runoob.com!"
```

括号及其里面的字符 (称作格式化字段) 将会被 format() 中的参数替换。

在括号中的**数字**用于指向传入对象在 format() 中的位置，如下所示：

```
>>> print('{0} 和 {1}'.format('Google', 'Runoob'))
Google 和 Runoob
>>> print('{1} 和 {0}'.format('Google', 'Runoob'))
Runoob 和 Google
```

如果在 format() 中使用了**关键字参数**, 那么它们的值会指向使用该名字的参数。

```
>>> print('{name}网址： {site}'.format(name='菜鸟教程', site='www.runoob.com'))
菜鸟教程网址： www.runoob.com
```

位置及关键字参数可以任意的结合

'!a' (使用 ascii()), '!s' (使用 str()) 和 '!r' (使用 repr()) 可以用于在格式化某个值之前对其进行转化:

```
>>> import math
>>> print('常量 PI 的值近似为： {}。'.format(math.pi))
常量 PI 的值近似为： 3.141592653589793。
>>> print('常量 PI 的值近似为： {!r}。'.format(math.pi))
常量 PI 的值近似为： 3.141592653589793。
```

用':' 和格式标识符，对值进行更好的格式化方法：

> **小数点后保留**： `print('常量 PI 的值近似为 {0:.3f}。'.format(math.pi))`
> **设定输出值对应域长度**：
> ```
> >>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
> >>> for name, number in table.items():
> ...     print('{0:10} ==> {1:10d}'.format(name, number))
> ...
> Runoob     ==>          2
> Taobao     ==>          3
> Google     ==>          1
> ```
> - **传入一个字典, 然后使用方括号 '[]' 来访问键值** :
> ```
> >>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
> >>> print('Runoob: {0[Runoob]:d}; Google: {0[Google]:d}; Taobao: {0[Taobao]:d}'.format(table))
> Runoob: 2; Google: 1; Taobao: 3
> ```
> 也可以通过在 table 变量前使用 '**' 来实现相同的功能：
> ```
> >>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
> >>> print('Runoob: {Runoob:d}; Google: {Google:d}; Taobao: {Taobao:d}'.format(**table))
> Runoob: 2; Google: 1; Taobao: 3
> ```

<a name="get-input"><h4>读取键盘输入 [<sup>目录</sup>](#content)</h4></a>

input() 从标准输入读入一行文本，默认的标准输入是键盘

input 可以接收一个Python表达式作为输入，并将运算结果返回。 

<a name="file-rw"><h4>文件读写 [<sup>目录</sup>](#content)</h4></a>

```
open(filename, mode)
```

open() 将会返回一个 file 对象

> filename：要访问的文件名称
> mode：打开文件的模式：只读，写入，追加等

|	模式	|	描述	|
|:---:|:---|
|	r	|	以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。	|
|	rb	|	以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。	|
|	r+	|	打开一个文件用于读写。文件指针将会放在文件的开头。	|
|	rb+	|	以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。	|
|	w	|	打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。	|
|	wb	|	以二进制格式打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。	|
|	w+	|	打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。	|
|	wb+	|	以二进制格式打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。	|
|	a	|	打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。	|
|	ab	|	以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。	|
|	a+	|	打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。	|
|	ab+	|	以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。	|


<img src=./picture/Beginning-python-file-operate.png width=800 />

<a name="file-method"><h4>文件对象的方法 [<sup>目录</sup>](#content)</h4></a>

<a name="file-method-read"><li>f.read()</li></a>

调用 f.read(size), 这将读取一定数目的数据, 然后作为字符串或字节对象返回。

size 是一个可选的数字类型的参数。 当 size 被忽略了或者为负, 那么该文件的所有内容都将被读取并且返回。

<a name="file-method-readline"><li>f.readline()</li></a>

从文件中读取单独的一行

<a name="file-method-readlines"><li>f.readlines()</li></a>

返回该文件中包含的所有行。

如果设置可选参数 sizehint, 则读取指定长度的字节, 并且将这些字节按行分割。 

<a name="file-method-iterate-read"><li>迭代文件对象读取每行</li></a>

```
for line in f:
    print(line, end='')
```

<a name="file-method-write"><li>f.write()</li></a>

将 string 写入到文件中, 然后返回写入的字符数

如果要写入一些不是字符串的东西, 那么将需要先进行转换

<a name="file-method-tell"><li>f.tell()</li></a>

返回文件对象当前所处的位置, 它是从文件开头开始算起的字节数。 

<a name="file-method-seek"><li>f.seek()</li></a>

如果要改变文件当前的位置, 可以使用 f.seek(offset, from_what) 函数。

> - from_what 
> 如果是 0 表示开头, 如果是 1 表示当前位置, 2 表示文件的结尾
>> seek(x,0) ： 从起始位置即文件首行首字符开始移动 x 个字符
>> seek(x,1) ： 表示从当前位置往后移动x个字符
>> seek(-x,2)：表示从文件的结尾往前移动x个字符
> - offset
> 移动的步伐与方向，"+"向右，"-"向左

<a name="file-method-close"><li>f.close()</li></a>

当你处理完一个文件后, 调用 f.close() 来关闭文件并释放系统的资源

当处理一个文件对象时, 使用 with 关键字是非常好的方式。在结束后, 它会帮你正确的关闭文件

```
>>> with open('/tmp/foo.txt', 'r') as f:
...     read_data = f.read()
>>> f.closed
True
```

<a name="pickle-module"><h4>pickle 模块 </h4></a>

 python的pickle模块实现了基本的数据序列和反序列化。

通过pickle模块的序列化操作我们能够将程序中运行的对象信息保存到文件中去，永久存储。

通过pickle模块的反序列化操作，我们能够从文件中创建上一次程序保存的对象。

基本接口：

```
pickle.dump(obj, file, [,protocol])
```

 有了 pickle 这个对象, 就能对 file 以读取的形式打开:
 
```
x = pickle.load(file)
```

<a name="os-file-path-method"><h3>OS 文件/目录方法 [<sup>目录</sup>](#content)</h3></a>

os 模块提供了非常丰富的方法用来处理文件和目录

<a name="os-access"><li>os.access()</li></a>

检验权限模式

> - path -- 要用来检测是否有访问权限的路径。
> - mode
>> - os.F_OK: 作为access()的mode参数，测试path是否存在。
>> - os.R_OK: 包含在access()的mode参数中 ， 测试path是否可读。
>> - os.W_OK 包含在access()的mode参数中 ， 测试path是否可写。
>> - os.X_OK 包含在access()的mode参数中 ，测试path是否可执行。

<a name="os-chdir"><li>os.chdir()</li></a>

改变当前工作目录到指定的路径

返回值：如果允许访问返回 True , 否则返回False

<a name="os-chmod"><li>os.chmod()</li></a>

更改文件或目录的权限

chmod()方法语法格式如下：

```
os.chmod(path, mode)
```

mode的flags取值

> - stat.S_IXOTH: 其他用户有执行权0o001
> - stat.S_IWOTH: 其他用户有写权限0o002
> - stat.S_IROTH: 其他用户有读权限0o004
> - stat.S_IRWXO: 其他用户有全部权限(权限掩码)0o007
> - stat.S_IXGRP: 组用户有执行权限0o010
> - stat.S_IWGRP: 组用户有写权限0o020
> - stat.S_IRGRP: 组用户有读权限0o040
> - stat.S_IRWXG: 组用户有全部权限(权限掩码)0o070
> - stat.S_IXUSR: 拥有者具有执行权限0o100
> - stat.S_IWUSR: 拥有者具有写权限0o200
> - stat.S_IRUSR: 拥有者具有读权限0o400
> - stat.S_IRWXU: 拥有者有全部权限(权限掩码)0o700
> - stat.S_ISVTX: 目录里文件目录只有拥有者才可删除更改0o1000
> - stat.S_ISGID: 执行此文件其进程有效组为文件所在组0o2000
> - stat.S_ISUID: 执行此文件其进程有效用户为文件所有者0o4000
> - stat.S_IREAD: windows下设为只读
> - stat.S_IWRITE: windows下取消只读

<a name="os-chown"><li>os.chown()</li></a>

用于更改文件所有者，如果不修改可以设置为 -1, 你需要超级用户权限来执行权限修改操作。

<a name="error"><h3>错误和异常 [<sup>目录</sup>](#content)</h3></a>

<a name="deal-with-error"><h4>错误处理 [<sup>目录</sup>](#content)</h4></a>

```
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```

try语句按照如下方式工作；

> - 首先，执行try子句（在关键字try和关键字except之间的语句）
> - 如果没有异常发生，忽略except子句，try子句执行后结束。
> - 如果在执行try子句的过程中发生了异常，那么try子句余下的部分将被忽略。如果异常的类型和 except 之后的名称相符，那么对应的except子句将被执行。最后执行 try 语句之后的代码。
> - 如果一个异常没有与任何的except匹配，那么这个异常将会传递给上层的try中。


一个 try 语句可能包含多个except子句，分别来处理不同的特定的异常。最多只有一个分支会被执行。

一个except子句可以同时处理多个异常，这些异常将被放在一个括号里成为一个元组，例如: 

```
except (RuntimeError, TypeError, NameError):
	pass
```

最后一个except子句可以忽略异常的名称，它将被当作通配符使用。你可以使用这种方法打印一个错误信息，然后再次把异常抛出。

try except 语句还有一个可选的else子句，如果使用这个子句，那么必须放在所有的except子句之后。这个子句将在try子句没有发生任何异常的时候执行。例如: 

```
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except IOError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

<a name="raise-error"><h4>抛出异常 [<sup>目录</sup>](#content)</h4></a>

使用 raise 语句抛出一个指定的异常。例如:

```
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
NameError: HiThere
```

raise 唯一的一个参数指定了要被抛出的异常。它必须是一个异常的实例或者是异常的类（也就是 Exception 的子类）。

如果你只想知道这是否抛出了一个异常，并不想去处理它，那么一个简单的 raise 语句就可以再次把它抛出。

```
>>> try:
        raise NameError('HiThere')
    except NameError:
        print('An exception flew by!')
        raise
   
An exception flew by!
Traceback (most recent call last):
  File "<stdin>", line 2, in ?
NameError: HiThere
```

<a name="customized-error"><h4>用户自定义异常 [<sup>目录</sup>](#content)</h4></a>


你可以通过创建一个新的exception类来拥有自己的异常。异常应该继承自 Exception 类，或者直接继承，或者间接继承，例如:

```
>>> class MyError(Exception):
        def __init__(self, value):
            self.value = value
        def __str__(self):
            return repr(self.value)
   
>>> try:
        raise MyError(2*2)
    except MyError as e:
        print('My exception occurred, value:', e.value)
   
My exception occurred, value: 4
>>> raise MyError('oops!')
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
__main__.MyError: 'oops!'
```

当创建一个模块有可能抛出多种不同的异常时，一种通常的做法是为这个包建立一个基础异常类，然后基于这个基础类为不同的错误情况创建不同的子类:

```
# Error继承自基础异常类
class Error(Exception): 
    """Base class for exceptions in this module."""
    pass

# 再基于Erro创建子异常类
class InputError(Error):
    """Exception raised for errors in the input.

    Attributes:
        expression -- input expression in which the error occurred
        message -- explanation of the error
    """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message


class TransitionError(Error): 
    """Raised when an operation attempts a state transition that's not
    allowed.

    Attributes:
        previous -- state at beginning of transition
        next -- attempted new state
        message -- explanation of why the specific transition is not allowed
    """

    def __init__(self, previous, next, message):
        self.previous = previous
        self.next = next
        self.message = message
```

大多数的异常的名字都以"Error"结尾，就跟标准的异常命名一样。

<a name="object-oriented"><h3>面向对象 [<sup>目录</sup>](#content)</h3></a>

<a name="object-define"><h4>类定义 [<sup>目录</sup>](#content)</h4></a>

语法格式如下：

```
class ClassName:
    <statement-1>
    .
    .
    .
    <statement-N>
```

<a name="object-operate"><h4>类对象操作 [<sup>目录</sup>](#content)</h4></a>

类对象支持两种操作：属性引用和实例化。
> - **属性引用** 属性引用使用和 Python 中所有的属性引用一样的标准语法：obj.name
> - **实例化**  创建一个类的实例，类的具体对象

```
class MyClass:
    """一个简单的类实例"""
    i = 12345
    def f(self):
        return 'hello world'
 
# 实例化类
x = MyClass()
 
# 访问类的属性和方法
print("MyClass 类的属性 i 为：", x.i)
print("MyClass 类的方法 f 输出为：", x.f())
```

**将对象创建为有初始状态**

类可能会定义一个名为 \_\_init\_\_() 的特殊方法（构造方法），像下面这样：

```
def __init__(self):
    self.data = []
```

类定义了 \_\_init\_\_() 方法的话，类的实例化操作会自动调用 \_\_init\_\_() 方法。

```
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart
x = Complex(3.0, -4.5)
print(x.r, x.i)   # 输出结果：3.0 -4.5
```

当然， \_\_init\_\_() 方法可以有参数，参数通过 \_\_init\_\_() 传递到类的实例化操作上。

```
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart
x = Complex(3.0, -4.5)
print(x.r, x.i)   # 输出结果：3.0 -4.5
```

<a name="object-method"><h4>类的方法 [<sup>目录</sup>](#content)</h4></a>

在类地内部，使用 def 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 self, 且为第一个参数，self 代表的是类的实例。 

```
#类定义
class people:
    #定义基本属性
    name = ''
    age = 0
    #定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0
    #定义构造方法
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s 说: 我 %d 岁。" %(self.name,self.age))
 
# 实例化类
p = people('runoob',10,30)
p.speak()
```

<a name="object-inherit"><h4>类的继承 [<sup>目录</sup>](#content)</h4></a>

派生类的定义如下所示:

```
class DerivedClassName(BaseClassName1):
    <statement-1>
    .
    .
    .
    <statement-N>
```

单继承实例：

```
#类定义
class people:
    #定义基本属性
    name = ''
    age = 0
    #定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0
    #定义构造方法
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s 说: 我 %d 岁。" %(self.name,self.age))
 
#单继承示例
class student(people):
    grade = ''
    def __init__(self,n,a,w,g):
        #调用父类的构函
        people.__init__(self,n,a,w)
        self.grade = g
    #覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级"%(self.name,self.age,self.grade))
 
 
 
s = student('ken',10,60,3)
s.speak()
```

多继承实例：

```
#类定义
class people:
    #定义基本属性
    name = ''
    age = 0
    #定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0
    #定义构造方法
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s 说: 我 %d 岁。" %(self.name,self.age))

#另一个类，多重继承之前的准备
class speaker():
    topic = ''
    name = ''
    def __init__(self,n,t):
        self.name = n
        self.topic = t
    def speak(self):
        print("我叫 %s，我是一个演说家，我演讲的主题是 %s"%(self.name,self.topic))

#多重继承
class sample(speaker,student):
    a =''
    def __init__(self,n,a,w,g,t):
        student.__init__(self,n,a,w,g)
        speaker.__init__(self,n,t)
```

<a name="object-attrs-method"><h4>类属性与方法 [<sup>目录</sup>](#content)</h4></a>

**类的私有属性**

\_\_private_attrs：两个下划线开头，声明该属性为私有，不能在类地外部被使用或直接访问。在类内部的方法中使用时 self.__private_attrs。

**类的方法**

在类地内部，使用 def 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 self，且为第一个参数，self 代表的是类的实例。

self 的名字并不是规定死的，也可以使用 this，但是最好还是按照约定是用 self。

**类的私有方法**

\_\_private_method：两个下划线开头，声明该方法为私有方法，只能在类的内部调用 ，不能在类地外部调用。self.__private_methods。 

类的私有属性实例：

```
class JustCounter:
    __secretCount = 0  # 私有变量
    publicCount = 0    # 公开变量
 
    def count(self):
        self.__secretCount += 1
        self.publicCount += 1
        print (self.__secretCount)
 
counter = JustCounter()
counter.count()
counter.count()
print (counter.publicCount)
print (counter.__secretCount)  # 报错，实例不能访问私有变量
```

类的私有方法实例：

```
class Site:
    def __init__(self, name, url):
        self.name = name       # public
        self.__url = url   # private
 
    def who(self):
        print('name  : ', self.name)
        print('url : ', self.__url)
 
    def __foo(self):          # 私有方法
        print('这是私有方法')
 
    def foo(self):            # 公共方法
        print('这是公共方法')
        self.__foo()
 
x = Site('菜鸟教程', 'www.runoob.com')
x.who()        # 正常输出
x.foo()        # 正常输出
x.__foo()      # 报错
```
