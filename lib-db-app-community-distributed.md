---
title: lib-db-app-community-distributed
tags: [community, database, distributed]
created: 2023-10-26T19:03:45.307Z
modified: 2023-10-26T19:04:00.318Z
---

# lib-db-app-community-distributed

> about database distributed/decentralized

# guide
- openraft's raft implementation is solid!
# discuss-stars
- ## 

- ## I learned today that TimescaleDB deprecated their distributed (multi-node) support
- https://twitter.com/a_prout/status/1777813707327684750
  - It reminded me that distributed databases come with a cost
  - [Distributed SQL Databases And The Costs of Being Distributed | by Adam Prout | Medium _202401](https://medium.com/@adamprout/distributed-sql-databases-and-the-costs-of-being-distributed-ab7b38b0fa50)

- ## 🆚️🤔 [有了分布式数据库，是不是就不需要分库分表了？ - 知乎](https://www.zhihu.com/question/356734992)
- 分布式数据库不能阻止你把一个表或者库搞的和宇宙争大小, 用好数据库永远需要人的参与，系统无法解决这个问题

- 不需要分库分表了，但是大多还会让你指定拆分键。 即使 SQL 不带 sharding key 也能执行，但是性能（尤其是 latency）也会打个折扣。 no silver bullet

- 只是不要手动分库分表，并不代表内部实现没有分库分表，数据库产品内部按照某种规则来帮助用户自动在线扩容而已另外自动分库分表虽带来了便利，但也带来了其他问题，如一些功能受限，或者性能下降等等

- 分布式数据库也无法避免，对于某些特殊表，要在运维层面手动设置分表逻辑，但是至少在应用层面可以不分了
  - 某些帐套型数据，分表其实不止是性能问题，结算后数据就不能动了，分表会更好管理

- 表大了就要 sharding，和分布不分布式没关系，，，

- ## [目前电商网站服务端是分库分表多，还是使用分布式数据库如TiDB，PolarDB多？ - 知乎](https://www.zhihu.com/question/449874451)
- 架构师应该考虑目前业务发展的阶段, 选择合适的解决方案, 过早优化是万恶之源.
- 首先能做MySQL分库分表这个体量到时候，一般都已经是沉积按年计的数据了，它们之间的表结构关系一定是很复杂的，newsql模仿的是SQL的翻译和解释，但要让如此大体量的关系型数据导入到tidb的key/value存储中，然后还能衔接好表之间的结构关联，这其中的工作量不是说说那么简单的，存储过程问题，列数问题，在迁移过程中各个都会整死工程师。
  - 其次tidb自身的架构也是非常庞大，尤其是使用了rocksdb后，对内存和SSD的强烈需求，而且需要更多的集群节点，那么这就要大动硬件资源配置了。而且tidb、pd、tikv，tispark的四组集群复杂度远远超过几个分库的MySQL，那么运维工程师是否能短期内拿的住这就是很大的疑问了。

- 大多数还是在使用分库分表中间件，用MySQL做存储节点构成若干个存储集群存储数据分片。

- TiDB属于看起来很美好，但实际没那么美好的事情，比如复杂JOIN，数据在多个节点间来回传递导致的网络问题。没有什么数据库包治百病，根据不同需求来做不同取舍吧

- ## [Kafka 为什么要抛弃 ZooKeeper？ - 知乎](https://www.zhihu.com/question/624795964)
- 大数据的生态变了，尤其是hadoop全家桶成为时代的眼泪了。
  - 以前各公司自己搭一套集群在机房里，hdfs，zookeeper这些东西属于是公共的服务。各种乱七八糟的组建都依赖zookeeper不是累赘，是充分利用资源加强可靠性。
  - 但是现在是云计算的时代，讲究的是弹性伸缩。集群在云上，机器，容器的数量大幅增加而且变化很快，甚至有很多托管和saas服务你都不在乎有多少机器。
  - 这样两套分布式系统之间的依赖就成了问题。如果你要新增几百个A服务节点，那么它依赖的B服务节点要不要扩容呢？如果要扩的话，增加多少，怎么保证扩容的过程两套系统的交流不出问题？
  - 这就是要去除zookeeper的原因，也是hdfs被类s3服务取代的原因

- Spark短时间内不会过时。hadoop要学的是集群思维，部署运维这种东西不用下功夫。
  - 国内hadoop还能撑一段时间，因为saas化程度低，自建集群的公司还是有，上云的公司很多是类s3的对象存储搭配纯计算的类emr服务，与其说是hadoop生态的残余，更像是hive metastore的生态。
  - 全上saas全托管的也有，都是有钱的公司。
  - 至于几大厂普遍喜欢自研，涉及到的东西比hadoop要底层。

- 你这只是底层存储变化（HDFS->S3)，本质上没太大差别，不过一个是对象存储，一个是类文件系统存储，对于计算服务来说，没看出本质差别

- Zookeeper加kafka 的架构，有三层角色，一层是zookeeper ，提供基础的状态持久化和状态通知服务。一层是controller ，基于zookeeper 提供的服务，给松散的broker 提供统一的状态服务，但它本身是没有状态服务的，它是依赖zookeeper 的服务来做主控。一层是broker ，无状态服务，因为他们无状态，无法自发组织起来，所以需要controller 为他们做主控。其中有一个broker 兼职了controller 角色。
  - 这个架构本来没什么问题，但是如果要优化，也是可以的。zookeeper 本来提供了状态服务，但是因为它不是kafka 的一部分，所以kafka 不得不设计一个controller 来做主控。假如controller 本身就可以提供状态服务，那上面的三层架构就可以简化成两层，也就是一层controller ，提供主控服务，一层broker ，无状态工作服务。
  - Kafka 抛弃zookeeper 就是做了这样的优化，自己开发了一个基于raft 共识算法的一致性服务kraft，为集群提供之前zookeeper 的状态服务的同时，也为broker 提供主控服务，也就是controller。这样相比之前的架构还有一个很大的优点，那就是controller 的故障切换会非常快，而且切换时间几乎不随集群规模而线性增长。
  - 原因是，以前的架构，controller 只有一个，如果做controller 的故障切换，那么新controller 需要全量从zookeeper同步集群所有元数据信息并构建到内存，来为做主控服务做准备，这些元数据信息包括topic 和分区信息，如果是一个大规模集群，topic 和分区很多，这个过程将会很耗时，也就会造成更久的停机时间。而kraft 的架构，controller有多个，只是只有一个是leader 提供主控服务，其他的作为follower ，会实时同步leader的元数据信息，也就是元数据在多个controller 里面是几乎保持一致的(raft 协议保证的)，所以故障切换的时候，几乎不需要再同步元数据，就可以完成controller 切换。

- 有点意思，Foundation DB也是多个controller的思路

- ## 🌰 When Discord started partitioning their data, they ran into unexpected issues.
- https://twitter.com/ProgressiveCod2/status/1734532331338342487
  - The main reason was their partitioning strategy.
  - In Discord's data model, every message belonged to a channel and was stored in a table known as Messages.
  - The Messages table was partitioned based on Channel ID and Bucket. The Bucket is basically a static time window.
  - This scheme had a serious implication: A Discord server with hundreds of thousands of members could potentially generate enough messages in a short period. This can overwhelm a partition in no time.
  - With reads more expensive than writes in Cassandra, this arrangement led to hot partitions.
  - How did Discord deal with this issue?
  - [SDC#8 - Database Replication Under the Hood](https://newsletter.systemdesigncodex.com/p/database-replication-under-the-hood)

- ## 🆚️ 如果今天还有人津津乐道什么分表分布式海量规模高并发，只能说明一件事：这哥们过去十年已经停止学习了，还活在上一个时代里。
- https://twitter.com/GobeUncleWang/status/1725311478528721026

- ### 👇🏻 支持分布式

- 对于海量数据而言，依然会装不进一台机器里，所以还是会需要分布式。 
  - 至于那些一上来就几个 PB 的存储也只是能存而已，要算的时候瓶颈立刻就出来了。
  - 最好的的系统还是既能在高性能节点上高效率运行，又能支持分布式
- 另外，如果所用的硬件没有 mainframe 那种硬件容错的能力，单个节点出现任何故障都会导致服务中断
  - 容灾这种事集中式数据库也有主从复制，其实也是广义上的分布式，就像我们也不会管一个CPU内的两百个核叫分布式一样，通常也不会管这种叫分布式就是了。

- AP还是需要存算分离做分布式。TP做分布式性能都损失了，这个tradeoff随着单机硬件变强越来越不划算
- OLAP的数据仓库场景，明显现在再强的单机肯定是不行的，顶多顶多的就是服务一个用户同时查询使用，多个机器同时协作来服务一个请求才能给一个即席化的统计分析场景提供很好的体验，甚至更好的服务一个多人同时使用的即席化使用场景

- 你这明显是误导。只要需求超越单机上限，你就得分布式。你见过HPC是单机吗？连CPU都得是分布式网状结构，就因为处理需求远超“单处理结构”的能力上限，必须集群化处理。

- 这文章没考虑到实际工程场景。单机必然是不安全的，外部因素比如网络抖动，断网断电，bug导致进程异常终结，内部因素比如特性更新/版本更新导致的重启。单机必然存在一定时间的停机，这在实际的工程场景中是无法忍受的。
  - 你说的叫冗余和文章说的分布式是两回事。文章的分布式是指同一个任务通过特定的协议分散到不同的主机上协同处理，单机需要怎么做冗余，分布式也是一样要做的。

- 存储能存 不代表要计算 查找的时候 能快速算得出来 查得出来。 

- ### 👇🏻 支持单机

- 你单机怎么保证availability
  - 主从

- 分布式是当年硬件算力不够的时代没有办法的办法。当时不是每个公司都能买得起一百多个CPU的服务器，现在硬件价格下来了，性能上去了，个人电脑都能64核，硬件这种强悍的性能，基本上企业90%的需求，买两三台服务器就能满足，再也不需要被迫搞一堆花里胡哨的配置来实现分布式。

- 大规模情况下的数据分片不均（倾斜）造成负载不均衡，这依然是一个固有的未曾解决好的问题，分库分表对应的是关系表这样的数据，但对于递归的图数据怎么做到分布式情况下的处理（rpc开销如何优化调度），也没有成熟方案吧
  - 单机内部就能调整

- 要是有底层库能用H100这样的显卡做加速，硬件的上限会更恐怖。

- 容灾不是分布式

- 
- 
- 

- ## 🕛🔥 [A history of the distributed transactional database | Hacker News_201812](https://news.ycombinator.com/item?id=18600404)
- 
- 
- 

- ## 🔥 [We put a distributed database in the browser and made a game of it | Hacker News_202307](https://news.ycombinator.com/item?id=36680535)
- Is this something similar to couch/pouchdb?
  - TigerBeetle is more domain-specific, i.e. focused on financial transactions and high-performance, high-availability. There are just two entity types in the database: accounts and transfers between accounts. 
- > In comparison to {C, P}ouchDB, I think the question is around offline-first availability.
  - Got it, thanks! Yeah that is indeed not how TigerBeetle works. If you ever cannot connect to the cluster, you keep retry messages (idempotently) until you connect and the message succeeds.

# discuss-cap
- ## 

- ## 

- ## 

- ## What is the difference between Linearizability and Serializability? 
- https://twitter.com/vaibhaw_vipul/status/1764525904045220312
- Linearizability in context of consistency refers to the "C" in CAP theorem. 
  - It is synonym of "atomic consistency". 
  - It is a guarantee about single operation on single objects. Writes appear instantaneous.  
- Serializability is the "I" or isolation in ACID. 
  - It is a guarantee about transaction or groups of one or more operations over one or more objects. 
  - It guarantees that the execution of a set of transactions (usually containing read and write operations) over multiple items is equivalent to some serial execution (total ordering) of the transactions. 
  - Serializability is a mechanism for guaranteeing database correctness.
  - Combining serializability and linearizability yields strict serializability

- In practice, your database is unlikely to provide serializability, and your multi-core processor is unlikely to provide linearizability—at least by default. 
  - As the above theory hints, achieving these properties requires a lot of expensive coordination.
# discuss-clock
- ## 

- ## 

- ## 

- ## How can you order events in a distributed system?
- https://twitter.com/Franc0Fernand0/status/1767167089385541760
- Distributed systems don't have a global clock to order events. They use logical clocks to measure time in terms of logical operations.
- There are two popular types of logical clocks.
- A Lamport clock uses a single counter initialized to 0 for each process.
  - A process increases its counter before each operation:
  - when sending a message, a process attaches a copy of its counter
  - when receiving a message, a process merges its and the received counter. The merge takes the maximum of the two counters.
- Vector clocks address this problem.
  - Such a clock uses a list of N counters for each process, where N is the number of processes.
  - A process increases its counter in its list before each operation:
  - when sending a message, a process attaches a copy of its list.
  - when receiving a message, a process merges its and the received list. The merge takes the maximum of each counter in the two lists.
- This mechanism gives a partial ordering between lists by comparing corresponding counters.
- One problem with vector clocks is that the required memory grows linearly with the process.
  - There are, however, variants of vector clocks that can fix this.

# discuss-decentralized/p2p
- ## 

- ## 

- ## 🔥[OrbitDB: Peer-to-Peer Databases for the Decentralized Web | Hacker News_202103](https://news.ycombinator.com/item?id=26310094)
- 
- 
- 

- ## 🔥 [OrbitDB: Peer-to-peer databases for the decentralized web | Hacker News_202004](https://news.ycombinator.com/item?id=22918467)
- 
- 
- 

- ## 🔥 [OrbitDB – serverless, peer-to-peer database on top of IPFS | Hacker News_201812](https://news.ycombinator.com/item?id=18748542)
- I'm looking for a distributed scalable P2P triple store (or graph database) to store and retrieve RDF using SPARQL.
  - SOLID (Tim Berners-Lee, RDF)
  - GUN (ours, graph)

# discuss-protocol-raft/paxos ⚖️
- ## 

- ## 

- ## 

- ## Log stacking can happen when using Raft/Paxos to replicate DBs w/ their own WALs. 
- https://twitter.com/strlen/status/1762933075783405649
  - Apache Kudu consolidates: the tablet WAL is also the Raft log. 
  - There have been experimental in other systems by disabling local WAL and using consensus log for recovery. 
  - Is there a generic solution?

- https://twitter.com/jorandirkgreef/status/1763073571616694751
  - This is why TigerBeetle’s global consensus protocol and local storage engine were co-designed:
  - not only to share the WAL, but also to
  - run directly on a raw block device
  - without requiring a filesystem

- I don't think it's possible in a multi-node system.  Whether you call it the log or the network.

- Back in the day we built Baardskeerder, an append-only B-tree'ish thing, to act as both the log and the database for Arakoon, a multi-Paxos key-value-store. Earlier version used traditional separation in log files and something BDB-like (TokyoCabinet).

- In Redpanda the only log is a Raft log.

- I believe AWS has such a generic building block _internally_ seen it called various names – AlfBus, transaction journal, and perhaps what they called Grover 
  - I am familiar with Grover, I worked on Aurora in 2016-2018. It is its storage system publicly discussed in the Aurora papers. It does provide centralized storage for both the data and log pages. Not sure about any changes since then.

- ## 偶然发现剑桥大学 2020 年对比 Paxos 和 Raft 的一篇论文，题目很有意思：“我们就共识协议达成共识了吗？”
- https://twitter.com/qtmuniao/status/1760552518051070087
  - 主要思路是用 Raft 的术语和思路去表述 MultiPaxos，以明晰两者的区别和联系。

- ## 🆚️ [Paxos vs. Raft: Have we reached consensus on distributed consensus? | Hacker News _202107](https://news.ycombinator.com/item?id=27831576)
- Since the article mentions Google as the outlier preferring Paxos, I may be able to shed some light from a few years ago.
  - The Paxos, paxosdb, and related libraries (despite the name, all are multi-paxos) are solid and integrated directly into a number of products (Borg, Chubby, CFS, Spanner, etc.). There are years of engineering effort and unit tests behind the core Paxos library and so it makes sense to keep using and improving it instead of going off to Raft. As far as I am aware the Google Paxos implementation predates Raft by quite a while.
- This makes sense to me. Very few of us have the resources to maintain, for example, the kind of globally synced (way beyond typical NTP) clock infrastructure that Google has (TrueTime)

- I hope that the "Paxos vs Raft" debate can die down, now that engineers are learning TLA+ and distributed systems more thoroughly. These days we can design new protocols and prove their correctness, instead of always relying on academics. For example, at MongoDB we considered adopting the reconfiguration protocol from Raft, but instead we designed our own and checked it with TLA+. 

- 👥 
- https://twitter.com/tweeshan/status/1756534657892679871
- Raft has the lowest availability and performance. IIUC Paxos has the best availability (because any replica can lead) but costs 2 round trips.
# discuss-sharding
- ## 

- ## 

- ## Top 4 data sharding algorithms explained.
- https://twitter.com/alexxubyte/status/1785330458408124790
  - We are dealing with massive amounts of data. Often we need to split data into smaller, more manageable pieces, or “shards”. 
- Here are some of the top data sharding algorithms commonly used
- 🔹 Range-Based Sharding
  - This involves partitioning data based on a range of values. 
  - For example, customer data can be sharded based on alphabetical order of last names, or transaction data can be sharded based on date ranges. 
- 🔹 Hash-Based Sharding
  - In this method, a hash function is applied to a shard key chosen from the data (like a customer ID or transaction ID). 
  - The result determines which shard the data will go to. 
  - This tends to distribute data more evenly across shards compared to range-based sharding. However, we need to choose a proper hash function to avoid hash collision.
- 🔹 Consistent Hashing
  - This is an extension of hash-based sharding that reduces the impact of adding or removing shards. 
  - It distributes data more evenly and minimizes the amount of data that needs to be relocated when shards are added or removed.
- 🔹 Virtual Bucket Sharding
  - Data is mapped into virtual buckets, and these buckets are then mapped to physical shards. 
  - This two-level mapping allows for more flexible shard management and rebalancing without significant data movement.

- ## There are two main ways to partition a table.
- https://twitter.com/Franc0Fernand0/status/1780571942438818192
  - Vertical partitioning moves columns to different tables. It's simple to understand and keeps data about certain features together. However, a new partition will be required in case of further data growth.
  - Horizontal partitioning divides a table into new tables with the same columns but fewer rows. Each new table represents a different data store.

- There are 3 popular ways to partition a table horizontally:
  1. Hash-based maps rows to new tables by applying a hash function to one or more columns.
  2. Range-based splits the data using ranges of values in one or more columns.
  3. Directory-based uses a dedicated lookup service to store the partition schema.

- It's flexible because it abstracts the schema and the number of machines from the application.
  - But it's more complex, and connecting to the service slows the performance.

- ## 🆚️ Sharding is overloaded, do you mean table partitioning, page partitioning, node partitioning or something else? Ignoring hash/range partition trade offs, separate discussion.
- https://twitter.com/sunbains/status/1769017995664437733
- Table partitioning is on the same node and consistency is preserved but problems with global indexes and foreign keys. 
  - The former complicates your queries. Usually suitable as a poor man’s time series type solution. 
  - You can drop old data by simple dropping the old partition, it’s not a general solution for scalability.
- With node partition like CitusDB or Vitesse, you have the above problems plus bigger problems with cross node consistency. 
  - It becomes the application problem, not good either. 
  - Manually shard the data and the application has to be aware of the location of the data. 
  - Resharding when you outgrow your shards is the stuff of nightmares. 
  - DDL. takes that pain to a different level, you have to have worked on very large data sets to understand it. 
  - Foreign keys forget it. Given the consistency issues, good luck.
- Automatic sharding at the page level, this is the architecture pioneered by Google Spanner. 
  - This gives strong consistency guarantees, no manual resharding, DDL is easy and can be scaled by using all the nodes in the network (look at TiDB Distributed eXecution Framwotk for an example). 
  - No stopping the world on DDL, see F1 online schema change paper. 
  - Foreign keys and constraints and all the benefits of RDBMS with proper distributed SQL queries. 
  - This isn’t the future. You can start small, try it with http://tiup.io , HA out of the box, excellent observability tools built in too.
  - TiDB does this and is MySQL compatible.

- Yugabyte and CockroachDB are Postgres compatible.

- ## Sharding is the most proven database scaling pattern. The rest is just noise
- https://twitter.com/isamlambert/status/1768341699334668676
- It’s basically the only pattern, but it’s not limited to sql of course
  - 
- Consistent hashing is another pattern... Sharding is just preferred because you can shard per account. A single account will (typically) never access another account's data.
  - Okay, okay... You have to split up the data to scale horizontally, of course. I guess ANOTHER scaling pattern would be MemSQL in order to process more/faster on a single instance.
# discuss
- ## 

- ## Byzantine failures only come up in crypto conversations. Never in distributed databases or other distributed system projects. 
- https://twitter.com/sunbains/status/1787376127708696928
  - Non-crypto  seem to care only about fail-stop.
- I don't think it's true that non-crypto distributed systems only care about fail-stop. Omission faults, authentication-detectable corruption, latency-related reorderings, and faults caused by failure recovery are typically considered.
  - I omitted the  faults you mention only for brevity. I agree they are considered. The Red Panda article you posted also says that the fsync issue  is a small part of Byzantine failures and in my understanding is related to the point above.

- ## 🤔❓ Modern distributed databases require scaling in two axis. Lots of small objects and small number of large objects.
- https://twitter.com/sunbains/status/1780293307861737643
  - In concrete terms, 100’s of millions of small tables and 10’s of thousands of very large tables.

- Often the way to solve for both is to turn one into the other somehow, then solve for that
  - The example I was thinking of was chopping one big table into multiple ranges to effectively get "many small tables" (I know not 1:1) that are easy to distribute over many machines

- ## Eventual Consistency (EC) means it’s impossible to diverge (a safety invariant: if all messages are sent, states are equal). 
- https://twitter.com/_Felipe/status/1777667242403999970
  - SEC(Strong EC) means the messages will, in fact, be eventually sent (a liveness property).
- Leslie Lamport’s TLA+ is an extension of LTL (Linear Temporal Logic).

- ## 🧩 Database guarantees durability using WAL, and it is possible due to LSN 
- https://twitter.com/sunbains/status/1771190591034102129
  - Databases dump every single operation in WAL before it is applied to the actual data, and the Log Sequence Number (LSN) is a unique identifier associated with each record added to the WAL.
  - LSNs are monotonically increasing enabling replicas to keep track of the replication. The master node keeps a record of the highest LSN it has written. The difference between the master_lsn and the LSN on the replica helps the database determine the Replication Lag.
- Thus LSNs are what enable us to achieve and implement three critical features of any durable database, and they are
  1. recovery from failure and rebuilding in-memory state of the database
  2. asynchronous replication between master and replica
  3. point-in-time snapshots by replaying changes from WAL until desired LSN

- You don’t necessarily need a WAL and LSN for replication, they are orthogonal(正交的). 
  - The idea of a WAL is to first write to the log (the A in WAL) then data files. 
  - Also, it doesn’t have to be a transaction aware log either. It can simply be a physical log and you can build the transaction log on top of it along with the replication, both synchronous and asynchronous.

- ## Scaling Database: When and How to Shard
- https://twitter.com/sahnlam/status/1764539121782112444
  - Database sharding refers to splitting data across multiple database servers and is commonly used for scaling. 
  - However, sharding introduces major operational and infrastructure complexity that should be avoided unless absolutely necessary.

- 💡 Alternative Scaling Approaches
  - Vertical Scaling:  Use more powerful single database servers with more CPUs, memory, storage and I/O bandwidth. Much simpler to manage than sharding.
  - SQL Optimization: Tune SQL queries and database schema to maximize performance on a single server using proper indexes, efficient SQL, etc.
  - Caching: Use in-memory caches like Redis to reduce database load by serving common queries from the cache instead of hitting the database every time.
  - Read Replicas + Load Balancer: Add horizontal read scaleability without full complexity of sharding. Directs reads across replicas.
- These optimization approaches should be exhausted before considering sharding.

- 💡 Sharding Methods
  - Vertical Sharding: Split database into columnar tables or sections vs rows. For example, having one table for names and another table for emails.
  - Horizontal Sharding: Split database into row partitions distributed evenly across multiple servers. Methods include range based, directory based, and hash based sharding.
- When sharding, use the simplest approach that meets requirements to minimize complexity. Seek to avoid sharding until necessary despite the scaling benefits. The infrastructure and operational overheads often outweigh gains.

- ## Distributed Services can't exist without Eventual Consistency.
- https://twitter.com/RaulJuncoV/status/1763220110251032900
- These are the 3 patterns to deal with it.
- A practical example: Imagine you have two services: Orders and Invoices. When the customer places an order, you must generate the associated invoice.
- 1. Background Synchronization Pattern
  - You save the order and then update/create the invoice in the background.
  - The job in schedule checks for new or changed orders and creates or updates invoices.
  - This approach decouples the services and reduces the latency on the user-facing service (Orders service).
  - You get Eventual Consistency but slowly.

- 2. Orchestrated Request-Based Pattern
  - You save the order and send it to the Invoices service. Unlike the previous pattern, this one attempts to process the entire distributed transaction. 
  - It requires some kind of Orchestrator Service, which can be a separate service or an existing one.
  - It requires compensating transactions.

- 3. Event-Based Pattern
  - Services emit events, and others listen to them to update their data. 
  - You save the order and emit an event of "order-created." The Invoices service listens for these events and creates a new invoice based on the order. 
  - The services do not need to know about each other and can scale independently.

- TL; DR
  - Background Synchronization offers simplicity and decouples services but introduces delays in data consistency.
  - Orchestrated Request-Response offers a controlled flow with reliability but increases response times.
  - Event-based brings loose coupling and scalability and allows services to react to changes at the cost of complexity.

- Eventual Consistency is the price for better performance, scalability, and availability.

- I prefer Event-Based but I have used background synchronization a lot in the past. You can set up synchronization between your database instances releasing the Application layer from that responsibility.
- If the latency to move data over is not a problem, Background Synchronization is the right solution.

- ## This summarizes quite well the diff between Data Sharding vs. Distributed SQL
- https://twitter.com/FranckPachot/status/1761673558206407031
  - Sharding with table families is not one logical DB: a single hierarchy of foreign key and no global index
  - Distributed SQL provides all relational SQL features at global level

- ## There's a difference between a database designed to scale up an existing MySQL or Postgres install and a distributed database that has chosen to try and be compatible with MySQL or Postgres.
- https://twitter.com/isamlambert/status/1758872040646615090
- Let me market my names:
  * AlloyDB, Neon, Aurora = DisaggSQL
  * Planetscale = ShardSQL
  * CockroachDB, TiDB, YugabyteDB = DistSQL
  * Oracle, MySQL, Postgres = TradSQL
  * MongoDB is DistMQL

- AlloyDB is a good example of a distributed database that is trying to be Postgres compatible.

- Scale up an existing MySQL or Postgres or scale out an existing setup? When folks try to scale out an existing installed: they tend to start building something like a distributed database and then get into frequent buy vs build debates

- ## The purpose of distributed systems has changed drastically over the last 2 decades.
- https://twitter.com/YingjunWu/status/1745213563755749806
  - When MapReduce first emerged, the need for dist. systems was to get better perf - single node wasn't powerful enough.  
  - But now, in the cloud era, we we can easily rent machines with big DRAM from AWS. Yet, people still need distributed systems, but primarily for high availability.
  - I bet more and more data systems will be optimized for scaling up, not scaling out. Examples include RisingWave, DuckDB, Neon, and many others.

- But it's trickier to manage in terms of autoscaling? Assume at peak time we need say 100 cores, but only for 1-2 hours, and for the rest of the day we need say 20 cores. We would need to use different machine types through the day which is not well automated scenario now.
  - That's a very good point. Yes, right now we still need a multi-node cluster in this case, as migrating terabytes of states from one machine to another is always a pain.
  - The idea of 'S3 as a primary storage, ' as adopted in many modern systems, can mitigate the problem. To scale up (let's say we just have one single machine), we only need to create a new machine and allow the new machine to load the entire states from S3. But unfortunately, at the moment (atm), S3 is not fast enough and loading data is still quite slow.
  - I'm keeping a close eye on S3 Express. If AWS really delivers low-latency S3 at low cost, then it may address the problem nicely.
- Great insights! In my personal opinion, scaling out could be still relevant and important for certain customers who anticipate explosive growth in data usages and want to position for the future (a few years out) in choosing DB vendors..

- ## DuckDB is great, but switching my code from single-node processing to distributed processing should be a no-brainer and invisible to me, like switching a flag. 
- https://twitter.com/ananthdurai/status/1733040083056701865
  - What to do with the current duckdb ecosystem to enable it? Is PySpark api support the answer for it?
- Write everything in SQL and then use SQLGlot to auto-transpile to Spark if you ever need it.  If you can avoid it, I wouldn't recommend using the Pyspark API (in duckdb or spark) because you get locked into it https://

- Check clickhouse-local.
  - Apart from clickhouse, if you use compute engine agnostic storage format (e.g. delta) and compute engine agnostic transformations engine (e.g. dbt), migration should be as easy as swapping?

- ## 🪧 快速了解下负载均衡6大算法
- https://x.com/qloog/status/1797255930905776240

- ## 🪧 6 Load Balancing ALGORITHMS you Must Know
- https://twitter.com/AmigosCode/status/1725507946950344949
1. Round Robin
 - Allocates incoming requests to each server in a circular sequence. It ensures an equal distribution of the workload among servers.
2. Sticky Round Robin
 - Similar to Round Robin, but with the added feature of maintaining session persistence. Once a client is assigned to a server, subsequent requests from that client continue to be directed to the same server.
3. Least Time
 - Assigns requests to the server with the least expected processing time. This algorithm considers factors like server response time and current load.
4. Least Connections
 - Directs traffic to the server with the fewest active connections. This helps distribute the load more evenly across servers, preventing overload on any single server.
5. IP/URL Hash
 - Uses a hash function on the client's IP address or URL to determine which server should handle the request. This ensures that requests from the same client are consistently directed to the same server.
6. Weighted Round Robin
 - Similar to Round Robin, but assigns different weights to servers based on their capacity or processing power. Servers with higher weights receive more requests, allowing for proportional load distribution.

- Each of these load balancing algorithms plays a crucial role in optimizing the performance and reliability of server clusters by efficiently distributing incoming requests.

- ## 有啥工具可以比较好的在单机模拟分布式的环境吗？主要是想模拟一下带宽限制和网络延迟
- https://twitter.com/leiysky/status/1725430083106836637
- sudo tc qdisc add dev wlan0 root netem delay 1000ms
- chaos-mesh + minikube （或者直接 tc。可以限制 bandwidth。都是用的 tc qdisc，限流是 tbf 延迟是 netem。
- 我用 Clojure 写的一个工具，jepsen

- ## 💡 Database Sharding Explained
- https://twitter.com/arcnotes/status/1719692415995425014
  - [Database Sharding Explained](https://architecturenotes.co/database-sharding-explained/)

- ## 🔥 [From coding bootcamp graduate to building distributed databases | Hacker News_202102](https://news.ycombinator.com/item?id=26209594)
- 
- 
- 

- ## 🔥 [The Inner Workings of Distributed Databases | Hacker News_202304](https://news.ycombinator.com/item?id=35602983)
- 
- 
- 

- ## 🔥 [Technical Challenges Developing a Distributed SQL Database | Hacker News_201904](https://news.ycombinator.com/item?id=19759101)
- 
- 
- 

- ## 🔥 [How does database sharding work? | Hacker News_202304](https://news.ycombinator.com/item?id=35476518)
- 
- 
- 

- ## 🛢️🔥 [Azure Cosmos DB, a globally distributed database | Hacker News_201705](https://news.ycombinator.com/item?id=14308814)
- 
- 
- 

- ## 🔥 [Distributed algorithms in NoSQL databases | Hacker News_201709](https://news.ycombinator.com/item?id=15367003)
- 
- 
- 

- ## 🔥 [Principles of Sharding for Relational Databases | Hacker News_201708](https://news.ycombinator.com/item?id=14971650)
- 
- 
- 
