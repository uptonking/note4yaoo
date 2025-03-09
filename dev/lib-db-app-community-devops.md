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

- ## Running your database using a non-UTC time-zone is a mistake. Fight me.
- https://x.com/GrahamJCampbell/status/1894419202976477664
- Yes, for all data tasks, everything shall be normalized and standardized and when it comes to dates it is Zulu, aka GMT aka UTC, which is used in science and space as well.

- That's fine as soon as you store the timezone along with the date time. But all SQL based database have a broken date time that uses a legacy string representation. At least postgres as a timestamptz. Guess what, MongoDB only stores UTC date times.
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

- ## those of you with databases inside a vpc what is your migration process like?
- https://x.com/thdxr/status/1891245539112489344
  - sst autodeploy can run in a vpc so there's no issue here but otherwise i deploy a lambda in a vpc that does the migration
  - do people actually setup the custom thing for github actions?

- My coworkers huddle me on Slack. They open GitHub, I open Supabase. We both count down from 3, and then they hit merge and simultaneously I manually run the migration in the Supabase SQL editor. Only way I’ve found to keep everything in sync
- think our approach is similar to yours but we use ECS so was quicker at the time to spin up a task that does the migration and exits

- One example I’ve built:
  - CI builds/pushes migration specific docker image
  - before deploying services, makes new migration ECS task def
  - ECS task execute migration docker
  - db migration succeeds? Move on to service deploy.

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

# discuss-db-cloud/k8s
- ## 

- ## 白嫖的supabase的项目不要暂停超过90天，否则你将升级到pro才能恢复数据。别问我怎么知道的。
- https://x.com/mundane799699/status/1896213016196333720
- 我赶紧去看看 appwrite 是不是也这样。

- 超过7天不活跃会被清理掉，但可以被恢复

- ## 你们平常更喜欢用severless的数据库还是喜欢自己独立部署自己维护一个数据库呢？
- https://x.com/PennyJoly/status/1898582842260742297
- 我选择自己部署，因为云服务数据库，一段时间不用就会被关掉，例如supabase，而自己部署不会有这个烦恼
- 如果考虑数据备份，数据库可用性等问题，还是直接用云服务商的数据库服务比较好。而且代码里用orm，在不同的数据库直接切换也会比较简单些。

# discuss
- ## 

- ## 

- ## 

- ## Every field being optional in Protobufs is actually the only scalable solution for schema migrations
- https://twitter.com/ChShersh/status/1783873173190009168
- Making a field required only means clients will fail the whole parsing operation. “required” should be enforced at the application layer, not at the transport layer.

- It just moves the problem somewhere else. Bytes are always optional.
  - At some point your code is going to need to assert the existence of a field (probably).
  - If you don't do it in the schema, then you have to do it somewhere else.
- protoc can’t generate the code that deals gracefully with missing required fields
  - Alright I see the point. I'd argue the problem is protoc then, not the required field, but now I'm with you! Point being: The field is no less required, you just get better errors.

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
