---
title: lib-db-app-community-architecture
tags: [architecture, community, database]
created: 2023-09-17T17:37:06.649Z
modified: 2023-09-17T17:37:19.913Z
---

# lib-db-app-community-architecture

> about database and application architecture

# guide

# discuss-stars
- ## 

- ## 🤔🔥 [Databases = Frameworks for Distributed Systems | Hacker News_202205](https://news.ycombinator.com/item?id=31459745)
- I was watching a video by one of Amazon’s distinguished engineers a while ago and for the life of me I can’t find it now but the thing that stuck with me from it is, 
  - “There are only three modes for a distributed system - it implements paxos/raft itself, it relies on a data store that implements paxos/raft or it’s wrong.”
  - Look at k8s and etcd for a very widely used example of this approach as well.

- While databases having been converging on composability for a long time, the model presented here is not the correct one and causes problems for many important and emerging use cases.
  - As an elementary observation, isolating the designs of storage, compute, and networking as separate modules is a reliable way to achieve poor performance and resource efficiency. Some of the most important scalability and performance optimizations in modern database architecture are schedule-driven, which requires tight coupling across the design of storage, compute, and networking. Ignoring this class of optimizations produces very large reductions in real-world workload performance, and feeds a narrative that the software is wasteful and not environmentally friendly.
  - Most of our distributed systems are modeled as giant distributed file systems, and that fits okay with the idea of horizontally partitioning compute, storage, and network. This is easy for developers to reason about because they are familiar with file systems. However, it is difficult to express important database-y operations in this model. For example, if you want to do ad hoc joins in a scale-out environment, you need mechanics like decentralized parallel orchestration which isn't really a concept in a "distributed file system" model of "distributed".

- I would say the author just tried to redefined "distributed", and ignored those real distributed systems, e.g. Paxos/Raft-based ones.
  - You are thinking of fully decentralised systems. A system where there is a centralised leader is still a distributed system so long as at least some of the processing takes place on other nodes.

- ## 💡🔥 [Immutable Databases | Hacker News_202005](https://news.ycombinator.com/item?id=23290769)
- 
- 
- 

- ## 🤔🔥 [Ask HN: Do you use foreign keys in relational databases? | Hacker News_202209](https://news.ycombinator.com/item?id=32731916)
- 
- 
- 

- ## 🔥 [The growing pains of database architecture | Hacker News_202306](https://news.ycombinator.com/item?id=36208420)
- 
- 
- 

- ## I think I want to change the way I write code from ‘projects’ to a library of code that is tagged in a database and queryable. 
- https://twitter.com/JungleSilicon/status/1713939838624501941
  - The queries could compose software dynamically or even be used as part of static site generation.
- Are there many examples of similar efforts? It would work really well with sync & user defined behaviours.
  - Check out @ValDotTown and @observablehq . Both store code in a database and let you import between the database entries. Observable has real-time sync, http://val.town does not.
  - That's very similar to what @ValDotTown is doing, a database of code snippets.

- Some former teammates of mine used https://glean.software to query code at the level of language constructs. IIRC you can extend it to include additional information in the code index.

- ## [General-purpose databases that never delete or update data in-place - Stack Overflow](https://stackoverflow.com/questions/13508035/general-purpose-databases-that-never-delete-or-update-data-in-place)
- I'm very much inspired by the approach to data management advocated by Rich Hickey, and implemented in Datomic, where the data is never mutated in-place, all the versions are always preserved and query-able, and the time is a first-class concept.

- I think both the BerkeleyDB Java Edition and CouchDB work like that internally
- Noms is versioned, forkable, syncable, append-only database. It is possible to see the entire history of the database
- LiteTree SQLite with Branches

- ## 🤔🔥 [How not to structure database-backed web apps: performance bugs in the wild | Hacker News_201806](https://news.ycombinator.com/item?id=17414383)
- 
- 
- 

- ## 🌐️🛢️ [为什么 JS 不能绕过后端代码直接调数据库，有哪些后端处理的逻辑，JS 不能写？ - 知乎](https://www.zhihu.com/question/307461543)

- 之所以不能直接对接到数据库，要中间服务代理一下（graphql 也需要“代理”），主要有几个原因：
  - 安全问题：直接暴露数据库连接地址、连接 token（不管是密码账号还是中间token），都可能导致数据库被脱库，容易被爆破、篡改
  - 性能问题：数据库 SQL 的优化很复杂，不是看到的简单 select 语句、CRUD，分库分表、索引优化都难以在前端实现，即使 GraphQL，也需要 db 的中间层

- 在前端用字符串拼接SQL语句，后端数据库直接执行，然后查询结果送回前端处理。写起来是挺爽的，开发效率奇高，因为基本不需要写后端了。
  - 但是这样会带来很大的安全性问题，很快我就决定全部重写。
- 主流的关系型数据库，比如MySQL, 只能支持到表级别的鉴权。也就是说，一个用户如果被授权访问一张表，那么他就能访问这张表里的所有数据。
  - 但是现实中的业务逻辑，通常不希望用户可以访问表里的所有数据。
  - 用户可以篡改一些信息
- 前端发来的请求都是不受信任的。后端要对它进行各种校验审查，最后才能执行并返回结果。
  - 比如要检查用户的登录状态，输入的参数是否合法有效，SQL语句要用专门的逻辑去清洁，而不能用简单的字符串拼接，以避免SQL注入这种攻击。
  - JavaScript运行在浏览器里，很容易被篡改。网络请求也可以在浏览器里被查看和修改。
- 当然，一些传统的桌面版信息管理系统软件，前端不是JavaScript写的，比如用C#, 甚至C++实现的。这些软件部署在企业内部的系统里，网络环境相对更加安全可靠。在这种情况下，其实是可以在“前端”直接操纵数据库的。传统的ERP软件很多都是这么做的。

- 直接用 SQL 也不是不能保障安全，有大概两种方法：
  - 1、用户与数据库用户统一，在创建网站用户时创建数据库用户并设置权限；
  - 2、代理层解析前端的 SQL，检测是否超过必要限定，或者附加限制条件等。
  - 方法 1 不太好实施，为了管理和统计方便，通常会把数据集中到一起，即使细分了账号也难以限定行级的操作；
  - 方法 2 要先将 SQL 解析成另一个方便检测和处理的数据结构，在检测和附加限定之后再拼装回 SQL，难度有点大。 

- 技术上根本没有障碍。JS可以做几乎任何事，但是很多事情会被浏览器给拦下来。
  - 比如你用js不借助file控件直接读写一个本地文件你觉得可能吗？如果真的可以后台直接操作，那当你打开某个网页时，你的所有电脑信息都可以被拷贝走
  - 但凡有点经验的开发都知道，所有放到前端的东西都是不安全的。
# discuss
- ## 

- ## 

- ## 

- ## 🔥 [Oops, You Wrote a Database | Hacker News_202302](https://news.ycombinator.com/item?id=34941650)
- 
- 
- 

- ## 🔥 [Feature Casualties of Large Databases | Hacker News_202012](https://news.ycombinator.com/item?id=25270107)
- 
- 
- 

- ## 🔥 [It's not Ruby that's slow, it's your database | Hacker News_202211](https://news.ycombinator.com/item?id=33524039)
- 
- 
- 

- ## 🔥 [Ask HN: Server-side web apps – is the database still a bottleneck? | Hacker News_201906](https://news.ycombinator.com/item?id=20123659)
- 
- 
- 

- ## 🔥 [Database Lab – Full-size staging databases as a service | Hacker News_202002](https://news.ycombinator.com/item?id=22258806)
- 
- 
- 

- ## 🔥 [The program is the database is the interface | Hacker News_202302](https://news.ycombinator.com/item?id=34761768)
- 
- 
- 

- ## 🔥 [We are splitting our database into Main and CI | Hacker News_202207](https://news.ycombinator.com/item?id=31956871)
- 
- 
- 

- ## 🔥 [Database of Databases | Hacker News_202009](https://news.ycombinator.com/item?id=24494403)
- 
- 
- 

- 🔥 [Database of Databases | Hacker News](https://news.ycombinator.com/item?id=37314622)

- ## 🔥 [The magic of small databases | Hacker News_202301](https://news.ycombinator.com/item?id=34558054)
- 
- 
- 

- ## 🔥 [Millions of Tiny Databases [pdf] | Hacker News_202002](https://news.ycombinator.com/item?id=22329256)
- 
- 

- ## 🔥 [Millions of Tiny Databases | Hacker News_202003](https://news.ycombinator.com/item?id=22481612)
- 
- 
- 

- ## I think one of the most important problems in databases right now is figuring out how to keep data really really close to users.
- https://twitter.com/ankrgyl/status/1717190980905189772
  - In OLAP this is all about loading and caching data in the browser, and then letting @duckdb rip.
- Figuring out which data you’ve loaded and knowing when to load more is a Really Hard Problem. Ideally you can also push filters or full queries to the backend depending on their shape/size. But if you solve it — the UX is truly magical
- Keeping it in the browser is an orthogonal problem, but yes once it’s in the browser Duckdb is magic

- ## 🤔 [Ask HN: Has anybody shipped a web app at scale with 1 DB per account? | Hacker News_202005](https://news.ycombinator.com/item?id=23305111)
- My startup currently does just this 'at scale', which is for us ~150 b2b customers with a total database footprint of ~500 GB. We are using Rails and the Apartment gem to do mutli-tenancy via unique databases per account with a single master database holding some top-level tables.
  - This architecture decisions is one of my biggest regrets, and we are currently in the process of rebuilding into a single database model.
  - However as we have grown this has become a huge headache. It is blocking major feature refactors and improvements. It restricts our data flexibility a lot. Operationally there are some killers. Data migrations take a long time, and if they fail you are left with multiple databases in different states and no clear sense of where the break occurred.
  - Lastly, if you use the Apartment gem, you are at the mercy of a poorly supported library that has deep ties into ActiveRecord. The company behind it abandoned this approach as described here

- Echoing this as well, I worked for Influitive and was one of the original authours of apartment (sorry!)
- There are **a lot of headaches involved with the "tenant per schema" approach**. Certainly it was nice to never have to worry about the "customer is seeing data from another customer" bug (a death knell if you're in enterprisish B2B software), but it added so many problems:
  - Migrations become a very expensive and time-consuming process, and potentially fraught with errors. Doing continious-deployment style development that involves database schema changes is close to impossible without putting a LOT of effort into having super-safe migrations.
  - You'll run into weird edge cases due to the fact that you have an absolutely massive schema (since every table you have is multiplied by your number of tenants). We had to patch Rails to get around some column caching it was doing.
  - Cloud DB hosting often doesn't play nice with this solution. We continually saw weird performance issues on Heroku Postgres, particularly with backup / restores (Heroku now has warnings against this approach in their docs)
  - It doesn't get you any closer to horizontal scalability, since connecting to a different server is significantly different than connecting to another schema.
  - It will probably push the need for a dedicated BI / DW environment earlier than you would otherwise need it, due to the inability to analyze data cross-schema.
- I still think there's maybe an interesting approach using partioning rather than schemas that eliminates a lot of these problems, but apartment probably isn't the library to do it (for starters, migrations would be entirely different if partioning is used over schemas)

- Can confirm, here be dragons. I did a DB per tenant for a local franchise retailer and it was the worst design mistake I ever made, which of course seemed justified at the time (different tax rules, what not), but we never managed to get off it and I spent a significant amount of time working around it, building ETL sync processes to suck everything into one big DB, and so on.
  - **Instead of a DB per tenant, or a table per tenant, just add a TenantId column on every table from day 1**.

- Nutshell does this! We have 5, 000+ MySQL databases for customers and trials. Each is fully isolated into their own database, as well as their own Solr "core."
  - We've done this from day one, so I can't really speak to the downsides of not doing it. The piece of mind that comes from some very hard walls preventing customer data from leaking is worth a few headaches.
  - We don't split ALBs / ASGs / application servers per customer. It's only the MySQL / Solr layer which is multi-tenant. Memcache and worker queues are shared.
  - We do a DB migration every few weeks. Like a single-tenant app would, we execute the migration under application code that can handle either version of the schema. Each database has a table like ActiveRecord's migrations, to track all deltas. We have tooling to roll out a delta across all customer instances, monitor results.
  - All of this makes it really easy to backup, archive, or snapshot a single customer's data for local development.

- ## 🤔 [Ask HN: Is there a way to efficiently subscribe to an SQL query for changes? | Hacker News_202104](https://news.ycombinator.com/item?id=26901352)
- Source: I worked on Google Cloud Firestore from it's launch until 2020 and was the on responsible for the current implementation and data structures of how changes get broadcasted to subscribed queries.
  - Without joins Google Cloud Firestore does exactly what you're describing.
  - With joins (or any data dependant query where you can't tell a row is in the result set without looking at other data) you need to keep the query results materialized otherwise you can't have enough information without going back to disk or keeping everything in memory, which isn't really feasible in most cases.

- I like this idea a lot. In a sense it's thinking of your application as a spreadsheet, where the database is a data tab and the frontend is the summary tabs. If there's a change to the data tab, the "spreadsheet engine" (or "materialized view engine" in your case) walks the dependency graph and updates all the relevant parts of the summary tabs.
  - The closest thing I'm aware of to this is BigQuery's materialized views, which take care of making otherwise expensive queries cheap fast, but they are rather limited (i.e. no subqueries or joins), and don't have the "streaming output of changes" you describe.

- This is the exact problem that we are solving here at Materialize! 
  - we (Materialize) have the TAIL operator, which was built to allow users to subscribe to changes
