---
title: toc-db-postgresql-sync-collab-io
tags: [collaboration, postgresql, synchronization]
created: 2023-10-26T15:29:43.670Z
modified: 2023-10-26T15:30:18.297Z
---

# toc-db-postgresql-sync-collab-io

# guide

# sync
- https://github.com/PeerDB-io/peerdb /1.3kStar/Elastic/202312/rust/go/ts
  - https://peerdb.io/
  - Postgres first ETL/ELT, enabling 10x faster data movement in and out of Postgres
  - [Launch HN: PeerDB (YC S23) – Fast, Native ETL/ELT for Postgres | Hacker News_202307](https://news.ycombinator.com/item?id=36895220)
    - support multiple features including log-based (CDC) / query based streaming, efficient syncing of tables with large (TOAST) columns, configurable batching and parallelism to prevent OOMs and crashes etc
# collab

# etl/import/export
- https://github.com/dimitri/pgcopydb /c
  - a tool that automates running `pg_dump | pg_restore` between two running Postgres servers. 
  - To make a copy of a database to another server as quickly as possible, one would like to use the parallel options of `pg_dump` and still be able to stream the data to as many `pg_restore` jobs.
# more
