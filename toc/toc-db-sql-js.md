---
title: toc-db-sql-js
tags: [database, js, sql, toc]
created: 2021-08-30T18:23:08.738Z
modified: 2021-08-30T18:56:14.863Z
---

# toc-db-sql-js

# guide

- http://sqlfiddle.com/
# query-builder
- knex /18.5kStar/MIT/202401/js
  - https://github.com/knex/knex
  - http://knexjs.org/
  - A query builder for MSSQL, MySQL, PostgreSQL, SQLite3, Oracle
  - 依赖commander、tarn
  - feathers.v5抽象出schema+resolver，通过knex+mongoose支持rdbms和nosql
  - knex-based orm: mikro-orm, bookshelf, objection.js

- https://github.com/kysely-org/kysely /8.9kStar/MIT/202403/ts
  - https://kysely.dev/
  - a type-safe and autocompletion-friendly typescript SQL query builder. 
  - Inspired by knex. 

- https://github.com/juanluispaz/ts-sql-query /259Star/MIT/202403/ts
  - Type-safe SQL query builder like QueryDSL or JOOQ in Java or Linq 
  - provides a way to build dynamic SQL queries in a type-safe way

- https://github.com/terkelg/sqliterally
  - Lightweight SQL query builder

- https://github.com/ukrbublik/react-awesome-query-builder
  - https://ukrbublik.github.io/react-awesome-query-builder/
  - User-friendly React component to build queries (filters).
  - 工具条设计很经典，and/or/not在上层

- https://github.com/vlcn-io/typed-sql /rust
  - Generates types for your SQL.
  - https://github.com/tantaman/TreeSQL
    - This is just a prototype of an alternate SQL syntax to pull hierarchies.
    - it compiles to plain SQL.
# db-sql-tools
- [SQL Workbench - Rapid prototyping SQL Queries & Data Visualizations](https://sql-workbench.com/)

- https://github.com/sqlpad/sqlpad
  - A web app for writing and running SQL queries and visualizing the results. 
  - Supports Postgres, MySQL, SQL Server, ClickHouse, Crate, Vertica, Trino, Presto, SAP HANA, Cassandra, Snowflake, Google BigQuery, SQLite

- https://github.com/sqlectron/sqlectron-gui /MIT/202202/ts/inactive
  - https://sqlectron.github.io/
  - lightweight SQL client desktop with cross database and platform support.

- https://github.com/dblens/app /202202/ts
  - database client that helps you to explore database with automatic ER diagrams, visualise and analyse internal DB metrics such as index utilisation sequential scans, slow running queries, storage and many more.

- https://github.com/EdurtIO/dbm /309Star/apache2/202209/ts
  - https://dbm.edurt.io/
  - Full platform database management tool, supports ClickHouse, Presto, Trino, MySQL, PostgreSQL, Apache Druid, ElasticSearch...
  - 依赖angular、jsstore
  - DBM can query data from any SQL-speaking datastore or data engine (ClickHouse and more).

- https://github.com/slashbaseide/slashbase /ts/go
  - Slashbase is an open-source minimal collaborative IDE for your databases in browser.
  - It's written in Golang and Nextjs React Framework and runs as a single binary.
  - Connect to your database, browse data, run a bunch of queries or share queries within your team, right from your browser. 
  - Works with two types of databases: PostgreSQL and MongoDB.

- https://github.com/tobymao/sqlglot
  - Python SQL Parser and Transpiler

- https://github.com/mWater/jsonql
  - SQL represented in an unambiguous way in JSON.
  - Safely convertible to SQL on server with no injection attacks
  - Everything is a json object: `{ type: type of object, ... }`.

- https://github.com/withtyped/withtyped
  - Type-safe RESTful framework for fullstack with all native implementation
  - Write native SQL-in-TS and get 4 tailored dev engines with no time

- https://github.com/datawan-labs/pg /MIT/202404/ts
  - https://pg.datawan.id/
  - In Browser PostgreSQL Playground, no server, just client and pglite (postgresql wasm)
# examples
- https://github.com/prostgles/ui
  - https://prostgles.com/ui
  - Web dashboard and SQL Editor for Postgres
  - Sorting, Filtering and Cross-Filtering joined tables
# sql-alternatives
- https://github.com/PRQL/prql /rust
  - https://prql-lang.org/
  - PRQL is a modern language for transforming data — a simple, powerful, pipelined SQL replacement
  - Like SQL, it's readable, explicit and declarative. 
  - Unlike SQL, it forms a logical pipeline of transformations, and supports abstractions such as variables and functions. 
  - 👉🏻 It can be used with any database that uses SQL, since it **compiles to SQL**.
  - PRQL's goals are fairly similar to @morel_lang , and the syntax looks similar in most cases.
  - [PRQL: Pipelined Relational Query Language | Hacker News](https://news.ycombinator.com/item?id=36866861)
# sql-extensions-mdx

# compiles-to-sql

- https://github.com/malloydata/malloy /ts/lookerBI
  - https://www.malloydata.dev/
  - Malloy is an experimental language for describing data relationships and transformations.
  - It is both a semantic modeling language and a querying language that runs queries against a relational database. 
  - Malloy currently supports BigQuery and Postgres, as well as querying Parquet and CSV files via DuckDB.
  - every Malloy query turns into a single SQL query
  - [A sequel to SQL? An intro to Malloy | Hacker News](https://news.ycombinator.com/item?id=32738874)
# sql-utils
- https://github.com/fibo/SQL92-JSON
  - can stringify a JSON into an SQL and viceversa parse an SQL and serialize it into a JSON

- https://github.com/goodybag/mongo-sql /201811/js
  - extensible SQL generation library for JavaScript with a focus on introspectibility
  - writing your SQL as JSON

- https://github.com/planetarydev/json-sql-builder2 /202108/js
  - When you need to write dynamic queries defined by the user, it is much easier to use JSON instead of generating a string-based query.
- https://github.com/2do2go/json-sql /202011/js
  - Node.js library for mapping mongo-style query objects to SQL queries.
  - it is only translator, you should use specific driver for your db

- https://github.com/turbot/steampipe /go
  - https://steampipe.io/
  - Use SQL to instantly query your cloud services (AWS, Azure, GCP and more). Open source CLI. 
  - No DB required.
  - Use SQL to instantly query your cloud services (AWS, Azure, GCP and more). Open source CLI. No DB required.

- https://github.com/atheck/db-sql-toolkit /202311/ts
  - Helps with SQL statements, database migration, and bulk execution
  - `sql` function is a tagged template function to write SQL statements and include parameters in the correct places.
# sql-parser
- https://github.com/DTStack/dt-sql-parser /ts
  - SQL Parsers for BigData, built with antlr4.
  - We have provided a monaco-sql-languages package, you can integrate with monaco-editor easily.
# more
- https://github.com/webqit/objective-sql /202201/js
  - Objective SQL is a query client that wraps powerful concepts in a simple, succint API.
  - The object-oriented, adaptive SQL for modern apps - query anything from the plain JSON object, to the client-side IndexedDB, to the server-side DB.

- https://github.com/ForbesLindesay/atdatabases
  - TypeScript clients for databases that prevent SQL Injection
  - Using tagged template literals for queries makes it virtually impossible for SQL Injection attacks to slip in un-noticed.
  - All the @databases libraries enforce the use of the sql tagged template literals, so you can't accidentally miss them.
