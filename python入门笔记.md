<a name="content">目录</a>

[python入门笔记]("title")
- [python基础语法](#basic-grammer)
	- [python保留字](#reserved-word)
	- [注释](#annotation)
	- [行与缩进](#indentation)
	- [字符串(String)](#string)
	- [等待用户输入](#get-input)
	- [多个语句构成代码组](#code-group)
	- [Print 输出](#print)
	- [import 与 from...import](#import)
- [Python3 基本数据类型](#type-of-data)
	- [多个变量赋值](#assignment-for-multivariable)
	- [Number（数字）](#number)
	- [String（字符串）](#string-detail)
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


<h1 name="title">python入门笔记</h1>

<a name="basic-grammer"><h3>python基础语法 [<sup>目录</sup>](#content)</h3></a>

<a name="reserved-word"><h4>python保留字 [<sup>目录</sup>](#content)</h4></a>

保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字： 

```
>>>import keyword
>>>keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 
'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

<a name="annotation"><h4>注释 [<sup>目录</sup>](#content)</h4></a>

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

<a name="indentation"><h4>行与缩进 [<sup>目录</sup>](#content)</h4></a>


python最具特色的就是使用缩进来表示代码块，不需要使用大括号 {} 。
 
缩进的空格数是可变的，但是同一个代码块的语句必须包含相同的缩进空格数

```
if True:
    print ("True")
else:
    print ("False")
```

<a name="string"><h4>字符串(String) [<sup>目录</sup>](#content)</h4></a>

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

<a name="get-input"><h4>等待用户输入 [<sup>目录</sup>](#content)</h4></a>

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

<a name="print"><h4>Print 输出 [<sup>目录</sup>](#content)</h4></a>

print 默认输出是换行的，如果要实现不换行需要在变量末尾加上 end=""：

```
print( x, end=" " )
```

<a name="import"><h4>import 与 from...import [<sup>目录</sup>](#content)</h4></a>

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

<a name="string-detail"><h4>String（字符串） [<sup>目录</sup>](#content)</h4></a>

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
