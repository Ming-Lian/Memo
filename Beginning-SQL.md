<a name="content">目录</a>

[SQL入门笔记](#title)
- [运行sql文件创建表格](#exe-sql)
- [MySQL之权限管理](#authorization-management)
	- [新增用户](#user-add)
	- [修改用户信息](#user-mod)
	- [删除用户](#user-delect)
	- [权限分配](#permission-assign)
	- [查看权限](#list-permission)
- [语法](#syntax)
- [创建 MySQL 表](#create-table)
- [SELECT 语句](#select)
	- [WHERE 子句](#where)
	- [结果集排序](#sort)
- [INSERT INTO 语句](#insert)
- [UPDATE 语句](#update)
- [DELETE 语句](#delete)


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

<a name="authorization-management"><h3>MySQL之权限管理 [<sup>目录</sup>](#content)</h3></a>

<a name="user-add"><h4>新增用户 [<sup>目录</sup>](#content)</h4></a>

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

<a name="user-mod"><h4>修改用户信息 [<sup>目录</sup>](#content)</h4></a>

用到 [UPDATE语句](#update)

```
 mysql> UPDATE `user` SET Password=PASSWORD("123456") WHERE Host='10.155.123.55' AND User='kaka';  
```

<a name="user-delete"><h4>删除用户 [<sup>目录</sup>](#content)</h4></a>

用到 [DELETE语句](#delete)

```
mysql> DELETE FROM `user` WHERE Host='10.155.123.55' AND User='kaka';
```

<a name="permission-assign"><h4>权限分配 [<sup>目录</sup>](#content)</h4></a>

使用 GRANT语句

```
GRANT 权限 ON 数据库.* TO 用户名@'登录主机' IDENTIFIED BY '密码' 
```

```
权限：  
   ALL,ALTER,CREATE,DROP,SELECT,UPDATE,DELETE  
   新增用户：权限为USAGE,即为："无权限",想要创建一个没有权限的用户时,可以指定USAGE  
数据库：  
     *.*              表示所有库的所有表  
     mylove.*         表示mylove库的所有表  
     mylove.loves     表示mylove库的loves表   
用户名：  
     MySQL的账户名  
登陆主机：  
     允许登陆到MySQL Server的客户端ip  
     '%'表示所有ip  
     'localhost' 表示本机  
     '10.155.123.55' 特定IP  
密码：  
      MySQL的账户名对应的登陆密码  
```

例如，给用户kaka分配test数据库下user表的查询select权限：

```
mysql> GRANT SELECT ON test.user TO kaka@'10.155.123.55' IDENTIFIED BY '123456';
```

<a name="list-permission"><h4>查看权限 [<sup>目录</sup>](#content)</h4></a>

```
mysql> show Grants for 'kaka'@'10.155.123.55';  
+-----------------------------------------------------------------------------------------------------------------+  
| Grants for kaka@10.155.123.55                                                                                   |  
+-----------------------------------------------------------------------------------------------------------------+  
| GRANT USAGE ON *.* TO 'kaka'@'10.155.123.55' IDENTIFIED BY PASSWORD '*6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9' |  
| GRANT SELECT ON `test`.`user` TO 'kaka'@'10.155.123.55'                                                         |  
+-----------------------------------------------------------------------------------------------------------------+  
```


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

- SELECT DISTINCT：用于返回唯一不同的值。

```
SELECT DISTINCT column_name,column_name FROM table_name;
```

<a name="where"><h4>WHERE 子句 [<sup>目录</sup>](#content)</h4></a>

WHERE 子句用于提取那些满足指定标准的记录。

```
SELECT column_name,column_name
FROM table_name
WHERE column_name operator value;
```

实例：

```
SELECT * FROM Websites WHERE country='CN';
```

SQL 使用单引号来环绕文本值，如果是数值字段，请不要使用引号。

<a name="sort"><h4>结果集排序 [<sup>目录</sup>](#content)</h4></a>

```
SELECT column_name,column_name
FROM table_name
ORDER BY column_name,column_name ASC|DESC;
```

ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

<a name="insert"><h3>INSERT INTO 语句 [<sup>目录</sup>](#content)</h3></a>

INSERT INTO 语句可以有两种编写形式。

- 第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```

- 第二种形式需要指定列名及被插入的值，用于在指定的列插入值：

```
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```

若表中有 id 列，则 id 列是自动更新的，表中的每条记录都有一个唯一的数字。

<a name="update"><h3>UPDATE 语句 [<sup>目录</sup>](#content)</h3></a>

用于 更新/修改 表中的记录。

```
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```

**警告！**

执行没有 WHERE 子句的 UPDATE 要慎重，再慎重。

<a name="delete"><h3>DELETE 语句 [<sup>目录</sup>](#content)</h3></a>

```
DELETE FROM table_name
WHERE some_column=some_value;
```

**请注意 SQL DELETE 语句中的 WHERE 子句！**

WHERE 子句规定哪条记录或者哪些记录需要删除。如果您省略了 WHERE 子句，所有的记录都将被删除！


