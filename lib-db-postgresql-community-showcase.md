---
title: lib-db-postgresql-community-showcase
tags: [community, examples, postgresql, showcase]
created: 2023-10-26T16:45:28.359Z
modified: 2023-10-26T16:45:47.318Z
---

# lib-db-postgresql-community-showcase

# guide

# discuss-stars
- ## 

- ## ⚡️ ParadeDB has built an open-source PostgreSQL extension to do analytics very fast with high compression by using Parquet under the hood 
- https://twitter.com/tobias_petry/status/1757355904205213843
  - near the performance of ClickHouse 
  - [pg_analytics: Transforming Postgres into a Fast OLAP Database - ParadeDB _](https://blog.paradedb.com/pages/introducing_analytics)
- How do backups work? I guess there is no way until WAL integration is done? But how will WAL work together with Parquet files?
  - We do support backups. Re: WALs, not yet but we soon will. Our current plan is to make Delta/Iceberg work with Postgres WAL logs instead, but TBD exactly! Things will change as we dive into the implementation

- DuckDB is equally fast as ClickHouse

- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 飞总发了一篇《2023年，中国对PostgreSQL的贡献≈0》所以我刚才翻阅了 OSSRank 收录的 188个 PostgreSQL 生态开源项目。
- https://twitter.com/GobeUncleWang/status/1744190341438472279
- 中国公司作为主导者或主要参与者的项目只有四个，分别是：
  - Pigsty：我@北京
  - duckdb_fdw：alitrack@杭州
  - zhparser：amutu@深圳
  - pg_roaringbitmap：陈华军@苏宁

- ## 🔥 [PolarDB, yet another open source database system based on PostgreSQL | Hacker News_202105](https://news.ycombinator.com/item?id=27330342)
- 
- 
- 

- ## [digitalOcean: Fully managed PostgreSQL databases | Hacker News_201902](https://news.ycombinator.com/item?id=19162729)
- 
- 
- 

- ## 🔥 [PostgREST – Serve a RESTful API from any Postgres database | Hacker News_202212](https://news.ycombinator.com/item?id=34172205)
- 
- 
- 

- ## 🔥 [PostgREST: REST API for any Postgres database | Hacker News_202011](https://news.ycombinator.com/item?id=25159097)
- 
- 
- 

- ## 🔥 [PostgREST – A fully RESTful API from any existing PostgreSQL database | Hacker News_201703](https://news.ycombinator.com/item?id=13959156)
- 
- 
- 

- ## 🔥 [PostgREST – REST API from any PostgreSQL database | Hacker News_201507](https://news.ycombinator.com/item?id=9927771)
- 
- 
- 

- ## ☁️🔥 [fly.io: Free Postgres databases for small projects | Hacker News_202201](https://news.ycombinator.com/item?id=30018197)

- Free tier of CloudFlare Pages/functions runs the app at the edge by default. For Fly.io, this scaling has to be manually configured for both the app and the DB. Are there any plans to offer it by default for the free tier? It is hard to evaluate the benefits of having the data center near the end user when it is not offered out of the box, especially since all the Fly.io blog posts talk about how great their service is for HTML-over-the-wire UIs like Phoenix live view and Rails Hotwire.
  - You can squeeze a hell of a lot more perf out of general purpose compute that is maybe an extra 15 ms away than one-shot workers lacking any in-RAM persistence, or ability to do much more than limited local k/v lookups. The equation is totally different. Many workers I've seen (or written) start by reaching out over the Internet to another backend. There goes most of your edge benefit almost immediately.

- For comparison, note also that ElephantSQL offers 20MB databases on their free tier with 5 concurrent connections. https://www.elephantsql.com/plans.html
- https://supabase.com/pricing - 500MB, 2GB download/month (can be used as plain PostgreSQL)
- https://www.cockroachlabs.com/pricing - 5GB, 250M "request units"/month distributed, PostgreSQL-ish

- ## 🔥 [PgOSQuery: Expose the operating system as a Postgres database | Hacker News_201410](https://news.ycombinator.com/item?id=8532835)
- 
- 
- 
