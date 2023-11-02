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
