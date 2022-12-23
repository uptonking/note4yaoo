---
title: lib-db-sql
tags: [database, sql]
created: 2020-12-18T05:02:42.251Z
modified: 2020-12-18T05:02:58.499Z
---

# lib-db-sql

# guide

# blogs

## [DQL、DML、DDL、DCL的概念与区别](https://blog.csdn.net/tomatofly/article/details/5949070)

1974年-----由Boyce和Chamberlin提出，当时称SEQUEL。
1976年-----IBM公司的Sanjase研究所在研制RDBMS SYSTEM R时改为SQL。
1979年-----ORACLE公司发表第一个基于SQL的商业化RDBMS产品。
1982年-----IBM公司出版第一个RDBMS语言SQL/DS。
1985年-----IBM公司出版第一个RDBMS语言DB2。
1986年-----美国国家标准化组织ANSI宣布SQL作为数据库工业标准。

- SQL是一个标准的数据库语言，是面向集合的描述性非过程化语言，简单易学易维护
  - 它是非过程性语言，即大多数语句都是独立执行的，与上下文无关，
  - 而绝大部分应用都是一个完整的过程，显然用SQL完全实现这些功能是很困难的。
  - 所以大多数数据库公司为了解决此问题，作了如下两方面的工作：
  - (1)扩充SQL，在SQL中引入过程性结构；
  - (2)把SQL嵌入到高级语言中，以便一起完成一个完整的应用。

- SQL语言共分为四大类：数据查询语言DQL，数据操纵语言DML，数据定义语言DDL，数据控制语言DCL。

1. 数据查询语言DQL
数据查询语言DQL基本结构是由SELECT子句，FROM子句，WHERE子句组成的查询块：
SELECT <字段名表>
FROM <表或视图名>
WHERE <查询条件>

2. 数据操纵语言DML
数据操纵语言DML主要有三种形式：
1) 插入：INSERT
2) 更新：UPDATE
3) 删除：DELETE

3. 数据定义语言DDL
数据定义语言DDL用来创建数据库中的各种对象-----表、视图、索引、同义词、聚簇等如：
CREATE TABLE/VIEW/INDEX/SYN/CLUSTER
DDL操作是隐性提交的！不能rollback

4. 数据控制语言DCL
数据控制语言DCL用来授予或回收访问数据库的某种特权，并控制数据库操纵事务发生的时间及效果，对数据库实行监视等。如：
1) GRANT：授权。
2) ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点。
回滚命令使数据库状态回到上次最后提交的状态。其格式为：
SQL>ROLLBACK; 
3) COMMIT [WORK]：提交。
在数据库的插入、删除和修改操作时，只有当事务在提交到数据库时才算完成。
在事务提交前，只有操作数据库的这个人才能有权看到所做的事情，别人只有在最后提交完成后才可以看到。
提交数据有三种类型：显式提交、隐式提交及自动提交。
(1) 显式提交
用COMMIT命令直接完成的提交为显式提交。其格式为：
SQL>COMMIT；

(2) 隐式提交
用SQL命令间接完成的提交为隐式提交。这些命令是：
ALTER，AUDIT，COMMENT，CONNECT，CREATE，DISCONNECT，DROP，
EXIT，GRANT，NOAUDIT，QUIT，REVOKE，RENAME。

(3) 自动提交
若把AUTOCOMMIT设置为ON，则在插入、修改、删除语句执行后，
系统将自动进行提交，这就是自动提交。其格式为：
SQL>SET AUTOCOMMIT ON；

# more
