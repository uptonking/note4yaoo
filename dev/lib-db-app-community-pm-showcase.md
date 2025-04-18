---
title: lib-db-app-community-pm-showcase
tags: [community, database, showcase]
created: 2023-10-26T17:12:46.541Z
modified: 2024-08-11T07:20:47.398Z
---

# lib-db-app-community-pm-showcase

# guide

# discuss-stars
- ## 

- ## 

- ## 我感觉 Supabase 是一个从 niche market 进入市场，然后不断拓展的很好例子。
- https://twitter.com/mingwb/status/1743084511708246285
  - 最开始主打的是通过 RLS 让客户端直连数据库，以及 Realtime 和 Auth；然后开始做主流的后端开发生态，集成 Deno，做数据库连接池，做 database branching。传统数据库服务商想反向提供 Supabase 的能力就没那么容易了。
  - 数据库服务商很难做是因为基因不同吧。Supabase 依靠个人开发者起家的，整个公司的决策和运转都依赖这个。目前看到的新兴的数据库服务商（特别是分布式数据库...）依靠的是有钱的大企业，和中小企业和个人开发者完全不一样。

# discuss
- ## 

- ## 

- ## 

- ## AI 正在改变软件开发方式：快速生成应用，无需后端，部署只需几分钟。面对这些变化，传统数据库已显得笨重。AI 时代的数据库需要重新设计，适应新需求
- https://x.com/earayu/status/1904123569405096051
- 特性 1：即开即用的服务化数据库（SaaS + Fast Provisioning） AI 生成的应用生命周期短，从开发到上线只需几分钟。数据库必须支持“即开即用”，无需繁琐配置，数秒内可用，摆脱传统数据库的繁重流程。
- 特性 2：前端直连数据库，支持 JWT 认证 AI 应用往往是无后端的纯前端项目，数据库需要支持前端直连。通过 JWT（JSON Web Token），用户权限可安全映射到数据库，降低开发与安全成本。
- 特性 3：极低成本 + 弹性扩展（Scale-to-Zero） AI 应用生命周期短，绝大多数不会“火”。数据库需要支持： 无请求时自动休眠，几乎零成本。 流量爆发时快速扩展，承载大量请求。 这是支持长尾效应的关键。
- 特性 4：数据库是技术投资，而非短期盈利工具 AI 生成的应用存在极大偶然性：1 万个应用中，可能只有 1 个爆火。但这个爆火应用能覆盖所有成本。数据库需要以低成本支持开发者，长期布局获胜。

- 非结构化的数据库比较合适，反正数据能塞进去拿出来就行

- ## Wanna work on/around databases? Here's ~216 database companies Alex Miller curated for you.
- https://x.com/eatonphil/status/1824505089303720119
  - this is a conservative list. This does not include companies with major database divisions like DataDog, Apple, Microsoft, Meta, Google, Bloomberg, etc. etc. etc.

- ## PlanetScale 取消了免费套餐，最便宜的付费计划是每月39美元，裁掉了所有 DevRel… _202403
- https://twitter.com/Hooopo/status/1765510587365142928
- 可以预见的结果啊，免费的代价就是大家疯狂地薅羊毛，况且本身也不是大财团旗下的，实际就是各大云厂商的套壳，成本打不住，做不成赛博菩萨。

- 策略：数据库是很多项目的底层，迁移成本很高，先让这帮羊毛党用起来，然后收费就行了; 
  - 结果：薅羊毛的不在乎
- 迁移成本不算高，Vercel 这种迁移成本才高，还有一堆和 node 不兼容的地方
- 是的，提供的扩展和定制化功能护城河不够深, 不然都得乖乖付费

- 淦以后不使用serverless 的理由又多一条

- ## Every DB vendor will end up providing a notebook 
- https://twitter.com/mim_djo/status/1756688158786535471
  - SingleStore: We launched a compute service that lets developers spin up GPUs and CPUs to run database-adjacent workloads including data preparation, ETL, third-party native application frameworks, etc.

- ## 🚀🛋️ [SpacetimeDB: A new database written in Rust that replaces your server entirely : programming_202308](https://www.reddit.com/r/programming/comments/15mgp4i/spacetimedb_a_new_database_written_in_rust_that/)
- > This means that you can write your entire application in a single language, Rust, and deploy it as a single binary. 
  - Am I the only one that sees that as a downside?
  - There is a time and place for monoliths and low complexity projects but for large projects you absolutely want to have the flexibility and scalability to have micro services and VMs etc.
  - I also don't see the advantage of my backend being merged into the database. Makes it harder to scale the backend independently
- It’s a massive downside and it literally doesn’t even make sense.
  - Having the application live inside the database makes even the most basic horizontal scaling tasks like sharding an absolute nightmare.
- It sounds like they map different regions of their game to different database-instances. Sounds to me like it could scale easily? Just crossing borders may be tricky, but I guess this is an issue in every other architecture as well

- Comments here are a bit salty(尖锐的, 辛辣的). It’s good to try out new models and see how they work.

- This actually reminds me of EdgeDB and SurrealDB, which just bake the API directly into the database.

- 🛋️ This idea was tried with CouchApp over a decade ago. 
  - It embedded all your data and logic into CouchDB which was already based on Javascript functions, so that was a natural development... 
  - as far as I know the developers themselves recommended against using it at some point (it has been deprecated by Cloudant), given the problems with integrating this kind of solution with anything else, like monitoring tools, profilers, debuggers etc.
- The tech has come a long way in 10 years. WebAssembly kind of changes the game in terms of all of the things you mentioned.

- There is a similar project for postgres called aquameta. https://github.com/aquametalabs/aquameta You write your app as javascript stored procs. It handles everything for you including the IDE, version control etc. All in postgres.
- There were also couch apps back in the day that use couchbase to serve HTML.

- SpacetimeDB is designed as an actor model where each database represents an actor. The world of BitCraft is run on many databases which all message each other. Our goal is 1, 000, 000 tx/sec/database. We're not near that at the moment, but we know how to get there from where we are.

- 🐛 Why would it be a security nightmare?
  - a. You've placed both the application and authorization (permission) logic into one application, running the database.
  - b. An attacker could exploit a vulnerability in the application logic to steal data from the database.
  - c. An attacker could exploit a vulnerability in the application logic to inject malicious code into the database. This malicious code could then be executed by any client that connects to the database.
  - d. An attacker could exploit a vulnerability in the application logic to disrupt the application. This could prevent users from accessing the application or cause the application to crash.

- ## [SpacetimeDB: A new database written in Rust that replaces your server | Hacker News_202308](https://news.ycombinator.com/item?id=37063565)
- We (Clockwork Labs) have been developing this database for several years as the backend engine for our MMORPG BitCraft
  - 100% of the game's logic is loaded into the database and then players connect directly to the database instead of to any game server. 
  - All the data is then synchronized with the client (trees, player positions, buildings, terrain, etc). 
  - We think it will substantially decrease the complexity of deploying a live service.
  - BitCraft is written in Unity and SpacetimeDB works out of the box with Unity, although we also support several client languages as well (Rust, Typescript, C#, Python).

- ## [Show HN: SpacetimeDB – A database that replaces your server | Hacker News_202308](https://news.ycombinator.com/item?id=37146952)
- It really reminds me of https://pocketbase.io/ which has sorta the same idea and can be extended with go/js. How does the database work under the hood? Is it also based on sqlite? Are rust modules built with a special runtime in mind like tokio or?
  - It's not based on sqlite. We have a custom database engine which we needed for performance reasons for BitCraft. We need to be able to control very carefully what is done in memory vs on disk so that we can manage latency for games and other real-time/soft real-time applications.
  - Rust modules are agnostic to all of that. Right now they're not async at all since they take place in a transactional context and you don't want to await while a transaction is held open.
- The advantage I see is that there's no more context switching between the app and DB, which is the IO between the two. Especially if the two are on different servers, as is often the case. So that should boost performance quite a bit.
  - Absolutely. This was the original reason that we built this system. We found that we could get much much better performance when dealing with persistent data by putting the logic in the same process as the system which persists the data.

- How does this compare to embedded databases like sqlite?
  - You can use SpacetimeDB as an embedded library as well. It depends on how you want to use it. sqlite doesn't really provide you a way to have replicas of your data or manage the data across multiple machines. It's complicated, but the idea is similar in a sense.

- ## [SpacetimeDB v0.7 Released: WebAssembly stored procedure database written in Rust | Hacker News_202310](https://news.ycombinator.com/item?id=37861765)
- SpacetimeDB combines your application server and database into a single service. You can write your application logic as WebAssembly stored procedures which are uploaded into your database, allowing clients to connect directly to your database.
  - The main benefit is you eliminate all the DevOps overhead of deploying servers and don't have to deal with the state synchronization with clients.
  - SpacetimeDB is used as the sole backend for https://bitcraftonline.com, a real-time MMORPG

- ## 🔥 [SurrealDB – Document-graph database, for the realtime web | Hacker News_202208](https://news.ycombinator.com/item?id=32550543)
- 
- 
- 

- ## 🔥 [Show HN: EdgeDB – Next generation database | Hacker News_201904](https://news.ycombinator.com/item?id=19638701)
- 
- 
- 

- ## 🔥 [immudb – world’s fastest immutable database, built on a zero trust model | Hacker News_202112](https://news.ycombinator.com/item?id=29702974)
- 
- 
- 

- ## 🔥 [Immudb 1.0 – open-source, immutable database with SQL and verified timetravel | Hacker News_202105](https://news.ycombinator.com/item?id=27275691)
- 
- 
- 

- ## 🔥 [Umbra: an ACID-compliant database built for in-memory analytics speed | Hacker News_202001](https://news.ycombinator.com/item?id=22153515)
- 
- 
- 

- ## 🔥 [Show HN: Dropbase 2.0 – Turn offline files into live databases | Hacker News_202008](https://news.ycombinator.com/item?id=24189582)
- 
- 
- 

- ## 🛢️🔥 [tigerbeetle: A database without dynamic memory allocation | Hacker News_202010](https://news.ycombinator.com/item?id=33192288)
- 
- 
- 

- ## 🛢️🔥 [YDB – An open-source Distributed SQL Database | Hacker News_202204](https://news.ycombinator.com/item?id=31081272)
- 
- 
- 

- ## 🔥 [The database servers powering Let's Encrypt (2021) | Hacker News_202309](https://news.ycombinator.com/item?id=37536103)
- 
- 
- 

- ## 🔥 [The database servers powering Let's Encrypt | Hacker News_202101](https://news.ycombinator.com/item?id=25861422)
- 
- 
- 

- ## 🛢️🔥 [Microsoft Access: The Database Software That Won't Die | Hacker News_201910](https://news.ycombinator.com/item?id=21401198)
- 
- 
- 

- ## 🔥 [BayesDB - a Bayesian database table | Hacker News_201312](https://news.ycombinator.com/item?id=6864339)
- 
- 
- 

- ## 🔥 [RethinkDB: An open-source distributed database built with love over three years | Hacker News_201211](https://news.ycombinator.com/item?id=4763879)
- 
- 
- 
