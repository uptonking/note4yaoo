---
title: lib-db-postgresql-community-pm-showcase
tags: [community, examples, postgresql, showcase]
created: 2023-10-26T16:45:28.359Z
modified: 2024-08-11T07:21:48.172Z
---

# lib-db-postgresql-community-pm-showcase

# guide

# pg-powered
- neon

- Crunchy Data. Trusted Open Source PostgreSQL and Enterprise PostgreSQL Support, Technology and Training
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

# discuss-pg-web/wasm
- ## 

- ## 

- ## [Learn Postgres at the Playground – Postgres compiled to WASM running in browser | Hacker News _202208](https://news.ycombinator.com/item?id=32498435)
- The playground seems to be using v86.js I don't see the required "Redistributions in binary form must reproduce the above copyright notice" 
  - v86 is an interesting choice, I wonder why they couldn't compile Postgres itself with Emscripten (AFAIK it's all C code).
  - I'm assuming there are too many details like syscalls and file system specific APIs that they needed a lower level virtualization?

# discuss-tools/apps
- ## 

- ## 

- ## 

- ## [What's the best PostgreSQL GUI setup in 2026? : r/PostgreSQL _202604](https://www.reddit.com/r/PostgreSQL/comments/1sbmi9f/whats_the_best_postgresql_gui_setup_in_2026/)
- Personally I use DBeaver because:
  - While mostly work with PostgreSQL, I need to work with Oracle and SQLIte occasionally. Sometimes I need to do ad hoc data transfers from e DB to another. DBeaver does this well enough for me!
  - I mainly do GIS work. Being able to view query results on a map is very handy. I know PGAdmin can do this as well, but my experience with viewing spatial data in DBeaver has been better.

- Datagrip is awesome. They just released a community edition
  - [DataGrip Is Now Free for Non-Commercial Use | The DataGrip Blog _202510](https://blog.jetbrains.com/datagrip/2025/10/01/datagrip-is-now-free-for-non-commercial-use/)
  - Which features are included under the free license?
  - All the features of the commercial version are available, including AI-powered code completion, an intelligent query console, an Excel-like data editor, Git integration, and support for multiple databases. 

- pgAdmin is pretty lightweight. Uses about 400 MB here on a Macbook.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Two projects in Postgres ecosystem I am excited about:
- https://x.com/iavins/status/1914177272522703311
  1. PgDog - to build the Vitess of Postgres (in rust, btw). Like Vitess, it's not an extension. It's a full fledged external system which works in conjunction with Postgres databases. 
  2. OrioleDb - It is a custom storage engine for Postgres (via an extension). Postgres came about 30 years ago, this one is being designed for modern hardware. It is also going to be distributed plus experiments with disaggregated storage.
- What is great about postgres is the great ecosystem of forks and extensions that make it evolve faster than the core, which must be more conservative. But the risk is the fragmentation of the solutions. Sharding? with Citus, Aurora Limitless, PgDog?
  - Fragmentation is also good for consulting — one can feel free to recommend the best, if you’re not the vendor

- ## OpenAI handles 800 million users on ChatGPT with just one PostgreSQL primary and 50 read replicas _202601
- https://x.com/arpit_bhayani/status/2014615870992163148
  - Today, OpenAI published an engineering blog explaining how they scaled their Postgres setup to support a massive 800 million users using a single primary and 50 multi-region replicas.
  - They dive into details around their scaling approach, the PgBouncer proxy, cache locking, and cascading read replicas. It is genuinely neat and impressive.
- > And they hit a wall, so they’re migrating off
  - > To mitigate these limitations and reduce write pressure, we've migrated, and continue to migrate, shardable (i.e. workloads that can be horizontally partitioned), write-heavy workloads to sharded systems such as Azure Cosmos DB, optimizing application logic to minimize unnecessary writes. We also no longer allow adding new tables to the current PostgreSQL deployment. New workloads default to the sharded systems.
- That quote is about offloading some write-heavy workloads to Cosmos. Same post says: "PostgreSQL has remained unsharded, with a single primary instance serving all writes." Single primary + ~50 read replicas.

- It's no more than a footnote in the original blog, but it's also worth noting that they use Azure Cosmos DB for write-heavy workloads (I assume all chat messages). Postgres is not the only durable storage powering ChatGPT.

- Glad I wasn’t the only one that noticed this. Having one primary has to be a bit easier when you’re actively trying to avoid writing to it

- ## OpenAI使用单一未分片的PostgreSQL集群（1主40从+）服务整个业务
- https://x.com/RonVonng/status/1924305840535978431
- OpenAI 的PG实践有力的证实了《分布式数据库是伪需求》，毕竟，OpenAI 能用一套主从PG集群干到现在5亿活跃用户，你的业务有极大概率也根本不需要分区Sharding或分布式数据库
  - 主从架构写是有上限的吧，这个问题理论上会是以后的瓶颈，而且我看了文章里也只是提到减少瞬时写

- 那Hadoop为代表的大数据是不是伪需求
  - Hadoop这套基本已经凉了。大数据则受到严峻挑战，可以看DuckDB 的宣言《Big Data is Dead》。

- ## Hyperdrive is: https://hyperdrive-demo.pages.dev - but tl; dr: access Postgres (so far…) databases directly from Workers, 
- https://twitter.com/elithrar/status/1766472461481054484
  - make them faster via our network, put a HTTP API in front of your DB, and offload frequently run queries to our dialect-aware cache.
- How does cache invalidation work with Hyperdrive?

- ## Introducing PGlite - WASM Postgres running in the browser, Bun and Node
- https://twitter.com/samwillis/status/1760735476343001553
- which extensions does it support? Does it WAL/sync back to a server?
  - No extensions yet, but we are looking to support pgvector. Syncing to/from the server with @ElectricSQL is coming very soon

- ## 🚀 PGlite, WASM Postgres running in the browser, Bun and Node. Only 3.7mb gzipped
- https://twitter.com/ElectricSQL/status/1760734511132995604
- I’ve literally been waiting years for something like this to exist so Postgres could run in @stackblitz
- How did you achieve persistent to idb? Is it block based writing or just whole db dump? If it is block based, what did you do with async writing? Did you use asyncify? So much questions, but I didn't find answers after brief repo review 

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
