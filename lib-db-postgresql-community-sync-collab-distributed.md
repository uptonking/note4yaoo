---
title: lib-db-postgresql-community-sync-collab-distributed
tags: [collaboration, community, distributed, postgresql, synchronization]
created: 2023-10-28T17:52:29.661Z
modified: 2023-10-28T17:52:51.915Z
---

# lib-db-postgresql-community-sync-collab-distributed

# guide

# discuss-stars
- ## 

- ## 

- ## For CDC users, one of the most exciting features in #Postgres version 16 is the support for logical replication from stand-by servers (a.k.a. read replicas). 
- https://twitter.com/gunnarmorling/status/1737158441611796623
- I remember having to watch replication lag like a hawk to make sure prod disk never blew up. We're huge postgres fans at work, and having the option to CDC from a replica only opens possibilities for our customers to safely move those tuples to an analytic store.
  - Yeah, alluding to that in the post too. You still can run into WAL growth issues also when using logical replication from a stand-by, if you have hot standby feedback on. Which you should, as otherwise the slot may become invalid after schema changes.
  - As of Postgres 13, you can limit the maximum WAL size to keep (only that you then may have to recreate replication slots if they fall too much behind, similar to how things work with binlog clients for MySQL).

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🔥 [Citus 6.1 Released – Horizontally scale your Postgres database | Hacker News_201702](https://news.ycombinator.com/item?id=13662166)
- 
- 
- 

- ## 🔥 [PgSync: Sync Postgres data between databases | Hacker News_202003](https://news.ycombinator.com/item?id=22676112)
- 
- 
- 
