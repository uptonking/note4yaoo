---
title: toc-db-postgresql-utils-extensions
tags: [extensions, postgresql, toc, utils]
created: 2023-10-26T15:29:07.458Z
modified: 2023-10-26T15:29:40.053Z
---

# toc-db-postgresql-utils-extensions

# guide

- extensions-list
  - [1000+ PostgreSQL EXTENSIONs](https://gist.github.com/joelonsql/e5aa27f8cc9bd22b8999b7de8aee9d47)
# popular
- https://github.com/brianc/node-postgres /MIT/202402/js
  - https://node-postgres.com/
  - Non-blocking PostgreSQL client for Node.js. 
  - Pure JavaScript and optional native libpq bindings.
  - This repo is a monorepo which contains the core pg module as well as related modules like pg-pool/cursor/protocol
  - [Support for multiple hosts](https://github.com/brianc/node-postgres/issues/1470)
    - we had to switch to this lib porsager/postgres#multi-host-connections---high-availability-ha, and can confirm it works and also support pretty much all functionalities. 

- https://github.com/michaelpq/pg_plugins/tree/main/blackhole_am /c
  - This module is a PostgreSQL extension template

- https://github.com/supabase/dbdev /apache2/202401/ts/rust
  - https://database.dev/
  - a package manager for Postgres trusted language extensions (TLE).

- https://github.com/tembo-io/trunk /202312/rust
  - https://pgt.dev/
  - open source package manager and registry for PostgreSQL (Postgres) extensions
  - Use the Trunk CLI (pg-trunk) to build, publish and install Postgres extensions of all kinds.

- https://github.com/pgxman/pgxman /202311/go
  - https://pgxman.com/
  - pgxman is npm for Postgres extensions. 

- https://github.com/graphile/worker /MIT/202312/ts
  - http://worker.graphile.org/
  - High performance Node.js/PostgreSQL job queue 
  - allows you to run jobs (e.g. sending emails, performing calculations, generating PDFs, etc) "in the background" so that your HTTP response/application code is not held up. 
  - Can be used with any PostgreSQL-backed application. Pairs beautifully with PostGraphile or PostgREST.

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

  - https://github.com/sastraxi/pgsh /MIT/202203/js/inactive
  - Branch your PostgreSQL Database like Git
  - pgsh provides a slightly-more-user-friendly interface to knex's migration system.
  - As your database schema evolves, you quickly realise the challenge of keeping the structure (and triggers, stored procedures, seed data...) of the database in sync with your codebase. 
  - You may have even witnessed the horror of inconsistent db builds due to "repeatable migrations". Instead, treat the database as a code repository itself: clone and switch between branches just like you do in git.

- https://github.com/zknill/sqledge /202308/go
  - SQLedge uses Postgres logical replication to stream the changes in a source Postgres database to a SQLite database that can run on the edge. 
  - [SQLedge: Replicate Postgres to SQLite on the Edge | Hacker News_202308](https://news.ycombinator.com/item?id=37063238)

- https://github.com/ChenHuajun/pg_roaringbitmap /apache2/202310/c
  - Roaringbitmap是一种高效的Bitmap压缩算法，目前已被广泛应用在各种语言和各种大数据平台上。
  - 本插件将Roaringbitmap功能集成到Greenplum数据库中，将Roaringbitmap作为一种数据类型提供原生的数据库函数、操作符、聚合等功能支持。
  - Bitmap位计算非常适合大数据基数计算，常用于去重、标签筛选、时间序列等计算中。

- https://github.com/orioledb/orioledb /PGLic/202401/c
  - a new storage engine for PostgreSQL, bringing a modern approach to database capacity, capabilities and performance to pg
  - OrioleDB consists of an extension, building on the innovative table access method framework and other standard Postgres extension interfaces.
  - OrioleDB implements the concepts of undo log and page-mergins, eliminating the need for dedicated garbage collection processes.
  - Designed to be distributed. OrioleDB implements a row-level write-ahead log with support for parallel apply. This log architecture is optimized for raft consensus-based replication allowing the implementation of active-active multimaster.

- https://github.com/sraoss/pg_ivm /202309/c
  - IVM (Incremental View Maintenance) implementation as a PostgreSQL extension
  - pg_ivm provides a kind of immediate maintenance, in which materialized views are updated immediately in AFTER triggers when a base table is modified.
  - [Status of IVM within Postgres · sraoss/pg_ivm](https://github.com/sraoss/pg_ivm/issues/57)
    - 202306: We hope this patch would be accepted in PostgreSQL 17 even in a limited form. In order to make this progress, we need more discussion in the community.
  - https://github.com/sraoss/pgsql-ivm

- https://github.com/djrobstep/migra /202209/python
  - https://databaseci.com/docs/migra
  - a schema diff tool for PostgreSQL, written in Python. 
  - Use it in your python scripts, or from the command line
# search
- https://github.com/paradedb/paradedb /AGPLv3/202402/rust/c
  - https://paradedb.com/
  - an ElasticSearch alternative built on PostgreSQL, engineered for lightning-fast full text, similarity, and hybrid search.

- https://github.com/amutu/zhparser /PostgreSQLLic(MIT)/202401/c
  - a PostgreSQL extension for full-text search of Chinese language
  - It implements a Chinese language parser base on the Simple Chinese Word Segmentation(SCWS).

- https://github.com/toluaina/pgsync /202312/python
  - https://pgsync.com/
  - a middleware for syncing data from Postgres to Elasticsearch/OpenSearch effortlessly. 
  - It allows you to keep Postgres as your source of truth and expose structured denormalized documents in Elasticsearch/OpenSearch.
  - Simply describe your document structure or schema in JSON and PGSync will continuously capture changes in your data and load it into Elasticsearch/OpenSearch without writing any code. PGSync transforms your relational data into a structured document format.
# query
- https://github.com/tozd/node-reactive-postgres /BSD/202204/js/inactive
  - brings reactive (or live) queries to PostgreSQL.
  - I have made something similar trying to match more the concept of a materialized view, but just on the client instead of inside the database
  - You can take an arbitrary SELECT query, using multiple joins, data transformations, and even custom functions, and besides the initial set of results also get real-time updates about any changes to those results. 
  - For every reactive query, a `TEMPORARY TABLE` is created in the database which serves as cache for query results.
  - Triggers are added to all query sources for the query, so that when any of sources change, this package is notified using LISTEN/NOTIFY that a source has changed
  - Because this package uses temporary tables, consider increasing `temp_buffers` PostgreSQL configuration so that there is more space for temporary tables in memory.
  - [Use ideas from Incremental View Maintenance to know what has changed_201901](https://github.com/tozd/node-reactive-postgres/issues/7)

- https://github.com/nothingisdead/pg-live-query /201608/js
  - This package makes it possible in PostgreSQL to get (almost) realtime notifications whenever the results of a query change.

- https://github.com/aarroyoc/postgresql-prolog /202310/prolog
  - A Prolog library to connect to PostgreSQL databases
  - [PostgreSQL-Prolog: A Prolog library to connect to PostgreSQL databases | Hacker News_202109](https://news.ycombinator.com/item?id=28660202)

- https://github.com/alitrack/duckdb_fdw /MIT/202312/cpp
  - a foreign data wrapper (FDW) to connect PostgreSQL to DuckDB database file
# json/mongo
- https://github.com/jadbox/mongoose-sql /201702/js
  - Mongoose compatible interface for PostgreSQL
  - uses Knex to interface with PostgreSQL

- https://github.com/fcoury/oxide /apache2/202210/rust
  - OxideDB is a translation layer that works as a MongoDB database server while using PostgreSQL's JSON capabilities as the underlying data store.
  - if your use-case leverages MongoDB as a distributed database, then unfortunately this project might not be for you. At least right now supporting multi-sharding and scale-out deployments is not part of the roadmap.
  - heavily inspired by FerretDB. The main difference is that there is no intention to support any database other than PostgreSQL (FerretDB is also supporting Tigris) and it's written in Rust, as opposed to Go.
# distributed
- https://github.com/citusdata/citus /AGPLv3/202402/c/vitess-like
  - https://www.citusdata.com/
  - Citus is a PostgreSQL extension that transforms Postgres into a distributed database
  - Distributed query engine routes and parallelizes SELECT, DML, and other operations on distributed tables across the cluster.
  - Columnar storage compresses data, speeds up scans, and supports fast projections, both on regular and distributed tables.
  - You can use these Citus superpowers to make your Postgres database scale-out ready on a single Citus node. Or you can build a large cluster 
  - You can use these Citus superpowers to make your Postgres database scale-out ready on a single Citus node. Or you can build a large cluster 
# pref
- https://github.com/le0pard/pgtune /1.9kStar/MIT/202401/js
  - https://pgtune.leopard.in.ua/
  - Tuning PostgreSQL config by your hardware. 
  - Based on original pgtune. Illustration by Kate.
  - https://github.com/gregs1104/pgtune /python/inactive
# devops
- https://github.com/Vonng/pigsty /2.2kStar/AGPLv3/202401/plpgsql
  - https://pigsty.cc/
  - A battery-included, local-first, open-source PostgreSQL RDS alternative.
  - 开箱即用的RDS：从内核到RDS发行版，在 EL7-9 下提供 12-16 版本的生产级 PostgreSQL 数据库服务
  - 深度整合 150+ 核心扩展，提供开箱即用的分布式的时序地理空间图文向量数据库能力。
  - PostgreSQL 是一个足够完美的数据库内核，但它需要更多工具与系统的配合才能成为一个足够好的数据库服务（RDS），而 Pigsty 帮助 PostgreSQL 完成这一步飞跃
  - Pigsty 支持的数据库版本覆盖 PostgreSQL 12 ～ 16，可以运行于 EL/Debian/Ubuntu 以及兼容操作系统发行版中。 除了数据库内核与大量开箱即用的扩展插件以外，Pigsty更是提供了数据库服务所需的完整运行时基础设施，与本地沙箱/生产环境/IaaS全自动部署方案。
  - Pigsty 提供了 Docker 模块与大量开箱即用的 Compose 模板。您可以使用 Pigsty 管理的高可用 PostgreSQL （以及 Redis 与 MinIO ）作为后端存储，以无状态的模式一键拉起这些软件： Gitlab、Gitea、Wiki.js、NocoDB、Odoo、Jira、Confluence、Habour、Mastodon、Discourse、KeyCloak 等等。

- https://github.com/graphile/migrate /MIT/202212/ts
  - Opinionated SQL-powered productive roll-forward migration tool for PostgreSQL.
  - roll-forward only — maintaining rollbacks is a chore, and in 10 years of API development I've never ran one in production
  - fully functional — sending SQL commands directly to PostgreSQL means you can use all of PostgreSQL's features
# more
