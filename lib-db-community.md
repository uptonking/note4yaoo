---
title: lib-db-community
tags: [community, database]
created: 2021-08-30T15:50:29.925Z
modified: 2021-08-30T15:50:54.515Z
---

# lib-db-community

# guide

# experts-fts-search
- eklem
  - search-index
  - https://github.com/eklem
# experts
- 郭忠明
  - https://www.zhihu.com/people/guo-zhong-ming-26
  - https://gitee.com/wlmqgzm/libhaisqlmalloc
    - Libhaisqlmalloc高性能内存分配库，管理堆内存，主要接口是malloc和free，用于降低频繁分配、释放内存造成的性能损耗，并且有效地控制内存浪费和内存碎片 

- https://github.com/skyzh
  - tikv maintainer
  - RisingLight: an educational OLAP database system.
  - BusTub: Relational Database Management System (Educational)
  - https://twitter.com/iskyzh
# discuss
- ## 

- ## 

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
  -Separating compute from storage
  -Json
  -Graph
  -Open table format ( Iceberg, delta)

- ## What database has the best query language that’s not sql?
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

- ## [联合主键和复合主键和联合索引](https://www.cnblogs.com/saoge/p/14431536.html)
- 复合主键 就是指你表的主键含有一个以上的字段组成
- 联合主键 就是多个主键联合形成一个主键组合，联合就在于主键A跟主键B形成的联合主键是唯一的。

- [提问关于 mysql得联合主键和复合主键的问题 - SegmentFault 思否](https://segmentfault.com/q/1010000021884619)
  - 在英文语境中只有 Composite Primary Key（也有叫 Compound Primary Key 的），就是一个表中如果是多个字段组成一个主键，那么这个主键就被称为这玩意儿。
  - 这种概念是中文编程界（或者说是中文编程博客界）人为造出的。
  - 上面的例子看看就得了，根本就是胡编一个 联合主键 的定义出来，你会发现它其实就是一个最简单的自增主键，只不过表的逻辑上 student_id + subject_id 是唯一的，id 就成了所谓的二者的 联合主键。
