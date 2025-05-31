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

- ## While SQL has its own limitations, scaling was actually the reason why FaceBook, UBER, Pinterest, Shopify, and Airbnb use MySQL instead of NoSQL databases.
- https://x.com/vlad_mihalcea/status/1885692781743555061
- Yes, MySQL scaled huge at FB/Uber/Airbnb, but let's not forget Netflix/Google/Amazon crushing it with NoSQL. Truth is: both scale well => pick based on your actual needs, not hype. Sometimes MySQL wins, sometimes NoSQL does.

- ## Decided to resurrect an old project this weekend. Embedded InnoDB.
- https://twitter.com/sunbains/status/1761628685973782870
  - Based on 5.1, a very old code base, but a lot simpler too. Should be good for learning. 
  - It's still the original C code, before the core optimizations and conversion to C++.
  - The long term plan is to slowly convert it to Zig (or Rust). Zig for now because it's easier to get started.

- People still use MySQL v5.1 in production, so this is not a toy storage engine. Last time this code was used in anger was in Riak AFAIK.
# discuss-perf
- ## 

- ## Now there are some numbers to put behind MySQL 8 performance regression, and they look pretty bad.
- https://twitter.com/kibertoad/status/1758800348490367046
- For comparison, here is the perf change over PostgreSQL versions: 
  - [Small Datum: Postgres versions 11, 12, 13, 14, 15, and 16 vs sysbench with a medium server _202310](https://smalldatum.blogspot.com/2023/10/postgres-versions-11-12-13-14-15-and-16.html)

1. If you don't expect any heavy load anytime soon — SQLite3
2. If you expect some load but don't need scaling — PG
3. Need heavy scaling — CRDB
4. WordPress — use whatever MySQL version it supports, how cares
# discuss-myrocks
- ## 

- ## 

- ## [你觉得MyRocks怎么样？ - 知乎](https://www.zhihu.com/question/271844793)
- MyRocks是MySQL的一个分支；MySQL的默认引擎是innodb，用rocksdb替换innodb就分支为MySocks。
  - innodb读性能远大于rocksdb；但是rocksdb的优点是写更快、存储空间占用更小（紧凑存储）。
  - innodb的B+树，在分裂时，会造成至少50%的空间浪费
  - rocksdb的SST可以将空间浪费控制在10%以下。
  - RocksDB 占用更少的存储空间，还具备更高的压缩效率，非常适合大数据量的业务。
  - RocksDB 采用追加的方式记录 DML 操作，将随机写变为顺序写；非常适合用在批量插入和更新频繁的业务场景
  - RocksDB 中的每一条记录都有一个 sequence number，这个 sequence number 存储在记录的 key 中。sequence number 是实现事务处理的关键，同时也是 MVCC的基础
  - MyRocks 目前只支持一种锁类型：排他锁（X锁），并且所有的锁信息都保存在内存中。在 RR 隔离界别下只在主键上实现 gap 锁。
  - RR没有解决幻读，因为MyRocks只实现了主键的gap-lock，没有实现辅助索引的gap-lock。事务的条件语句中如果含有辅助索引，那么将出现幻读问题。

# discuss-vendors
- ## 

- ## GitHub的数据库是MySQL，从5.1一路更新到8.0, 没有使用分布式数据库，数据量变大之后是拆分微服务并且垂直分表
- https://x.com/changwei1006/status/1877603560038293530
  - 在水平拆表之前使用SQL linters优化查询并确定拆分边界，后期使用Vitess实现MySQL扩展

- ## wesql: MySQL distribution which uses S3 as storage backend
- https://x.com/iavins/status/1859985872227344451
- The founder of this project was the founder of PolarDB, which is Aurora of AliCloud. WeSQL does share some design with neon, but this has already became the standard scheme to build a cloud database.

- slatedb dose this too

- what are the deciding factors for relying on an object store vs directly manipulating "disk" blocks (EBS maybe)?
  - The readme and their site talk about benefits. It's mostly for reliability and ease of scaling as you don't need to manage the infra.
- I wonder how this is implemented on a relatively coarse grained API like S3 without compromising on query execution latency. For example to list multiple objects they would've to issue individual getobject calls
  - Depending on the use case, the data transfer costs can also be enormous

- if it works with S3 compatible systems, should work with Minio right?
  - yes. it is S3 compatible, so Minio etc should be fine.
- According to the bug tracker cloudflare's S3 compatible storage doesn't seem to be supported yet. Not sure if http://min.io is more compliant?
  - Not supported yet but it’s on their roadmap.

- That will be very expensive if not written well. Ops on S3 actually cost a lot. Hopefully they do some sort of local WAL and then push to S3. Will check it out for sure
  - litestream (similar project but for SQLite) is rather cheap in practice, and afaik is implemented exactly this way (WAL)

- S3 performance sucks.  Using it as a store for a relational database is questionable.

- that's indeed a fascinating approach. Currently we are using Debezium to load change data capture stream into S3. This solution seems promising for me.

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

# discuss-devops-mysql
- ## 

- ## 

- ## [Connection Java - MySQL : Public Key Retrieval is not allowed - Stack Overflow](https://stackoverflow.com/questions/50379839/connection-java-mysql-public-key-retrieval-is-not-allowed)

```
jdbc:mysql://localhost:3306/db?allowPublicKeyRetrieval=true&useSSL=false
```

- [Troubleshooting DBeaver: “Public Key Retrieval is not allowed” Error ](https://medium.com/@kiena/troubleshooting-dbeaver-public-key-retrieval-is-not-allowed-error-29f203d745c5)
- Open DBeaver and navigate to your database connection. Right-click on the connection and select “Edit Connection”.
  - Go to the “Driver Properties” section. Locate the property named “allowPublicKeyRetrieval”. By default, it is set to “false”. Change the value of “allowPublicKeyRetrieval” to “TRUE”.

- ## Built a MySQL branching tool for GitHub Actions - similar to PlanetScale but runs directly in your CI/CD pipeline. 
- https://x.com/earayu/status/1871833634703131094
  - Create database copies and test schema changes without touching prod.
  - [MySQL Branch Action · Actions · GitHub Marketplace](https://github.com/marketplace/actions/mysql-branch-action)
- love this functionality. i recall that when Minio was first started, it took a test-environment-first strategy, and it finally proved to be a successful strategy to attract adopters.
  - Indeed, database access in CI/CD pipelines has always been a challenging issue, particularly when dealing with test data and executing DDL statements.
  - Currently, we offer an experience similar to PlanetScale. Moving forward, we aim to match the developer experience provided by Neon.

# discuss-news
- ## 

- ## 

- ## Introducing JavaScript support in MySQL_202312
- https://twitter.com/OnlyXuanwo/status/1736439160402243750
  - Enterprise Edition only
  - Presented in Percona Live 2018. Finally, although it seems it's not OSS
- I wish for this feature to be added to MySQL Community Edition. Shifting business logic to the front end is a trend, and the ideal future architecture would be front end plus service-oriented databases. This could mark MySQL's move towards service orientation.
- I didn't experience the era when stored procedures were popular. Are they truly useful? It seems that today's frontend developers prefer to manage everything on their own.
  - I don't like procedures either; they lack capabilities such as version control and canary releases that code has. I believe the front end simply desires a user-friendly SaaS database.

# discuss-distributed/replication
- ## 

- ## 

- ## MySQL Cluster nodes assemble using std TCP/IP.  
- https://twitter.com/frazerclement/status/1778021984200249434
  - Dataplane then setup as a mesh of Transporters, by default using OS TCP/IP (over loopback, Ethernet, Infiniband...)  Co-located API+Data nodes use a Shared Memory Transporter for perf.

- ## 🧩 Tables + indexes are horizontally partitioned across #MySQL Ndb Cluster nodegroups for read + write scale out.
- https://twitter.com/frazerclement/status/1767715870984282225
  - Fully Replicated (FR) tables are instead replicated to every nodegroup trading write scale + storage for read scale + locality.
- The MySQL optimizer like Postgres assumes a single node. How does that work with NDB Cluster data distribution across the nodes?
  - Yes the MySQL optimizer is not aware of data distribution or intra query parallelism.  The Ndb SE supplies controlled table + index statistics and engine capabilities to the optimizer to influence the execution plan.
  - The Ndb SE also identifies operations, filters and nested-loop query fragments that can be shipped to the data nodes for execution to reduce data transfer.
  - A transaction coordinator (TC) instance on the data nodes routes operations and query fragments to data nodes containing the relevant partition replicas for execution, in parallel if possible or required.
  - Query fragments are handled by a special component in the data nodes called SPJ which performs a [parallel slice] of a parallel query, and may involve routing subrequests to other data nodes if required.
  - So the data distribution is primarily handled across the Ndb storage engine (SE) layer in the MySQL Server, the NdbApi and the Transaction Coordinator (TC) and Select-Project-Join (SPJ) components in the data nodes, rather than the MySQL Optimizer.

- The fully replicated tables are very useful for lookup tables, so the joins can happen locally.
  - Yes, this is a good use case - e.g. dimension tables in a star schema.  The resulting join is effectively a Distributed Parallel Partitioned Hash Join.
- Yes especially for tables that are quite static and small and don’t have the same partition key of the main ones. Guys looking at this conversation is a jump in the past! I miss all of you so much.
- Good point. Intuitively you would think that it is better to fully replicate as small a number of tables as possible, but in a star schema fact_tables >>> dimension_tables, so this makes sense.
# discuss-internals-mysql
- ## 

- ## MySQL builds the best join plans incrementally to make sure it figures out the most optimal join order. 
- https://x.com/arpit_bhayani/status/1908147587397439653
  - It goes from single-table access paths to 2-table joins, then to 3-table joins, and so on. As an optimization, it prunes any subtrees that are guaranteed to result in suboptimal costs.

- ## InnoDB default setting IIRC is to use DIRECT IO not buffered IO.  Only the WAL uses buffered IO always.
- https://twitter.com/sunbains/status/1757237923219656991
  - If you want to have fun look at the algorithm inside InnoDB for writing out zip pages, it needs to trade off between CPU and IO.  
  - Another fun area in normal background flushing is the complication to determine the batch size and select which pages to flush to persistent store. Especially when there are very few (or none) free pages. This is what makes storage engine design and implementation fun 

# discuss-cdc-mysql
- ## 

- ## 

- ## [How To Use Triggers to Track Changes in MySQL | Hacker News _200805](https://news.ycombinator.com/item?id=182529)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 优先使用 MYSQL 这种最简单，最不容易出错，最好招聘，资料和工具最丰富的技术，因为项目成功率本来就低
- https://x.com/skywind3000/status/1860161984056135837
  - 前期探索又尝尝变来变去，你应该把时间花在快速迭代上，等 dau 过百万了，项目也挣大钱了，需求也稳定了，那时候你招堆人进来爱换啥换啥。
- 什么sql不重要。业务还没起飞，就设计一套扛住春运期间大流量大并发的抢购架构，这就是过度设计。整个技术团队的偏好或者玩的比较熟的是最好的，等业务起飞了，遇到瓶颈了再来考虑换啥。市面上某些公司某些团队，业务QPS不超过100，系统用户不过千，微服务、集群、k8s、配置中心、多级缓存、读写分离

- PostgreSQL 比 MySQL 简单啊, 你看文本都不用区分类型，直接 TEXT，时间戳也不用担心精度和范围，TIMESTAMPTZ 微秒管够。索引想怎么建就怎么建，永远有回转空间。
  - pgsql运维比mysql难招

- 我的项目也这样，而且MySQL也直接用云厂商的RDS，不用自己维护，不够用时升下配置就好。暂时没碰到扛不住的情况。

- 必须是pg，既支持关系数据，也支持对象存储，还支持向量存储，最关键是真正免费，没有license限制。

- ## Interesting to compare how Uber and GitHub approached their upgrades of MySQL to 8.0 differently
- https://x.com/rmoff/status/1824510857293811765

- ## Grouping transaction effects together in #MySQL Ndb Cluster epoch transactions improves the computation 2 communication ratio per Binlog transaction, improving compression, storage + communication, increasing apply parallelism + optimising commit processing. 
- https://twitter.com/frazerclement/status/1763275358663541190
- It is the old systems trick of batching for performance. Just, most people don't Conover it for OLTP. Sequential disk writes no longer as big a requirement with nvme.
  - Performance is improved @ the source too as independent commits are unordered. Defining + recording an artificial commit order for discrete transactions for the Binlog @ the source would be a waste.  They are batched and ordered on epoch boundaries only avoiding unnecessary coord
- Yes, it's a different tradeoff on coordination between processes compared to existing systems. The only required coordination between transactions is a timestamp for its epoch - but without the need for an oracle service handing out transaction IDs. Replace that service with a periodic global transaction commit protocol is a good tradeoff for many apps, IMO.

- ## 美团做的这个MySQL的优化也太极限了
- https://twitter.com/changwei1006/status/1722343947459330417
  - [Intel PAUSE指令变化影响到MySQL的性能，该如何解决？ - 掘金](https://juejin.cn/post/6844904129626636302)
- 还不够极限，既然他已经 target 具体 intel 处理器，sapphire rapids 上还可以用 tpause 指令来替代这种多次 pause 在自旋锁场景下。能够更好优化 CPU 的 thermal 管理从而让锁的另一侧的性能提升，能有更好的性能。dpdk 里就是这么做的。

- ## GitHub 使用MySQL的原因😂：
- https://twitter.com/Hooopo/status/1629399543740788742
  - “我们几乎早就从 MySQL 迁移到 Postgres，甚至有一个分支正在运行，但我为私人消息功能编写的一些可怕的 SQL 查询在 Postgres 中不起作用。所以，MySQL留了下来。”
  - I remember there being a "GROUP BY" from hell that I had trouble rewriting, and eventually gave up. Probably was using some MySQL-specific features.
