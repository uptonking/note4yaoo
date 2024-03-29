---
title: lib-db-app-community-model-nosql
tags: [community, database, database-design, nosql]
created: 2023-09-17T18:10:03.415Z
modified: 2023-10-27T07:07:52.778Z
---

# lib-db-app-community-model-nosql

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 🆚️ Why are Relational databases (RDBMS) not a good fit for horizontal scaling? Why are NoSQL databases a good fit?
- https://twitter.com/deisbel/status/1764342602843779282
  - RDBMS stores related data using many small pieces, establishing data integrity restrictions between them that are hard to split and migrate. 
  - Besides, RDBMS need to maintain many indexes on top of data.
  - NoSQL uses only one unit of storage for each piece of data.

- ## 🔥 [How NoSQL forced the evolution of a scalable relational database | Hacker News_201807](https://news.ycombinator.com/item?id=17520809)
- 
- 
- 

- ## [到现在为止，NoSQL 运动给数据库系统留下什么宝贵的思想？ - 知乎](https://www.zhihu.com/question/264416654/answers/updated)
- https://www.zhihu.com/question/264416654/answer/2713792035
- 如果非要给NoSQL一个历史定位的话，那应该是一次对关系型数据库的解构运动。
  - 这次解构运动的发起是由于互联网应用的兴起，由于互联网对存储的使用重规模轻逻辑，所以导致传统的关系型数据库使用成本过高。
  - 问题在于当时那群年轻的互联网程序员没有好好回顾数据库的发展史，而是带着操作系统（文件系统）的包袱去解构的，再加上操作系统阵营和数据库阵营历来的对垒，导致了这场不应该发生的重复造轮子运动。 
  - 如果对数据库内核开发了解的同学应该知道，所有关系型数据库都是从键值数据库发展起来的，数据存储引擎最底层都是一个键值数据库。还有现在流行的各种消息中间件（RABBIT MQ之流）也是关系数据库中的一个零件而已（connection），是在网络兴起后，数据库提供CS架构下诞生的远程访问方案。所以就像一个小男孩喜欢拆玩具车，把电动机拿下来单独转；把轮子拆下来单独滚，自得其乐。

- Nosql强盗团伙生生从关系型数据库一统天下的局面里撕下一大块肉，这些年Nosql提供了前所未有的scalability能力和可用性，在超大并发情况下，我个人经验是基于Nosql的系统比基于关系型数据库痛苦少些。
  - 在Nosql架构中，不同节点之间不“share”数据，每个节点只要管自己那一亩三分地就好，你可以非常容易的把数据分布到成千上万的服务器上，读和写都更容易搞，一小部分节点“坏”了，也不容易让你的服务完全跪了，你也比较容易替换，各种姿势做rolling restart。
  - Mysql当然也能sharding，提供的功能是一样一样的，不过你分开之后这个sql查询可就受限制了，要不代价更大。
  - 现在我们来看Mysql等，自动sharding或者说auto-scale是有各种解决方案了，不过这是落后一步的，MongoDB等nosql是提前三到五年就玩的转了。这些年，Nosql团伙是逼着Mysql和Oracle在scalability方面不断改革
  - 另一方面，也出现了Newsql这个这种方案，鉴于Nosql分布式存储的优势，newsql的底层还是Nosql那种，顶层又要和sql兼容，那中间就需要一个对用户透明的自动sharding层。这玩意能做到多好，如何优化，就具体项目具体对待了。

- 一开始直接快刀斩乱麻，BigTable就是KV抽象加GFS，结果这种架构抛弃了事务和SQL能力，解决了一些问题和带来了新的问题，有新的问题就要解决。

- 说白了NOSQL就是仅提供原子层面的存储（结构化及非结构化）服务至于事务及SQL兼容性不是NOSQL必须该负责的内容，从而大大提升了扩展性和性能

- ## 🔥 [Database expert on why NoSQL mattered – and SQL still matters | Hacker News_201507](https://news.ycombinator.com/item?id=9964306)
- 
- 
- 
