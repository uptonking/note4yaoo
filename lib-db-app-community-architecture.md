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

- ## 🔁 at Facebook, our experience was that client–server roundtrips are expensive and server–DB roundtrips are mostly fine; 
- https://twitter.com/sophiebits/status/1728536177110905215
  - this is reflected in the design of both Relay and XHP/RSC
  - (whether this is applicable outside FB depends on how your DB is set up)
- Does relay hoist fragments to the top or no?
  - relay does (to avoid client–server waterfalls); xhp doesn’t

- https://twitter.com/OlegLustenko/status/1728498563292811385
- 90% of time we do need top-level fetching. Waterfall is a real perf bottleneck for the first meaningful screen.

- ## Data Pipelines Overview
- https://twitter.com/huangyun_122/status/1725519643580760501
  - 动画示意图

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

- ## 🧭🛢️ [为什么 JS 不能绕过后端代码直接调数据库，有哪些后端处理的逻辑，JS 不能写？ - 知乎](https://www.zhihu.com/question/307461543)

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
# discuss-db-per-user
- ## 

- ## 

- ## [Apple built iCloud to store billions of databases | Hacker News_202401](https://news.ycombinator.com/item?id=39028672)
- I leveraged FoundationDB and RecordLayer to build a transactional catalog system for all our data services at a previous company, and it was honestly just an amazing piece of software. 
  - Adding gRPC into the mix for the serving layer felt so natural since schemas / records are defined using Protobuf with RecordLayer.
  - 🐛 The only real downside is that the onramp for running FoundationDB at scale is quite a bit higher than a traditional distributed database.

- Given that FoundationDB is built on top of SQLite, I wonder if that team is eyeing the HCTree engine for it.
  - It's still in experimental mode but provides literally 10x improvement on read/writes to SQLite.
- They have built their own storage engine named Redwood, which has some very FoundationDB-specific optimizations (like prefix compression). 

- How would you handle schema migrations in a system like this?
  - It depends on the layer, some of the layers might be able to take advantage of how the data is persisted. For example, if you use avro/protobuf, the decoder will handle it for you. If that's not the case, you would have to implement the migration by yourself.

- CouchDB implements a DB per user approach. Personally, I've found it much easier to use than an SQL DB for web apps
- 
- 
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

# discuss
- ## 

- ## 

- ## 

- ## 

- ## I am wrapping my head around Snapshot Isolation (SI) with a minimal computational model
- https://twitter.com/DominikTornow/status/1760054290146873397
  - SI presents a transaction with a consistent snapshot of the database at the start of the transaction and allows to commit only if there are no conflicts with other concurrent transactions' writes

- ## If SQL is considered a programming language, then relational databases function as virtual machines that execute SQL, similar to how the JVM executes Java.
- https://twitter.com/criccomini/status/1759375042847314000
- SQL-speaking databases are both query compilers and runtimes for the resulting execution plan.

- ## 9 strategies to make your system more scalable in the long run.
- https://twitter.com/ProgressiveCod2/status/1754827378436841922
  [1] Horizontal Scalability
  [2] Load Balancing
  [3] Caching
  [4] Database Replication
  [5] Database Sharding
  [6] Stateless Services
  [7] Containerization
  [8] Async Processing
  [9] Adopting Serverless

- Separate WRITE and READ workloads gives good scalability as well.

- ## 🏘️ It's hard to design a software system that can work on a large scale.
- https://twitter.com/Franc0Fernand0/status/1750801088310095905
1. Adding server clones  
- This is the quickest and cheapest way to scale a system from scratch. 
- This method works best for services that don't keep any state, so there is nothing to sync. 
- Whenever the load balancer receives a request, it should be able to send it to any server without knowing where the previous request went.  

1. Partitioning servers  
- A more complex approach is dividing the system into groups of servers with different roles. 
- Ideally, each group of servers is a self-contained application that can make decisions independently. 
- This separation allows each part to be scaled on its own, depending on its needs. It promotes efficient management, as teams can work on different parts of the system simultaneously without interfering with each other. 
- However, it requires more initial effort, and there's a limit to how much you can partition a system before it becomes too complex.  

1. Partitioning data  
- A third approach is dividing and distributing the entire dataset across multiple machines, each having a subset of the data. 
- This setup speeds up data processing and storage as each server only has to deal with a smaller amount of it at a time. 
- It also makes the system scalable, so as the amount of data grows, you can add more computers and change how the data is distributed between them.
- The partitioning strategy, however, makes things more complicated.
  - You need a system to track where each piece of data is stored to direct queries to the correct server. 
  - Also, it can be hard to make queries that cover more than one data partition work well.

- ## 🗳️ What's your favorite way to work with a database?
- https://twitter.com/jamesqquick/status/1730592106517790752
  - raw sql?
  - ORM (prisma, drizzle, etc.)?
  - custom product SDK?
- In an application, ORM for sure. Anything else makes little sense.
- I was was always fan of ORM. IMHO there just be a clear data/logic separation. Plus I wouldn't trust most of BE devs to secure raw queries properly. I also come from the world of Laravel and Eloquent is best data layer abstraction I've used.

- Raw SQL for anything more than the simplest queries, otherwise a query builder.
- Keep trying ORM approach and always come back to compiled raw SQL for anything even moderately complex (Personally enjoy Kysely). Still use query builder for simple requests. So much easier to iterate, adapt, and find help online with. Will sometimes re-factor into built queries
- Query builder (personally node + knex). When the application/queries get too complicated for ORMs, you always resort to sql anyways

- ## Amazon has joined the shared-nothing relational databases club by introducing Amazon Aurora Limitless, 
- https://twitter.com/denismagda/status/1729552540784586867
  - a service capable of scaling write throughput and storage capacity beyond the limits of a single Aurora writer instance.

- ## 把公司里的一个存算强耦合的 AP 系统尝试改造成存算分离，存和算之间用 RPC 通讯。发现改造完后性能不但没有损失太多，在某些场合还改进不少。
- https://twitter.com/r0_ayanami/status/1728979172373193155
- 一般内网带宽是极大富裕的，吞吐我感觉肯定是存算分离的优势，不过需要考虑延迟的变化
- 存算一旦彻底解耦了，算的那部分可以无限弹性扩容了，性能立马原地起飞
  - IO不是瓶颈的计算任务真是太爽了
- 不够就上fiber，RoCE

- 好奇细节，一般存算耦合的 ap 系统一分离都延迟爆炸了
  - 其实我们早就把数据存在 S3 里了。这里的上下文是把 MemTable 独立出来。AP 系统里 in-memory 的 MemTable 的数据量级一般肯定会比 on-disk 的数据小很多，所以性能损失一般不会太离谱。实现上抓了不少火焰图做了一些小的优化，比如 key 下推，减小 proto 编码解码的代价之类的。
  - 其实这个项目真正难的地方不在于性能，而在于如何从存算耦合的架构不宕机地迁移到存算分离的架构上
- 灰度切流往往会提升项目的实现难度
  - 是的，这个东西主要是新旧系统返回不一致的话，定位也很困难。

- ## Separating storage and compute is cool, but separating data and metadata is cooler
- https://twitter.com/richardartoul/status/1726642180473909752
  - [Unlocking Idempotency with Retroactive Tombstones - WarpStream](https://www.warpstream.com/blog/unlocking-idempotency-with-retroactive-tombstones)
  - WarpStream is an Apache Kafka protocol compatible data streaming system built directly on top of object storage. 
  - It has zero local disks, and incurs zero inter-zone bandwidth costs. 
  - many people aren’t aware that Kafka supports more advanced features like idempotent produce requests which allows a Kafka client to produce the same batch of data multiple times, but ensure it’s only appended to the log once.
  - it was one of the primary reasons why we created our own metadata store instead of reusing something off the shelf.
  - In this post, we’ll go over in detail how we added support for the idempotent producer functionality to WarpStream’s storage engine.

- ## Been thinking about S3 as primary storage for serverless infra. 
- https://twitter.com/criccomini/status/1725183323474190704
  - For OLTP, a transactional KV store on S3 would id a necessary building block. @PingCAP ’s TiKV is one such example. 
  - [Production Flink Usage, Key-Value Stores on S3, Titan is Terraform for Data, and more...](https://materializedview.io/p/flink-usage-kv-store-on-s3-terraform-for-data)

- ## 🐛 The biggest problem with shared-storage OLTP is that the data volume is limited by single machine. 
- https://twitter.com/YingjunWu/status/1723832509098766801
  - Some big customers moved away from Aurora to CRDB/TiDB because they felt frustrated when hitting the storage limit. 
  - But most companies don’t store so much data in OLTP DBs and won’t hit the limit.

- 🤔 This is not a problem for shared storage, you can split the data into different storage nodes via sharding. Where each shard is a shared storage architecture (multi tenant) and lives on its own machine - CRDB does this.
  - Aurora could theoretically do this as well. The storage limit has nothing to do with the shared storage architecture.

- But what you said is not quite true -- Oracle RAC is there. Also we need to look and see whether the issue is raw storage capacity or or read througput/tps or write throughput/tps, etc., each has its own answers.
- Haven’t studied Oracle RAC before, but the 128 TB hard limit is a pain for Aurora.
  - Aurora has limitations for sure but most workloads don’t need a lot and secondly you can add more clusters. But RAC I believe scales to multiple PBs.
- The storage capacity is not a problem for those who run on Aurora. The last time I checked it was possible to scale beyond 60 TB. The inability to scale write workloads across zones and regions is what shared-storage architecture doesn’t deal with. That’s why Amazon turns to DynamoDB to scale both reads & writes. But that should change soon once Amazon introduces a distributed shared-nothing version of Aurora

- ## what is the reason in your mind that none of the database vendors are able to crack the moat(城壕；护城河) of Oracle and RAC, in a meaningful way?  I am curious to hear your thoughts.
- https://twitter.com/sv_techie/status/1723777534406332517
- Snowflake and Databricks in the analytics space. OLTP is tricky, hard to build, hard to earn developer trust. That's why @neondatabase bets on Postgres and strive to become default cloud Postgres

- ## There has been several startups building an operational relational databases focused on OLTP with a shared nothing architecture. 
- https://twitter.com/nikitabase/status/1723579854266966399
  - @neondatabase is using a different approach - shared storage.  What's the difference?
- In a shared nothing architecture you take a cluster of machines and assign a subset of data (shard) to each machine using range or hash partitioning.
  - Incoming SQL queries are split into parts that can be  run on each machine. If need be the results of those queries are reshuffled, potentially multiple times, and finally collected on one node to generate the final result.
  - While this architecture allows you to scale your TPS for simple reads and writes it has several disadvantages:
  - 1. Some write transactions are only touching one shard and some multiple. So some write queries scale MUCH (10-100x) worse than others.
  - 2. To achieve consistency you need to implement 2 phase commit (or other distributed protocols) to preserve transactional semantics, which requires two network roundtrips with each participant so you transaction latency is inconsistent.
  - 3. Cross shard foreign keys and uniqueness are super hard to implement in a shared nothing system. You need to go over the network to validate presence of foreign keys and uniqueness. Radical performance implications.
  - The list can go on. Mature shared nothing systems achieved an incredible engineering feat of supporting all the query processing use cases, but even the best ones sacrifice surface area and DEFINITELY break compatibility with the single node system they are based upon.
  - Because even if in fullness of time you implement all the surface area it's impossible to preserve performance compatibility. In addition to having to go over the network for some queries, you also have a different query optimizer which breaks performance compatibility.
  - The result is that most shared nothing systems support a subset of features of single node systems and try to convince their users that those don't matter or don't scale.
  - This means you can't migrate back and forth from Postgres or MySQL to a shared nothing system. Most developers start on Postgres or MySQL, so companies building shared nothing systems need to find workloads that ran out of scale on single node databases.
  - Attempts to build a popular shared nothing system have been here since the 80ies. None of the shared nothing OLTP systems took off. Microsoft had two attempts with SQL Server - both failed.
- Lets now look at shared storage systems. In a shared storage system there is a separate storage: either page based or row based. 
  - E.g. Postgres stores everything in 8k pages.
  - Storage systems like this is MUCH easier to make distributed - it's a glorified key value store.
  - Then you can "attach" compute - a single node database system to the distributed storage. Which has the following benefits.
  - 1. I/O is infinite. You can still run out of network for pushing writes into the system, but you won't run out of iops.
  - 2. 100% compatibility with the single node system. Which means your apps don't need to change. Just change the connection string.
  - 3. Compute is now stateless - you can move it around nodes in a multi-tenant system. And this allows you to build serverless compute on top of a traditional SQL database
  - 4. Read replicas don't need to copy data to start replicating. They attach to the same storage.
  - The most successful systems are shared storage: Oracle RAC, SQL Server Hyperscale, and AWS Aurora. @neondatabase is shared storage which lets us be serverless.
- Oracle RAC is different from others as it provides HA (resilience to node failure, online patching). All cluster nodes are full-feature read-write, sharing not only the storage but also the buffer cache, the prepared statements and the distributed locks
  - I was about to reply that Oracle RAC has been around in this segment for a while now until I read this last tweet. Even RAC had its own issues which shared nothing databases actually solved. Even Oracle introduced the concept of sharding recently.
  - RAC is only one part of the Maximum Availability Solution and is about global cache and lock manager. They distribute storage with ASM, they replicate with Data Guard, they shard on top of it. It is not binary like shared nothing or shared storage

- Shared storage systems are not reliable: you can’t have efficient replication and assume storage is “local” so no way to allow entire continents to lose connection. Any system which needs more than one machine is niche

- nice write-up! shared storage also means some of your data will come from over the network everytime, depending on how you've distributed your data across the shared storage -- if you have fast drives and good bandwidth on the network this becomes less of concern.. how are failover to DR sites handled in this architecture?

- There is also a combined approach where you build a fully distributed database on shared storage. In this design, the database nodes share the storage, while the storage nodes share nothing. This approach is used at @YDBPlatform

- Detached compute from storage is the right approach when possible.

- ## 💡 People always talk about Create, Read, Update and Delete.
- https://twitter.com/andrewingram/status/1722291782564602202
  - They never talk about Duplicate, Split and Merge. The far more gnarly actions that are commonly required in any real system.
- CRUD erases any intent in our system. Why did the address change ? Has the user moved ? Was he correcting a typo ? I do not understand why CRUD is a thing. Any CRUD system becomes unmaintainable when we need to implement workflows such as duplicating, etc as you mentioned
  - Yeah, I prefer my "write" operations to be centred around use cases (Jobs To Be Done) rather than just plain old entity manipulation. I tend to enjoy the CQRS-type approach that GraphQL gives me when set up effectively.

- Don't forget reorder!

- Duplicate = Read + Create
  - Split = Read + Create
  - Merge = Read + Read + Create + Delete

- But we don't have HTTP verbs for them, making them un-possible.

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
- You nailed it, it's a spreadsheet - but one that doesn't constraint all data to live on the same application window, but could access and transform it throughout the whole system - just like copy/paste can transfer data from one program to another, where it can be transformed with a different toolset.
  - Copy/paste is the most fundamental tool in the toolbox of the end user, since it's the only universal* way to transfer data between apps without accessing an API programmatically, so I think it's undeservedly(不该得到的; 不该受的) neglected as a tool to build real life practical workflows.
  - Intents on mobile devices are similar, but they are not universal - many times the app to which you want to transfer data is not recognized as a valid target for the shared data.
- Incidentally, spreadsheets are one of the most versatile and successful End-User Development tools, allowing users to build information systems tailored to their business purposes. A system combining those design capabilities with the flexibility of building system-wide workflows could transcend the current model of siloed apps.

- The Unix pipe seems like scriptable copy & paste.
  - It's not, because you can't easily spawn transient pipes between running processes. The OS probably allows this, but I've never seen it exposed in the UI layer.
  - Pipes are primarily used to build ad-hoc pipelines that run in batch mode. Copy&paste is a tool for moving specific bits of data on demand between two running programs, or within the same program. Copy&paste interaction model is "please take this and put it there", and the ability to select the this and the there is just as important as transferring the data itself.

- 🤔 Whenever I stumble on an article like that*, I can't stop wondering why do so many developers think that SQL is hard/clunky in comparaison?
- > A database introduces a different data model - I have to translate between database data-types and my programming languages native data-types.
  - It doesn't matter how difficult or simple it is; the problem is that it's a different model, so it creates translation inefficiencies and makes it more difficult to reason about.
  - The object-relational impedance mismatch is a known problem; having data in one place and format, accessed through a single programming model will typically be easier than a separate service with a different language and model, no matter how efficient.
- I wonder about going the other way, and turning SQL into a full scripting language.
  - That's what PL/SQL and T-SQL basically are. They work, but they have a somewhat weird programming model, halfway between programming and declarative sql but being neither, with table cursors and stateful SQL queries. And of course, their scope is limited to interacting with the database itself, not the outer world.
- SQL is... clunky, but it's still a wonderful way of working with data, compared to hand-rolling imperative loops or functional transforms.

- ## 🔥 [We are splitting our database into Main and CI | Hacker News_202207](https://news.ycombinator.com/item?id=31956871)
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
