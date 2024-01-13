---
title: lib-db-duckdb-examples
tags: [duckdb, examples]
created: 2022-12-24T06:46:08.417Z
modified: 2023-12-15T18:02:24.488Z
---

# lib-db-duckdb-examples

# guide

- ref
  - [DuckDB WASM Playground](https://sekuel.com/playground/)
    - Run SQL queries directly in your desktop or mobile browser.
# popular
- https://github.com/uwdata/mosaic /413Star/BSD/202311/js
  - https://uwdata.github.io/mosaic/
  - An Extensible Framework for Linking Databases and Interactive Views
  - Visualize, select, and filter datasets with millions or billions of records.
  - Mosaic pushes computation to DuckDB, both server-side and in your browser via WebAssembly.
  - Build data-driven web apps, or interact with data directly in Jupyter notebooks.
  - The key idea is to have interface components "publish" their data needs as declarative queries that can be managed, optimized, and cross-filtered by a coordinator that proxies access to DuckDB.

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

- https://github.com/duckdb/duckdb-wasm /cpp/rust/ts
  - https://shell.duckdb.org/
  - DuckDB-Wasm brings DuckDB to every browser thanks to WebAssembly.
  - Duckdb-Wasm speaks Arrow fluently, reads Parquet, CSV and JSON files backed by Filesystem APIs or HTTP requests

- https://github.com/cwida/ivm-extension /MIT/202309/cpp
  - Incremental View Maintenance support for DuckDB
# examples

# utils

# more
