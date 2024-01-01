---
title: algs-tree-lsm
tags: [algorithms, LSM-Tree, tree]
created: 2023-04-20T08:05:32.815Z
modified: 2023-04-20T08:05:44.256Z
---

# algs-tree-lsm

> LSM(Log Structured Merge Tree)

# guide
- who is using #LSM-Tree
  - LevelDB
  - RocksDB: TiKV, CockroachDB
  - HBase, Cassandra
  - ClickHouse中的MergeTree也是LSM树的思想
  - Flink Table Store 目前采用了类似于 RocksDB 的通用合并策略
  - 新的InfluxDB的存储引擎看起来和LSM树很像
  - couchbase-magma

- redis
  - [Redis Internal Data Structure : Skiplist, sds/Simple Dynamic Strings, dictionary, adlist/Doubly Linked List, ](https://blog.wjin.org/archive.html)
    - Skip List gets O(log n) time complexity on average. And it is easy to implement compared to AVL tree or Red-Black tree. So Redis uses it to implement ordered set.
    - Redis provides SDS because it supports efficient functions to get the string length and append another string to the end without allocating memory each time.
    - dictionary is implemented by means of hash table and there are two hash tables in dictionary to implement incremental rehashing.

- resources
  - [LSM-Tree 论文的中文翻译](https://github.com/tangwz/LSM-Tree-CN/blob/main/LSM-Tree-CN.md)
# blogs

## 🌲☕️ [Log-Structured Merge Tree overview | Medium](https://medium.com/@tomfran/log-structured-merge-tree-a79241c959e3)

- https://github.com/tomfran/LSM-Tree /202311/java
  - Log-Structured Merge Tree Java implementation

- I studied LSM trees at university and after encountering them twice in Designing Data-Intensive Applications and Database Internals I decided to implement something in Java.
- The idea behind this project is not to provide the most efficient implementation ever, but to experiment with storing data on disk

- There is a lot that could be done to improve the project, skip lists could be optimized further, bloom filters could be made more cache efficient, and proper crash recovery could be implemented.

## [LSM树由来、设计思想以及应用到HBase的索引 - yanghuahui - 博客园](https://www.cnblogs.com/yanghuahui/p/3483754.html)

- 讲LSM树之前，需要提下三种基本的存储引擎，这样才能清楚LSM树的由来：
- #️⃣ 哈希存储引擎
  - 是哈希表的持久化实现，支持增、删、改以及随机读取操作，但**不支持顺序扫描**，对应的存储系统为key-value存储系统。
  - 对于key-value的插入以及查询，哈希表的复杂度都是O(1)，明显比树的操作O(n)快, 如果不需要有序的遍历数据，哈希表就是your Mr. Right
- 🌲 B树存储引擎
  - 是B树的持久化实现，不仅支持单条记录的增、删、读、改操作，还支持顺序扫描（B+树的叶子节点之间的指针），对应的存储系统就是关系数据库（Mysql等）。
- 🌲 LSM树（Log-Structured Merge Tree）存储引擎和B树存储引擎一样，同样支持增、删、读、改、顺序扫描操作。
  - 而且通过批量存储技术规避磁盘随机写入问题。
  - 当然凡事有利有弊，LSM树和B+树相比，LSM树牺牲了部分读性能，用来大幅提高写性能。

- LSM树的设计思想非常朴素：
  - 将对数据的修改增量保持在内存中，达到指定的大小限制后将这些修改操作批量写入磁盘，
  - 不过读取的时候稍微麻烦，需要合并磁盘中历史数据和内存中最近修改操作，
  - 所以写入性能大大提升，读取时可能需要先看是否命中内存，否则需要访问较多的磁盘文件。
  - 极端的说，基于LSM树实现的HBase的写性能比Mysql高了一个数量级，读性能低了一个数量级。
- LSM树原理把一棵大树拆分成N棵小树，它首先写入内存中，随着小树越来越大，内存中的小树会flush到磁盘中，磁盘中的树定期可以做merge操作，合并成一棵大树，以优化读性能。

- LSM树的核心特点是利用顺序写来提高写性能，代价就是会稍微降低读性能（读放大），写入量增大（写放大）和占用空间增大（空间放大）。
  - LSM 树主要被用于 NoSql 数据库中，如 HBase、RocksDB、LevelDB 等，
  - 知名的分布式关系型数据库 TiDB 的 kv 存储引擎 TiKV 底层存储就是用的上面所说的 RocksDB，也就是用的 LSM 树。

## [数据库存储与索引技术（二） 分布式数据库基石——LSM树-OceanBase分布式数据库](https://open.oceanbase.com/blog/1793245952)

- LSM-Tree 全称是 Log Structured Merge Tree，是一种分层、有序、面向磁盘的数据结构，其核心思想是充分利用磁盘的顺序写性能要远高于随机写性能这一特性，将批量的随机写转化为一次性的顺序写。
  - 其最早是在1996年的论文《The Log-Structured Merge-Tree (LSM-Tree)》中提出。
- LSM树由两个或以上的存储结构组成，比如在论文中为了方便说明使用了最简单的两个存储结构。
  - 一个存储结构常驻内存中，称为C0 tree，具体可以是任何方便健值查找的数据结构，比如红黑树、map之类，甚至可以是跳表。
  - 另外一个存储结构常驻在硬盘中，称为C1 tree，具体结构类似B树。

## [数据库存储与索引技术（三）LSM树实现案例-OceanBase分布式数据库](https://open.oceanbase.com/blog/1815380224)

- 多款分布式数据库都使用了LSM树作为底层的存储引擎，其中就包括TiDB和Oceanbase。
- 与TiDB等数据库的存储引擎将RocksDB作为一个黑盒使用不同，虽然OceanBase的存储虽然也是基于LSM树，但却是完全自己实现，并且和自己的存储引擎做了深度的定制和整合。
- 与RocksDB中可能存在5，6层的LSM不同，OceanBase的实现中，将LSM树划分为三层，第一层MemTable，第二层OceanBase成为增量层，也称转储层(即LSM树C0层)，第三层OB称为基线层(即LSM树C1)层。
- 与RocksDB中实现一样，OceanBase的增量层(C0)多个SSTable之间Key会存在区间重叠的关系，读取的时候需要遍历查找每个增量SSTable才能确定Key是否存在，
- 本文将以OceanBase 3.x版本为例，讲解其如何针对这一问题进行优化。
- OceanBase 的基线层数据是全局有序的，所有SSTable之间的Key不会存在区间重叠的问题。

## [TiKV | B-Tree vs LSM-Tree](https://tikv.org/deep-dive/key-value-engine/b-tree-vs-lsm/)

## [RocksDB 简介 | PingCAP 文档中心](https://docs.pingcap.com/zh/tidb/stable/rocksdb-overview)

## [Tokutek White Paper: A Comparison of Log-Structured Merge (LSM) and Fractal Tree Indexing_201408](http://highscalability.com/blog/2014/8/6/tokutek-white-paper-a-comparison-of-log-structured-merge-lsm.html)

- CouchDB uses a modified B+ tree.
- We've learned a lot fascinating details over the years about the use of Log-structured merge-trees in Cassandra, HBase and LevelDB. 
- What may not be so familiar is Tokutek's Fractal Tree Indexing technology that is supposed to be even better than B+ trees and LSMs.
  - The paper starts with an explanation of write amplification, read amplification, and space amplification, the metrics that will be used to compare B trees, FT indexes, and LSMs.
# more-lsm
- [Key-Value Separation in LSM Storage Engines_202312](https://www.skyzh.dev/blog/2023-12-31-lsm-kv-separation-overview/)

- [LSM树详解 - 知乎](https://zhuanlan.zhihu.com/p/181498475)
- [万字详解常用存储结构：B+树、B-Link树、LSM树一网打尽](https://dbaplus.cn/news-141-4980-1.html)
- [聊一聊B+树、LSM树与TDengine存储引擎的关系 - TDengine | 涛思数据](https://www.taosdata.com/techtalk/14688.html)
- [Flink Table Store文件存储结构——LSM树 | JohnsonLin](https://www.linjiangxiong.com/2023/03/10/lsm-tree-intro/)
- [存储引擎 · influxdb2](https://yuzhigang.gitbooks.io/influxdb2/content/Concepts/storage_engine.html)
  - 在InfluxDB开发过程中，我们尝试了一些更受欢迎的选项。
  - 我们从LevelDB开始，这是一种基于LSM树的引擎，针对写入吞吐量进行了优化。
  - 之后，我们尝试了BoltDB，这是一个基于内存映射B+ Tree的引擎，它是针对读取进行了优化的。
  - 最后，我们最终建立了我们自己的存储引擎，它在许多方面与LSM树类似。
