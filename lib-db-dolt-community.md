---
title: lib-db-dolt-community
tags: [community, database, dolt]
created: 2023-08-25T21:16:51.669Z
modified: 2023-08-25T21:17:11.979Z
---

# lib-db-dolt-community

# guide

# discuss-versioning
- ## 

- ## [数据库版本管理应该如何实现？ - 知乎](https://www.zhihu.com/question/20080857/answers/updated)
- 😣 目前是把DDL、存储过程、函数、核心数据整理成SQL文件，做为baseline，提交SVN；
  - 每次修改，均记录到文件、整理成增量的sql update语句，提交svn；同时更新整体的SQL语句。
  - 很复杂，尤其是开发、内部测试、客户手上多个版本，想死的心都有了

- [用版本控制工具将数据库版本化](https://blog.csdn.net/tywo45/article/details/2480078)
  - 版本化数据库的起点——创建一个数据库Schema基线，这个基线是一些数据库脚本（包括 create table ，alter table ，drop table ，insert data ，update data ，delete data等）。
  - 这些脚本可以位于同一.sql文件中，也可根据其它规划分别位于不同文件中，例如将视图脚本，初始化数据脚本，建表脚本分别置于不同的文件中。
# discuss-dolt
- ## 

- ## 

- ## 

- ## 

- ## [Dolt performance comparison to postgres and mysql](https://github.com/dolthub/dolt/issues/6536)
- I suspect there might be two actual issues at play: one causing our client to behave slowly, and another slowing down the actual execution of the query. (Hence why connecting with a mysql client is approximately as fast as running the query locally.)

- ## [Document Version Control · frappe-erp](https://github.com/frappe/frappe/issues/22075)

# discuss-terminusdb
- ## 

- ## 

- ## 

- ## 

- ## With there only being a handful of temporal, datalog based databases out there, what sets TerminusDB apart from XTDB, and when would one choose one over the other?
- https://discord.com/channels/689805612053168129/689892819678134354/1133508959341395969
- TerminusDB works with RDF while XTDB data-model is bespoke(定制的), 
  - and while I'm not the biggest fan of RDF, I found data-export generally unpleasant in Datomic family databases. (you can kinda export to EDN, but it's not data-exchange first like RDF is)
- XTDB has SQL with extra stuff and Datomic/EDN query notation, TerminusDB has GraphQL queries as well as its own query language called WOQL, depending on your background/environment you might gravitate towards one or the other
- In XTDB transactions are appended in some immutable log e.g. single partition Kafka topic, which makes it behave like a plain old database. 
  - TerminusDB is more like git, where commits are first class citizens, can be rebased, merged, forked, exported e.t.c.
- They seem to have different approaches to bitemporality. 
  - In a temporal database, bitemporal data is both the valid time and transaction time of the data.
  - XTDB is using two timestamp ranges per triple, with transactions manifested in one of the timestamps. 
  - In TerminusDB bitemporality is achieved via it's commits, but it doesn't give every triple a "valid-time" range like TXDB does.

- TerminusDB makes heavy use of succinct(简洁的) datastructures and will probably have lower memory footprint than in-memory XTDB, 
  - but otoh graph processing is limited to in-memory processing (which is fine imho, most databases become unusable once their indexes no longer fit into memory even with disk storage, and the succinct datastructures mean that you can fit a lot of data in memory), 
  - TXDB has a wide array of index, document and log backend (in-memory and on-disk) at the cost of more memory usage.

- ## Having a Javascript client running in browser, where does the client side TerminusDB store data?
- https://discord.com/channels/689805612053168129/689892819678134354/1130494867575943188
  - is there any limitation that would prevent it's use in an offline mobile application?
- **client side really only connects to a server, it has no local data**. 
  - but you could maybe ship your app with an instance of terminusdb in which case it'd store on that localhost terminusdb. 
  - Then whenever you have internet access again, you can make that local terminusdb push/pull to syncrhonize with some server if you like.
  - That said I don't think we've had anyone develop a proper app with terminusdb and i'm not sure how viable it is to have the server running on a phone. 
  - We know we can build on ARM (as long as it is 64 bit) so that shouldn't be the issue. The issue is more going to be in packaging it all

- ## I've been looking for a graph database that might have the possibility of being used in an offline-first mobile application written in Rust and run through Tauri
- https://discord.com/channels/689805612053168129/689892819678134354/1130415411792453744
  - I came across the Terminus-Store Github repo, which is the new Terminus datastore layer and is compatible with Rust and offers a "triple store".
  - Would using the Terminus-Store package still give you the same querying power  (especially that Datalog syntax)  as the regular Terminus DB clients ?
- store will not give you the same querying power. 
  - The only thing it can do is iterate over all triples, or look up by a few predefined patterns (by subject, by subject-predicate, by object, or by predicate).
  - All the actual dataloggy stuff, as well as all the document extraction logic, is in terminusdb proper 
- we have been pushing more and more things down into rust though_20230717, and it's not unimaginable that at some point, we will have a standalone rust version for at least a significant portion of the server. 
  - But at this point that's a dream for the future, and nowhere near completion
- interesting to see that a lot of Terminus is written in Prolog. What areas do you feel Prolog is the best fit vs Rust / when do you choose one tool over the other?
- prolog is pretty good for search algorithms so it's a pretty natural fit for writing a query language
- so we use rust to produce iterators over triples for us, then drive their iteration from prolog in creative ways
  - but rust is much better when it comes down to actually storing things, doing bit-level operations, synchronizing access, etc
  - much faster too
  - we also tend to push things down into rust once we understand an area well and the interface to it has stabilized, but we want it to go faster. In that case it's worth spending the extra effort to get a bit more power
