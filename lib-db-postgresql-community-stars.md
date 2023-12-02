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
