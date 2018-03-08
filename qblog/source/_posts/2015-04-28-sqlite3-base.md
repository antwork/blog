---
date: 2015-04-28 16:31:12
layout: post
title: sqlite3的使用
categories: 日志
tags: sqlite3
---

### sqlite3的使用

创建数据库(调用该方法,如果数据库中不存在该数据并不会立即创建,直到数据库内部创建一些内容,如表或试图才会创建该数据库):	

```
$ sqlite3 test.db 
```

创建表:	

```
sqlite> create table test (id integer primary key, value text);
```

插入数据(名为id的主键列,该列默认具备自动增长的属性,插入时不提供该列,sqlite会查找该列下一值后自动产生一个):	

```
sqlite> insert into test(id, value) values(1, 'eenie');
sqlite> insert into test(id, value) values(2, 'meenie');
sqlite> insert into test(value) values('min');
sqlite> insert into test(value) values('mo');
```

修改输出配置并查询: 	

```
sqlite> .mode column
sqlite> .headers on
sqlite> select * from test;
----------------------------------------------------------------------
id          value
----------  ----------
1           value1
2           value2
3           value3
4           value4
```

添加索引和视图	

```
sqlite> create index test_idx on test(value);
sqlite> create view schema as select * from sqlite_master;

```

退出:	

```
sqlite> .exit
```

获取数据库的Schema信息

获取所有的表和视图列表
```
sqlite> .tables

--------------

schema test
```

获取创建的表和试图schema	

```
sqlite> .indices test

--------------------------------

test_idx

查看一个表的结或试图的定义语句(DDL)
sqlite> .schema test
	
-------------------------------

CREATE TABLE test (id integer primary key, value text);
CREATE INDEX test_idx on test (value);

不传table名称获取所有数据库队形(table, index, view, triger)的定义语句
sqlite> .schama

-------------------------------

CREATE TABLE test (id integer primary key, value text);
CREATE VIEW schema as select *from sqlite_master;
CREATE INDEX test_idx on test (value);
```		

####导出数据
(将整个数据库导出为数据库定义语言(DDL)和书库操作语言(DML)命令,适合重新创建数据库对象和其中的数据库,默认输出到屏幕,使用.dump[filename]命令,将所有输出重定向到指定的文件中, 若要恢复输出到屏幕,只需要执行.out stdout):	

```
sqlite> .output file.sql
sqlite> .dump
sqlite> .output stdout

-------------------------
file.sql内容:

PRAGMA foreign_keys=OFF;
BEGIN TRANSACTION;
CREATE TABLE test (id integer primary key, value text);
INSERT INTO "test" VALUES(1,'value1');
INSERT INTO "test" VALUES(2,'value2');
INSERT INTO "test" VALUES(3,'value3');
INSERT INTO "test" VALUES(4,'value4');
CREATE INDEX test_idx on test (value);
CREATE VIEW schema as select *from sqlite_master;
COMMIT;

```	

###导入数据
1. 文件由sql语句构成, 可以使用.read命令导入(执行)文件中包含的命令
2. 文件包括由逗号或者其他分隔符组成,可使用.import[file][table]命令
查询当前默认的分隔符	

```
     echo: off
  explain: off
  headers: off
     mode: list
nullvalue: ""
   output: stdout
separator: "|"
    stats: off
    width:
```

```
sqlite> drop table test;
sqlite> drop view schema;
sqlite> .read file.sql
```

### 备份数据库

```
slqite3 test.db .dump > test.sql

sqlite3 test.db < test.sql
```

### 注意

1. sqlite中默认的字符常量值是大小写敏感的,因此'Mike'与'mike'是不同的
2. sql不区分关键词和标识符的大小写,详见注意2示例
3. sqlite支持以单引号或双引号界定字符串,但是建议只使用单引号,对于已存在单引号,采用连续两个单引号,如 Kenny's chicken 要改成 'Kenny''s chicken'
4. 单行注释采用两个连续连字符'--'
5. 多行注释采用 /* */

注意2示例:

```
下列语句具有相同效果
SELECT * from foo;
seleCt * frOm FOO;
```

?? 1. 数据库中的类型

*.mode column效果展示:* 用列分隔数据

```
0||Good News Bad News
1|1|Male Unbonding
2|1|The Stake Out
3|1|The Robbery
...

sqlite> .mode column
0                       Good News Bad News
1           1           Male Unbonding
2           1           The Stake Out
3           1           The Robbery

```

*.header on* 带标题

```
0||Good News Bad News

之后:

id          season      name
----------  ----------  ------------------
0                       Good News Bad News

```

