---
title: lib-db-clickhouse-dev
tags: [clickhouse, olap]
created: 2023-01-08T15:31:25.315Z
modified: 2023-12-15T18:01:18.391Z
---

# lib-db-clickhouse-dev

# guide

- pros
  - ?

- cons
  - ?

- who is using #clickhouse
  - openai: [Why OpenAI chose ClickHouse for petabyte-scale observability _202506](https://clickhouse.com/blog/why-openai-uses-clickhouse-for-petabyte-scale-observability)
# dev

# blogs

## [Extracting, converting, and querying data in local files using clickhouse-local_202301](https://clickhouse.com/blog/extracting-converting-querying-local-files-with-sql-clickhouse-local)

- clickhouse-local is designed and optimized for data analysis using the local compute resources on your laptop

## more-blogs

- [Using TTL to Manage Data Lifecycles in ClickHouse](https://clickhouse.com/blog/using-ttl-to-manage-data-lifecycles-in-clickhouse)
  - Databases should make it easy to delete stale data, whether to save on storage costs or for compliance reasons.
  - Read about how you can use TTL (time-to-live) clauses in ClickHouse to delete, reset, or compress old data that’s no longer necessary.
# more
- [ClickHouse and The One Billion Row Challenge _202401](https://clickhouse.com/blog/clickhouse-one-billion-row-challenge?utm_source=twitter&utm_medium=social&utm_campaign=blog)
# discuss-news
- ## 

- ## 

- ## Today(20240308) @ClickHouseDB announced they're moving into the embedded OLAP engine space, with their acquisition of @chdb_io , and directly competing with @duckdb .
- https://twitter.com/medriscoll/status/1765785275014557831
  - Because @chdb_io , like @duckdb , provides a cheaper, faster, and SQL-ier alternative to Spark for crunching data on the data lake.
- If I understood correctly @chdb_io only had a Python API so far? If so, I don’t think that it’s currently on-par with @duckdb
  - Yes agree @duckdb has far more APIs for running in-process, though I suspect Python represents the majority of use cases

- Photon runs inside of Spark as an accelerator for parts of the pipeline, not as a standalone engine, per se.

- @sunchao 's Rust-based Comet project looks awesome and is an open-source alternative to Photon (only available in Databricks Cloud)
# discuss-wasm
- ## 

- ## 

- ## 

- ## 

- ## Introducing chDB-Wasm 
- https://x.com/auxten/status/2072232611284762874
  - https://wasm.chdb.io/
  - A complete ClickHouse OLAP engine, compiled to WebAssembly, running fully client-side. No server. No install. Just open a tab and run SQL.
- Under the hood:
  • Full ClickHouse SQL
  • Reads Parquet, CSV, JSON directly
  • Query remote sources (S3, URLs) from the browser
  • Runs entirely in WebAssembly, no backend

- Most modern browsers support multi threaded wasm.

- ❓ 和 duckdb 相比如何
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 5 years operating ClickHouse
- https://x.com/eatonphil/status/1907074469748682988
  - [I've operated petabyte-scale ClickHouse® clusters for 5 years _202504](https://www.tinybird.co/blog-posts/what-i-learned-operating-clickhouse)

- ## Interesting language feature in ClickHouse: LIMIT .. BY column (in addition to ordinary LIMIT). 
- https://twitter.com/lukaseder/status/1768220718469206478
  - It corresponds to PostgreSQL's DISTINCT ON clause, but:
  - 1) is (way) more intuitive, IMO
  - 2) supports more than TOP-1 per group rows
  - Of course, both syntaxes aren't strictly necessary. They're just convenice for ROW_NUMBER() filtering from a derived table, or using QUALIFY, if available

- ## 近期准备写一个clickhouse性能优化三板斧的文章。
- https://twitter.com/li_taiyang/status/1615559241296928769
  1. 反编译
  2. 性能比对工具
  3. 分析热点

- ## 🔥 [ClickHouse: An open-source column-oriented database management system | Hacker News_202105](https://news.ycombinator.com/item?id=27310247)
- 
- 
- 
