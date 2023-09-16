---
title: lib-db-app-community
tags: [community, database]
created: 2021-08-30T15:50:29.925Z
modified: 2023-09-16T17:54:11.257Z
---

# lib-db-app-community

# guide

# discuss
- ## 

- ## 

- ## This document from ScyllaDB makes a strong case why B-trees make a good choice for in-memory collections as well
- https://twitter.com/debasishg/status/1688551567044251648
  - B-trees are usually used for disk based storage. 
  - [The Taming(驯服) of the B-Trees - ScyllaDB](https://www.scylladb.com/2021/11/23/the-taming-of-the-b-trees/)
- Also TIL: Google has implemented a C++ template library that implements B-tree containers with an analogous interface to the standard STL map, set, multimap, and multiset containers
- I tested several B-tree implementations on the JVM in https://github.com/szeiger/forest/tree/master/main/src/main/scala/forest/mutable. 
  - I don't remember the exact benchmark results but there was no conclusive case to use them instead of the red-black trees in Scala's TreeMaps.

- Obvious in retrospect, but I just realized that if you use prolly trees for your DB indices, you can run queries against any historical state of your DB (by simply not GC'ing old data). And in fact, @DoltHub supports that

- ## 今天发现 在 DB 里面对于 时间/空间或者多维的数据操作 , 用 R tree  来减少工作量似乎是个冷知识了.
- https://twitter.com/fuergaosi/status/1658470145109680132
- 已经见过好几次有老哥为了计算时间区间, 把数据拉到内存里面 For loop 计算了
- 当年 LBS 跟现在的 AIGC 一样火的时候，R tree 都可以写到简历上来吹牛逼了。

- ## 和ChatGPT聊DB设计获得新知，Nested Set Model：
- https://twitter.com/TooooooBug/status/1659041013800001536
  - 将父子关系映射到数轴上变为数字范围的包含关系，然后通过数字范围大小就能计算出各条记录的父子关系，避免反复递归。

- ## [Mongo (Atlas) vs. Planetscale for my simple SaaS? : Database](https://www.reddit.com/r/Database/comments/wh9rd1/mongo_atlas_vs_planetscale_for_my_simple_saas/)
- Mongo:
- Pros: I have the most experience with it, super easy to get up and running, built for simple document structure like my use case, very cheap pay-as-you-go pricing on Atlas.
- Cons: Database doesn't enforce schema (ofc) so while as a dev I love it, as a business owner it feels maybe too risky. Has low connection limit (500) which could possibly bottleneck with serverless connections.

- Planetscale:
- Pros: Enforces schema and even has cool branching/merging of schema changes so feels much "safer" than Mongo to protect it from me doing something dumb. Unlimited connections so no bottleneck there.
- Cons: Free tier is probably good for a while but then immediately jumps to $29 unlike mongo where prices scales with me (though obviously thats not too bad, just more). Don't necessarily need a relational DB, but doesn't hurt I guess. A little bit more setup/work than Mongo because I have to build/migrate/merge the DB branches/schemas.

- I second the suggestion of trying CockroachDB serverless.
  - What about CockroachDB free tier serverless? You would go a very long time before paying a bill.

- Actually you can create a schema validation in Mongo. Check it out
  - [Schema Validation — MongoDB Manual](https://www.mongodb.com/docs/manual/core/schema-validation/)

- my advice would be to stick to what you know. If you know Mongo well go for it. 
  - If you're starting a business, proving the idea and marketing it is going to be a lot more important than the tech unless you're doing something bleeding-edge. 
  - Try to not overfocus on the tech. NextJS + your preferred DB seems like a good place to start.

- ## this is an excellent lecture on the history of DB, 
- https://twitter.com/mim_djo/status/1632318627142852610
  - although Google Map reduce system was a bad idea, all new shared disk DWH ( BigQuery, Snowflake, Dremio, Databricks etc ) stole the best part from it, which is separating Storage from Compute
- relational DB system are just too good in stealing other people innovations.
  - Separating compute from storage
  - Json
  - Graph
  - Open table format (Iceberg, delta)

- ## [联合主键和复合主键和联合索引](https://www.cnblogs.com/saoge/p/14431536.html)
- 复合主键 就是指你表的主键含有一个以上的字段组成
- 联合主键 就是多个主键联合形成一个主键组合，联合就在于主键A跟主键B形成的联合主键是唯一的。

- [提问关于 mysql得联合主键和复合主键的问题 - SegmentFault 思否](https://segmentfault.com/q/1010000021884619)
  - 在英文语境中只有 Composite Primary Key（也有叫 Compound Primary Key 的），就是一个表中如果是多个字段组成一个主键，那么这个主键就被称为这玩意儿。
  - 这种概念是中文编程界（或者说是中文编程博客界）人为造出的。
  - 上面的例子看看就得了，根本就是胡编一个 联合主键 的定义出来，你会发现它其实就是一个最简单的自增主键，只不过表的逻辑上 student_id + subject_id 是唯一的，id 就成了所谓的二者的 联合主键。
