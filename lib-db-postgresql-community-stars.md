---
title: lib-db-postgresql-community-stars
tags: [community, postgresql]
created: 2023-10-26T19:17:23.144Z
modified: 2023-10-26T19:17:54.537Z
---

# lib-db-postgresql-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 📦 Are there major builds of OSS Postgres offered by different groups like there are JDKs?
- https://twitter.com/eatonphil/status/1744141903669465227
  - For example: Postgres builds with different allocators, configuration defaults, builtin plugins, etc.
  - The reason I ask is that almost every guide for running postgres in production says you need to tune it because the defaults are for the lowest common denominator.
  - So, why not have various distributions with sensible defaults for modern hardware?

- [Percona Distribution for PostgreSQL](https://docs.percona.com/postgresql/)
  - Percona Distribution for PostgreSQL is a collection of tools to assist you in managing your PostgreSQL database system: it installs PostgreSQL and complements it by a selection of extensions that enable solving essential practical tasks efficiently

- @TimescaleDB looks pretty good for time-series data
# discuss-performance
- ## 

- ## 

- ## Interesting perf problem with Postgres 9. 
- https://twitter.com/MarkCallaghanDB/status/1744385306475040911
  * table has a PK and 3 secondary indexes
  * inserts at one end - in ascending PK order
  * deletes from other end - find/delete N rows with smallest  value for PK col
  - Problem is that query planner takes ~100ms per `DELETE` .
  - So the planner is doing a lot more work than it needs to, something I have experienced with MySQL a few times. Although with MySQL I can use hints to reduce that waste. For my problem here, I will do some tests to see if more frequent ANALYZE helps.
- My case here is from PG 9, I try to test versions in order so it will be a few days before I see how this behaves with PG 16. But `get_actual_variable_range` is still there in modern PG.
  - A workaround is to delete more rows per `DELETE` statement so that the planner overhead is amortized over more rows. But in this case, by design I can't do that.
- That's true. But get_actual_variable_range has been enhanced several times since. Always with the aim of avoiding various pathological cases (possibly including this one). 
- I have seen this cause problems many times... saw a situation some years ago where planning with a cold cache took 20 minute and the query executed in milliseconds 

# discuss
- ## 

- ## 

- ## 

- ## Any tips on improving insertion speed to Postgres with the JDBC driver?
- https://twitter.com/MichaelDrogalis/status/1730655983696048493
- We’ve had the best luck with `UNNEST` for large inserts. Significantly faster for our workloads.
- I optimized PostgreSQL write operations in the past. Initially, we used batch processing, but the performance improvement was not significant. However, after consulting the official documentation, we switched to the COPY mode, resulting in a significant performance boost.
- addBatch is your friend.
- COPY command

- ## 🔍🔥 [Postgres full-text search: A search engine in a database (2021) | Hacker News_202207](https://news.ycombinator.com/item?id=32059566)
- 
- 
- 

- ## 🔍🔥 [Postgres Full-Text Search: A search engine in a database | Hacker News_202107](https://news.ycombinator.com/item?id=27973497)
- 
- 
- 

- ## 🕸️🔥 [Postgres as a graph database | Hacker News_202303](https://news.ycombinator.com/item?id=35386948)
- I designed and maintain several graph benchmarks in the Linked Data Benchmark Council, including workloads aimed for databases. We make no restrictions on implementations, they can any query language like Cypher, SQL, etc.
  - In our last benchmark aimed at analytical systems, we found that SQL queries using WITH RECURSIVE can work for expressing reachability and even weighted shortest path queries. However, formulating an efficient algorithm yields very complex SQL queries and their execution requires a system with a sophisticated optimizer such as Umbra developed at TU Munich. Industry SQL systems are not yet at this level but they may attain that sometime in the future.
  - **Another direction to include graph queries in SQL is the upcoming SQL/PGQ (Property Graph Queries) extension**. I'm involved in a project at CWI Amsterdam to incorporate this language into DuckDB.

- ## 🛢️🔥 [PostgreSQL is the worlds’ best database | Hacker News_202004](https://news.ycombinator.com/item?id=22766681)
- 
- 
- 

- ## 🔥 [At 22 years old, Postgres might just be the most advanced database yet | Hacker News_201812](https://news.ycombinator.com/item?id=18610601)
- 
- 
- 

- ## 🔥 [What PostgreSQL has over other open source SQL databases: Part II | Hacker News_201510](https://news.ycombinator.com/item?id=10445129)
- 
- 
- 
