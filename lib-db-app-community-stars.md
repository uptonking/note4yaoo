---
title: lib-db-app-community-stars
tags: [community, database]
created: 2021-08-30T15:51:01.157Z
modified: 2023-09-16T17:54:21.231Z
---

# lib-db-app-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## [Reddit’s database has two tables_201209](https://kevin.burke.dev/kevin/reddits-database-has-two-tables/)
  - Lesson: Don’t worry about the schema.
  - it looks like they use two tables for each “thing”, so a thing/data pair for accounts, a thing/data pair for links, etc.

- ## Most databases were built when data was static and queries were dynamic. 
- https://twitter.com/tantaman/status/1699826662408409383
  - For applications, most queries are static and the data is dynamic
- What you really want is a database where a query is the same things as an index, is the same thing as a subscription... These are all the same underlying mechanic.

- ## Myth(神话，想像或虚构的人物): Using UUID as the primary key will slow down inserts. 
- https://twitter.com/gwenshap/status/1686148804821811200
  - Fact: Not in Postgres.
  - I often recommend using UUIDs instead of integer sequences as primary keys. I was surprised to discover that many developers are uncomfortable with them and believe they will slow down inserts. 
  - [UUIDs are Bad for Performance in MySQL - Is Postgres better? Let us Discuss - YouTube](https://www.youtube.com/watch?v=Y5mWz4vK10A)
- It makes the code easier as well because you can generate IDs on the client.
  - Exactly! this also makes the system as a whole more scalable. This is not something you need early on, but changing PKs later is super hard and starting with UUIDs is not.

# discuss-sql
- ## 

- ## 

- ## 

- ## 🤔 What database has the best query language that’s not sql?
- https://twitter.com/aboodman/status/1607790827996327936
- tinybase > tinyQL
- I think graphQL occupies a pretty useful and pragmatic niche.
  - SQL suffers from cartesianification. Results are a square tabular matrix, which does not effeciently express heirarchical data. Probably graphQL tree shaped results actually fits app data better.
- i’m biased (due to previous employment), but definitely think neo4j and cypher is the answer you’re looking for!  ASCII art ftw!  
- Vertipaq with DAX language
- #datomic's #datalog is very intuitive if all you need are inner joins, which is just unification of variables. The minute you need anything else, things get ugly. Uglier than SQL? Who knows, pick your poison.
- Kusto Query Language (KQL), used by Azure Data Explorer and other Azure products. I'm a skeptic when it comes to query languages and DSLs and yet... KQL is awesome IMO
- Malloy fixes my vote for SQLs biggest flaw — combining entity relationships with querying. Malloy separates them, which is genius, especially for ML
- EdgeDB is an open-source database designed as a spiritual successor to SQL and the relational paradigm
- My biggest gripe with SQL is the lack of composability. When writing complex code, I can easily pull out functions. When complex writing SQL, I end up with a giant unmaintainable blob. I hope whatever solution you find addresses this!
- @perplexity_ai ‘s birdsql. Query in natural language (English), GPT figures out the sql. Hot take: natural language is the best query language.

# discuss-db-oplog
- ## 

- ## 

- ## 

- ## 

- ## Write-ahead logging is a standard way to ensure data integrity and reliability. 
- https://twitter.com/arpit_bhayani/status/1508665078929047552
  - Any changes made on the database are first logged in an append-only file called write-ahead Log or Commit Log. 
  - Then the actual blocks having the data (row, document) on the disk are updated
  - An operation like Update Query, Delete Query is logged in the commit log and not the actual changes making the write lightning-fast.
  - WAL also takes care of its data integrity by writing a CRC-32 before logging the operation. This CRC is checked during reading and replicating

- Advantages of using WAL
  - we can skip flushing the data to the disk on every update
  - significantly reduce the number of disk writes
  - we can recover the data in case of a data loss
  - we can have point-in-time snapshots

- A write-ahead log is the append-only source of truth in a database; each transaction appends events to it before table files are updated. Change data capture (which Marta is referring to) lets you retrieve and consume changes from that log. 
# discuss-db-streaming
- ## 

- ## 

- ## Understanding the Differences between Lambda and Kappa Data Processing Architectures for Big Data_202303
- https://twitter.com/moderndatastack/status/1637808211565891584
  - [Data processing architectures — Lambda vs Kappa for Big Data_202303](https://medium.com/towards-data-engineering/data-processing-architectures-lambda-vs-kappa-for-big-data-8cc9a7edeffd)
  - [Modern Data Architecture: An Overview of Lambda and Kappa Architectures_202003](https://www.credera.com/insights/modern-data-architecture-an-overview-of-lambda-and-kappa-architectures)

- Lambda and Kappa are two data processing architectures used to analyze large volumes of data in real time
- Lambda Architecture has three layers  
  - the batch layer, which processes historical data in batches, 
  - the speed layer, which processes real-time data streams in a distributed manner, 
  - and the serving layer, which provides queryable views of the data.
- Kappa Architecture, on the other hand, eliminates the batch layer and processes real-time data using a stream processing system, which stores the data in a database.
- Lambda is ideal for scenarios where historical data analysis is important, while Kappa is perfect for situations where real-time insights are critical.
- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## [sql server - Will index be fully loaded into memory_201011](https://stackoverflow.com/questions/4296027/will-index-be-fully-loaded-into-memory)
- No, it's treated like any other data stored on disk. It's loaded into memory disk page by disk page. And a page stays in memory as long as it's regularly accessed.

- The answer to this is in several parts:
  - The size of the index.
  - What parts are accessed.
  - Memory pressure.
- SQL Server cached the index in memory as it was being read.
  - However, if I had put other memory pressure on SQL Server, it would have dropped out those cached index pages by order of lowest reads.

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
- ## dbt (data build tool) enables analytics engineers to transform data in their warehouses by simply writing select statements. 
  - dbt handles turning these select statements into tables and views.
  - dbt does the T in ELT (Extract, Load, Transform) processes – it doesn’t extract or load data
  - A dbt project is a directory of .sql and .yml files. 

# uuid vs auto-increment

## [Best practices on primary key, auto-increment, and UUID in RDBMs and SQL databases](https://stackoverflow.com/questions/52414414)

- What I always do, even if it's redundant, is I create primary key on auto increment column (I call it `technical key`) to keep it consistent within the database, 
  - allow for "primary key" to change in case something went wrong at design phase 
  - and also allow for less space to be consumed in case that key is being pointed to by foreign key constraint in any other table 
  - and also I make the candidate key unique and not null.
- Technical key is something you don't normally show to end users, unless you decide to. 
  - This can be the same for other technical columns that you're keeping only at database level for any purpose you may need like modify date, create date, version, user who changed the record and more.

```SQL
CREATE TABLE users(
  pk INT NOT NULL AUTO_INCREMENT,
  id UUID NOT NULL,
  PRIMARY KEY(pk),
  UNIQUE(id)
);
```

- This question is quite opinion-based so here's mine.
- My take is use the second one, a separate UUID from the PK. The thing is:
  - The PK is unique and not exposed to the public.
  - The UUID is unique and may get exposed to the public.
- If, for any reason, the UUID gets compromised, you'll need to change it. Changing a PK may be expensive and has a lot of side effects. If the UUID is separate from the PK, then its change (though not trivial) has far less consequences.

- if you make it an increasing number, your competitors will know how many users you have and how fast you are adding new ones.

- I came across a nice article that explains both pros and cons of using UUID as a primary key. 
  - In the end, it suggests using both but **Incremental integer for PK and UUIDs for the outside world**. 
  - Never expose your PK to the outside.
