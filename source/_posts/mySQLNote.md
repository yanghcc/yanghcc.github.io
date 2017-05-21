---
title: mySQLNote
date: 2017-02-20 21:46:39
tags:
      - mySQL
categories: others
---
## mySQL常用命令

选择数据库：`use databaseName;`
显示数据库：`show databases;`
查看数据／：`select * from tableName;`
创建数据库：`create databaseName (
列名 数据类型／／创建table时
);`
删除数据库：`drop databaseName;`
删除数据表：`drop table tableName;`
插入数据：`insert into target_tbl (字段1-n) values(
‘123123’,’123’,’123’,…,’n'
)`
例子1：单表的MySQL UPDATE语句：
```
   UPDATE [LOW_PRIORITY] [IGNORE] tbl_name SET col_name1=expr1 [, col_name2=expr2 ...] [WHERE where_definition] [ORDER BY ...] [LIMIT row_count]
```
例子2：多表的UPDATE语句：
```
UPDATE [LOW_PRIORITY] [IGNORE] table_references SET col_name1=expr1 [, col_name2=expr2 ...] [WHERE where_definition]
```
命令：alter table 表名 add字段 类型 其他;
例如：在表MyClass中添加了一个字段passtest，类型为int(4)，默认值为0
```
   mysql> alter table MyClass add passtest int(4) default '0'
```
加索引
   mysql> alter table 表名 add index 索引名 (字段名1[，字段名2 …]);
```
例子： mysql> alter table employee add index emp_name (name);
```
加主关键字的索引
  mysql> alter table 表名 add primary key (字段名);
```
例子： mysql> alter table employee add primary key(id);
```
加唯一限制条件的索引
   mysql> alter table 表名 add unique 索引名 (字段名);
```
例子： mysql> alter table employee add unique emp_name2(cardnumber);
```
删除某个索引
    mysql> alter table 表名 drop index 索引名;
```
例子： mysql>alter table employee drop index emp_name;
```
增加字段：
```
mysql> ALTER TABLE table_name ADD field_name field_type;
```
修改原字段名称及类型：
```
mysql> ALTER TABLE table_name CHANGE old_field_name new_field_name field_type;
```
删除字段：
```
MySQL ALTER TABLE table_name DROP field_name;
```
命令：rename table 原表名 to 新表名;
```
例如：在表MyClass名字更改为YouClass
   mysql> rename table MyClass to YouClass;
```