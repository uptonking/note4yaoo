---
title: toc-db-postgresql
tags: [postgresql, toc]
created: 2023-10-26T15:28:28.832Z
modified: 2023-10-26T15:28:53.748Z
---

# toc-db-postgresql

# guide

# popular
- https://github.com/sunng87/pgwire /MIT/rust
  - PostgreSQL wire protocol implemented as a rust library.
  - This library implements PostgreSQL Wire Protocol, and provide essential APIs to write PostgreSQL compatible servers and clients.
  - Postgres Wire Protocol is a relatively general-purpose Layer-7 protocol. 
  - note that Postgres Wire Protocol has no semantics about SQL, so literally you can use any query language, data formats or even natural language to interact with the backend.
  - The response are always encoded as data row format. And there is a field description as header of the data to describe its name, type and format.
  - Projects using pgwire: greptimedb, sqld, risinglight, peerdb, 

- https://github.com/centerofci/mathesar /GPLv3/python/svelte
  - https://mathesar.org/
  - open source tool that provides a spreadsheet-like interface to a PostgreSQL database.
  - You can use Mathesar to build data models, enter data, and even build reports.
  - [Show HN: Mathesar – open-source collaborative UI for Postgres databases | Hacker News_202303](https://news.ycombinator.com/item?id=34999774)
# pg-viewer

# powered-by-pg

- https://github.com/tensorchord/pgvecto.rs /202311/rust
  - Vector database plugin for Postgres, written in Rust, specifically designed for LLM
  - a Postgres extension that provides vector similarity search functions. 
  - It is written in Rust and based on pgrx

- https://github.com/kapilratnani/pgfire /202006/python/inactive
  - A Firebase like real time database based on Postgresql. 
  - Leverages the JSON data type and Listen/Notify constructs of postgresql.
  - Convert your postgresql database to a Realtime NoSql database accessible via REST APIs. Inspired from Firebase.

- https://github.com/neondatabase/neon /10.5kStar/apache2/202312/rust
  - https://neon.tech/
  - Neon is a serverless open-source alternative to AWS Aurora Postgres. 
  - It separates storage and compute and substitutes the PostgreSQL storage layer by redistributing data across a cluster of nodes.

- https://github.com/aquametalabs/aquameta /1.1kStar/GPLv3/202401/go
  - Web development platform built entirely in PostgreSQL
  - Aquameta is organized into seven PostgreSQL extensions, that each corresponds to a layer or tool in a typical web stack. 
  - The database schema contains ~60 tables, ~50 views and ~90 stored procedures that together make a minimalist, fairly unopinionated web stack that should be familiar to most web developers, except that it's all in the database
  - A thin Golang daemon handles the connection to the database and runs a web server.
# pg-rewrite
- pg-mem /1.6kStar/MIT/202310/ts
  - https://github.com/oguimbal/pg-mem
  - https://oguimbal.github.io/pg-mem-playground/
  - An in memory postgres DB instance for your unit tests
  - It works both in Node or in the browser.
  - 依赖immutable.v4、functional-red-black-tree、json-stable-stringify、lru-cache、moment、pgsql-ast-parser、@mikro-orm/core~pg
  - The sql syntax parser is home-made. Which means that some features are not implemented, and will be considered as invalid syntaxes.
  - limitations
    - Materialized views are implemented as views (meaning that they are always up-to-date, without needing them to refresh)
    - Indices implementations are basic
    - All number-like types are all handled as javascript numbers, meaning that types like `numeric(x,y)` could not behave as expected.
    - No support for timezones
  - https://github.com/oguimbal/pgsql-ast-parser
    - a Postgres SQL syntax parser. 基于nearley、moo实现
    - This parser does not support (yet) PL/pgSQL.

- https://github.com/chotchki/feophant /AGPLv3/202110/rust/inactive
  - A PostgreSQL inspired SQL database written in Rust.
  - We now have support for persistent storage! Not crash safe but I'm getting there!
  - Data is persisted to disk, not crash safe and the on disk format is NOT stable.
  - Connecting unauthenticated using a postgres client/driver.
  - You can create tables, insert data and query single tables.
  - [Feophant: PostgreSQL inspired SQL database written in Rust | Hacker News_202109](https://news.ycombinator.com/item?id=28512343)

- https://github.com/qnighy/featherpg /202107/rust/inactive
  - PostgreSQL-compatible on-memory DB for testing

## pg-like

# more
