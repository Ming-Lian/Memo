<a name="content">目录</a>

[Git入门笔记](#title)
- [1. 起步](#get-start)
	- [1.1. 关于版本控制](#about-version-control)
	- [1.2. 基本工作原理](#principle)
- [3. GitHub远程仓库](#remote-repository-github)
	- [3.1. 连接GitHub远程仓库](#connect-to-github)
	- [3.2. 与GitHub的交互](#interact-with-github)
		- [3.2.1. 远程库-本地库绑定与解绑](#link-and-unlink-for-remote-local-repo)
		- [3.2.2. 提取远程仓库](#fetch-remote-repo)
		- [3.2.3. 推送到远程仓库](#push-remote-repo)
- [4. 搭建 Git 服务器](#setup-git-server)


<h1 name="title">Git入门笔记</h1>

<a name="get-start"><h2>1. 起步 [<sup>目录</sup>](#title)</h2></a>

<a name="about-version-control"><h3>1.1. 关于版本控制 [<sup>目录</sup>](#title)</h3></a>

- **本地版本控制系统**

在硬盘上保存补丁集（补丁是指文件修订前后的变化）；通过应用所有的补丁，可以重新计算出各个版本的文件内容。

- **集中化的版本控制系统**

解决不同系统上的开发者协同工作。有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新

好处：每个人都可以在一定程度上看到项目中的其他人正在做些什么，管理员也可以轻松掌控每个开发者的权限

缺点：中央服务器的单点故障

- **分布式版本控制系统**

客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来

这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。 因为每一次的克隆操作，实际上都是一次对代码仓库的完整备份

<a name="principle"><h3>1.2. 基本工作原理 [<sup>目录</sup>](#title)</h3></a>

**直接记录快照，而非差异比较**

- **其他VCS系统**

其它大部分系统以文件变更列表的方式存储信息。 这类系统（CVS、Subversion、Perforce、Bazaar 等等）将它们保存的信息看作是一组基本文件和每个文件随时间逐步累积的差异。

<p align="center"><img src="https://git-scm.com/book/en/v2/images/deltas.png" width=800 /></p>

- **Git**

Git 不按照以上方式对待或保存数据。 反之，Git 更像是把数据看作是对小型文件系统的一组快照。 每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。 为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。

<p align="center"><img src="https://git-scm.com/book/en/v2/images/snapshots.png" width=800 /></p>

<a name="remote-repository-github"><h2>3. GitHub远程仓库 [<sup>目录</sup>](#title)</h2></a>

<a name="connect-to-github"><h3>3.1. 连接GitHub远程仓库 [<sup>目录</sup>](#title)</h3></a>

由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息，即提供本地仓库与GitHub仓库之间能够相互识别校验的SSH key

先检查一下本地是否已经存在SSH key。检查方法为在`~/.ssh`文件夹下是否存在`id_dsa.pub`文件

若没有SSH key，需要新建一个：

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

新建的SSH key需要用户提供邮箱来进行标记（是否需要与GitHub中提供的邮箱一致，目前还不清楚，所以谨慎起见，还是用GitHub中提供的邮箱）

执行该命令后，会询问你SSH key信息文件的保存位置，直接回车会保存在默认位置`~/.ssh`。然后会询问你passphrase

这样就在`~/.ssh`文件夹下生成了以下两个文件：

> - id_rsa
> - id_rsa.pub

打开并复制`id_rsa.pub	`中的信息至剪切板中，然后用电脑浏览器进入GitHub网站，进入Setting菜单，左边选择 SSH and GPG keys，然后点击 New SSH key 按钮,title 设置标题，可以随便填，粘贴在你电脑上生成的 key。

为了验证是否成功，输入以下命令：

```
$ ssh -T git@github.com
```

随后你会看到以下的警告信息

```
The authenticity of host 'github.com (IP ADDRESS)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?
```

输入yes然后回车，若输出以下信息则说明连接成功

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

从GitHub的 `Account` => `Settings` => `SSH and GPG keys` 也可以看到，原先灰色的钥匙图标被点亮激活了，变成了绿色的

<a name="interact-with-github"><h3>3.2. 与GitHub的交互 [<sup>目录</sup>](#title)</h3></a>

<a name="link-and-unlink-for-remote-local-repo"><h4>3.2.1. 远程库-本地库绑定与解绑 [<sup>目录</sup>](#title)</h4></a>

现在GitHub网站上新建一个仓库，例如新建的仓库名为：**lianm-git-test**

在本地也新建一个相同名字的仓库

```
$ mkdir lianm-git-test
$ cd lianm-git-test
$ echo "# lianm-git-test" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
```

远程库与本地仓库绑定起来，只需绑定一次即可

```
$ git remote add origin https://github.com/Ming-Lian/lianm-git-test.git

# 查看是否绑定成功
$ git remote
origin
```

若不想要保留这种绑定关系，可以进行解绑，即删除远程仓库

```
$ git remote rm [别名]
```

<a name="fetch-remote-repo"><h4>3.2.2. 提取远程仓库 [<sup>目录</sup>](#title)</h4></a>

假设你配置好了一个远程仓库，并且你想要提取更新的数据，你可以首先执行 `git fetch [alias]` 告诉 Git 去获取它有你没有的数据，然后你可以执行 `git merge [alias]/[branch]` 以将服务器上的任何更新（假设有人这时候推送到服务器了）合并到你的当前分支。 

1、从远程仓库下载新分支与数据：

```
$ git fetch origin
```

2、从远端仓库提取数据并尝试合并到当前分支：

```
$ git merge origin/master
```

<a name="push-remote-repo"><h4>3.2.3. 推送到远程仓库 [<sup>目录</sup>](#title)</h4></a>

推送你的新分支与数据到某个远端仓库命令:

```
$ git push [alias] [branch]
```

以上命令将你的 [branch] 分支推送成为 [alias] 远程仓库上的 [branch] 分支

<a name="setup-git-server"><h2>4. 搭建 Git 服务器 [<sup>目录</sup>](#title)</h2></a>

之前，我们远程仓库使用了 Github，Github 公开的项目是免费的，但是如果你不想让其他人看到你的项目就需要收费。这时我们就需要自己搭建一台 Git 服务器作为私有仓库使用。

1、创建一个git用户组和用户，用来运行git服务：

```
$ groupadd git
$ useradd git -g git
```

2、创建证书登录

收集所有需要登录的用户的公钥，公钥位于 `id_rsa.pub` 文件中，把我们的公钥导入到 `/home/git/.ssh/authorized_keys` 文件里，一行一个。

如果没有该文件创建它：

```
$ cd /home/git/
$ mkdir .ssh
$ chmod 755 .ssh
$ touch .ssh/authorized_keys
$ chmod 644 .ssh/authorized_keys
```

3、初始化Git仓库

首先我们选定一个目录作为Git仓库，假定是 `/home/gitrepo/runoob.git`，在 `/home/gitrepo` 目录下输入命令：

```
$ cd /home
$ mkdir gitrepo
$ chown git:git gitrepo/
$ cd gitrepo

$ git init --bare runoob.git
Initialized empty Git repository in /home/gitrepo/runoob.git/
```

以上命令Git创建一个空仓库，服务器上的Git仓库通常都以.git结尾。然后，把仓库所属用户改为git：

```
$ chown -R git:git runoob.git
```

4、克隆仓库

````
$ git clone git@192.168.1.20:/home/gitrepo/runoob.git
Cloning into 'runoob'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

192.168.1.20 为 Git 所在服务器 ip ，你需要将其修改为你自己的 Git 服务 ip。

这样我们的 Git 服务器安装就完成。







参考资料：

(1) [Pro Git book](https://git-scm.com/book/zh/v2)

(2) [菜鸟教程：Git](http://www.runoob.com/git/git-tutorial.html)

(3) [GitHub官方帮助文档：Connecting to GitHub with SSH](https://help.github.com/articles/connecting-to-github-with-ssh/)
