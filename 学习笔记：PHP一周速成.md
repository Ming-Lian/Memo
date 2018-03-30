<a name="content">目录</a>

[学习笔记：PHP一周速成](#title)
- [写在前面](#firstly)
	- [测试Web服务器是否work](#test-web-server)
	- [测试PHP是否work](#test-php)
	- [web服务器默认工作目录](#web-server-workdir-default)
	- [linux文本编辑器的简单介绍](#txt-editor-introduct)
		- [nano](#nano)
		- [vim](#vim)
	- [编辑你的第一个php脚本](#edit-php-script)
- [PHP 语法](#syntax)
- [变量](#variable)
	- [变量作用域](#variable-scope)
- [echo 和 print 语句](#echo-print)
- [EOF(heredoc)](#heredoc)
- [数据类型](#data-types)
- [运算符](#operator)
- [数据结构](#data-structure)
	- [常量](#constant)
	- [字符串变量](#string)
	- [数组](#array)
		- [数组排序](#array-sort)
- [条件判断](#condition-judgment)



<h1 name="title">学习笔记：PHP一周速成</h1>

<a name="firstly"><h3>写在前面 [<sup>目录</sup>](#content)</h3></a>

<a name="test-web-server"><h4>测试Web服务器是否work [<sup>目录</sup>](#content)</h4></a>

在浏览器地址栏输入`ip:port`，回车。ip为树莓派服务器ip，port为树莓派服务器的web服务端口，比如ip为：124.16.111.23，port为9000，则输入：`124.16.111.23:9000`

若打开以下界面则说明Web服务器正常运行

<p align="center"><img src=https://github.com/Ming-Lian/Hello-RaspberryPi/blob/master/picture/Beginning-raspi-webserver-apache.png width=800 />

<a name="test-php"><h4>测试PHP是否work [<sup>目录</sup>](#content)</h4></a>

在浏览器地址栏输入`ip:port/phptest.php`

若打开以下界面则说明PHP正常运行

<p align="center"><img src=https://github.com/Ming-Lian/Hello-RaspberryPi/blob/master/picture/Beginning-raspi-webserver-php.png width=800 />

<a name="web-server-workdir-default"><h4>web服务器默认工作目录 [<sup>目录</sup>](#content)</h4></a>

web服务器默认工作目录：直接在浏览器地址栏输入`ip:port`后，所进入的服务器文件系统的路径

默认工作目录为 `/var/www`

比如有以下树形结构的文件路径

```
/var/www/
|-- bioinfo-course
|-- html
|	|-- login1.html
|	|-- login.php
```
如果你想在浏览器上打开文件`login1.html`，怎么实现？
> 1. 用`ip:port`进入web服务器默认工作目录`/var/www`
> 2. 添加`login1.html`文件对应默认工作目录的相对路径：`html/login1.html`
> 3. 结合1和2中的信息，构造访问`login1.html`的URL：`ip:port/html/login1.html`

<p align="center"><img src=./picture/Beginning-php-how-to-access-file.png width=800 />

**注意 ! ! !**

为了更好地归档和管理用户的数据，服务器管理员已经特地在web服务器默认工作目录`/var/www`下，创建了一个专门用于用户学习和练习PHP的文件夹`learningPHP`，请在该文件夹下再创建一个属于用户自己的文件夹，命令参考下面：

```
# 新建文件夹your_new_dir，具体文件夹名自行指定
$ mkdir /var/www/learningPHP/your_new_dir
# 修改文件夹操作权限，关闭同组成员的写权限
$ chmod g-w /var/www/learningPHP/your_new_dir
```

<a name="txt-editor-introduct"><h4>linux文本编辑器的简单介绍 [<sup>目录</sup>](#content)</h4></a>

<a name="nano"><h4>nano [<sup>目录</sup>](#content)</h4></a>

大家在Linux上用的文本编辑器，一般是**Vim**之类的，不过对于初学者可能门槛较高，学起来比较吃力，所以这里给初学者推荐一款比较容易入门上手的编辑器：nano

操作实例（比如有个文件`test.txt`)：
```
$ nano test.txt
```

<p align="center"><img src=./picture/Beginning-php-nano-1.png width=500 />

编辑方法：
> - 输入字符：直接敲键盘就行
> - 移动输入位置：键盘中的上下左右键
> - 编辑后保存：`ctrl+x` -> `y` -> 回车

<a name="vim"><h4>Vim [<sup>目录</sup>](#content)</h4></a>

vim是目前Linux操作系统下最流行的几款文本编辑器之一

Vim/vi 是一个功能强大的全屏幕文本编辑器，是 Linux/UNIX 上最常用的文本编辑器，它的作用是建立、编辑、显示文本文件。 Vim/vi 没有菜单，只有命令。

<li />启动Vim

```
$ vim filename
```

界面

<p align="center"><img src=./picture/Beginning-php-vim-1.png width=700 />

<li />Vim的三种模式及其切换

三种模式：

> - **命令模式**（Command Mode）
> 
> Vim 启动后的默认模式，所输入的任何内容都被解释成命令。在此模式中，用户可以执行一般的
编辑器命令，比如移动光标、删除文本等等。在命令模式中，有很多方法可以进入输入模式，比较普通的方式是按“a”（append，追加）键或者“i”（insert，插入）键。
>
> **在该模式下我一般不会做太多操作，除了一些光标移动操作**
> > - 移动到文件末尾：`shift + g`
> > - 移动到当前行的行首：`shift + ^`
> > - 移动到当前行的行尾：`shift + $`
>
> ![](./picture/Beginning-php-vim-2.png)
> 
> - **输入模式**（Insert Mode）
> 
> 在此模式中，才能对文本进行正常的编辑
>
> ![](./picture/Beginning-php-vim-3.png)
> 
> - **末行模式**（Last Line Mode） 
> 
> 在末行模式中可以输入会被解释并执行的命令。例如执行命令（“:”键），搜索（“/”和“?”
键）或者过滤命令（“!”键）。在命令执行之后， Vim 返回到末行模式之前的模式，通常是普通模式（命令模式）。
>
> **在该模式下我一般不会做太多操作，除了保存文件及退出**
> > - 保存文件：`w`
> > - 退出：`q`
> > - 保存并退出：`wq`
> > - 强制退出，不保存文件：`q!`
> 
> ![](./picture/Beginning-php-vim-4.png)

三个模式之间的转换

<p align="center"><img src=./picture/Beginning-php-vim-3model.png width=500 />

注意：**输入模式与末行模式之间无法直接转换，需要命令模式作为中介**

<a name="edit-php-script"><h4>编辑你的第一个php脚本 [<sup>目录</sup>](#content)</h4></a>

打开文本编辑器，这里以nano为例，这里将文件命名为`test.php`（文件名自行定义，但后缀必须是php）：

```
$ nano /var/www/learningPHP/lianm/test.php
```

然后在编辑器中输入以下PHP脚本语句

```
<?php
echo "Hello World!";
?> 
```

然后保存：`ctrl+x` -> `y` -> 回车。

在浏览器中访问你刚才编辑好的php脚本，在浏览器地址栏输入该脚本的URL：`124.16.111.23:9000/learningPHP/lianm/test.php`

<p align="center"><img src=./picture/Beginning-php-first-phpscript.png width=500 />

运行成功，congratulation ！ ！ ！

<a name="syntax"><h3>PHP 语法 [<sup>目录</sup>](#content)</h3></a>

<li>基本的 PHP 语法：</li>

```
<?php
// PHP 代码
?> 
```

PHP 中的每个代码行都**必须以分号结束**。分号是一种分隔符，用于把指令集区分开来。

通过 PHP，有两种在浏览器输出文本的基础指令：echo 和 print。
<br>
<li>注释</li>

```
<?php
// 这是 PHP 单行注释

/*
这是
PHP 多行
注释
*/
?>
```

<a name="variable"><h3>变量 [<sup>目录</sup>](#content)</h3></a>

```
<?php
$x=5;
$y=6;
$z=$x+$y;
echo $z;
?>
```

<a name="variable-scope"><h4>变量作用域 [<sup>目录</sup>](#content)</h4></a>

<li>全局变量</li>

在所有函数外部定义的变量，拥有全局作用域。要在一个函数中访问一个全局变量，需要使用 global 关键字。 

```
<?php
$x=5;
$y=10;
 
function myTest()
{
    global $x,$y;
    $y=$x+$y;
}
 
myTest();
echo $y; // 输出 15
?>
```

PHP 将所有全局变量存储在一个名为 $GLOBALS[index] 的数组中。 index 保存变量的名称。这个数组可以在函数内部访问，也可以直接用来更新全局变量。

```
<?php
$x=5;
$y=10;
 
function myTest()
{
    $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
} 
 
myTest();
echo $y;
?>
```

<br>
<li>局部变量</li>

在 PHP 函数内部声明的变量是局部变量，仅能在函数内部访问

<br>
<li>Static 作用域</li>

当一个函数完成时，它的所有变量通常都会被删除。然而，有时候您希望某个局部变量不要被删除。

要做到这一点，请在您第一次声明变量时使用 static 关键字：

```
<?php
function myTest()
{
    static $x=0;
    echo $x;
    $x++;
}
 
myTest();
myTest();
myTest();
?>

# 输出结果： 012
```

<a name="echo-print"><h3>echo 和 print 语句 [<sup>目录</sup>](#content)</h3></a>

echo 和 print 区别:

> - echo - 可以输出一个或多个字符串，字符串之间用**逗号**隔开
> - print - 只允许输出一个字符串，返回值总为 1

<a name="heredoc"><h3>EOF (heredoc) [<sup>目录</sup>](#content)</h3></a>

```
<?php
echo <<<EOF
    <h1>我的第一个标题</h1>
    <p>我的第一个段落。</p>
EOF;
// 结束需要独立一行且前后不能空格
?>
```

> 1. 必须后接分号，否则编译通不过。
> 2. EOF 可以用任意其它字符代替，只需保证结束标识与开始标识一致。
> 3. **结束标识必须顶格独自占一行(即必须从行首开始，前后不能衔接任何空白和字符)。**
> 4. 开始标识可以不带引号或带单双引号，不带引号与带双引号效果一致，解释内嵌的变量和转义符号，带单引号则不解释内嵌的变量和转义符号。
> 5. 当内容需要内嵌引号（单引号或双引号）时，不需要加转义符，本身对单双引号转义，此处相当与q和qq的用法。

<a name="data-types"><h3>数据类型 [<sup>目录</sup>](#content)</h3></a>

<li />字符串

将任何文本放在单引号和双引号中

<li />整型

整型可以用三种格式来指定：十进制， 十六进制（ 以 0x 为前缀）或八进制（前缀为 0）。

var_dump( ) 函数返回变量的数据类型和值

<li />浮点型

浮点数是带小数部分的数字，或是指数形式。

<li />布尔型

布尔型可以是 TRUE 或 FALSE。

<li />数组

数组可以在一个变量中存储多个值。

```
$cars=array("Volvo","BMW","Toyota");
```

<li />对象


在 PHP 中，对象必须声明。首先，你必须使用class关键字声明类对象。类是可以包含**属性**和**方法**的结构。

``` 
<?php
class Car
{
  var $color;
  function Car($color="green") {
    $this->color = $color;
  }
  function what_color() {
    return $this->color;
  }
}
?> 
```

以上实例中PHP关键字this就是指向当前对象实例的指针，不指向任何其他对象或类。

<a name="operator"><h3>运算符 [<sup>目录</sup>](#content)</h3></a>

- 逻辑运算符

> - 与：`and` 或 `&&`
> 
> - 或：`or` 或 `||`
> 
> - 异或：`xor`，有且仅有一个为 true，则返回 true

- 数组运算符

|	运算符	|	名称	|	描述	|
|:---|:---|:---|
|	x + y	|	集合	|	x 和 y 的集合	|
|	x == y	|	相等	|	如果 x 和 y 具有相同的键/值对，则返回 true	|
|	x === y	|	恒等	|	如果 x 和 y 具有相同的键/值对，且顺序相同类型相同，则返回 true	|
|	x != y	|	不相等	|	如果 x 不等于 y，则返回 true	|
|	x <> y	|	不相等	|	如果 x 不等于 y，则返回 true	|
|	x !== y	|	不恒等	|	如果 x 不等于 y，则返回 true	|

- 三元运算符

```
(expr1) ? (expr2) : (expr3) 
```

对 expr1 求值为 TRUE 时的值为 expr2，在 expr1 求值为 FALSE 时的值为 expr3。

自 PHP 5.3 起，可以省略三元运算符中间那部分。表达式 expr1 ?: expr3 在 expr1 求值为 TRUE 时返回 expr1，否则返回 expr3。常用在判断 $_GET 请求中含有 user 值

```
<?php
// 如果 $_GET['user'] 不存在返回 'nobody'，否则返回 $_GET['user'] 的值
$username = $_GET['user'] ?? 'nobody';
// 类似的三元运算符
$username = isset($_GET['user']) ? $_GET['user'] : 'nobody';
?>
```

- 组合比较符(PHP7+)

组合比较运算符，英文叫作combined comparison operator，符号为<=>，它有一个形象的名字，叫作**太空船操作符**。组合比较运算符可以轻松实现两个变量的比较。

```
$c = $a <=> $b
```

> - 如果$a > $b，$c 的值为1
> - 如果$a == $b，$c 的值为0
> - 如果$a < $b，$c 的值为-1

<a name="data-structure"><h3>数据结构 [<sup>目录</sup>](#content)</h3></a>

<a name="constant"><h4>常量 [<sup>目录</sup>](#content)</h4></a>

常量是一个简单值的标识符。该值在脚本中不能改变。常量在整个脚本中都可以使用。

```
define ( string $name , mixed $value [, bool $case_insensitive = false ] )
```

> - name：必选参数，常量名称，即标志符。
> - value：必选参数，常量的值。
> - case_insensitive ：可选参数，如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的。

```
<?php
// 区分大小写的常量名
define("GREETING", "欢迎访问 Runoob.com");
echo GREETING;    // 输出 "欢迎访问 Runoob.com"
echo '<br>';
echo greeting;   // 输出 "greeting"
?>
```

<a name="string"><h4>字符串变量 [<sup>目录</sup>](#content)</h4></a>

- 字符串连接：

运算符 (.) 用于把两个字符串值连接起来。

```
 <?php
$txt1="Hello world!";
$txt2="What a nice day!";
echo $txt1 . " " . $txt2;
?> 
```

- strlen( )：返回字符串的长度（字符数）

- strpos( )：用于在字符串内查找一个字符或一段指定的文本

如果在字符串中找到匹配，该函数会返回第一个匹配的字符位置。如果未找到匹配，则返回 FALSE。

完整参考手册请点 [这里](http://www.runoob.com/php/php-ref-string.html)

<a name="array"><h4>数组 [<sup>目录</sup>](#content)</h4></a>

在 PHP 中，有三种类型的数组：
> - 数值数组 - 带有数字 ID 键的数组
> - 关联数组 - 带有指定的键的数组，每个键关联一个值
> - 多维数组 - 包含一个或多个数组的数组

- 数值数组

创建数值数组

```
$cars=array("Volvo","BMW","Toyota");
```

count( )：获取数组的长度

- 关联数组

创建关联数组

```
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
```

使用指定的键访问数组中对应的键值

```
<?php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
echo "Peter is " . $age['Peter'] . " years old.";
?>
```

- 多维数组

多维数组是包含一个或多个数组的数组。

```
<?php
// 二维数组:
$cars = array
(
    array("Volvo",100,96),
    array("BMW",60,59),
    array("Toyota",110,100)
);
?>
```

访问多维数组的值：`$sites['runoob'][0]`

<a name="array-sort"><h4>数组排序 [<sup>目录</sup>](#content)</h4></a>

> - sort() - 对数组进行升序排列
> - rsort() - 对数组进行降序排列
> - asort() - 根据关联数组的值，对数组进行升序排列
> - ksort() - 根据关联数组的键，对数组进行升序排列
> - arsort() - 根据关联数组的值，对数组进行降序排列
> - krsort() - 根据关联数组的键，对数组进行降序排列

<a name="condition-judgment"><h3>条件判断 [<sup>目录</sup>](#content)</h3></a>

- If...Else 语句

```
if (条件)
{
	if 条件成立时执行的代码;
}
elseif (条件)
{
	elseif 条件成立时执行的代码;
}
else
{
	条件不成立时执行的代码;
} 
```

- Switch 语句

```
<?php
switch (n)
{
case label1:
    如果 n=label1，此处代码将执行;
    break;
case label2:
    如果 n=label2，此处代码将执行;
    break;
default:
    如果 n 既不等于 label1 也不等于 label2，此处代码将执行;
}
?>
```
