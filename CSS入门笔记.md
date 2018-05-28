<a name="content">目录</a>

[CSS入门笔记](#title)
- [语法](#syntax)
- [id 和 class 选择器](#id-class)
	- [id 选择器](#id)
	- [class 选择器](#class)


<h1 name="title">CSS入门笔记</h1>

<a name="syntax"><h2>语法  [<sup>目录</sup>](#content)</h2></a>

<p align="center"><img src=./picture/Beginning-css-syntax.jpg width=800 /></p>

注释:CSS注释以 "/*" 开始, 以 "*/" 结束

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


