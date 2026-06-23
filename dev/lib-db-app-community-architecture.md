---
title: lib-db-app-community-architecture
tags: [architecture, community, database]
created: 2023-09-17T17:37:06.649Z
modified: 2023-09-17T17:37:19.913Z
---

# lib-db-app-community-architecture

> about database and application architecture

# guide
- who is using #db-per-user
  - bluesky
# discuss-stars
- ## 

- ## 

- ## 

- ## Poll: When your automated tests run on your CI server, what database does your app call?
- https://x.com/housecor/status/1955624930487497212
- Why run these tests at all? I ran them on my machine, we're good, right?
- I truncate all tables between every test case, but I guess its technically only a unique db per build
- I wonder if the size of the test data would matter & what is the purpose of that test?

- ## [Synchronizing local state with the database : r/rust _202306](https://www.reddit.com/r/rust/comments/14jfcen/synchronizing_local_state_with_the_database/)
- I'm working on a websocket server too, and I'm completely forgoing the DB for real time updates.
  - Roughly, each thing a user might open a WS connection for is managed in-memory by a tokio task. This tokio task pulls in input, applies it to its local copy of the state, and then pushes the updates to other connections. This keeps everything entirely in-memory to avoid as much latency as possible.
  - To persist things to the DB, there is a separate task running that writes to the DB. Depending on what data you're storing, you can either communicate via a channel that your state has changed and should be read or you can just send the updates via the channel directly. In the first case, you'll want to store your document in something like a left-right. In the second case, your persistence task can probably write directly to the DB.

- Meilisearch does something extremely similar; they call it autobatching requests. 

- 
- 

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
# discuss-arch-per-user 👣
- ## 

- ## 

- ## [Plane: Per-user backends for web apps | Hacker News _202210](https://news.ycombinator.com/item?id=33178797)
  - Plane came from our desire to build tools that have the low friction to use of running in the browser, but use more memory and compute than the browser will allocate. The basic idea is to run a remote background process, connect to it over WebSocket, and stream data.
- A related and also very useful usage pattern: "backend instance per customer". 
  - Because… There are many ways to implement multi-tenant SaaS; but a highly underrated approach is to write a single tenant app, then use infrastructure to run an instance of it per (currently logged in) customer. Plus a persistent database per customer of course.
  - This has the tremendous advantage that you can add another column to your pricing page easily: the "bring a truckload of money and we will set you up to run this behind your firewall" tier. There are still a lot of orgs out there, large ones with considerable financial capacity, who really want this.

- The implementation makes some weird choices like rebuilding a bunch of services like DNS, cert, weird dependency on SQLite. Wish people would stop reimplementing Kubernetes and just build on top of it.
  - I think "per-user" is probably the wrong killer feature for something like this. Much more potential in shared distributed processes that support multiple users (chat, CRDT/coauthoring). Appears that the underlying layer can probably do that.

- This seems similar to an Elixir/Phoenix use case where you have a GenServer per user. At first glance, it seems like that approach would be functionally equivalent.
  - Yes, the BEAM/OTP/{Erlang/Elixir} stack is unique in that it provides similar primitives as part of the runtime.
  - My impression of that approach is that it’s good for IO-bound work and stateful business logic, but less so for the CPU/memory-bound applications that we’re targeting. I’d love to know if there are counterexamples to that though. It’s admittedly been over a decade since I touched Erlang and I’m not up to date, only peripherally familiar with Elixir and Phoenix.
- Yes, for CPU bound processed on the BEAM you'll want to use a NIF (native implemented function) but that leaves you open to taking down the entire VM with bad NIF code (segfaults, infinite loops, etc). 

- I think CouchDB kind of has a db per user kind of model. I was wondering, what's the best way to persist a session. This kind of per-user model I think is super useful for local-first, decentralized apps.

- This is the same concept that Cloudflare has with Durable Objects. 
  - Yes, DOs have a similar approach. Plane is sort of like DOs but using containers instead of V8 isolates, allowing you to run code that couldn’t run in the browser (either for cpu/memory needs, or because it just won’t compile to JS/wasm).
- If I remember correctly, CF liked isolates because they have a superb cold start time. How does Plane do there?
  - On the order of a few seconds, which is certainly slower than isolates, but fast enough to e.g. spin up a Jupyter backend in a reasonable amount of time. We're playing around with some ideas to make it even faster, like snapshotting.

- most messaging apps and almost all bi-directional websocket based apps do something very similiar. mobile apps/webapps become thin clients with a web socket.
  - that said, it's nice to abstract it away, and with a container - makes it very generic which is nice.

- 
- 

# discuss-db-per-user 👣
- ## 

- ## 

- ## 

- ## Apps used to have one database for multiple users. Now many have one database per user. Soon we will have multiple databases for each user.
- https://x.com/jamespearce/status/1943114966162379234
  - This is a pattern I find myself using increasingly with @tinybasejs : some of a user’s app data is private. Some is local. Some is in the cloud. Some is shared. Some is synced. 
  - Makes sense to shard it out into different databases altogether, each with different behaviors.

- ## We are writing a massive multitenant database at Turso. A node is capable of running hundreds of thousands of databases, concurrently. 
- https://x.com/iavins/status/1900220354985169332
  - We also decided to write our own asynchronous runtime implementation (instead of using `Tokio` ) for reasons. Now this bad boy is all bare bones, we don't use Rust's `async` yet.
  - For disk or network we use io_uring (of course). Since it's a database, that's pretty much all it does: talk with io. And that requires a state machine. You submit a request, wait for some time to poll or for callback to trigger. That means, a function doesn't always have a result ready; sometimes it says, my friend wait for sometime, I don't have result ready yet: `Ok(None)` . When it's done you get: `Ok(Some(T))` .
  - The entire codebase is pretty much `Result<Option<T>>` 

- Fallible Iterators also use Result`<Option<T>>. Ok(Some(T))`: when there's valid next item. Ok(None) when iteration's complete.

- ## The idea of having a separate database per tenant in a multi-tenant application always felt way too complicated to me.
- https://x.com/marcelpociot/status/1802942305143296136 
  - But now I'm thinking: doesn't SQLite make this a lot easier?

- We use separate DBs per tenant and it's a lifesaver, for a couple reasons:
  - you can bill tenants for their DB Usage
  - you don't have noisy neighbours
- The core issues with it (we use it for HelpSpot for legacy reasons) is schema changes are burdensome as things may go wrong in one account, but not another etc. On the other hand, it does mean things only go wrong with one customer in that case and not all the customers! So overall for our scale and desired stress level I do like it. 

- ## 🐛 read this before you go do the “db per user” pattern
- https://twitter.com/thdxr/status/1766450800425865279
  - it makes a lot of things harder
  - you cannot easily query across customers and while your primary application might not need to do this, internal functions often will
  - any analytics questions you have, any admin or operations workflows require extra special architecture
  - it forces replicating your data into a central place way earlier (we used bigquery) but that only works for reads
  - schema and data migrations need to be fanned out N times - lot of stuff you have to invent for this
  - it was worth it for us given the specific circumstances but i doubt i’d really ever do it again
- Not to mention the problems you hit if/when you need a product feature to share data between users.
  - What is the problem you're really trying to solve with db per user? Authorization. This is why I'm a fan of things like row level security.

- What’s your opinion on something like ATTACH in SQLite. Allows you to connect to multiple DBs in a transaction. Would something like that have solved your issues?
  - that maybe could have been helpful but probably still needs a few exotic things
  - we used lmdb (similar, single file on disk) and the problem was not all files were on the same machine

- Was doing this with Replicache + Turso and it definitely makes some things a bit more annoying
  - I asked yesterday about the schema and data migration issue and they said they will have something to solve that in their launch week soon

- Had to go in this direction of multi-tenancy two years back and instead chose to use RLS with custom policies in PostgreSQL to achieve the logical isolation.

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

# discuss-multi-tenants
- ## 

- ## 

- ## 

- ## 

- ## [Multi-tenant SaaS Architecture: PostgreSQL Schema per Tenant vs Shared Database vs Database per Tenant : r/PostgreSQL _202606](https://www.reddit.com/r/PostgreSQL/comments/1ucs1ap/multitenant_saas_architecture_postgresql_schema/)
- Row level security to make it impossible to access data that is not yours, and table partitioning per tenant for large amounts of data. This also reduces the need for indexes on the tenant id since all data in the partition belongs to a single tenant.

- We do both. Free users get shared database with low specs, we also route the requests to specific instances. Premium users get premium stuff. Per tenant database and depending on size, per tenant instances. Pretty easy to manage nowadays.
# discuss-db-in-memory
- ## 

- ## 

- ## 

- ## 

- ## 

- ## ⌛️ In-memory database systems were a game changer when they first came out in the early 2010s. But it looks like everyone moved back to persistent storage.
- https://x.com/cedar_db/status/1863986711845306799
- 📝 [The History of the Decline and Fall of In-Memory Database Systems | CedarDB - The All-In-One-Database _202412](https://cedardb.com/blog/in_memory_dbms/)
  - So what did we learn from the story of in-memory database systems? 
  - For one thing, main memory capacity is now enough to fit a significant share of data, allowing us to rethink data processing algorithms. 
  - Also, it is important to try to take advantage of new trends in computer hardware so as not to get stuck with the performance and capabilities of the current generation. 
  - However, the painful lesson is that committing to a single technology is a huge gamble that is unlikely to pay off. 
  - So it is important to be prepared for future changes in all components of the system, from the storage layer to address the cloud, to join algorithms for time series, to completely different data models.
  - Regardless of whether CXL takes off, and whatever other trends the future brings, building a modular system that allows components like the storage tier to be easily swapped out seems like the best way forward.

# discuss-db-cloud
- ## 

- ## 

- ## [Repl.it Database | Hacker News _202009](https://news.ycombinator.com/item?id=24472941)
- Can I ask what you're using under the hood to power this?
  - It's Postgres under the hood. The key-value service itself is Go and we run it on GKE alongside some of our other services.
- For filtering/search queries, is the idea to use the prefix system to group related items together, and then run matches using that?
  - Yep, that's the idea. If you had a user with ID 1, one scheme to get all her info could be storing attributes in keys. Then a prefix search for "user:1:" would get you the relevant keys for that user.
  - But you could also go another way and drop a JSON-encoded object in a single key and work with it inside your app, since that might be the fastest way to get something off the ground!
- I didn't look super closely, but it looks like your database works similarly to DynamoDB, in which case it could use similar data modeling. Here is a great post on single table design for DynamoDB that would probably be mostly applicable here: https://www.alexdebrie.com/posts/dynamodb-single-table/ The post author actually wrote an entire book on data modeling with a single key/value table.

- This sounds like a database-per-tenant architecture, which is something I'm interested in. Are you having to build a lot of custom tooling to manage that many databases? Does the existing repl.it code make it easy to just spin up an extra docker container for each session? Or are there off-the-shelf tools that make this easy?

- Did you consider SQLite for this?
  - We did! Our infrastructure has some unique constraints around filesystem persistence. We use btrfs and regularly take snapshots of the repl's filesystem while someone is editing the repl. However, we don't take snapshots when a repl is only acting as a web server without anyone editing it, meaning that we would need a solution that lives outside of the repl's filesystem.
  - Keeping each database outside of the filesystem also gives us the flexibility to let people access the same database across multiple repls in the future.
  - I have lots of love for SQLite; early prototypes of Database were backed by it!
- Totally makes sense - SQLite is very dependent on a traditional filesystem. I've been figuring out how to run backups recently and grabbing a copy of the file isn't enough - you need to be sure there are no transactions going on, so you need to use the SQLite backup API or run VACUUM INTO a separate copy, which then doubles the amount of disk space you need.

- Having a simple database it a great feature for prototyping, but I think having custom Dockerfile support would be even better.
# discuss-storage-compute-separation
- 分离案例
  - known: clickhouse, quickwit, kafka, neondatabase, yugabytedb, Doris v3+, xtdb v2, OrioleDB, PolarDB
  - 可参考前端状态管理/db的持久化方案
- tips
  - [Ramifications and status of 'Separation of Storage and Compute' (mentioned in 2022 Roadmap) · Issue · ClickHouse/ClickHouse](https://github.com/ClickHouse/ClickHouse/issues/41791)
  - [A Comparative Study of Storage and Compute Decoupling - RisingWave: Real-Time Event Streaming Platform _202407](https://risingwave.com/blog/a-comparative-study-of-storage-and-compute-decoupling/)

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Ramifications and status of 'Separation of Storage and Compute' (mentioned in 2022 Roadmap) · Issue · ClickHouse/ClickHouse _202209](https://github.com/ClickHouse/ClickHouse/issues/41791)
- ClickHouse already support the usage of S3 and HDFS as table engine. By using them, you are effectively separating compute and storage, and you can scale either of them independently.

- [Clickhouse计算与存储分离调研 · Issue · cloudnativecube/octopus _202103](https://github.com/cloudnativecube/octopus/issues/48)
- mergetree引擎支持S3
  - replicatedmergetree 引擎支持S3
- insert：
  - 用户直接将数据插入到某一个replica后，其他replica会通过zookeeper进行感知，将元数据从该replica fetch过来加载到内存和写入本地以保持同步（同理，新加入replica也会如此而进行同步），元数据文件存储在本地磁盘，但是文件里的内容其实是s3的文件名，真实的数据统统存储在s3上，所有replica共享这些数据，当有多个replica同时操作共享文件时会对文件进行加锁，从而保证数据的一致性。
- merge:
  - 多个replica可以让其中一个replica做merge操作，其他replica等他其merge操作完成后，向其索要merge后的元数据文件保存到本地，从而减少性能损耗。
- select:
  - 经过验证目前是可以支持分布式表查询多个shards(均共用底层s3存储)，从而支持并发查询，查询请求可以落到多个replicas(水平扩缩)，底层共用s3存储。
- delete:
  - 在进行删除操作时，clickhouse内部会有share data lock机制，该机制确保所有的replica的元数据全都删除后才会真正的去删除s3对象存储上的数据。

- cloud.tencent.com/developer/article/1759109 腾讯云CK计算存储分离的经验

- ## It's wild that @databricks chose to pay $1 billion (with a 200x multiple) for the slowest Postgres, @neondatabase _202506
- https://x.com/pucchkaa/status/1933650926365257993
- I think this is because of their decoupled architecture where they separate the storage and the compute. This gives them benefits like autoscaling, serverless, branching etc. but comes with an unavoidable network hop from compute to pageservers. They use WAL for decoupling.
  - This does remind me of @isamlambert tweet where he mentioned why it might be bad to separate storage and compute. Planetscale got some really good raw performance with NVMes.

- But it's serverless

- https://x.com/nikitabase/status/1725394868619342198
  - It's MUCH easier to scale stateless systems - so let's separate storage and compute. Storage is a glorified key value store (okay a bit more than that but close). So now we can turn Postgres on and off and move it from one machine to another and not lose state. This is key!
  - When a query comes in it hits our proxy which forwards it to the right Postgres process. But where should the Postgres process live? VM, container, bare metal?
  - There are many reasons to use VMs. Primarily due to security boundary and live VM migrations (more on that later)
  - You can also use containers. In this case you need to be sure that an attacker won't break out of the process. Postgres and its extensions are NOT secure by default and hence container didn't work for us.

- [Why separating storage and compute can be a problem for OLTP workloads. | PlanetScale posted on the topic | LinkedIn _202506](https://www.linkedin.com/posts/planetscale_while-separating-storage-and-compute-has-activity-7333155501230243843-ONWt)

- ## Every time we separate compute from storage, we bring it back together it seems. And then we do it again a decade later. _202503
- https://x.com/kellabyte/status/1900649147234955489
- is this about the PlanetScale’s?
  - Yup but also just a general observation
- I know the planetscale folks are pushing hard on Metal, but Aurora/AlloyDB/SQL Hyperscale are all tiered systems already.  They cache hot data on fast local NVMe disks on the same machine as the SQL compute ("SSD Cache" in the diagram here)

- That's a natural cycle, I think. 
  - 1) Separate to get perf from parallel access, then 
  - 2) combine again when HW has caught up and remove complexity.

- IMO, all the approaches have pros and cons. It is about tradeoffs and the problems you are trying to solve. Vendors make it very hard to have this discussion and don't acknowledge the tradeoffs. There are legit benefits for storage/compute decoupling for OLTP, and there are definite benefits of putting every component of an OLTP on one machine.

- With @spacetime_db we're skipping right to the next decade.
# discuss-scaling
- ## 

- ## 

- ## 

- ## Scaled from 1, 000 to 100, 000 users. Here's what broke.
- https://x.com/brankopetric00/status/2011561755927826910

At 5, 000 users:
- Single database became the bottleneck
- Added read replicas

At 20, 000 users:
- Session storage overwhelmed Redis
- Switched to JWT tokens

At 50, 000 users:
- File uploads killed our servers
- Moved to S3 with presigned URLs

At 75, 000 users:
- Search became unusable
- Implemented Elasticsearch

At 100, 000 users:
- DNS became single point of failure
- Multi-region with Route53 failover

Every stage felt like the final architecture.

None of them were.

Scaling isn't a destination. It's a continuous series of bottleneck discoveries.

- your DB broke at 5k users what the fuck was it a json file?
- At 5, 000 users: - Single database became the bottleneck - Added read replicas This seems unlikely - We have 25k users on a single db and it works flawlessly.

- A single DB became a bottleneck at 300k users for us, but we could solve it with partition schemes and scale to millions. Just added some read replicas for dashboard and report generation.

- I think most people scale too early.
  - That's also true, wast on cloud resources is crazy.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Easier to think of a database = storage layer + data model + query layer (language + optimizer)
- https://x.com/redixhumayun/status/1919669471377310166
- I don't think query layer in necessary. AFAIK rocks doesn't have one. API is all you need.
  - Query layer makes a lot of things easier though. Also hard to write performant queries without an optimizer Data model is the logical structure of the data - relational or document etc

- Same spirit pursued by Apache datafusion project. 
  - Query + data model + storage. 
  - Datafusion gives these components as composable pieces => acts as LLVM for databases .

- ## 现在数据库用 Rust 写 extensions 越来越流行了
- https://x.com/yihong0618/status/1860542339267330185
  - pg -> pgrx
  - sqlite-> sqlite-loadable-rs
  - duckdb -> extension-template-rs

- ## 🎞️ How Zoom supports 300 million video calls a day:
- https://x.com/systemdesign42/status/1806551695331139635
  - They use scalable video coding (SVC) to stream video
  - SVC scales well because it sends only a single video stream
  - They separate video stream processing from stream routing
  - The client processes the video streams to reduce server load
  - They send separate video streams from each participant to the client
  - They do multimedia routing to send streams at low latency
  - They set up the client to check the stream quality
  - They use UDP to send video data

- ## 根据我个人 10 几年的企业应用经验，总结出的企业信息化系统的设计规范描述方法论：
- https://twitter.com/xqliu/status/1789127844435521880
* 业务模型设计（相当于数据库设计）
通俗的说，就是有哪些数据库表，有哪些字段，表之间的关联是什么样的
* 表单设计（包括 CRUD 和多步骤表单）
各个对象的 CRUD 表单都是什么样的，字段有哪些需要设置默认值、需要特殊校验、字段之间需要联动、动态显影、字段如何分组、各个表单都开放给什么用户等。
* 仪表盘设计, 从业务需求角度，需要创建哪些大屏仪表盘，每个仪表盘有哪些 Widget 等。
* 对象生命周期设计 （CRUD 每个节点的逻辑设计）, 每个对象的 CRUD 生命周期有哪些校验、集成、额外的业务逻辑等。
* 核心流程设计（流程审批等）。 对象的生命周期，是否有相关流程关联。
* 动态操作设计（对于类及对象有哪些操作）, 对于每一类对象，都有哪些业务层面的操作，这些操作是对哪些用户启用，启用的逻辑是什么，具体操作的逻辑又是什么。
* 系统间集成设计。 有哪些对接的第三方系统，具体集成的方向、方式各是什么，尤其特殊的几类是：SSO 单点登录和用户、组织架构同步，这往往在项目实施中是必选项。
* 定时任务设计。根据业务需求，需要做哪些定时任务的设计，包括系统启动时运行、单次运行、周期运行等等。
* 报表及单据打印设计。业务上有哪些报表需要设计，有哪些单据需要设计打印版式。
* 界面交互设计。需求方有没有特殊的界面交互需求，如果有，先使用原型工具画出交互全过程。
- 基本上以上的后台逻辑理清了之后，企业应用开发需求后台逻辑的 80% - 90% 大概已经理清了。
- 其中比较核心的几点是
  1. 整体的业务模型设计
  2. 对象生命周期管理及设计
  3. 动态操作设计
- 我们的系统是真正将企业信息化数字化过程的最佳实践，通过系统设计的方式，固化到我们的低代码平台中了。同时，针对其中比较容易跑偏，坑比较多的点，也利用系统的核心架构，做了相应的防御和应对。
  - 按照我们系统的范式来进行企业信息化系统的设计，一定错不到哪里去。使用我们的牧言低代码平台进行企业信息化系统开发，不管是对客户，还是对内部业务部门，一定可以成功快速交付。

- ## 简明易懂的分片原理教程，来自Architecture Notes——这家网站真的是宝藏，里面有不少带有漂亮手绘图的好文章。
- https://twitter.com/huangzworks/status/1776087981214101659

- ## Use synchronous by default, asynchronous when necessary.
- https://twitter.com/RaulJuncoV/status/1770789583375974471
- Sync is more convenient in most cases. But can lead to low scalability, reliability, and other undesirable characteristics.
- Async can provide performance benefits and scale. But can present a host of headaches:
  • data synchronization
  • deadlocks
  • Race conditions
  • Debugging, and so on

- ## 4 must-know strategies to build high-availability systems:
- https://twitter.com/ProgressiveCod2/status/1768176860037517417
- [1] Replication
  - Involves duplicating data on servers spread across different locations & data centers  
  - If one server goes down, the other can support the workload  
  - Also, protects against data loss by increasing durability

- [2] Load Balancing
  - Distribute traffic across multiple servers to share the load  
  - This ensures no single server gets overwhelmed by incoming requests  
  - Also, if certain servers go down, other servers are present to take over

- [3] Auto Scaling
  - Sometimes a dramatic increase in load can result in a loss of availability  
  - Auto-scaling helps a system scale out based on demand
  - This ensures that the overall availability is not impacted

- [4] Rate Limiting
  - Denial-of-Service attacks can cripple a system’s availability
  - Rate limiting based on IP addresses or users can ensure that the system is not abused by a malicious actor  
  - This ensures that genuine users are not impacted

- Backups and disaster recovery plans
- Auto Scaling is critical for elasticity! Just make sure to set your Rate Limiter to avoid a surprising bill

- ## 🌰 Memory allocation by layers in YugabyteDB:
- https://twitter.com/FranckPachot/status/1767219717037490550
  - YSQL (PostgreSQL backend), visible in pg_stat_activity.allocated_mem_bytes
  - DocDB Block Cache for reads (Block Based Table)
  - DocDB MemTable for writes (Tablet Overhead)
  - goes to SST Files when flushed

- ## Database-per-Service said each service should have its own private database. You can only access the data through its API.
- https://twitter.com/RaulJuncoV/status/1766092301955113113
  - In monolithic architectures, different parts of the application share data schemas.
  - Imagine you need to remove the Foreign keys and Views from your database.
  - That's what you have to do if you want a Database-per-Service pattern in microservices.

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
- There are **a lot of headaches involved with the "tenant per schema" approach** . Certainly it was nice to never have to worry about the "customer is seeing data from another customer" bug (a death knell if you're in enterprisish B2B software), but it added so many problems:
  - Migrations become a very expensive and time-consuming process, and potentially fraught with errors. Doing continious-deployment style development that involves database schema changes is close to impossible without putting a LOT of effort into having super-safe migrations.
  - You'll run into weird edge cases due to the fact that you have an absolutely massive schema (since every table you have is multiplied by your number of tenants). We had to patch Rails to get around some column caching it was doing.
  - Cloud DB hosting often doesn't play nice with this solution. We continually saw weird performance issues on Heroku Postgres, particularly with backup / restores (Heroku now has warnings against this approach in their docs)
  - It doesn't get you any closer to horizontal scalability, since connecting to a different server is significantly different than connecting to another schema.
  - It will probably push the need for a dedicated BI / DW environment earlier than you would otherwise need it, due to the inability to analyze data cross-schema.
- I still think there's maybe an interesting approach using partioning rather than schemas that eliminates a lot of these problems, but apartment probably isn't the library to do it (for starters, migrations would be entirely different if partioning is used over schemas)

- Can confirm, here be dragons. I did a DB per tenant for a local franchise retailer and it was the worst design mistake I ever made, which of course seemed justified at the time (different tax rules, what not), but we never managed to get off it and I spent a significant amount of time working around it, building ETL sync processes to suck everything into one big DB, and so on.
  - **Instead of a DB per tenant, or a table per tenant, just add a TenantId column on every table from day 1** .

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
