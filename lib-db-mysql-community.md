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

# discuss-mysql-v8
- ## 

- ## What makes MySQL 8.0 slower than 5.6 on the Insert Benchmark?
- https://twitter.com/MarkCallaghanDB/status/1729189298849874001
  * it isn't a few new hot spots
  * it is new memory system stress distributed throughout the code (more misses, loads, stores for cache and TLB)
  * much of the new overhead arrives in pre-GA 5.7 and pre-GA 8.0.

# discuss-latest
- ## 

- ## 

- ## Introducing JavaScript support in MySQL_202312
- https://twitter.com/OnlyXuanwo/status/1736439160402243750
  - Enterprise Edition only
  - Presented in Percona Live 2018. Finally, although it seems it's not OSS
- I wish for this feature to be added to MySQL Community Edition. Shifting business logic to the front end is a trend, and the ideal future architecture would be front end plus service-oriented databases. This could mark MySQL's move towards service orientation.
- I didn't experience the era when stored procedures were popular. Are they truly useful? It seems that today's frontend developers prefer to manage everything on their own.
  - I don't like procedures either; they lack capabilities such as version control and canary releases that code has. I believe the front end simply desires a user-friendly SaaS database.

# discuss
- ## 

- ## 

- ## 

- ## 美团做的这个MySQL的优化也太极限了
- https://twitter.com/changwei1006/status/1722343947459330417
  - [Intel PAUSE指令变化影响到MySQL的性能，该如何解决？ - 掘金](https://juejin.cn/post/6844904129626636302)
- 还不够极限，既然他已经 target 具体 intel 处理器，sapphire rapids 上还可以用 tpause 指令来替代这种多次 pause 在自旋锁场景下。能够更好优化 CPU 的 thermal 管理从而让锁的另一侧的性能提升，能有更好的性能。dpdk 里就是这么做的。

- ## GitHub 使用MySQL的原因😂：
- https://twitter.com/Hooopo/status/1629399543740788742
  - “我们几乎早就从 MySQL 迁移到 Postgres，甚至有一个分支正在运行，但我为私人消息功能编写的一些可怕的 SQL 查询在 Postgres 中不起作用。所以，MySQL留了下来。”
  - I remember there being a "GROUP BY" from hell that I had trouble rewriting, and eventually gave up. Probably was using some MySQL-specific features.
