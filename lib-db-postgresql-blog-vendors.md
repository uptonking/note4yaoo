---
title: lib-db-postgresql-blog-vendors
tags: [blog, postgresql, vendors]
created: 2023-10-26T18:11:46.163Z
modified: 2023-10-26T18:14:17.038Z
---

# lib-db-postgresql-blog-vendors

# guide

# blogs

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

## 📝 [notion: Herding elephants: Lessons learned from sharding Postgres at Notion_202110](https://www.notion.so/blog/sharding-postgres-at-notion)

## [从 Notion 分片 Postgres 中吸取的教训(Notion 工程团队) - 为少 - 博客园_202110](https://www.cnblogs.com/hacker-linner/p/16243380.html)

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
