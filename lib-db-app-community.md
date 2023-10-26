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

- ## 🔥 [Searchable and sortable H1B salary database | Hacker News_202306](https://news.ycombinator.com/item?id=36277706)
- 
- 
- 

- ## 🔥 [If All You Have Is a Database, Everything Looks Like a Nail | Hacker News_202012](https://news.ycombinator.com/item?id=25330223)
- 
- 
- 

- ## [Ask HN: Why are we so fragmented in databases options? | Hacker News_202210](https://news.ycombinator.com/item?id=33345464)
- Relational databases have dominated since the 1980s. 

- ## this is an excellent lecture on the history of DB, 
- https://twitter.com/mim_djo/status/1632318627142852610
  - although Google Map reduce system was a bad idea, all new shared disk DWH ( BigQuery, Snowflake, Dremio, Databricks etc ) stole the best part from it, which is separating Storage from Compute
- relational DB system are just too good in stealing other people innovations.
  - Separating compute from storage
  - Json
  - Graph
  - Open table format (Iceberg, delta)

# discuss-db-dev-xp
- ## 

- ## 

- ## 

- ## 🔥 [Leveraging Rust in our Java database | Hacker News_202309](https://news.ycombinator.com/item?id=37557880)
- 
- 
- 

- ## [Things I learned after getting users | Hacker News_202303](https://news.ycombinator.com/item?id=35132223)
- i relied on a SQL ORM which in short is a tool that makes writing SQL easier to pick up and faster to develop. the biggest downside is that it might execute 50 queries to your database to get a list of information, when it probably only needs 1, which will cause slowdown
  - I appreciate this honesty. Listen to this old man's advise: learn SQL properly. It's not that hard. Focus on it for a few weeks intensely and you've mastered it for life. Then just write SQL directly.

# discuss-regularly
- ## 

- ## [Confluent收购Immerok：我的观点 - 知乎_202301](https://zhuanlan.zhihu.com/p/597220515)

- ## [重新思考流处理与流数据库 - 知乎](https://zhuanlan.zhihu.com/p/600701331)

- ## [RisingWave的2022年年终复盘与展望 - 知乎](https://zhuanlan.zhihu.com/p/593169897)

- ## [投资实时数据系统最前沿：走进Current 2022 - 知乎](https://zhuanlan.zhihu.com/p/574022136)

- ## 🎯 [Databases in 2022: A year in review | OtterTune](https://ottertune.com/blog/2022-databases-retrospective)

- ### 👥🔥 [Databases in 2022: A Year in Review | Hacker News_202301](https://news.ycombinator.com/item?id=34220524)
- There are a number of ideas in the database space that the industry is adopting across the board:
  - Separation of storage and compute (Neon, AlloyDB, Aurora). Every cloud database should built one. It's a big undertaking, but benefits are undeniable.
  - Good query processor for analytics (Snowflake, Velox, Singlestore)
  - Open source. Especially in OLTP open source == trust
  - HTAP. Can run mixed workload (Singlestore, Unistore): both OLTP (apps) and OLAP (reporting). This has always been a dream, but we still live in the world of dedicated systems: E.g. Snowflake and Postgres.
  - Shared nothing sharding (Vitess). This is the most controversial as you lose compatibility with the mothership (MySQL for Vitess). So it's unclear this will be the dominant architecture in the future. I think the world may get to "dynamic sharding" where storage stays separate and compute can be multinode and the user can easily and instantly change the number of nodes.

- ClickHouse has switchable IO engines: - read; - pread; - mmap; - pread_threadpool; 

- 
- 

- ## [投资数据库领域：2021年总结（NoSQL、图、时序） - 知乎](https://zhuanlan.zhihu.com/p/453556881)

- ## 🎯 [投资数据库领域：2021年总结（OLTP、OLAP、streaming） - 知乎](https://zhuanlan.zhihu.com/p/452628664)

- ## 🎯 [Databases in 2021: A year in review | OtterTune](https://ottertune.com/blog/2021-databases-retrospective)
- 
- 
- 

- 👥🔥 [Databases in 2021: A Year in Review | Hacker News_202112](https://news.ycombinator.com/item?id=29731885)
- 
- 
- 
