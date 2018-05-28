<a name="content">目录</a>

[CSS入门笔记](#title)
- [语法](#syntax)
- [id 和 class 选择器](#id-class)
	- [id 选择器](#id)
	- [class 选择器](#class)
- [创建样式表](#create)
	- [外部样式表](#external-style-sheet)
	- [内部样式表](#internal-style-sheet)
	- [内联样式](#inline-style)
	- [多重样式](#multi-css)
- [背景](#backgroud)
	- [正规写法](#backgroud-formal)
	- [简写属性](#backgroud-simplify)
- [文本格式](#text-format)
- [字体](#font)
- [链接](#link)
- [列表](#list)
- [表格](#table)







<h1 name="title">CSS入门笔记</h1>

<a name="syntax"><h2>语法  [<sup>目录</sup>](#content)</h2></a>

<p align="center"><img src=./picture/Beginning-css-syntax.jpg width=800 /></p>

不要在属性值与单位之间留有空格（如："margin-left: 20 px" ），正确的写法是 "margin-left: 20px" 

注释：CSS注释以 "/\*" 开始, 以 "\*/" 结束

```
/*这是个注释*/
p
{
text-align:center;
/*这是另一个注释*/
color:black;
font-family:arial;
}
```

<a name="id-class"><h2>id 和 class 选择器  [<sup>目录</sup>](#content)</h2></a>

如果你要在HTML元素中设置CSS样式，你需要在元素中设置"id" 和 "class"选择器。

<a name="id"><h3>id 选择器  [<sup>目录</sup>](#content)</h3></a>

设置

```

#para1
{
    text-align:center;
    color:red;
}
```

引用

```
<p id="para1">Hello World!</p>
```


**ID属性不要以数字开头，数字开头的ID在 Mozilla/Firefox 浏览器中不起作用**

<a name="class"><h3>class 选择器  [<sup>目录</sup>](#content)</h3></a>

用于描述一组元素的样式，class 选择器有别于id选择器，class可以在多个元素中使用

设置

```
.center {text-align:center;}
```

引用

```
<h1 class="center">标题居中</h1>
<p class="center">段落居中。</p> 
```

也可以指定特定的HTML元素使用class

```
p.center {text-align:center;}
```

<a name="create"><h2>创建样式表  [<sup>目录</sup>](#content)</h2></a>

插入样式表的方法有三种:

- 外部样式表(External style sheet)
- 内部样式表(Internal style sheet)
- 内联样式(Inline style)

<a name="external-style-sheet"><h3>外部样式表  [<sup>目录</sup>](#content)</h3></a>

当样式需要应用于很多页面时，外部样式表将是理想的选择

可以通过改变一个文件来改变整个站点的外观。每个页面使用 `<link>` 标签链接到样式表

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

外部样式表可以在任何文本编辑器中进行编辑。文件不能包含任何的 html 标签。样式表应该以 .css 扩展名进行保存

<a name="internal-style-sheet"><h3>内部样式表  [<sup>目录</sup>](#content)</h3></a>

当单个文档需要特殊的样式时，就应该使用内部样式表

使用 `<style>` 标签在文档头部定义内部样式表

```
<head>
<style>
hr {color:sienna;}
p {margin-left:20px;}
body {background-image:url("images/back40.gif");}
</style>
</head>
```

<a name="inline-style"><h3>内联样式  [<sup>目录</sup>](#content)</h3></a>

由于要将表现和内容混杂在一起，内联样式会损失掉样式表的许多优势

```
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

<a name="multi-css"><h3>多重样式  [<sup>目录</sup>](#content)</h3></a>

如果某些属性在不同的样式表中被同样的选择器定义，那么属性值将从更具体的样式表中被继承过来。

例如，外部样式表拥有针对 h3 选择器的三个属性：

```
h3
{
    color:red;
    text-align:left;
    font-size:8pt;
}
```

而内部样式表拥有针对 h3 选择器的两个属性：

```
h3
{
    text-align:right;
    font-size:20pt;
}
```

那么，最终 h3 得到的样式是：

```
color:red;
text-align:right;
font-size:20pt;
```

多重样式优先级:

**(内联样式）Inline style** > **（内部样式）Internal style sheet** >（**外部样式）External style sheet** > **浏览器默认样式**

<a name="backgroud"><h2>背景  [<sup>目录</sup>](#content)</h2></a>

<a name="backgroud-formal"><h3>正规写法  [<sup>目录</sup>](#content)</h3></a>

CSS 属性定义背景效果:

- background-color 背景颜色

	CSS中，颜色值通常以以下方式定义:

	- 十六进制 - 如："#ff0000"
	- RGB - 如："rgb(255,0,0)"
	- 颜色名称 - 如："red"


- background-image 背景图像

	默认情况下，背景图像进行平铺重复显示，以覆盖整个元素实体
	
	```
	body {background-image:url('paper.gif');}
	```
- background-repeat 水平或垂直平铺

	图像只在水平方向平铺 (repeat-x)
	
	```
	body
	{
	background-image:url('gradient2.png');
	background-repeat:repeat-x;
	} 
	```
	
	如果你不想让图像平铺
	
	```
	background-repeat:no-repeat;
	```

- background-attachment
- background-position 设置定位

	可以利用 background-position 属性改变图像在背景中的位置:
	
	```
	body
	{
	background-image:url('img_tree.png');
	background-repeat:no-repeat;
	background-position:right top;
	} 
	```

<a name="backgroud-simplify"><h3>简写属性  [<sup>目录</sup>](#content)</h3></a>

可以将这些属性合并在同一个属性中

```
body {background:#ffffff url('img_tree.png') no-repeat right top;}
```

 当使用简写属性时，属性值的顺序为：:

> - background-color
> - background-image
> - background-repeat
> - background-attachment
> - background-position

<a name="text-format"><h2>文本格式  [<sup>目录</sup>](#content)</h2></a>

- 文本颜色

```
h1 {color:#00ff00;}
```

- 文本的对齐方式

```
h1 {text-align:center;}
```

- 文本修饰：从设计的角度看 text-decoration属性主要是用来删除链接的下划线

```
a {text-decoration:none;}
```

也可以这样装饰文字：

<table>
<tr>
	<td><img src=./picture/Beginning-css-text-decorate-code.png width=400 /></td>
	<td><img src=./picture/Beginning-css-text-decorate.png width=400 /></td>
</tr>
</table>

- 文本转换

可用于所有字句变成大写或小写字母，或每个单词的首字母大写。

<table>
<tr>
	<td><img src=./picture/Beginning-css-text-transform-code.png width=400 /></td>
	<td><img src=./picture/Beginning-css-text-transform.png width=400 /></td>
</tr>
</table>

- 文本缩进

```
p {text-indent:50px;}
```

<a name="font"><h2>字体  [<sup>目录</sup>](#content)</h2></a>

字体属性定义字体，加粗，大小，文字样式

<img src=./picture/Beginning-css-font.png width=800 />

- 字体系列

	font-family 属性应该设置几个字体名称作为一种"后备"机制，如果浏览器不支持第一种字体，他将尝试下一种字体
	
	如果字体系列的名称超过一个字，它必须用引号，如Font Family："宋体"
	
	```
	p{font-family:"Times New Roman", Times, serif;} 
	```
	
- 字体样式

	主要是用于指定斜体文字的字体样式属性
	
	> - 正常 - 正常显示文本 `p.normal {font-style:normal;}`
	> - 斜体 - 以斜体字显示的文字 `p.italic {font-style:italic;}`

- 字体大小

	font-size 属性设置文本的大小

	绝对大小：
	> - 设置一个指定大小的文本
	> - 不允许用户在所有浏览器中改变文本大小
	> - 确定了输出的物理尺寸时绝对大小很有用

	相对大小：

	> - 相对于周围的元素来设置大小
	> - 允许用户在浏览器中改变文字大小

	```
	h1 {font-size:40px;}
	```

<a name="link"><h2>链接  [<sup>目录</sup>](#content)</h2></a>

四个链接状态：

> - a:link - 正常，未访问过的链接
> - a:visited - 用户已访问过的链接
> - a:hover - 当用户鼠标放在链接上时
> - a:active - 链接被点击的那一刻

当设置为若干链路状态的样式，也有一些顺序规则：

> - a:hover 必须跟在 a:link 和 a:visited后面
> - a:active 必须跟在 a:hover后面

<a name="list"><h2>列表  [<sup>目录</sup>](#content)</h2></a>

CSS列表属性作用如下：

> - 设置不同的列表项标记为有序列表
> 
>     列表项标记用特殊图形（如小黑点、小方框等）
> 
> - 设置不同的列表项标记为无序列表
> 
>     列表项的标记有数字或字母
> 
> - 设置列表项标记为图像

```
ul.a {list-style-type: circle;}
ul.b {list-style-type: square;}
 
ol.c {list-style-type: upper-roman;}
ol.d {list-style-type: lower-alpha;}
```

指定列表项标记的图像

```
ul
{
    list-style-image: url('sqpurple.gif');
}
```

<a name="table"><h2>表格  [<sup>目录</sup>](#content)</h2></a>

- 表格边框

<table>
<tr>
	<td><img src=./picture/Beginning-css-table-border-1-code.png width=400 /></td>
	<td><img src=./picture/Beginning-css-table-border-1.png width=400 /></td>
</tr>
</table>

在上面的例子中的表格有双边框。这是因为表和th/ td元素有独立的边界

为了显示一个表的单个边框，使用 border-collapse 属性

<table>
<tr>
	<td><img src=./picture/Beginning-css-table-border-2-code.png width=400 /></td>
	<td><img src=./picture/Beginning-css-table-border-2.png width=400 /></td>
</tr>
</table>

- 表格宽度和高度

Width和height属性定义表格的宽度和高度

- 表格文字对齐

text-align属性设置水平对齐方式，像左，右，或中心：

```
td
{
text-align:right;
}
```

vertical-align属性设置垂直对齐，比如顶部，底部或中间：

```
td
{
height:50px;
vertical-align:bottom;
}
```



