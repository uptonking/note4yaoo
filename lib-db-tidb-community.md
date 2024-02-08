---
title: lib-db-tidb-community
tags: [community, database, tidb]
created: 2024-02-08T16:03:58.798Z
modified: 2024-02-08T16:04:30.976Z
---

# lib-db-tidb-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🆚️ [TiDB和FoundationDB各有什么优劣？ - 知乎](https://www.zhihu.com/question/274003103)
- FoundationDB和TiKV是一个层次的东西，都是一个支持分布式事务ACID的ordered KV map。
- 架构：都是shared nothing，TiKV单机引擎rocksdb，核心数据结构skiplist，FoundationDB单机基于磁盘的B-Tree。
  - 两者都强调分层，下面是存储，上面是接口层，TiDB是TiKV的SQL接口层，FoundationDB core就是下面的存储层。
  - 稍一点不同的是，因为TiKV本质上还是为TiDB服务的，所以加了一些接口专门给TiDB用，主要是为了计算下推。
- 隔离级别：都是SSI，基本就是拿一个快照，然后事务内的写自己能读到(不确定TiKV是SI还是SSI)。
- 事务冲突检测：TiKV冲突检测在各个TiKV节点上，FoundationDB拎了一个单独的叫做resolver的组件出来做冲突检测，这个组件可以有多个，组件会把最近5s的已经提交的写的key放在内存中，这也是known limitations中一个事务中最大只支持5s的原因之一。
- 副本复制协议：TiKV用raft，FoundationDB用paxos。
- share nothing指的是节点之间，不是region之间

# discuss-internals-tidb
- ## 

- ## 

- ## How does TiDB execute a query?
- https://twitter.com/sunbains/status/1744048698710171953
- For simplicity I’ve skipped the transaction part. 
  - Prepare a plan for this request
  - Get the metadata of the table from TiKV.
  - Fetch region/tablet location  for each related key in the SQL query from the Placement Driver (PD).
  - Group the related keys by Region
  - Dispatch the tasks to the TiKV instances that contain the regions concurrently
  - Reassemble the data retuned by the TiKV instances
  - Return the data to the client.
- TiKV has a query push down mechanism called Coprocessor to reduce the traffic between the nodes.


- ## TiDB Serverless is a MySQL compatible true Serverless solution. 
- https://twitter.com/sunbains/status/1755265066629570974
  - Doesn’t use any MySQL code and is architected to leverage the elasticity of the cloud infrastructure with goodies like disaggregated storage (primary storage is S3, which reduces cost significantly), query pushdown, optimized for space efficiency and lots more

# discuss
- ## 

- ## 

- ## 
