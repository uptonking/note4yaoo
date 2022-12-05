---
title: toc-db-utils
tags: [db, toc, utils]
created: 2022-11-06T11:21:17.190Z
modified: 2022-11-06T11:21:27.612Z
---

# toc-db-utils

# guide

# rest
- https://github.com/PostgREST/postgrest /haskell
  - PostgREST serves a fully RESTful API from any existing PostgreSQL database. 
  - It provides a cleaner, more standards-compliant, faster API than you are likely to write from scratch.
# apps
- https://github.com/multiprocessio/datastation /ts/go
  - DataStation is an open-source data IDE for developers. 
  - It allows you to easily build graphs and tables with data pulled from SQL databases
  - Write embedded scripts as needed in languages like Python, JavaScript, R or SQL. All in one application.

- tad /2.5kStar/MIT/202212/ts/duckdb/SlickGrid
  - https://github.com/antonycourtney/tad
  - Tad desktop application enables you to quickly view and explore tabular data in several of the most popular tabular data file formats: CSV, Parquet, and SQLite and DuckDb database files. 
  - 依赖aggtree、reltab
  - Internally, the application is powered by an in-memory instance of `DuckDb`, a fast, embeddable database engine optimized for analytic queries.
  - The core of Tad is a React UI component that implements a hierarchical pivot table that allows you to specify a combination of pivot, filter, aggregate, sort, column selection
  - Tad uses `SlickGrid` for rendering the data grid. 
  - Tad was initially released in 2017 as a standalone desktop application for viewing and exploring CSV files.
  - reltab
    - The core abstraction used in Tad for programmatically constructing and executing relational SQL queries.
    - This also defines the driver interface implemented by specific database back-ends, and a small, transport-agnostic remoting layer to allow queries and results to be transmitted between a web browser (or electron renderer process) and a reltab backend server.
# utils
- https://github.com/w3tecch/typeorm-seeding
  - A delightful way to seed test data into your database.
  - Inspired by the awesome framework laravel in PHP and of the repositories from pleerock
# db-cache
- https://github.com/CyCraft/magnetar
  - Magnetar is a state management library.
  - A library that brings a simple syntax for reading and writing data and allows you to easily work with this data in your app like a global store.
  - A framework-agnostic syncing solution that auto-connects any DB/API with your local data store and has optimistic-UI built in
  - Magnetar has 2-way sync database integration for Google Firestore (and others coming). You do not need to learn to work with the database SDK.
# db-client
- https://github.com/mlaanderson/database-js
  - Database-js implements a common, promise-based interface for SQL database access. 
  - Inspired by JDBC, it uses connection strings to identify the database driver. 

- https://github.com/slashbaseide/slashbase /ts/go
  - Collaborative in-browser database IDE for your team. 
  - Supports PostgreSQL & MongoDB.

 - https://github.com/dbeaver/cloudbeaver
   - CloudBeaver is a web server which provides rich web interface. 
   - Server itself is a Java application, web part is written on TypeScript and React.
 # more

- https://github.com/mlaanderson/database-js
  - Database-js implements a common, promise-based interface for SQL database access. 
  - Inspired by JDBC, it uses connection strings to identify the database driver.

- https://github.com/prsn/redux-persist-sqlite-storage
  - A redux-persist store adaptor that uses SQLite to persist store
