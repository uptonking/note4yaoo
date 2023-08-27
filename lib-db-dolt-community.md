---
title: lib-db-dolt-community
tags: [community, database, dolt]
created: 2023-08-25T21:16:51.669Z
modified: 2023-08-25T21:17:11.979Z
---

# lib-db-dolt-community

# guide

# discuss-versioning
- ## 



- ## [数据库版本管理应该如何实现？ - 知乎](https://www.zhihu.com/question/20080857/answers/updated)
- 😣 目前是把DDL、存储过程、函数、核心数据整理成SQL文件，做为baseline，提交SVN；
  - 每次修改，均记录到文件、整理成增量的sql update语句，提交svn；同时更新整体的SQL语句。
  - 很复杂，尤其是开发、内部测试、客户手上多个版本，想死的心都有了

- [用版本控制工具将数据库版本化](https://blog.csdn.net/tywo45/article/details/2480078)
  - 版本化数据库的起点——创建一个数据库Schema基线，这个基线是一些数据库脚本（包括 create table ，alter table ，drop table ，insert data ，update data ，delete data等）。
  - 这些脚本可以位于同一.sql文件中，也可根据其它规划分别位于不同文件中，例如将视图脚本，初始化数据脚本，建表脚本分别置于不同的文件中。
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Dolt performance comparison to postgres and mysql](https://github.com/dolthub/dolt/issues/6536)
- I suspect there might be two actual issues at play: one causing our client to behave slowly, and another slowing down the actual execution of the query. (Hence why connecting with a mysql client is approximately as fast as running the query locally.)

- ## [Document Version Control · frappe-erp](https://github.com/frappe/frappe/issues/22075)
