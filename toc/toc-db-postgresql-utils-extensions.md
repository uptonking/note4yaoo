---
title: toc-db-postgresql-utils-extensions
tags: [extensions, postgresql, toc, utils]
created: 2023-10-26T15:29:07.458Z
modified: 2023-10-26T15:29:40.053Z
---

# toc-db-postgresql-utils-extensions

# guide

# popular
- https://github.com/PeerDB-io/peerdb /rust/go
  - a Postgres-first data-movement platform that makes moving data in and out of Postgres fast and simple. 

- https://github.com/michaelpq/pg_plugins/tree/main/blackhole_am /c
  - This module is a PostgreSQL extension template

- https://github.com/pgxman/pgxman /202311/go
  - https://pgxman.com/
  - pgxman is npm for Postgres extensions. 

- https://github.com/pgq/pgq /sql/c
  - Generic Queue for PostgreSQL
  - PostgreSQL extension that provides generic, high-performance lockless queue with simple API based on SQL functions.
# plugins

# utils
- https://github.com/pgcentralfoundation/pgrx /202310/rust
  - a framework for developing PostgreSQL extensions in Rust and strives to be as idiomatic and safe as possible.
  - supports Postgres v11-v15
  - [PGX: Write Postgres extensions in Rust instead of C | Hacker News_202007](https://news.ycombinator.com/item?id=23821112)

- https://github.com/tcdi/plrust 
  - a loadable procedural language that enables writing PostgreSQL functions in the Rust programming language. 
  - These functions are compiled to native machine code. Unlike other procedural languages, PL/Rust functions are not interpreted.

- https://github.com/sastraxi/pgsh /js
  - Branch your PostgreSQL Database like Git
  - pgsh provides a slightly-more-user-friendly interface to knex's migration system.

- https://github.com/zknill/sqledge /202308/go
  - SQLedge uses Postgres logical replication to stream the changes in a source Postgres database to a SQLite database that can run on the edge. 
  - [SQLedge: Replicate Postgres to SQLite on the Edge | Hacker News_202308](https://news.ycombinator.com/item?id=37063238)
# search
- https://github.com/paradedb/paradedb /AGPLv3/rust
  - https://paradedb.com/
  - an ElasticSearch alternative built on PostgreSQL, engineered for lightning-fast full text, similarity, and hybrid search.
# query
- https://github.com/tozd/node-reactive-postgres /202204/js/inactive
  - brings reactive (or live) queries to PostgreSQL.
  - I have made something similar trying to match more the concept of a materialized view, but just on the client instead of inside the database
  - You can take an arbitrary SELECT query, using multiple joins, data transformations, and even custom functions, and besides the initial set of results also get real-time updates about any changes to those results. 
  - For every reactive query, a `TEMPORARY TABLE` is created in the database which serves as cache for query results.
  - Triggers are added to all query sources for the query, so that when any of sources change, this package is notified using LISTEN/NOTIFY that a source has changed
  - Because this package uses temporary tables, consider increasing `temp_buffers` PostgreSQL configuration so that there is more space for temporary tables in memory.

- https://github.com/aarroyoc/postgresql-prolog /202310/prolog
  - A Prolog library to connect to PostgreSQL databases
  - [PostgreSQL-Prolog: A Prolog library to connect to PostgreSQL databases | Hacker News_202109](https://news.ycombinator.com/item?id=28660202)
# json/mongo
- https://github.com/fcoury/oxide /apache2/202210/rust
  - OxideDB is a translation layer that works as a MongoDB database server while using PostgreSQL's JSON capabilities as the underlying data store.
  - if your use-case leverages MongoDB as a distributed database, then unfortunately this project might not be for you. At least right now supporting multi-sharding and scale-out deployments is not part of the roadmap.
  - heavily inspired by FerretDB. The main difference is that there is no intention to support any database other than PostgreSQL (FerretDB is also supporting Tigris) and it's written in Rust, as opposed to Go.
# devops
- https://github.com/Vonng/pigsty /202312/python/plpgsql
  - https://pigsty.cc/
  - A battery-included, local-first, open-source PostgreSQL RDS alternative.
  - 开箱即用的RDS：从内核到RDS发行版，在 EL7-9 下提供 12-16 版本的生产级 PostgreSQL 数据库服务
  - 深度整合 150+ 核心扩展，提供开箱即用的分布式的时序地理空间图文向量数据库能力。
  - PostgreSQL 是一个足够完美的数据库内核，但它需要更多工具与系统的配合才能成为一个足够好的数据库服务（RDS），而 Pigsty 帮助 PostgreSQL 完成这一步飞跃
  - Pigsty 支持的数据库版本覆盖 PostgreSQL 12 ～ 16，可以运行于 EL/Debian/Ubuntu 以及兼容操作系统发行版中。 除了数据库内核与大量开箱即用的扩展插件以外，Pigsty更是提供了数据库服务所需的完整运行时基础设施，与本地沙箱/生产环境/IaaS全自动部署方案。
  - Pigsty 提供了 Docker 模块与大量开箱即用的 Compose 模板。您可以使用 Pigsty 管理的高可用 PostgreSQL （以及 Redis 与 MinIO ）作为后端存储，以无状态的模式一键拉起这些软件： Gitlab、Gitea、Wiki.js、NocoDB、Odoo、Jira、Confluence、Habour、Mastodon、Discourse、KeyCloak 等等。
# more
