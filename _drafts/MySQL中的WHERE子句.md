---
title: MySQL中的WHERE子句
toc: false
date: 2019-06-30 17:09:54
category: MySQL
tags: MySQL
---

MySQL中的WHERE子句

<!--more-->

语法

```mysql
SELECT field1,field2,...fieldN FROM table_name1,table_name2,... [WHERE condition1 [AND [OR]]conditon2...
```

+ 可以使用一个或多个表，表之间用`,`分开，并使用WHERE语句来设定查询条件
+ 可以使用AND或OR指定一个或多个条件
+ WHERE可运用在查询或DELETE或UPDATE命令中

```mysql
SELECT * from tb_book WHERE book_name="learn java"
```

+ MySQL的WHERE子句的字符串比较是不区分大小写的，可以使用BINATY关键字来设置区分大小写

```mysql
SELECT * from tb_book WHERE BINARY book_name="learn java"
```

过滤条件操作符有：

```my
=,<>,!=,<,<=,>,>=,BETWEEN AND,IS NULL
```

