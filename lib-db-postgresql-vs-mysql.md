---
title: lib-db-postgresql-vs-mysql
tags: [comparison, database, mysql, postgresql]
created: 2020-12-18T13:23:08.190Z
modified: 2023-11-01T14:13:41.390Z
---

# lib-db-postgresql-vs-mysql

# guide

- mysql特点
  - 支持修改更新索引

- postgresql特点
  - 支持并行创建索引

- [PostgreSQL vs. MySQL](https://www.postgresqltutorial.com/postgresql-vs-mysql/)
  - PG: MIT-style license; MY: GPL
  - PG-NO && MY-YES
    - Unsigned integer
    - Multiple storage engines e.g., InnoDB and MyISAM
  - PG-YES && MY-NO
    - Identity Column
    - Analytic functions
    - IP address data type
    - Materialized views
    - Table inheritance
    - FULL OUTER JOIN
    - INTERSECT
    - EXCEPT
    - Partial indexes
    - Bitmap indexes
    - Expression indexes

- [mysql 和 postgresql哪个更适合互联网企业？](https://www.zhihu.com/question/324036100/answers/updated)
  - pg除了不能针对单个数据库进行备份恢复，复制，即时点恢复(这给日常维护带来了很大的麻烦)，其它完美。我一个服务器上都有几十上百个数据库。
    - pg开发爽，维护不爽，sql server维护起来真的很方便

- [PostgreSQL 与 MySQL 相比，优势何在？](https://www.zhihu.com/question/20010554/answers/updated)
  - pg有很多数据库的新特性，很多学术的都会用postgresql
# dev

# discuss-mysql-pg

- ## 

- ## 

- ## 🆚️ Old Postgres and old MySQL had similar performance on sysbench. 
- https://twitter.com/MarkCallaghanDB/status/1719500763666452654
  - But modern Postgres is usually faster than modern MySQL because Postgres has avoided CPU perf regressions over time.
  - [Small Datum: Postgres vs MySQL: the impact of CPU overhead on performance](https://smalldatum.blogspot.com/2023/10/postgres-vs-mysql-impact-of-cpu.html)
- Do you mean that new features introduced perf regression in MySQL?
  - Yes. Have seen the same in other DBMS too, just not in Postgres.

- ## 🆚️🔥 [Ask HN: What could a modern database do that PostgreSQL and MySQL can't | Hacker News_202109](https://news.ycombinator.com/item?id=28425379)
- 
- 
- 

# more
- [postgresql也很强大，为何在中国大陆，mysql成为主流](https://www.zhihu.com/question/31955622/answers/updated)
