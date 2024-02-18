---
title: lib-db-mysql-blog-vendors
tags: [blog, mysql, vendors]
created: 2023-10-26T18:16:21.775Z
modified: 2023-10-26T18:16:35.523Z
---

# lib-db-mysql-blog-vendors

# guide

# blogs

# blogs-github

## [Upgrading GitHub.com to MySQL 8.0 - The GitHub Blog_202312](https://github.blog/2023-12-07-upgrading-github-com-to-mysql-8-0/)

- GitHub分享了他们将自己1200+节点、300+TB数据存储的MySQL机群从5.7升级至8.0的故事
# blogs-facebook

## [Migrating Facebook to MySQL 8.0 | Hacker News_202107](https://news.ycombinator.com/item?id=27922097)

# blogs-uber

## [How Uber Serves Over 40 Million Reads Per Second from Online Storage Using an Integrated Cache | Uber Blog _202402](https://www.uber.com/blog/how-uber-serves-over-40-million-reads-per-second-using-an-integrated-cache/)

- Docstore is mainly divided into three layers: a stateless query engine layer, a stateful storage engine layer, and a control plane. 
  - For the scope of this blog, we will talk about its query and storage engine layers. 
- The stateless query engine layer is responsible for query planning, routing, sharding, schema management, node health monitoring, request parsing, validation, and AuthN/AuthZ. 
- The storage engine layer is responsible for consensus via Raft, replication, transactions, concurrency control, and load management. 
  - A partition is typically composed of MySQL nodes backed by NVMe SSDs, which are capable of handling heavy read and write workloads. 
  - Additionally, data is sharded across multiple partitions containing one leader and two follower nodes using Raft for consensus.
- At Uber we provide Redis™ as a distributed caching solution. 
- A typical design pattern for microservices is to write to database and cache while serving reads from the cache for improved latencies.
- We decided to build an integrated caching solution, CacheFront for Docstore, with following goals in mind:
  - Minimize the need for vertical and/or horizontal scaling to support low-latency read requests
  - Replace most of the custom-built caching solutions that were (or will be) built by the individual teams 

### 👥 [Uber does 40 million reads a second on tens of PB of data.](https://twitter.com/isamlambert/status/1758909084731142314)

- MySQL! We’re doing 400-500k per second on it.
- Interesting how similar this pattern is to DynamoDB

- All this text to tell me that they used a redis cache
- its literally redis - 40 million reads a second from a cache isn't a big deal. It's not 40 million transactions.

- Only 40 mil per second? Not a lot tbh. One Postgres machine with 8 cores easy up to 300k per sec so it’s just 100-200 servers or even less like 10-20 high cpu/io
# more
