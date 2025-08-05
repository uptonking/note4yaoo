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
  - Projects using pgwire: greptimedb, sqld, risinglight, peerdb

- https://github.com/electric-sql/pglite /apache2/202402/ts
  - PGlite is a WASM Postgres build packaged into a TypeScript client library that enables you to run Postgres in the browser, Node.js and Bun, with no need to install any other dependencies.
  - It is only 3.7mb gzipped.
  - It can be used both as an ephemeral in-memory database or with persistance to the file system (Node/Bun) or indexedDB (Browser).
  - Unlike previous "Postgres in the browser" projects, PGlite does not use a Linux virtual machine - it is simply Postgres in WASM.
  - It is being developed at ElectricSQL in collaboration with Neon. 
  - 🚧 Parameterized queries are not currently supported, but this will be added soon.

- https://github.com/centerofci/mathesar /GPLv3/python/svelte
  - https://mathesar.org/
  - open source tool that provides a spreadsheet-like interface to a PostgreSQL database.
  - You can use Mathesar to build data models, enter data, and even build reports.
  - [Show HN: Mathesar – open-source collaborative UI for Postgres databases | Hacker News_202303](https://news.ycombinator.com/item?id=34999774)

- https://github.com/gajus/slonik /BSD/202403/ts
  - A Node.js PostgreSQL client with runtime and build time type safety, and composable SQL
  - A battle-tested Node.js PostgreSQL client with strict types, detailed logging and assertions.
# pg-viewer

# powered-by-pg

- https://github.com/cloudberrydb/cloudberrydb /apache2/202409/c
  - https://cloudberrydb.org/
  - Open source alternative to Greenplum Database. Created by the original Greenplum developers.
  - We aim to bring modern computing capabilities to the traditional distributed MPP database to support Analytics and AI/ML workloads in one platform.
  - As a derivative of Greenplum Database 7, Cloudberry Database is compatible with Greenplum Database, but it's shipped with a newer PostgreSQL 14.4 kernel (scheduled kernel upgrade yearly) and a bunch of features Greenplum Database lacks or does not support. 

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
  - 🆚️ [PlanetScale vs. Neon: the Continued Saga between MySQL and PostgreSQL](https://www.bytebase.com/blog/planetscale-vs-neon/)
    - PlanetScale: The shared-nothing architecture grants near-linear scalability up to 1 million QPS. 
    - Neon is a shared-storage architecture. It separates the compute and storage. The compute part is just normal PostgreSQL server, the storage part is a custom-built multi-tenant storage system shared by all Postgres compute nodes.
    - Neon can not scale as much as PlanetScale. After all, it's a single-node PostgreSQL instance. Neon separates the storage and compute, thus each can scale individually.

- https://github.com/aquametalabs/aquameta /1.1kStar/GPLv3/202401/go
  - Web development platform built entirely in PostgreSQL
  - Aquameta is organized into seven PostgreSQL extensions, that each corresponds to a layer or tool in a typical web stack. 
  - The database schema contains ~60 tables, ~50 views and ~90 stored procedures that together make a minimalist, fairly unopinionated web stack that should be familiar to most web developers, except that it's all in the database
  - A thin Golang daemon handles the connection to the database and runs a web server.

- https://github.com/omnigres/omnigres /apache2/202401/c
  - https://docs.omnigres.org/
  - Omnigres makes Postgres a developer-first application platform. 
  - Running application logic inside or next to the database instance

- https://github.com/tembo-io/tembo /1.1kStar/pgLic/202412/rust
  - https://tembo.io/
  - Tembo aims to improve the experience developers have with deploying, managing, and scaling Postgres
  - Tembo Stacks - workload-configured Postgres deployable to Kubernetes
  - Tembo Self Hosted is a self-hosted version of the Tembo Platform that runs in your own Kubernetes cluster.
# pg-rewrite
- pg-mem /1.6kStar/MIT/202310/ts
  - https://github.com/oguimbal/pg-mem
  - https://oguimbal.github.io/pg-mem-playground/
  - An in memory postgres DB instance for your unit tests
  - It works both in Node or in the browser.
  - 依赖immutable.v4、functional-red-black-tree、json-stable-stringify、lru-cache、moment、pgsql-ast-parser、@mikro-orm/core~pg
  - adapter支持pg-native, node-postgres, knex, typeorm
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

- https://github.com/divyenduz/fakegres /202402/go
  - Toy distributed PostgreSQL backed by SQLite
  - Based on https://notes.eatonphil.com/distributed-postgres.html
  - https://twitter.com/divyenduz/status/1759917106743693580
    - Basically 95% the same as @eatonphil 's post, just SQLite used as KV in favor of bolt.
    - Would be interesting to see something like "not parsing the SQL queries but passing them through to SQLite data stores" in the future.

## pg-like

# pg-ha/vitess
- https://github.com/multigres/multigres /1.1kStar/apache2/202508
  - https://multigres.com/
  - Multigres is a project to build an adaptation of Vitess for Postgres.
  - [How will Multigres be different from PlaneScale Vitess for Postgres _202507](https://github.com/multigres/multigres/discussions/23)
    - Recently PlanetScale announced that they are gonna support Postgres. they mentioned that they will not use Vitess but rather build a new system from scratch (in the blog post also calling it "Vitess for Postgres").
    - 👷: It's hard to infer much from that statement. All I can say is that Multigres is 100% open source and we'll be building it in public.
  - [External contributions _202506](https://github.com/multigres/multigres/discussions/6)
    - The initial phase of this project involves bulk-importing code from Vitess. This work requires intimate knowledge of Vitess, knowing what is generic vs what is MySQL specific.
    - During this phase, we will not be accepting external contributions.
  - [Announcing Multigres: Vitess for Postgres _202506](https://supabase.com/blog/multigres-vitess-for-postgres)
    - Vitess is a database clustering system for scaling MySQL: Sharding, Connection pooling,Query routing, Resiliency and failover, Cloud-native orchestration (Kubernetes)
    - Multigres is a new proxy that sits in front of your Postgres database. It shares the same goals as Vitess but it will be focused on the Postgres ecosystem. 
    - Like Vitess, Multigres will be open source using the same license: Apache 2. 

- https://github.com/wesql/wescale /apache2/202401/go
  - a database proxy that cares about your application, the development experience, and supports OnlineDDL.
  - fork自vitess的，但改造了它的架构，并且为它支持了读写分离、Read After Write Consistency、透明Failover等功能
# more
