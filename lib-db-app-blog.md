---
title: lib-db-app-blog
tags: [blog, database]
created: 2022-12-20T05:38:59.782Z
modified: 2023-09-16T17:49:13.534Z
---

# lib-db-app-blog

# guide

# blogs
- [DM 源码阅读系列文章 TiDB Data Migration](https://cn.pingcap.com/blog/?tag=DM%20%E6%BA%90%E7%A0%81%E9%98%85%E8%AF%BB)

## kappa-lambda

- [三张图讲清楚大数据基础设施Hadoop、Lambda、kappa架构 - 知乎](https://zhuanlan.zhihu.com/p/337520151)
  - 第一代基础设施：以Hadoop为代表的离线数据处理。
    - 底层以HDFS分布式文件系统做数据存储，所有的数据都通过MapReduce计算模型进行处理
  - 第二代基础设施：以Lambda为代表的流批数据处理。
    - 通过把数据分解为ServingLayer、SpeedLayer、BatchLayer三层来解决在不同数据集的数据需求。
    - 优点是将流处理和批处理分开，很好的结合了实时计算和流计算的优点，架构稳定，实时计算成本可控，提高了整个系统的容错性、降低了复杂性。
    - 缺点是离线数据和实时数据很难保障数据的一致性，开发人员需要维护两套系统。
  - 第三代基础设施：以Kappa为代表的集成流批数据处理。
    - Lambda架构的流批分离解决了数据一致性问题，也提高了效率，但对应的也增加了系统的复杂性。
    - Kappa架构利用流计算的分布式特征，增加流计算的并发性，加大流数据的时间窗口，统一批处理和流处理数据。
    - Kappa架构在Lambda架构的基础上删除了Batch层，所有的数据都是流处理实时计算，计算好了之后可以直接给到业务层使用，也可以放在数据湖中，需要进行离线分析时使用。
    - Kappa架构的优点是开发人员只需要维护实时处理模块，不需要离线实时数据合并，
    - 缺点是在实时处理时可能会存在信息丢失情况。

- [Flink architecture and execution engine - Practical Real-time Data Processing and Analytics [Book]](https://www.oreilly.com/library/view/practical-real-time-data/9781787281202/e1aa468d-c22d-4dc3-afce-498a084c1ee3.xhtml)
  - The core of Flink is a streaming dataflow engine. 
  - Flink is based on Kappa architecture. 
  - Kappa architecture was introduced in 2014 by Jay Kreps
  - 

- [Apache Flink 101: Understanding the Architecture](https://techlake.dev/apache-flink-101-understanding-the-architecture)
  - In Kappa architecture, batch processing is a special case of stream processing hence it is able to perform both batch and real-time processing, especially for analytics, with a single technology stack.
  - Apache Flink is built on Kappa architecture hence it excels at processing unbounded and bounded data sets.

- [实时数仓之 Kappa 架构与 Lambda 架构 - 知乎](https://zhuanlan.zhihu.com/p/584255261)

- [Kappa Architecture 1:1 - How to Build a Modern Streaming Data Architecture?](https://nexocode.com/blog/posts/kappa-architecture/)

## [MySQL索引数据结构红黑树，Hash，B+树详解 - 博客园](https://www.cnblogs.com/yufeng218/p/12465694.html)

- 索引是帮助MySQL高效获取数据的排好序的数据结构；
- 使用 select * from t where t.clo2 = 89 查询；
- 1、若表中没有创建索引，则会全表扫描，一条一条的遍历查询，需要遍历 6 次，查询一行数据至少和磁盘做一次I/O操作（I/O是很耗性能的），至少要做 6 次 I/O 操作；
- 2、表中建立了索引：
  - （1）若索引底层是二叉树（左边的子元素小于父元素，右边的子元素大于父元素）存储的，则如下图所示：
    - 当然，在极端情况下，若按照大小顺序插入二叉树，则会形成单边增长的二叉树，这样使用索引的时候和全表扫描是一样的了；
  - （2）若索引底层是红黑树存储的，则如下图所示：
    - 红黑树：当单边的节点大于3时候，就会自动调整，这样可以解决二叉树的弊端；红黑树也叫平衡二叉树；
    - 当然，红黑树也有弊端的，当数据量特别大的时候，红黑树的高度特别大；假如有500W条数据，则红黑树高度为 23，若我们要查找的刚好是红黑树的叶子节点，则需要查找 23 次才可以，即要发生 23 次的磁盘 I/O 操作，性能就太差了；
- 3）若索引底层是 B-Tree 存储的
  - （叶子节点具有相同的深度，叶节点的指针为空；所有索引元素不重复；一个节点可以存储多个元素，节点中的数据索引从左到右递增排列）
  - 当然 B-Tree 也是有弊端的；以下是 B-Tree 的存储，数字为key，data为对应的数据；
  - 若一个节点我们申请的空间为16KB，若data中的数据过大，则一个节点能放的数据量越小，这样就会造成树的高度比较大了（比红黑树高度小点）；
- （4）MySQL的索引底层使用的 B+Tree 存储的（数据存储在叶子节点）
- B+Tree：
  - 非叶子节点不存储data，只存储索引（冗余），可以放更多索引；
  - 叶子节点包含所有索引字段，即所有的data元素存储在叶子节点上；
  - 叶子节点使用指针连接，提高区间访问的性能；
  - 从左到右一次递增; 
- B+Tree 相对于 B-Tree的优化点：
  - 优化点1： B-Tree的所有节点都存储了 data 元素， B+Tree的非叶子节点不存储 data元素，则 B+Tree 的一个非叶子节点可以存储更多的索引；
  - 优化点2： B+Tree在叶子节点之间增加了指针连接；对 select * from t where col2 > 20 的范围查找有很好的支持；
- MySQL 对 B+Tree 做了优化，叶子节点使用的是双向指针；  
  - I. 先将根节点的数据(15, 56, 77) 做一次磁盘 I/O 操作取出加载到内存中，然后再在内存中做比对，找到对应的指针，查找到其对应的节点；
  - II. 将指针指向节点的数据(15, 20, 49) 做一次磁盘 I/O 操作取出加载到内存中，然后再在内存中做比对，找到对应的指针，接着去叶子节点获取数据；

- MySQL页文件默认为16KB，树的高度为3，能够存储多少数据？
  - 我们先看非叶子节点，假设主键ID为 bigint 类型，那么长度为8B，指针大小在Innodb源码中6B，一共14B，那么一页（即一个节点）可以存储  16KB/14B=1170 个索引元素和 1170个指针；根节点有1170个索引和1170个指针，树高度为2的节点就有1170个，那么叶子节点的数量为 1170x1170；每个叶子节点可以存储16KB，若每条数据比较大为1KB，那么每个叶子节点可以存储16条数据；那么，高度为3的 B+Tree 的叶子节点可以存储的数据量为 1170x1170x16=2000W；

- 在实际的MySQL中表的索引存储可以选择 Hash 或 BTree

- （5）若索引使用的 Hash 存储的，存储的时候先做一次hash运算，根据 hash 的值就可以快速的定位数据的磁盘指针，这样就不管表里面有多少数据，我们的查询效率都非常的快；
- 在实际中为什么使用 B-Tree 或 B+Tree 来存储索引的方式更多，而不太使用 hash 呢？
  - 原因1：若使用 select * from t where clo2 > 6，这种查找范围的SQL，那Hash就不能搞定了，就不会走索引了；而且对排序hash也没有办法；
  - 原因2：hash会产生 hash 碰撞，MySQL的底层对hash做了处理，很少会发生hash碰撞的；

- 同一个数据库中，不同的表可以设置不同的存储引擎；
  - MySQL的数据存储在 data 目录下， data 目录下的 文件夹是以 数据库为单位的，数据库文件夹下面存放的表数据；  data / {数据库名} /表文件

### MyISAM存储引擎索引实现

- MyISAM存储引擎的索引文件和数据文件是分离的（非聚集）；
- MyISAM 存储引擎的一个表有3个文件：  
  - `*.frm` 文件存储的表的结构； 
  - `*.MYD` 文件存储表的数据； 
  - `*.MYI` 文件存储表中的索引数据；
- MYISAM 存储引擎的索引的叶子节点的data中存储的是索引所在行的磁盘指针； ---- 非聚集索引
- MYISAM 存储引擎的主键索引 和 非主键索引的存储是差不多的，InnoDB 存储引擎的 主键索引 和 非主键索引存储是不一样的；

### InnoDB 存储引擎-索引实现

- InnoDB存储引擎索引文件和数据文件是合一的(聚集)；
- InnoDB 存储引擎的1个表有2个文件：  
  - `*.frm` 文件存储表的结构； 
  - `*.ibd` 文件存储的是索引和数据；
- InnoDB表的数据文件本身就是按 B+Tree 组织的一个索引结构文件；
  - 聚集索引叶子节点包含了完整的数据记录；
- InnoDB 存储引擎的索引的叶子节点的data中存储的是索引对应的所有数据；----聚集

- 问题1：为什么InnoDB表必须有主键，并且推荐使用整型的自增主键？
  a. 因为 MySQL对于 InnoDB 表设计的就是按照 B+Tree 组织存储数据的，若没有主键就没有办法去存储数据了；但是在平常我们建表的时候没有指定主键也是可以建成功的，这是因为 MySQL 会生成一个 rowid 作为数据的唯一标识；
  b. 若使用的 UUID 作为主键，在查找的时候需要去比较大小，字符串UUID比较的效率肯定低于数据的比较；在进行比较的时候会把数据拿到内存空间中做比较，UUID为字符串占用的内存空间就会较多；
  c. 若是递增的，则插入的数据直接向后排，这个节点满了，直接新增一个节点就好了；若不是递增的，有个节点存储满了（5, 9），但是新插入了一个数据

- InnoDB 的非主键索引
  - 在使用非主键索引查找的时候，先从非主键索引的树中查询到对应的主键值，然后使用主键值去到主键索引的树中去查找；
  - 对于非主键单值索引，若索引字段的值为 null，则它的数据不会放到非叶子节点上，是放在叶子节点的链表的最前面的；（强烈不建议字段设置为null）

- 为什么非主键索引结构叶子节点存储的是主键值？（一致性和节省存储空间）
  - 因为在插入数据之前先要维护一下索引，然后再将数据插入进去；
  - 若 主键索引 和 非主键索引 的叶子节点都存储具体的数据，则一个 insert 语句插入成功的判断就是 向主键索引中插入成功 且 向非主键索引中也插入成功，这样就造成了事务的问题，事务是很耗性能的；
  - 当然，主键索引和非主键索引的叶子节点都存储具体数据，会造成数据的同样的数据存储了几份，就造成了空间的浪费；

- 联合索引在存数据或比较的时候，先比较联合索引最前面的字段，若最前面的字段值一样，则再比较第二个字段的值；
  - 联合索引的索引字段中有一个值为null，则将其放在叶子节点的最前面；可以认为null值是最小的。

## [数据库计算向量化 | plantegg](https://plantegg.github.io/2021/11/26/%E6%95%B0%E6%8D%AE%E5%BA%93%E8%AE%A1%E7%AE%97%E5%90%91%E9%87%8F%E5%8C%96/)

- 在做向量化之前数据库一直用的是volcano模型来处理SQL
- volcano火山模型
  - 对于如下一条SQL, 数据库会将它解析成一颗树，这棵树每个节点就是一个operator(简单理解就是一个函数，进行一次计算处理)
  - 火山模型实现简单，只需要根据不同的计算提供一堆算子(operator)就可以了，然后根据不同的SQL只需要将operator进行组装（类似搭积木一样），就能得到一个递归调用结构（火山模型），
  - 每行数据按照这个调用逻辑经过每个operator进行嵌套处理就得到最终结果。
- 火山模型不但实现简单，框架结构性也非常好容易扩展。
- 但是火山模型效率不高:
  - 每个operator拆分必须到最小粒度，导致嵌套调用过多过深；
  - 嵌套都是虚函数无法内联；
  - 这个处理逻辑整体对CPU流水线不友好，CPU希望你不停地给我数据我按一个固定的逻辑(流程)来处理，而不是在不同的算子中间跳来跳去。

- 向量化加速的CPU原理
  - 内存访问比CPU计算慢两个数量级
  - cpu按cache_line从内存取数据，取一个数据和取多个数据代价一样
  - 以及数据局部性原理
- 局部性原理: CPU访问存储器时，无论是存取指令还是存取数据，所访问的存储单元都趋于聚集在一个较小的连续区域中。 

- 向量化执行的思想就是不再像火山模型一样调用一个算子一次处理一行数据，而是一次处理一批数据来均摊开销：
  - 这个开销很明显会因为一次处理一个数据没用利用好cache_line以及局部性原理，导致CPU在切换算子的时候要stall在取数据上，表现出来的结果就是IPC很低，cache miss、branch prediction失败都会增加。
- 向量化之后的版本不再是每次只处理一条数据，而是每次能处理一批数据，而且这种向量化的计算模式在计算过程中也具有更好的数据局部性。
- 向量化核心是利用数据局部性原理，一次取一个和取一批的时延基本是同样的。
  - volcano模型每次都是取一个处理一个，跳转到别的算子；而向量化是取一批处理一批后再跳转。整个过程中最耗时是取数据（访问内存比CPU计算慢两个数量级）
- 如果把向量化计算改成批量化处理应该就好理解多了，但是low，向量化多玄乎啊
- 为了支持这种批量处理数据的需求，CPU设计厂家又搞出了SIMD这种大杀器，SIMD (Single Instruction Multiple Data，单指令多数据)
- SIMD指令的作用是向量化执行(Vectorized Execution)，中文通常翻译成向量化，但是这个词并不是很好，更好的翻译是数组化执行，表示一次指令操作数组中的多个数据，而不是一次处理一个数据；向量则代表有数值和方向，显然在这里的意义用数组更能准确的表达。

## [A Graph-Based Firebase](https://stopa.io/post/296)

- In A Database in the Browser(blog), I wrote that the schleps(艰难的旅途) we face as UI engineers are actually database problems in disguise(装扮；伪装)
- my co-founder Joe and I decided to build one and find out. This became Instant. 
  - I’d describe it as a graph-based successor to Firebase.
  - You have relational queries and basic auth. Optimistic updates come out of the box, and everything is reactive. 
- we started with SQL but ended up with a triple store and a query language that transpiles to Datalog.
- Why triple store? What query language? read on.

- Delightful Apps
  - Optimistic Updates
  - Multiplayer
  - Offline-Mode

- Bespoke Solutions
A. DB
B. Permissions
C. Sockets
D. In-Memory Store
E. IndexedDB
F. Screens
G. Mutations

- Inspiration
  - if we look at how Figma, Linear, and Notion work, we find clues. Squint, and their architecture looks like a database!
- If our Local DB and Backend DB spoke the same language, both could understand and apply the same mutations. 
- Databases handle replication. So what if we made the client a special node? The Local DB already knows the queries to satisfy. So it can talk to the backend and get the data it needs.

- A SQL-based tool is closest at hand. I enjoyed looking at absurd-sql. This uses sql.js (SQLLite compiled to webassembly) and persists state into IndexedDB.
- SQL has a schema. Schema is useful, but it make things less easy than Firebase. 
- SQL isn’t simple or easy. It’s a tough combination of lots of features, with little of it being useful for the frontend.

- So we wrote a graph database to find out. 
  - We chose Triple Stores, one of the simplest kinds of graph databases. 
- If you haven’t tried one, here’s a quick intuition:
  - we need to be able to express a node with attributes. These sentences translate to lists
  - Then we want a way to describe references.these translate to lists just as well
- Put these lists in a table, and you have a triple store! Triple is the name of the list we’ve been writing
  - The first item is always an `id`, the second the `attribute`, and the third, the `value`. 
  - Turns out triples are all we need to express a graph. 
- once you’ve expressed a graph, you can traverse it. 
  - Triple stores have interesting query languages. 
  - Here’s Datalog

- ### [A Graph-Based Firebase | Hacker News_202208](https://news.ycombinator.com/item?id=32595895)

- I came to many similar conclusions completely independently, even attempted to build a typesafe in memory datalog in typescript.
  - I also came to the conclusion that just exposing datalog triples as a query language would never feel right and tried to expose a graphql like language that generated the datalog triples.

- I have built my own similar reactive in-memory triple store with typescripts type safety, but then I realized I still need transactions which are a bit of a pain, because transactions are bundling the otherwise separete triplets, so the atomic, independent logic of triplets and related effects breaks a bit. (I am sure it's solvable.)
  - The example code uses a `transact` function. But it really depends on what you mean by “transaction”. 
  - 👉🏻 We don’t use a triple store at Notion, but we do use an abstraction that ensures a collection of operations either all succeed or all fail. 
  - We don’t support “interactive” transaction, where you can read, modify, write as an atomic group. 
  - This just isn’t desirable in a multiplayer or offline system - in cases we need that kind of consistency we use a normal HTTP API which is online-only.

- Datalog also has nothing to do with triples, they are two completely orthogonal concepts.

- tripletstore/datalog actually seems like a decent compromise between SQL and no-SQL that could actually work out! Awesome idea!

## [Caching Partially Materialized Views Consistently](https://blog.the-pans.com/caching-partially-materialized-views-consistently/)

- According to the PostgreSQL wiki
  - A materialized view is a table that actually contains rows, but behaves like a view. 
  - That is, the data in the table changes when the data in the underlying tables changes.

- According to Wikipedia
  - a materialized view is a database object that contains the results of a query.
  - For example, it may be a local copy of data located remotely, or may be a subset of the rows and/or columns of a table or join result, or may be a summary using an aggregate function.

- A materialized view is a cache. 
  - Since any data can be described with the relational model, we can also say every cache is a partially materialized view – I mean every cache. 
  - No matter if it is a cpu cacheline, a DNS entry cached in your browser, or some value in memory your application memoized, it can be reasoned about as a partially materialized view. 
  - Even a cached computation result is a partially materialized view; 
- A cache and a partially materialized view are essentially the same thing. In a database (e.g. PostgreSQL, Oracle, etc.), the materialized view is explicitly defined.
# data-model-lsm/btree
- [What is a LSM Tree? - DEV Community](https://dev.to/creativcoder/what-is-a-lsm-tree-3d75)
  - Sled is another embedded key value store in Rust, that uses a hybrid architecture of B+ Trees and LSM Tree (Bw Trees)

- [Bw-Trees](https://sinsay.github.io/db/chapter_6_6_bw_trees.html)
  - Bw-Tree 是 B-Tree 的一个有趣的变种，做了许多重要的优化：写放大，非堵塞的访问以及缓存友好性。一个修改过的实现版本是 Sled，CMU 数据库组织实现了一个基于内存的 Bw-Tree 版本，称为 OpenBw-Tree
# db-dev-xp
- [BeyondStorage: why we failed](https://xuanwo.io/2023/01-beyond-storage-why-we-failed/)
  - 介绍了 BeyondStorage 开源社区的失败并分享了 #OpenDAL 在此基础上的经验教训
  - BeyondStorage 构建 go-storage 是为了满足迁移服务的需求，而迁移服务的需求来自于 go-storage 能力的自然延伸。不难发现这套逻辑中出现了一个可怕的循环，链条中完全没有真实用户的参与，项目从发展伊始就在朝着错误的方向狂奔。
  - BeyondStorage 失败的最直接原因是失去了最大金主：青云科技。
  - OpenDAL 最幸运的地方在于它孵化自 Databend 的真实场景。Databend 持续不断地提出新需求，这些需求帮助我判断需求的必要性、调整任务优先级并修正错误假设。
# blogs-db-vendors
- [Building and operating a pretty big storage system called S3](https://www.allthingsdistributed.com/2023/07/building-and-operating-a-pretty-big-storage-system.html)

- [Database branching: three-way merge for schema changes](https://planetscale.com/blog/database-branching-three-way-merge-schema-changes)
# more
- [处理海量数据：列式存储综述（存储篇） - 知乎](https://zhuanlan.zhihu.com/p/35622907)

- [Database in the Browser, a Spec](https://stopa.io/post/279)

- [Things DBs Don't Do - But Should](https://www.thenile.dev/blog/things-dbs-dont-do)

- [Database Systems: 8Base, Dolt, MindsDB, Xata – SQL Rob](https://sqlrob.com/2023/04/17/database-systems-8base-dolt-mindsdb-xata/)
  - [15 futuristic databases you’ve never heard of - YouTube](https://www.youtube.com/watch?v=jb2AvF8XzII)
