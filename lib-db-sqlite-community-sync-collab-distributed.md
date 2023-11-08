---
title: lib-db-sqlite-community-sync-collab-distributed
tags: [collaboration, community, distributed, sqlite, synchronization]
created: 2023-10-26T19:02:54.110Z
modified: 2023-10-26T19:03:22.063Z
---

# lib-db-sqlite-community-sync-collab-distributed

# guide

# discuss-stars
- ## 

- ## 
# discuss-sqlite-sync
- ## 

- ## 

- ## 🔥 [LiteSync – Easy synchronization of SQLite databases | Hacker News_202301](https://news.ycombinator.com/item?id=34265261)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## Has anyone built something like a distributed (write-back) page cache that sits above S3? 
- https://twitter.com/criccomini/status/1721918972604682362
  - Idea would be to reduce read latency and API calls? Similar to WarpStream’s mmap.
- Arguably libSQL and LiteFS are just that. The only gotcha is that you can only access the page cache with SQL
  - What if I want multiple simultaneous readers and writers?
- Write-back is a bit scary no, or maybe I'm missing something? I think those systems should be write-through (or read-through, with cache expiry)
  - Yes, write-back requires its own replication and stuff. But you get batching. I think you want write-back if the API is a KV store. If the API is just S3 compatible, I think write-through is fine. Main advantage for write-back would be batching (which you want in KV stores).
- Ah yes, I get what you're saying now. For a sophisticated implementation you do need the WAL-memtable-type thingy you're describing, or it'll be very expensive. Or, if you're lucky... your clients do most of their updates in big batches
- I'd be super interested if such a thing exists. We want to move our materialized view stores to S3 at @responsive_apps , but the write latency is prohibitive(贵得用不起（或买不起）的).
- Not sure it fits your need, but have a look at fsspec/s3fs. It has caching options that may help

- ## There are so many exciting local-first projects around SQLite 
- https://twitter.com/penberg/status/1719779549766934545
  - such as @ElectricSQL , CR-SQLite (by @tantaman ), SQLSync (by @carlsverre ), and @evoluhq , but I fear API fragmentation might be holding back adoption. 
  - As an application developer, which one do you pick and why?
- How do they handle authentication and authorization ? I can’t seem to find how access controls are done with local-first without a server being involved
  - If there isn’t a server involved it’s more of a “will send” and “will accept” type of model. A node will send a row to you if you pass its auth checks for the row. A node will accept a write from you if you pass it’s auth checks to write the row.

- RxDB used PouchDB under the hood for a while, but now there's a bunch of storage drivers to pick from. The problem for me seems to stem from trying to sync too much data at a time, and the sync chokes. I have a podcast app with thousands of episodes and 100+MB of data.
- Since RxDB v13 or so, the sync works in parallel in both directions for better performance. So maybe there should be a throttle when much data is synced.
  - [FIX Throttle calls to forkInstance on push-replication to not cause m…](https://github.com/pubkey/rxdb/pull/5194) 

- ## 💡🔥 [Cross-Database Queries in SQLite | Hacker News_202102](https://news.ycombinator.com/item?id=26217754)
- 
- 
- 

- ## 🔥 [mvSQLite: Turning SQLite into a Distributed Database | Hacker News_202208](https://news.ycombinator.com/item?id=32539360)
  - [Turning SQLite into a distributed database_202208](https://su3.io/posts/mvsqlite)

- 
- 
- 
