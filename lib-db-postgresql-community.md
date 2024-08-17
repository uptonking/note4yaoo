---
title: lib-db-postgresql-community
tags: [community, postgresql]
created: 2022-06-13T03:00:54.134Z
modified: 2022-06-13T03:01:05.956Z
---

# lib-db-postgresql-community

# guide

# discuss-not-yet
- ## 

- ## Incremental View Maintenance in PG. Not implemented, but a neat page. PG really is going to eat everything, isn't it?
- https://x.com/criccomini/status/1814351383715590382
- Last time I looked into it, it wasn't really useful yet. Limited support for which SQL is supported in incrementally materialized views, and very locking-heavy.

- Its actively being worked on. The development is currently happening as the `pg_ivm` extension already supported by some cloud providers. The plan is to merge it into PG one day when it has high feature completeness for most SQL operations.
# discuss-pg-olap
- ## 

- ## 

- ## Lots of buzz lately around the idea of baking OLAP query engines into Postgres. Is anyone working on making this possible on read replicas (only)? 
- https://x.com/gunnarmorling/status/1824521817811226997
  - By definition, analytics workloads don't require ms range data freshness, so I think it's better to offload these queries to separate nodes and keep the precious CPU cycles on the primary for OLTP transactions.
- OLAP on row-based storage will be unimpressive.
  - 🤔 Data would be stored twice, in columnar form for efficient OLAP usage.
- Couldn’t you just run your OLAP queries on the replicas?
  - Sure, but just propagating any data changes to the OLAP engine on the primary will cost CPU and disk I/O.
- Yes, the product I work on, Postgres Distributed (pgd), is coming out with analytics via Delta Lake and using DataFusion. While you can run these analytics queries from any Postgres node, pgd has a concept of a writer leader and read-only routing to avoid the write leader

# discuss
- ## 

- ## 

- ## 

- ## great to see more posts on table access methods for postgres (I.e. pluggable storage engines)
- https://twitter.com/eatonphil/status/1765456975012282750
  - Here was my take on this topic a bit ago
- So could we use this for audit trails/logs? Those are not use frequently and are only read-only. Even if you have to ship it manually every day to a new table.
  - Yeah, we could. I imagined a use case like where a table is partitioned per day and child tables are converted to road every day to compact the whole partitioned table.

- ## What do you call "dead tuple" in PostgreSQL?
- https://twitter.com/mmeent_pg/status/1764657105825374319
  - when xmax < current xid
  - when xmax < xmin horizon for all ongoing tx or replication 
  - when lp_flags=dead (and space is reusable)
- It depends on what you expect. The answers given don't really provide a correct answer from an internals PoV
  - A tuple is considered dead if the transaction indicated in xmin has aborted, or if the transaction indicated by xmax has committed and has passed the global xmin horizon (or, if you're looking from a visibility snapshot PoV, if the xmin/xmax rules apply within the snapshot).

- ## 实现了 pg wire protocol 的数据库是不是都是 pg 了
- https://twitter.com/leiysky/status/1764242517472752040
- 那种只能算PG生态。DuckDB虽然是 PG wire protocol，但是有 duckdb_fdw 和 pg_quack 给包进来，能让 PG 本体主干直接利用上，所以算是个例外。

- ## 🔥 [How Postgres is more than a relational database: Extensions | Hacker News_201811](https://news.ycombinator.com/item?id=18555276)
- 
- 
- 

- ## 🔥 [Designing a SaaS Database for Scale with Postgres | Hacker News_201610](https://news.ycombinator.com/item?id=12649734)
- 
- 
- 

- ## 🤔🔥 [How to Manage Connections Efficiently in Postgres, or Any Database | Hacker News_201810](https://news.ycombinator.com/item?id=18220906)
- 
- 
- 

- ## 中国的公有云数据库市场中，PG 的营收仅有 MySQL 的 0.1-0.3%
- https://twitter.com/baotiao/status/1680804553942515712

- ## [pg_jieba postgres14 分词和预期结果不一致](https://github.com/jaiminpan/pg_jieba/issues/54)

- ## [PostgreSQL中三种自增列sequence，serial，identity区别](https://www.cnblogs.com/wy123/p/13367486.html)
- 对于自增字段，无特殊需求的情况下，sequence不适合作为“自增列”，作为最最次选。
  - sequence在所有数据库中的性质都一样，它是跟具体的字段不是强绑定的，其特点是支持多个对个对象之间共享。
  - sequence类型的字段表，在使用CREATE TABLE new_table LIKE old_table的时候，新表的自增字段会已久指向原始表的sequence
  - sequence作为自增字段值的时候，对表的写入需要另外单独授权sequence
- identity是serial的“增强版”，更适合作为“自增列”使用。
  - identity本质是为了兼容标准sql中的语法而新加的，
  - 修复了serial的缺陷，如无法通过alter table的方式实现增加或者删除serial字段
- sequence，serial，identity共同的缺点
  - 是在显式插入之后，无法将自增值更新为表中的最大Id，这一点再显式插入的情况下是潜在自增字段Id冲突的
  - 自增列在显式插入之后，一定要手动重置为表的最大Id
