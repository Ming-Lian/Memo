<a name="content">目录</a>

[SQL入门笔记](#title)
- [运行sql文件创建表格](#exe-sql)
- [MySQL用户管理](#user-management)
- [语法](#syntax)
- [SELECT 语句](#select)
- []()




<h1 name="title">SQL入门笔记</h1>

SQL 是用于访问和处理数据库的标准的计算机语言。

数据库包括：MySQL、SQL Server、Access、Oracle、Sybase、DB2 等等。 

<a name="exe-sql"><h3>运行sql文件创建表格 [<sup>目录</sup>](#content)</h3></a>

从教程网站上下载教学用的Websites 表 SQL 文件

```
$ wget -c http://static.runoob.com/download/websites.sql
```

登录mysql，进入指定数据库，运行SQL文件

```
# 登录
$ mysql -u root -p

#创建数据库
mysql> create database testdb;

# 进入指定数据库
mysql> use testdb;

# 运行SQL文件，使用绝对路径
mysql> source /var/lib/mysql/testdb/websites.sql;
```

查看表格是否成功创建

```
mysql> show tables;
```

<a name="user-management"><h3>MySQL用户管理 [<sup>目录</sup>](#content)</h3></a>

如果你需要添加 MySQL 用户，你只需要在 mysql 数据库中的 user 表添加新用户即可。

只有MySQL的root用户才有用户管理权限

```
# 进入 mysql 数据库
mysql> use mysql;

# 添加新用户
mysql> INSERT INTO user 
          (host, user, password, 
           select_priv, insert_priv, update_priv) 
           VALUES ('localhost', 'guest', 
           PASSWORD('guest123'), 'Y', 'Y', 'Y');

# 重新载入授权表
mysql> FLUSH PRIVILEGES;
```

在添加用户时，请注意使用MySQL提供的 PASSWORD() 函数来对密码进行加密。

注意： 在添加成功新用户后，新用户还处于未激活状态，所以随后**必须执行 FLUSH PRIVILEGES 语句来重新载入授权表**。如果你不使用该命令，你就无法使用新创建的用户来连接mysql服务器，除非你重启mysql服务器。 

<a name="syntax"><h3>语法 [<sup>目录</sup>](#content)</h3></a>

**SQL 对大小写不敏感：SELECT 与 select 是相同的**。

某些数据库系统要求**在每条 SQL 语句的末端使用分号**。

<a name="select"><h3>SELECT 语句 [<sup>目录</sup>](#content)</h3></a>

SELECT 语句用于从数据库中选取数据。

结果被存储在一个结果表中，称为结果集。

- SQL SELECT 语法

```
SELECT column_name,column_name FROM table_name;
```
与
```
SELECT * FROM table_name;
```
