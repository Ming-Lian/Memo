目录
- [1. 安装](#install)
- [2. 使用](#use)


# doctoc安装与使用

![](https://nodei.co/npm/doctoc.png?downloads=true&stars=true)

[doctoc](https://www.npmjs.com/package/doctoc)是一个JS包，用于给markdown文件创建目录。[npm](https://docs.npmjs.com/)是JS包管理工具，所以下载与安装doctoc需要借助于npm，在安装doctoc之前需要安装npm。由于npm是包含在Node.js中，所以在使用npm之前需要给系统安装上Node.js


<a name="install"><h3>1. 安装</h3></a>

- 安装Node.js

在安装Node.js之前先安装***node version manager***（nvm)
```
wget -c -P ~/Bin https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh
sh ~/Bin/install.sh
```
关闭终端重新打开，完成nvm的安装，运行命令`command -v nvm`来检查是否安装成功
接着安装Node.js
```
nvm install node
```

- 安装doctoc

```
nvm use node # 使用Node.js需要先载入
npm install -g doctoc
```

<a name="use"><h3>2. 使用</h3></a>
doctoc的使用很简单
```
doctoc file1.md [file2.md ... ]
```
一次可以指定多个md文件进行转换

其实doctoc对md文件创建目录的原理十分简单，就是通过识别文本中以一个或连续多个`#`开头的行，将它们判定为不同等级的标题，然后在原始md文本的开头创建链接
- **链接名** 原标题的字符串
- **链接地址** 以`#`开头，后接小写化的原标题的字符串，如果原字符串单词之间有空格，则改用连接符`-`连接起来，如果其中含有汉字则用base64进行编码，但是这样会使得连接失效，所以一旦存在汉字，需要进行特殊处理，具体处理方法后面会说明

例如：

原md文本中的标题行为：
```
### Title
```
经过doctoc转换后为：
```
[Title](#title)
```
但是当标题中存在**汉字**时这种转换会出现问题，使得链接失效，处理方法为：用html语言来改写标题行

例如：

原md文本中的标题行为：
```
### 标题
```
用用html语言来改写：
```
<a name="title"><h3>标题</h3></a>
```
这样就可以就可以用`name`参数的值"title"来作为internal navigation来进行目录跳转了

参考资料：
(1) [Install 1: How to Install npm & Manage npm Versions](https://docs.npmjs.com/getting-started/installing-node)
(2) [Install 2:Node Version Manager](https://github.com/creationix/nvm/blob/master/README.md#installation)
(2) [Markdown Questions](http://markdownpad.com/faq.html#markdown-namedanchors)