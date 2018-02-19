<a name="content">目录</a>

[Jupyter Notebook 使用指南](#title)
- [试用 Jupyter Notebook](#try-jupyter)
	- [浏览器中打开（无需安装）](#try-in-browser)
- [安装 Jupyter Notebook](#install-jupyter)
	- [安装 Anaconda](#install-anaconda)
		- [Anaconda使用入门(Windows)](#get-started-with-anaconda)
- [运行Notebook Server](#run-notebook)



<h1 name="title">Jupyter Notebook 使用指南</h1>

<a name="try-jupyter"><h3>试用 Jupyter Notebook [<sup>目录</sup>](#content)</h3></a>

<h4 name="try-in-browser">浏览器中打开（无需安装）</h4>

点击 https://try.jupyter.org 在浏览器中打开 jupyter

<img src=/picture/Jupyter-note-try-in-browser-1.png width="800" />

点击**"Welcome to Python.ipynb"**

<img src=/picture/Jupyter-note-try-in-browser-2.png width="800" />

在代码框内可以输入相应代码，按**"SHIFT+ENTER"**执行代码框内的代码

<a name="install-jupyter"><h3>安装 Jupyter Notebook [<sup>目录</sup>](#content)</h3></a>

jupter可以运行多种语言，即在代码框中可以输入多种编程语言，包括Python和R。在安装jupyter之前需要提取安装好Python，因为jupyter是建立在Python语言之上的。

<h4 name="install-anaconda">安装Anaconda</h4>
安装Python推荐用Anaconda或Conda：https://www.anaconda.com/download/ ，安装方法见官方手册。最简单的方法就是点击Anaconda安装包，选好安装路径然后一路狂点Yes。

<a name="get-started-with-anaconda">Anaconda使用入门(Windows)</a>

点击开始菜单，选择所有程序，然后选择Anaconda Navigation:

<img src=/picture/Jupyter-note-install-anaconda.png width="800" />

在Navigation的Home面板，展示出了多个可供使用的相关应用。

用Python编写程序需要使用Python的IDE，一般安装好Anaconda后同时安装好**Spyder IDE**，如果没有安装好，在面板的右侧找到Spyder应用，点击下方的**Install**。安装好之后点击下方的**Launch**。安装好之后点击下方的**Launch**，运行Spyder IDE：

<img src=/picture/Jupyter-note-install-Spyder.png width="800" />

<a name="run-notebook"><h4>运行Notebook Server [<sup>目录</sup>](#content)</h4></a>

打开Notebook：`开始菜单` -> `所有程序` -> `Anaconda3(64bit)` -> `Jupyter Notebook`

也可以在命令行中打开：

```
jupyter notebook
```

随后 Jupyter Notebook Server 会在浏览器中打开

<img src=/picture/Jupyter-note-run-jupyter.png width="800" />


参考资料：

(1) Tutorail: Anaconda

(2) Tutorial: Jupyter Notebook
