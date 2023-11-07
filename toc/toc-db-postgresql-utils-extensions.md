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
# more
