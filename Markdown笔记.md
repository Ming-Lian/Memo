<a name="content"><h3>目录</h3></a>
                 
- [Markdown笔记](#title)
  - [1. 标题](#head)
  - [2. 强调](#emphasize)
  - [3. 列表](#list)
  - [4. 区块引用](#block-quote)
  - [5. 链接与图片](#link-image)
  - [6. 表格](#table)
  - [7. 代码框](#code)
  - [8. 分割线](#cut)
  
<a name="title"><h1>Markdown 笔记</h1></a>
---
               
<a name="head"><h3>1. 标题</h3></a>
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

<a name="emphasize"><h3>2. 强调</h3></a>
> - **倾斜** `*text*`或`_text_`
> - **加粗** `**text**`或`__text__`
> - **删除线** `~~Scratch this~~`，该用法在不同的Markdown编辑器中会有差别

<a name="list"><h3>3. 列表</h3></a>
> - **有序列表** `1. text`，即序号+点+空格+文本，其中序号不需要准确填写，只需要保证该位置输入的为数字就行，Markdown会自动编号
> - **无需列表** 在文本前加上`*`、`-`或`+`，当然还有加空格

<a name="block-quote"><h3>4. 区块引用</h3></a>
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

<a name="link-image"><h3>5. 链接与图片</h3></a>
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

``There is a literal backtick (`) here.``
插入链接与插入图片的语法很像，区别在一个 !号
> - 链接 `[]()`
> - 图片 `![]()`

<a name="table"><h3>6. 表格</h3></a>
例子如下：
```
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
```

这种语法生成的表格如下：

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | \$1600 |
| col 2 is      | centered      |   \$12 |
| zebra stripes | are neat      |    \$1 |
注意，表格的第二行的冒号位置表示在该单元格的对齐方式：
> - `|:-----:|` 居中对齐
> - `|:----- |` 左对齐
> - `| -----:|` 右对齐

<a name="code"><h3>7. 代码框</h3></a>
> - 在首行与末行加上``(```)``
> - 用`tab`键缩进

<a name="cut"><h3>8. 分割线</h3></a>
下面每种写法都可以建立分隔线：
```
* * *

***

*****

- - -

---------------------------------------
```


参考资料：

1. [Markdown Here Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet#emphasis)

2. [Markdown 语法说明 (简体中文版) ](http://wowubuntu.com/markdown/#list)



