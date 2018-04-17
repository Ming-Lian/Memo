<a name="content">目录</a>

[SQL入门笔记](#title)
- [运行sql文件创建表格](#exe-sql)
- [MySQL用户管理](#user-management)
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

<a name="create-table"><h3>创建 MySQL 表 [<sup>目录</sup>](#content)</h3></a>

```
CREATE TABLE MyGuests (
id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
firstname VARCHAR(30) NOT NULL,
lastname VARCHAR(30) NOT NULL,
email VARCHAR(50),
reg_date TIMESTAMP
) 
```

数据类型指定列可以存储什么类型的数据

在设置了数据类型后，你可以为每个列指定其他选项的属性：

> - NOT NULL - 每一行都必须含有值（不能为空），null 值是不允许的。
> - DEFAULT value - 设置默认值
> - UNSIGNED - 使用无符号数值类型，0 及正数
> - AUTO INCREMENT - 设置 MySQL 字段的值在新增记录时每次自动增长 1
> - PRIMARY KEY - 设置数据表中每条记录的唯一标识。 通常列的 PRIMARY KEY 设置为 ID 数值，与 AUTO_INCREMENT 一起使用。

查看表格的列信息

```
mysql> DESC tbname;
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


