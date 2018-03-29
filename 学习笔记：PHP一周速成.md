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
