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

# changes
- https://github.com/BemiHQ/bemi /SSPL/202403/ts
  - https://bemi.io/
  - Bemi automatically tracks database changes ensuring 100% reliability and a comprehensive understanding of every change. 
  - It does it by connecting PostgreSQL's Write-Ahead Log (WAL) and implementing Change Data Capture (CDC) data pattern. 
  - Designed with simplicity and non-invasiveness in mind, Bemi operates in the background and doesn't require any alterations to your existing database tables
  - Time travel querying and ability to easily filter changes
  - Optional application-specific context by using ORM packages
  - Bemi consists of three main parts:
    - Debezium, a very flexible tool for implementing Change Data Capture that is written in Java
    - NATS JetStream, a cloud-native messaging system written in Go.
    - Bemi Worker, a process responsible for stitching data change with app context sent via our open-source ORM packages and storing data changes. 
  - https://github.com/BemiHQ/bemi-typeorm
  - https://github.com/BemiHQ/bemi-prisma
  - https://github.com/BemiHQ/bemi-prisma-example

- https://github.com/Horusiath/pgrdt /apache2/202103/rust/inactive
  - Postgres extension for conflict-free distributed programming utilities written in Rust
# etl/import/export
- https://github.com/dimitri/pgcopydb /c
  - a tool that automates running `pg_dump | pg_restore` between two running Postgres servers. 
  - To make a copy of a database to another server as quickly as possible, one would like to use the parallel options of `pg_dump` and still be able to stream the data to as many `pg_restore` jobs.
# more
