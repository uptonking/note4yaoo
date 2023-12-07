---
title: lib-db-app-community-devops
tags: [community, database, devops]
created: 2023-10-26T18:47:03.513Z
modified: 2023-10-26T18:47:22.664Z
---

# lib-db-app-community-devops

> about database migration/upgrade

# guide

# discuss-stars
- ## 

- ## 
# discuss-change-schema
- ## 

- ## 

- ## Problem: We need to rename a DB column, but we want to avoid a breaking change. Solution:
- https://twitter.com/housecor/status/1729893167812555124
  1. Add new column (Ticket 1)
  2. Update all code to reference new column (Ticket 2)
  3. Release. Now no code references the old column. 😀
  4. Delete the old DB column (Ticket 3)
- Don't forget migrating the data and updating any DB logic (sprocs, etc.) to reference the new column.
- Expand and contract pattern
- Or just use MongoDB

# discuss-migration/upgrade
- ## 

- ## 

- ## 

- ## 太久没做数据迁移都忘了要后建索引。
- https://twitter.com/forevertjt/status/1719732968636465590
  - 插入到千万级之后索引就明显影响插入速度了，把索引都干掉就快很多了。

- ## 🔥 [Ask HN: How do you manage direct updates to databases in a production system | Hacker News_202112](https://news.ycombinator.com/item?id=29563226)
- 
- 
- 

- ## 🔥 [Migrating a 40TB SQL Server Database | Hacker News_202007](https://news.ycombinator.com/item?id=23998503)
- 
- 
- 

- ## 🔥 [Ask HN: How does your development team handle database migrations? | Hacker News_201905](https://news.ycombinator.com/item?id=19880334)
- Would be cool to have git for databases.
  - That’s basically the proposition of any event sourcing system. but you’re kinda right, that involves a level of code complication (but then it would be so simple as you described to restore / rebase / etc)

- ## 🔥 [An Unlikely Database Migration | Hacker News_202101](https://news.ycombinator.com/item?id=25767128)
- 
- 
- 

- ## 🔥 [On Uber’s Choice of Databases | Hacker News_201607](https://news.ycombinator.com/item?id=12187797)
- 
- 
- 

- ## 🔥 [Migrating bajillions of database records at Stripe | Hacker News_201509](https://news.ycombinator.com/item?id=10150438)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 我在探探当 PostgreSQL DBA时，10分钟故障弄不好奖金泡汤，再久Job没了
- https://twitter.com/GobeUncleWang/status/1724677788811264261
  - 软件故障基本没有，数据库变更发布由我们自己在工作时间窗口内处理，更主要还是研发同事给力靠谱。有全局监控（https://demo.pigsty.cc），别说28分钟，2.8分钟都不用就够定位绝大多数故障根因了。
  - 要验证也很简单，因为我把整套数据库架构方案与工具都开源出来了
  - https://github.com/Vonng/pigsty /python/plpgsql
- pigsty 有没有计划支持下 http://fly.io 这种基于容器的环境呢？
  - 暂时没有，其他组件放容器都行。数据库我选择基于裸OS做。就是为了尽可能减少不必要的依赖，比如阿里云里对认证的额外依赖一样
- 吹牛没问题，不对称对比加拉踩就没必要了。
- 你这只是一家后端服务集群，人家是整个云服务供应商，两者不在一个水平上吧。其实阿里云真正的问题在于很多东西依赖于Java，它早就应该分散这种对单一语言的依赖的

- ## Lukewarm(微温的; 不热烈的) take for database products - focus on winning new workloads, don't worry so much about migrations. 
- https://twitter.com/MarkCallaghanDB/status/1724454882785304672
  - RoI on features that win new workloads >>> RoI on features that get migrations.
- One way to “hack” this paradigm is to build based on Postgres, and then contribute/collaborate on open source migration tooling.
- Even more lukewarm take - don’t build a database. Build a data based product within a niche. Then generalize from there if you survive year four.

- ## 🔥 [What we learned after I deleted the main production database by mistake | Hacker News_202209](https://news.ycombinator.com/item?id=32903367)
- 
- 
- 

- ## 🔥 [We deleted the production database by accident | Hacker News_202010](https://news.ycombinator.com/item?id=24813795)
- 
- 
- 

- ## 🔥 [Managing database schema changes without downtime | Hacker News_201803](https://news.ycombinator.com/item?id=16665447)
- 
- 
- 
