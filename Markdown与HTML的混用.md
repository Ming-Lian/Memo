<a name="content"><h3>目录</h3></a>
                 
[Markdown与HTML的混用技巧](#title)
  - [1. 标题](#head)
  - [2. 强调](#emphasize)
  - [3. 列表](#list)
  - [4. 区块引用](#block-quote)
  - [5. 链接与图片](#link-image)
  - [6. 表格](#table)
  - [7. 代码框](#code)
  - [8. 分割线](#splitter)
  - [9. 构建目录](#construct-content)
  
<a name="title"><h1>Markdown与HTML的混用技巧</h1></a>

Markdown本质上就是简化版的HTML，它与HTML相比优点在于，它比HTML更轻量，书写更简洁。但是同时这也是它的缺点，毕竟Markdown是阉割过的HTML，对于一些标签可以设置的属性受到了限制，举个例子，对于一段文本，Markdown只能左对齐，如果想要居中或右对齐，抱歉，臣妾做不到(~_~)，而用HTML加一个align属性就解决了，所以左手Markdown，右手HTML，写笔记无敌了！！！

<table>
<tr>
	<td><img src=/picture/Markdown-HTML-fixed-Markdown-logo.png width ="400" border=0></td>
	<td><img src=/picture/Markdown-HTML-fixed-HTML-logo.jpg width ="400" border=0></td>
</tr>
</table>

<a name="head"><h3>1. 标题 [<sup>目录</sup>](#content)</h3></a>

```
# H1
## H2
### H3
#### H4
##### H5
###### H6
```
在标题下加下划线
```
### H1
---
```
效果为
### H1
---

当需要在标题后接一个返回目录的链接时，可以用html来书写：

```
<a name="title-example"><h3>示例标题 [<sup>目录</sup>](#content)</h3></a>
```

效果为：

![](/picture/Markdown-HTML-fixed-title-example.png)

<a name="emphasize"><h3>2. 强调 [<sup>目录</sup>](#content)</h3></a>

> - **倾斜** `*text*`或`_text_`
> - **加粗** `**text**`或`__text__`
> - **删除线** `~~Scratch this~~`，该用法在不同的Markdown编辑器中会有差别

强调对应的html标签为`<strong>`

<a name="list"><h3>3. 列表 [<sup>目录</sup>](#content)</h3></a>

> - **有序列表** `1. text`，即序号+点+空格+文本，其中序号不需要准确填写，只需要保证该位置输入的为数字就行，Markdown会自动编号
> - **无需列表** 在文本前加上`*`、`-`或`+`，当然还有加空格

<a name="block-quote"><h3>4. 区块引用 [<sup>目录</sup>](#content)</h3></a>

在每句话前加一个`>`

```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
```

区块引用的一些用法：
> - 区块引用可以嵌套，只要根据层次加上不同数量的`>`
> - 引用的区块内也可以使用其他的 Markdown 语法，包括标题、列表、代码区块等

<a name="link-image"><h3>5. 链接与图片 [<sup>目录</sup>](#content)</h3></a>

Markdown 支持两种形式的链接语法： **行内式**和**参考式**两种形式。

> - **行内式** 只要在方块括号后面紧接着圆括号并插入网址链接即可，只要在网址后面，用双引号把 title 文字包起来即可，例如：
`This is [an example](http://example.com/ "Title") inline link.`
如果你是要链接到同样主机的资源，你可以使用相对路径：
`See my [About](/about/) page for details.`
> - **参考式** 在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记
`This is [an example][id] reference-style link.`
接着，在文件的任意处，你可以把这个标记的链接内容定义出来：
`[id]: http://example.com/  "Optional Title Here"`
链接内容定义的形式为：
>> - 方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
>> - 接着一个冒号
>> - 接着一个以上的空格或制表符
>> - 接着链接的网址
>> - 选择性地接着 title 内容，可以用单引号、双引号或是括弧包着

如果想要链接的目标是当前页面的某一个标签，则需要在圆括号后紧接着一个井字符 `#`，再接着该标签的 id 或者标签名，例如当前页面中有一个标签如下：

```
# 本例子用的是标签名，如果使用 id 则要设定 id 属性
<p name="tag">abc</p>
```

那么链接需要写成：

```
[目标标签](#tag)
```

这样就实现了在当前页面的位置跳转，这在构建目录时很有用。

<br>

插入链接与插入图片的语法很像，区别在一个 !号
> - 链接 `[]()`
> - 图片 `![]()`

Markdown中的图片插入方法无法设置图片大小与对齐方式，用 html 方法可以实现：

```
<p align="center"><img src=/picture/test.jpg width="600"/></p>
```

注意，不知道为什么，无法直接通过`<img>`标签内部的 align 属性设置图片的对齐方式，html 还没学到精髓，不过条条大路通罗马，可以通过在`<p>`标签实现图片对齐方式的设置。

<a name="table"><h3>6. 表格 [<sup>目录</sup>](#content)</h3></a>

例子如下：

```
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
```

这种语法生成的表格如下（注意表格前必须有一个空行）：

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | \$1600 |
| col 2 is      | centered      |   \$12 |
| zebra stripes | are neat      |    \$1 |

注意，表格的第二行的冒号位置表示在该单元格的对齐方式：
> - `|:-----:|` 居中对齐
> - `|:----- |` 左对齐
> - `| -----:|` 右对齐

其实个人感觉，Markdown中的表格语法也挺繁琐的，没比html的方便多少:

```
<table>
<tr>
	<td><p>text1</p></td>
	<td><p>text2</p></td>
</tr>
<tr>
	<td><p>text3</p></td>
	<td><p>text4</p></td>
</tr>
<table>
```

效果：

<table>
<tr>
	<td><p>text1</p></td>
	<td><p>text2</p></td>
</tr>
<tr>
	<td><p>text3</p></td>
	<td><p>text4</p></td>
</tr>
<table>

如果想要实现多个图片并列摆放，可以通过将图片放入表格的单元格实现，效果：

<p align="center"><img src=/picture/Markdown-HTML-fixed-tableImg-example.png width="600"/>

<a name="code"><h3>7. 代码框 [<sup>目录</sup>](#content)</h3></a>

> - 在首行与末行加上``(```)``
> - 用`tab`键缩进

<a name="splitter"><h3>8. 分割线 [<sup>目录</sup>](#content)</h3></a>
下面每种写法都可以建立分隔线：
```
* * *

***

*****

- - -

---------------------------------------
```

<a name="construct-content"><h3>9. 构建目录  [<sup>目录</sup>](#content)</h3></a>

在页面的初始位置，写入目录：

```
<a name="content"><h3>目录</h3></a>
                 
[Markdown与HTML的混用技巧](#title)
  - [1. 标题](#head)
  - [2. 强调](#emphasize)
  - [3. 列表](#list)
  - [4. 区块引用](#block-quote)
  - [5. 链接与图片](#link-image)
  - [6. 表格](#table)
  - [7. 代码框](#code)
  - [8. 分割线](#splitter)
  - [9. 构建目录](#construct-content)
```

然后在该文本的其他位置放置响应的标签即可：

```
<a name="title"><h1>Markdown与HTML的混用技巧</h1></a>

<a name="head"><h3>1. 标题 [<sup>目录</sup>](#content)</h3></a>
.
.
.
```

参考资料：

1. [Markdown Here Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet#emphasis)

2. [Markdown 语法说明 (简体中文版) ](http://wowubuntu.com/markdown/#list)



