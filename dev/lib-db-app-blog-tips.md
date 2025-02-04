---
title: lib-db-app-blog-tips
tags: [blog, database, dev-xp]
created: 2023-10-26T17:23:29.916Z
modified: 2023-10-28T07:03:58.197Z
---

# lib-db-app-blog-tips

# guide

# blogs-db-dev-xp

## 📝 [42 things I learned from building a production database | mahesh’s blog_202110](https://maheshba.bitbucket.io/blog/2021/10/19/42Things.html)

- 
- 
- 

## 👥🔥🔥 [Things I learned from building a production database | Hacker News_202111](https://news.ycombinator.com/item?id=29322515)

- 
- 
- 

## 📝 [Things I Wished More Developers Knew About Databases_202004](https://rakyll.medium.com/things-i-wished-more-developers-knew-about-databases-2d0178464f78)

- You are lucky if 99.999% of the time network is not a problem.
- ACID has many meanings.
- Each database has different consistency and isolation capabilities.
- Optimistic locking is an option when you can’t hold a lock.
- There are anomalies other than dirty reads and data loss.
- My database and I don’t always agree on ordering.
- Application-level sharding can live outside the application.
- AUTOINCREMENT’ing can be harmful.
- Stale data can be useful and lock-free.
- Clock skews happen between any clock sources.
- Latency has many meanings.
- Evaluate performance requirements per transaction.
- Nested transactions can be harmful.
- Transactions shouldn’t maintain application state.
- Query planners can tell a lot about databases.
- Online migrations are complex but possible.
- Significant database growth introduces unpredictability.

## 👥🔥🔥 [Things I wished more developers knew about databases | Hacker News_202004](https://news.ycombinator.com/item?id=22942278)

- 
- 
- 

- Go code often reinvents/reimplements a lot of things from scratch, reintroducing problems that have been addressed long ago in other systems. It's like this new trend, let's rewrite everything in Go to be cool. Financially makes little to no sense.
  - Let’s not just target Go with that sentiment, it applies almost universally.how is anyone supposed to learn, if not from their mistakes?

- 
- 

## 📝 [Relational Databases Explained_202206](https://architecturenotes.co/things-you-should-know-about-databases/)

- 
- 
- 

## 👥🔥🔥 [Things to know about databases | Hacker News_202206](https://news.ycombinator.com/item?id=31895623)

- 
- 
- 

# blog-design

## [Data modeling in SQL: A Beginner's Guide_202305](https://medium.com/@guowili16/data-modeling-in-sql-584e56e3b6ff)

## [Ten Common Database Design Mistakes - Simple Talk](https://www.red-gate.com/simple-talk/databases/sql-server/database-administration-sql-server/ten-common-database-design-mistakes/)

### Poor design/planning

### Ignoring normalization

### Poor naming standards

### Lack of documentation

### One table to hold all domain values

### Using identity/guid columns as your only key

### Not using SQL facilities to protect data integrity

### Not using stored procedures to access data

### Trying to build generic objects

### Lack of testing

### 👥 discussions

- EAV tables:
  - Yuk, hate them - think they are better off using a NoSQL solution instead, I believe there are all kinds of options that stop one breaking the data integrity notions of a sql database for generic tables.
# more
- [BeyondStorage: why we failed](https://xuanwo.io/2023/01-beyond-storage-why-we-failed/)
  - 介绍了 BeyondStorage 开源社区的失败并分享了 #OpenDAL 在此基础上的经验教训
  - BeyondStorage 构建 go-storage 是为了满足迁移服务的需求，而迁移服务的需求来自于 go-storage 能力的自然延伸。不难发现这套逻辑中出现了一个可怕的循环，链条中完全没有真实用户的参与，项目从发展伊始就在朝着错误的方向狂奔。
  - BeyondStorage 失败的最直接原因是失去了最大金主：青云科技。
  - OpenDAL 最幸运的地方在于它孵化自 Databend 的真实场景。Databend 持续不断地提出新需求，这些需求帮助我判断需求的必要性、调整任务优先级并修正错误假设。

- [Reverse Engineering Existing Databases with Entity Framework Core _202307](https://blog.jetbrains.com/dotnet/2023/07/20/reverse-engineering-existing-databases-with-entity-framework-core/)
  - You’ll likely need to develop on top of or extend existing databases in the Enterprise world.
  - With EF Core’s reverse engineering tools, you can avoid the complexity of modeling a large database schema by hand and trust what EF Core sees in your database
  - However, reverse engineering has some limitations, including logical concepts like table inheritance, owned types, and table splitting.
