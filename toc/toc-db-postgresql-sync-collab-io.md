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
# utils
- https://github.com/krylosov-aa/pg-status /MIT/202605/c
  - lightweight and fast microservice (sidecar) that helps instantly determine the status of your PostgreSQL hosts including whether they are alive, which one is the master, which ones are replicas, and how far each replica is lagging behind the master.
  - [pg-status 2.1.0 — HTTP discovery for PostgreSQL streaming replication, now with read-your-writes : r/PostgreSQL _202605](https://www.reddit.com/r/PostgreSQL/comments/1thok27/pgstatus_210_http_discovery_for_postgresql/)
    - a tiny C microservice that polls your PostgreSQL hosts and exposes their status over HTTP — answers questions like "who's the primary?", "which replica is lagging less than 100 ms?", "which replica has already replayed this specific LSN?".
    - TL;DR — what it is: a sidecar that lives next to your app, polls a static list of PG hosts in the background, and answers HTTP requests in sub-millisecond time. It is not a SQL proxy — your app still connects to Postgres directly, pg-status just tells it which host.
  - Maybe I don’t get it but what’s the difference compare to Patroni with consul?
    - In the case of patroni, the difference is really small. But there are other tools that provide a failover mechanism but do not provide good discover mechanism. And even in the case of patroni, there seems to be no ready-made mechanism for obtaining a host by min lsn.
  - LSN: Log Sequence Number.
    - In PostgreSQL, it is a position marker in the WAL (Write-Ahead Log). You can think of it as a unique “offset” or “bookmark” that identifies a specific point in the database’s change stream.
    - LSN is a specific coordinate or "timestamp" in the database's internal transaction log. It acts as a unique, ever-increasing ID for every single change made to the database.
# async
- https://github.com/microsoft/pg_durable /1.2kStar/PGLic/202606/rust
  - Durable Execution inside PostgreSQL
# more
