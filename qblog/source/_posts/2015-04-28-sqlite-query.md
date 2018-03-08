---
date: 2015-04-28 17:23:12
layout: post
title: sqlite3的使用1-操作
categories: 日志
tags: sqlite3
---
sqlite3的基本用法
<!--more-->
### sqlite3的操作


```
select id from foods where name='jujyfruit'
| 动词 | 主语        | 谓语                 |


创建表
--------------------------------------------
==语法==
create [temp|tempname] table table_name (column_definitions [, constraints]);

==说明==
使用temp或temporay关键字声明的表是临时表,这种表是临时的-只存活于当前对话,一旦连接断开,就会被自动销毁

==示例==
create table contacts (id integer, primary key, 
						name text not null collate nocase,
						phone text not null default 'UNKNOWN',
						unique (name, phone));




修改表
-------------------------------------------
==语法==
alter table table_name { rename to name | add column column_def }

==说明==
花括号表示选择其中一项,实际使用不需要花括号,即要么重命名,要么添加

==示例==
sqlite> alter table contacts
		add column email text not null default '' collate nocase;
sqlte> .schema contacts




select
-------------------------------------------

选择操作(一种关系)的输出可以是另一个select语句的输入,如:
select name from (select name, type_id from (select * from foods));
里层的结果作为次层的输入

sql命令的通用形式如下:

select [distinct] heading
from tables
group by columns
having predicate
order by columns
limit count, offset;

常用形式:
select heading from tables where predicate;

示例1:
sqlite> select id, name from food_types;

示例2:
sqlite> select * from dogs where color='purple' and grin = 'toothy';

操作符,包括*+- == != IN AND or等
操作符使用一个或多个输入并产生一个新值作为输出, 只所以叫'操作符',是因为它完成某种操作并产生结果.
eg:
x = count(episodes.name) 
sqlite> select * from foods where name='july' and type_id=9;


LIKE
sqlite> select id, name from foods where name like 'J%';

上例中表示匹配以J开头的食品
模式中的百分号(%)相当于正则中的*,表示0个或多个字符匹配
下划线(_)可与任意单个字符匹配,相当于正则中的+
sqlite> select id, name from foods where name like '%ac%p%';
通过将%放入左边或右边来进行匹配

NOT
sqlite> select id, name from foods where name like '%ac%p%' and name not like '%Sch%';

GLOB
同like,不过匹配是大小写敏感,并且使用'*'来匹配0到多个,'?'匹配单一字符

限定和排序

sqlite> select * from food_types order by id limit 1 offset 1;
sqlite> select * from foods where name like 'B%' order by type_id desc, name limit 10;

sqlite> select * from foods where name like 'B%' order by type_id desc, name limit 1 offset 2;
等于下列,使用缩写时,offset总是优先于limit,不过个人感觉还是不要写缩写
sqlite> select * from foods where name like 'B%' order by type_id desc, name limit 2, 1;


limit:限制结果集大小
offset:限制结果集范围
注意:limit/offset不会加速查询

Function和聚合
upper(), lower(), abs(), count()

sqlite> select id, upper(name), length(name) from foods where type_id =1 limit 10

结果
id  upper(name) length(name)
--  ----------  ------------
1   BAGELS      6
2   BAGELS, RAI 14

函数可以是任意表达式的一部分,所以函数也可以用在WHERE子句中:
sqlite> select id, upper(name), length(name) from foods where length(name) < 5 limit 5;

聚合是一类特殊的函数,它从一组记录中计算聚合值,标准的聚合函数包括sum(), avg(), count(), min(), max(),

示例:
sqlite> select count(*) from foods where type_id = 1;
count()返回关系中所有行的数目

sqlite> select avg(length(name)) from foods;

分组:
聚合的主要部分就是分组,聚合不只是能够将计算整个结果集的聚合值,黑啊可以吧结果分为多个组,然后计算每个组的聚合值
sqlite> select type_id from foods group by type_id;
group by查询到结果,然后将结果分为共享某个字段上同等值的小组,这些组再传递给select子句.

sqlite> select type_id, count(*) from foods group by type_id;
type_id count(*)
------- -------
1       47
2       15

group by 使用类似的值创建分组,但是没有在select子句处理前过滤这些组,having具备这以功能, having 是一个可以应用到group by的断言,having的断言是针对聚合值的
sqlite> select type_id, count(*) from foods group by type_id having count(*) < 20;

去重复:
distinct
sqlite> select distinct type_id from foods

多表连接join:
连接是多表数据工作的关键,它是select命令的第一个操作,连接操作的结果作为输入,供select语句的其他部分(过滤)处理.

sqlite> select foods.name food_types.name from foods, food_types where foods.type_id=food_types.id limit 10

备注:
使用table_name.column_name的方式,区分哪个字段是那个表的

内连接(求交集):
sqlite> select * from foods inner join food_types on foods.id == food_types.id;

左外连接:
sqlite> select * from foods left outer join foods_episodes on foods.id= foods.episodes.food_id;

举例:
有张表是会员表(左表),有张表是状态表,左连接会员表查询所有会员的状态是吧
如果会员状态不存在就Null,否则将右表的会员状态加到左表结果去


名称和别名:
select foods.name, food_types.name from foods, food_types where foods.type_id = food_types.id limit 10;

等于

select f.name, t.name from foods f, food_types t where f.type_id = t.id limit 10

=说明=
foods表取别名f, food_types取别名t,方便某些表明比较长时重复输入长表名

sqlite> select f.name as food, e1.name e1.session.e2.anme, e2.season 
        from episodes e1, foods_episoeds f1, foods f, epsiondes e2, 
        foods_episodes fe2
        where 
        -- Get foods in season 4
        (e1.id = fe1.epsode_id and e1.season = 4) and fe1.food_id = f.id
        -- link foods with all other episodes
        and (fe1.food_id = fe2.food_id)
        -- link with their respective episodes and filter out e1's season
        and (fe2.episode_id = e2.id and e2.season ! = e1.season)
        oreder by f.name
        
 food      name        season    name      season
 Bool      The Shoes   4         The abc   1
 
 =说明=
 as关键词是可选的,但倾向保留,不容易混淆
 
 
子查询:
IN 操作符是一个双目操作,输入一个值和一列值,如果输入的单值存在与列值中,返回真,否则返回假
sqlite> select 1 in (1, 2, 3)
1
sqlite> select 2 in (3, 4, 5)
0

sqlite> select count(*) from foods where type_id in (1, 2)
可以写成这样
sqlite> select count(*) from foods where type_id in (select id from food_types where name='Ba' or name ='bc');
 
复合查询:
* 涉及的关系字段数目必须相同
* 只能有一个order by子句,并且处于复合查询的最末尾, 对联合结果进行排序
* 
union:联合两个Select语句的结果,会消除重复,不消除采用union all
intersect:求交集
expect:求在a不在b的结果
 
null
使用is null 或者 is not null来判断,不要使用== null,将什么都查不到




```

###修改数据
1. 插入数据

insert into table (column_list) values (value_list);;
变量table指明数据插入到哪个表中.变量column_list使用逗号分隔的字段名称,这些字段必须是表中存在的.变量value_list是用逗号分隔的值列表, 这些值与column_list的字段一一对应.
插入一行:
sqlite> insert into foods (name, type_id) vlaues ('cxxx', 1);
sqlite> insert into foods values(NULL, 1, 'xxx)

sqlite可以使用last_insert_rowid()获取最后插入的rowid

2. 更新记录

update table set update_list where predicate;
update_list 是一个或多个"字段赋值"的列表,字段赋值的格式为column_name=value,
sqlite> update foods set name='Cxx' where name = 'xxx';

3. 删除记录

delete from table where predicate;

delete from foods where name='chonljl';

###完整性

unique
primary key
not null
foreign key
check 
collate
default

示例:
id integer primary key autoincreament
name text not null collate nocase  //大小写不敏感
create table times(id int, date not null default current_date,
time not null default current_time,
timestamp not null default current_timestamp);

current_date YYYY-MM-DD
current_time HH:MM:SS
current_timestamp YYYY-MM-DD HH:MM:SS

create table contact (id integer primary key, unique(name, phone), check(length(phone)>=7));

所有字段的check约束都在修改发生前评估,要想 修改成功,所有约束的表达式必须判断为真.

外键约束:
create table table_name
(column_definition references foreign_table(column_name)
on {delete|update} integerity_action
[not] deferrable[intially {deferred|immediate}.]
-);

示例:

```
create table food_types (
	id integer primary key,
	name text
);

create table foods (
	id integer primary key,
	type_id integer,
	name text
);

create table foods (
	id integer primary key,
	type_id integer references food_types(id)
	on delete restrict
	deferrable initially deffered,
	name text
);

set null, 如果父值被删除或者不存在了, 剩余的子值改为null
set default, 如果父值被删除或者不存在了,剩余的子值将修改为默认值
cascade:更新父值时,更新所以u匹配的子值,删除父值时,删除所有的子值
restrict:更新或删除父值可能会出现孤立的子值,从而阻止事务
no action:不干涉执行,只是观察

deferrable控制定义的约束是立即强制实施还是延迟到整个事务结束


```




