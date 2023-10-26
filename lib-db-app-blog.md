---
title: lib-db-app-blog
tags: [blog, database]
created: 2022-12-20T05:38:59.782Z
modified: 2023-09-16T17:49:13.534Z
---

# lib-db-app-blog

# guide

- [TiKV 源码解析 | PingCAP](https://cn.pingcap.com/blog/tag/tikv-source-code-analysis/)
- [TiDB 源码阅读 | PingCAP](https://cn.pingcap.com/blog/tag/tidb-source-code-reading/)
# blogs

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

- [Apache Flink 101: Understanding the Architecture](https://techlake.dev/apache-flink-101-understanding-the-architecture)
  - In Kappa architecture, batch processing is a special case of stream processing hence it is able to perform both batch and real-time processing, especially for analytics, with a single technology stack.
  - Apache Flink is built on Kappa architecture hence it excels at processing unbounded and bounded data sets.

- [实时数仓之 Kappa 架构与 Lambda 架构 - 知乎](https://zhuanlan.zhihu.com/p/584255261)

- [Kappa Architecture 1:1 - How to Build a Modern Streaming Data Architecture?](https://nexocode.com/blog/posts/kappa-architecture/)


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


## [What is a Vector Database? | Pinecone](https://www.pinecone.io/learn/vector-database/)

### 👥🔥 [What is a Vector Database? (2021) | Hacker News_202305](https://news.ycombinator.com/item?id=35826929)
# blogs-data-model-lsm/btree
- [What is a LSM Tree? - DEV Community](https://dev.to/creativcoder/what-is-a-lsm-tree-3d75)
  - Sled is another embedded key value store in Rust, that uses a hybrid architecture of B+ Trees and LSM Tree (Bw Trees)

- [Bw-Trees](https://sinsay.github.io/db/chapter_6_6_bw_trees.html)
  - Bw-Tree 是 B-Tree 的一个有趣的变种，做了许多重要的优化：写放大，非堵塞的访问以及缓存友好性。一个修改过的实现版本是 Sled，CMU 数据库组织实现了一个基于内存的 Bw-Tree 版本，称为 OpenBw-Tree
# blogs-materialized-view

## [Incremental View Maintenance - PostgreSQL wiki](https://wiki.postgresql.org/wiki/Incremental_View_Maintenance)

- PostgreSQL has supported materialized views since 9.3. 
  - This feature is used to speed up query evaluation by storing the results of specified queries. 
  - One problem of materialized view is its maintenance. Materialized views have to be brought up to date when the underling base relations are updated.
- Incremental View Maintenance (IVM) is a technique to maintain materialized views which computes and applies only the incremental changes to the materialized views rather than recomputing the contents as the current REFRESH command does. 
  - This feature is not implemented on PostgreSQL yet. 
- IVM computes and applies only the incremental changes to the materialized views. 
  - Suppose that `view V` is defined by `query Q` over a state of base `relations D`.
  - When D changes `D' = D + dD`, we can get the new view state V' by calculating from D' and Q, and this is re-computation performed by `REFRESH MATERIALIZED VIEW` command. 
  - On the other hand, IVM calculates the delta for view (dV) from the base tables delta (dD) and view definition (Q), and applies this to get the new view state `V' = V + dV`.
- In theory, the view definition is described in a relational algebra (or bag algebra) form. For example, a (inner) join view of table R and S is defined as V = R ⨝ S.

- How to extract changes on base tables
  - There are at least two approaches. 
  - One is using AFTER triggers and Transition Tables, which is a feature of AFTER trigger introduced from PostgreSQL 10. This was implemented originally aiming to support IVM, and in fact the proposed patch uses this. This enables collect row sets that include all of the rows inserted, deleted, or modified by the current SQL statement.
  - Another candidate is using logical decoding of WAL.

- How to calculate the delta to be applied to materialized views
  - This is basically based on relational algebra or bag algebra. 
  - In theory, we can handle various view definition. Views can be defined using several operations: selection, projection, join, aggregate, union, difference, intersection, etc. 
  - If we can prepare a module for each operation, there is possibility of extensive implementation of IVM.

- When to maintain materialized views
  - There are two approaches, immediate maintenance and deferred maintenance.
  - In immediate maintenance, views are updated in the same transaction where the base table is updated. The proposed patch implements a kind of immediate maintenance, that is, materialized views are updated immediately in AFTER triggers when a base table is modified. SQL statement modify only one base table and the changes can be extracted by using Transition Tables mentioned above.
  - In deferred maintenance, views are updated after the transaction is committed, for example, when the view is accessed, as a response to user command like REFRESH, or updated periodically, and so on.

- How to identify rows to be modified in materialized views
  - When applying the delta to materialized views, we have to identify which tuple in materialized views is corresponding to a tuple in the delta. 
  - A naive method is matching by using all columns in a tuple, but clearly this is inefficient. If a materialized view has unique index, we can use this. 

## [Caching Partially Materialized Views Consistently](https://blog.the-pans.com/caching-partially-materialized-views-consistently/)

- According to the PostgreSQL wiki
  - A materialized view is a table that actually contains rows, but behaves like a view.
  - That is, the data in the table changes when the data in the underlying tables changes.

- According to Wikipedia
  - a materialized view is a database object that contains the results of a query.
  - For example, it may be a local copy of data located remotely, or may be a subset of the rows and/or columns of a table or join result, or may be a summary using an aggregate function.

- 👉🏻 A materialized view is a cache.
  - Since any data can be described with the relational model, we can also say every cache is a partially materialized view – I mean every cache. 
  - No matter if it is a cpu cacheline, a DNS entry cached in your browser, or some value in memory your application memoized, it can be reasoned about as a partially materialized view. 
  - Even a cached computation result is a partially materialized view; 
- A cache and a partially materialized view are essentially the same thing. In a database (e.g. PostgreSQL, Oracle, etc.), the materialized view is explicitly defined.

# more
- [处理海量数据：列式存储综述（存储篇） - 知乎](https://zhuanlan.zhihu.com/p/35622907)

- [Database in the Browser, a Spec](https://stopa.io/post/279)

- [Things DBs Don't Do - But Should](https://www.thenile.dev/blog/things-dbs-dont-do)

- [Database Systems: 8Base, Dolt, MindsDB, Xata – SQL Rob](https://sqlrob.com/2023/04/17/database-systems-8base-dolt-mindsdb-xata/)
  - [15 futuristic databases you’ve never heard of - YouTube](https://www.youtube.com/watch?v=jb2AvF8XzII)

