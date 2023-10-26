---
title: lib-db-mysql-community
tags: [community, mysql]
created: 2022-06-13T02:59:45.181Z
modified: 2022-06-13T03:00:06.041Z
---

# lib-db-mysql-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-vendors
- ## 

- ## 🔥 [Azure dropping database support for MariaDB. Users advised to migrate to MySQL | Hacker News_202309](https://news.ycombinator.com/item?id=37715209)
- 
- 
- 

- ## 🔥 [Partitioning GitHub’s relational databases to handle scale | Hacker News_202109](https://news.ycombinator.com/item?id=28678647)
- 
- 

- Why not to migrate to the PostgreSQL which can handle more data and load than MySQL or MariaDB? It's also better at partitioning.
  - Migrating is a huge, difficult, expensive project at Github's scale -- almost as bad as a rewrite
- How much data and load Postgres can handle vs MySQL is determined by lots of variables. It's neither absolute nor consistent. It depends more on database and infrastructure design than on the underlying RDBMS.
- The best reason to choose Postgres over MySQL is not hardware efficiency but rather developer efficiency, although some projects get both.

- Uber once chose to switch from postgres to mysql, for performance reasons. There was a lot of debate and discussion on HN about it. I think there is enough complexity in either system, that you can't make generalizations that a given system can "can handle more data and load".

- ## 🔥 [PlanetScale – Database for Developers | Hacker News_202105](https://news.ycombinator.com/item?id=27197873)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## GitHub 使用MySQL的原因😂：
- https://twitter.com/Hooopo/status/1629399543740788742
  - “我们几乎早就从 MySQL 迁移到 Postgres，甚至有一个分支正在运行，但我为私人消息功能编写的一些可怕的 SQL 查询在 Postgres 中不起作用。所以，MySQL留了下来。”
  - I remember there being a "GROUP BY" from hell that I had trouble rewriting, and eventually gave up. Probably was using some MySQL-specific features.
