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

- https://github.com/cwida/ivm-extension /MIT/202309/cpp
  - Incremental View Maintenance support for DuckDB
# examples
- https://github.com/incentius-foss/WhatTheDuck /MIT/202403/js/vue
  - https://whattheduck.incentius.com/
  - WhatTheDuck is an open-source web application built on DuckDB. 
  - It allows users to upload CSV files, store them in tables, and perform SQL queries on the data.
# utils

# duckdb-wasm

- https://github.com/duckdb/duckdb-wasm /cpp/rust/ts
  - https://shell.duckdb.org/
  - DuckDB-Wasm brings DuckDB to every browser thanks to WebAssembly.
  - Duckdb-Wasm speaks Arrow fluently, reads Parquet, CSV and JSON files backed by Filesystem APIs or HTTP requests

- https://github.com/holdenmatt/duckdb-wasm-kit /202311/ts
  - Hooks and utilities to make it easier to use duckdb-wasm in React apps.

- https://github.com/tobilg/ducklings /MIT/202601/ts/cpp
  - https://ducklings-api.serverless-duckdb.com/
  - A minimal DuckDB Wasm build for browsers and serverless environments like Cloudflare Workers

- https://github.com/Datakitpage/Datakit /AGPL/202512/ts
  - https://datakit.page/
  - a browser-based data analysis platform that processes multi-gigabyte files (Parquet, CSV, JSON, etc) locally (with the help of duckdb-wasm).
  - All processing happens in your browser - no data is sent to external servers.
  - You can also connect to remote sources like Motherduck and Postgres with a datakit server in the middle.
  - Local File Support: Import CSV, Excel (XLSX), JSON, and Parquet files directly in your browser
  - [DataKit: your all in browser data studio is open source now : r/dataengineering](https://www.reddit.com/r/dataengineering/comments/1phcw6h/datakit_your_all_in_browser_data_studio_is_open/)

- https://github.com/nshiab/simple-data-analysis /MIT/202409/ts
  - https://nshiab.github.io/simple-data-analysis/
  - Easy-to-use and high-performance JavaScript library for data analysis. Works with tabular and geospatial data.
  - The library is based on DuckDB, a fast in-process analytical database.
    - Under the hood, SDA sends SQL queries to be executed by DuckDB. 
    - We use duckdb-node and duckdb-wasm. 
    - SDA can run in the browser and with Node.js and other runtimes.
    - For geospatial computations, we rely on the duckdb_spatial extension.
  - The syntax and the available methods were inspired by Pandas (Python) and the Tidyverse (R).
  - The library is maintained by Nael Shiab, computational journalist and senior data producer for CBC News.
  - SDA is born out of the frustration of switching between Python, R, and JavaScript to produce data journalism projects
  - https://github.com/nshiab/journalism
    - Helper functions for journalism projects.
# more
- [Duckbook.ai - SQL + AI in your browser](https://www.duckbook.ai/)
  - Duckbook is an AI-powered SQL notebook that runs in your browser.
  - Notion-like SQL notebook built on Tiptap, DuckDB, and GPT-4
