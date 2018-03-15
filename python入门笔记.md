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
- [Python3 基本数据类型](#type-of-data)
	- [多个变量赋值](#assignment-for-multivariable)
	- [Number（数字）](#number)
	- [String（字符串）](#string)
	- [List（列表）](#list)
	- [Tuple（元组）](#tuple)
	- [Set（集合）](#set)
	- [Dictionary（字典）](#dictionary)
- [Python3 运算符](#operator)
	- [算术运算符](#arithmetic-operators)
	- [位运算符](#bit-operators)
	- [逻辑运算符](#logistic-operators)
	- [成员运算符](#memeber-operators)
	- [身份运算符](#id-operators)
- [Python3 数字(Number)](#number-detail)
- [Python3 字符串](#string-detail)
	- [字符串格式化](#str-format)
	- [三引号](#triple-quotes)
	- [字符串内建函数](#str-function-inbuild)


<h1 name="title">python入门笔记</h1>

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
|	      %s	|	 格式化字符串	|
|	      %d	|	 格式化整数	|
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

