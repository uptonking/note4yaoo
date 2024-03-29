---
title: lib-db-postgresql-blog-vendors
tags: [blog, postgresql, vendors]
created: 2023-10-26T18:11:46.163Z
modified: 2023-10-26T18:14:17.038Z
---

# lib-db-postgresql-blog-vendors

# guide

# blogs

## ⚖️ [Why does Neon use Paxos instead of Raft, and what's the difference? - Neon _202208](https://neon.tech/blog/paxos)

- TLDR: Neon separates storage and compute, substituting the PostgreSQL persistency layer with a custom-made distributed storage written in rust. 
  - Due to this separation, some nodes don’t have persistent disks. 
  - The original Raft paper works only with uniform nodes, but Paxos variants support proposers without storage and allow the acceptors to be the only nodes that have storage. 
  - We use a Paxos-like separation of concerns and recovery procedure, Raft-like election procedure, and TLA⁺ to check our modifications.

## [Lessons Learned From 5 Years of Scaling PostgreSQL _202104](https://onesignal.com/blog/lessons-learned-from-5-years-of-scaling-postgresql/)

- For nearly a decade, the open-source relational database PostgreSQL has been a core part of OneSignal. 
  - Over the years, we've scaled up to 75 terabyte (TB) of stored data across nearly 40 servers. 
- Our real-time segmentation features have benefited greatly from PostgreSQL’s performance, but we've also struggled at times due to bloat caused by our heavy write load and limitations of the PostgreSQL upgrade path.

- Partitioning
  - Large tables can be problematic for a lot of reasons, including: disk size, CPU count to serve queries, time taken for index scans, time taken for autovacuums, your ability to manage bloat, and so on. 
  - To address these issues, you can partition your tables.
  - Newer versions of PostgreSQL come with great support for splitting up your tables using their built-in partitioning feature. 
  - One advantage of using the built-in support is that you can query one logical table and get results, or split data between a number of underlying tables.
  - We currently partition both our subscribers and notifications data by tenant across 256 partitions. Due to increasing scale, we will likely be upping that to 4096 partitions — both for reasons of wanting to utilize more servers and also for improving the efficiency of queries and maintenance processes.
  - If you find yourself growing quickly and needing to partition, I recommend creating a lot of partitions upfront to save yourself some trouble later on.

- Sharding
  - Sharding is a natural extension of partitioning, though there is no built-in support for it. 
  - Briefly, sharding means to split your data across multiple database processes, typically on separate servers. This means more storage capacity, more CPU capacity, and so on.
  - If you have more than one application, it's generally a good idea to keep knowledge of the database topology out of your application (including both partition and shard level).
  - We are, however, making big strides towards creating a data proxy that is the sole application aware of the partition and shard topology.
  - We originally sharded our partitions by tenant ID/uuid
  - This was sufficient early on, but we now want the flexibility to move partitions around as part of incremental database upgrades and to isolate larger tenants. The data proxy initiative we have in-progress will support this

## [HTTP vs. WebSockets: Which protocol for your Postgres queries at the Edge - Neon _202307](https://neon.tech/blog/http-vs-websockets-for-postgres-queries-at-the-edge)

- A Comparative Analysis of SQL-over-HTTP and WebSockets in Edge and Serverless Environments

- We recently introduced SQL-over-HTTP to our driver, which previously only supported WebSockets. Why did we do that? And which approach is faster?
  - the main challenge with WebSockets is minimizing network round-trips since state persistence is typically lacking between requests in Edge environments. After several significant optimizations to the WebSockets driver, we successfully reduced the number of round-trips from nine to four. 
- We experimented with different protocols and compared our WebSocket driver latencies to those of SQL-over-HTTP via fetch. Why HTTP, you ask? 
  - The short answer is: to reduce latencies.
  - The advantage WebSocket has over SQL-over-HTTP drivers is Postgres compatibility. HTTP does not support sessions, transactions, or Postgres features such as NOTIFY and the COPY protocol, but it works well for simple, one-shot queries.

- Conclusion
  - With @neondatabase/serverless driver, you get both in a single package to accommodate your use case. 
  - Do you run single-shot queries? In this case, you might want to consider using HTTP. 
  - Do you execute multiple queries in a single connection? Then WebSockets can bring latencies down to 4ms once the connection is established.
  - Another interesting finding, however, is that the runtime matters as much as the protocol. 
  - The Edge network is far larger than the Serverless one, making it geographically closer to the end user. However, with connection cache, HTTP queries executed in Serverless environments show even lower latencies than the ones executed in Edge runtimes.

- Therefore, developers who strive for lower latency queries using serverless runtimes should consider the following:
  - Query type: Do you execute single-shot queries? Or run multiple queries for each function?
  - Regions: Where are your users located? Are they in one region or scattered across multiple geographies? Where is your database located?
  - API: Do you use Node.js specific functions? 

## 💠 [how Figma built a sharded Postgres environment _202403](https://www.figma.com/blog/how-figmas-databases-team-lived-to-tell-the-scale/)

- https://twitter.com/eatonphil/status/1768336441715658938
  - Doesn't Aurora Limitless solve this problem?

### [Why Has Figma Reinvented the Wheel With PostgreSQL? _202403](https://medium.com/@magda7817/why-has-figma-reinveted-the-wheel-with-postgresql-3a1cb2e9297c)

- The Figma engineering team was aware of, and evaluated, several existing options that could have made their database layer horizontally scalable. 
  - But still, they decided to build their own sharding solution from scratch.

### 👥 [How Figma's databases team lived to tell the scale | Hacker News _202403](https://news.ycombinator.com/item?id=39706968)

- Serverless Aurora is incredibly expensive for most workloads. I have yet to find a use case for any SaaS product that is used >4 hours a day. Since all my products span at least 3 time zones there is at least 12 hours of activity a day.
  - We found this out the hard way in a small startup. The per query and I/O expense was through the roof.

## 💠 [notion: Lessons learned from sharding Postgres at Notion _202110](https://www.notion.so/blog/sharding-postgres-at-notion)

- [从 Notion 分片 Postgres 中吸取的教训(Notion 工程团队) - 为少 - 博客园_202110](https://www.cnblogs.com/hacker-linner/p/16243380.html)

## 🔥🔥 [retool: How we upgraded our 4TB Postgres database | Hacker News_202204](https://news.ycombinator.com/item?id=31084147)

- 
- 
- 

## 📝 [Scaling the GitLab database | GitLab_201710](https://about.gitlab.com/blog/2017/10/02/scaling-the-gitlab-database/)

- 
- 

## 👥🔥 [Scaling the GitLab database | Hacker News_201710](https://news.ycombinator.com/item?id=15586488)

- 
- 
- 

# blogs-pg-powered

## 🔥 [Building a distributed time-series database on PostgreSQL | Hacker News_201908](https://news.ycombinator.com/item?id=20760324)

- [Building a distributed time-series database on PostgreSQL](https://www.timescale.com/blog/building-a-distributed-time-series-database-on-postgresql/)

- 
- 
- 

# more
