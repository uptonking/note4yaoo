---
title: lib-olap-duckdb-dev
tags: [duckdb, olap]
created: 2022-12-05T16:00:35.384Z
modified: 2022-12-05T16:00:55.721Z
---

# lib-olap-duckdb-dev

# guide

# blogs
- [DuckDB -- table的存储格式 | Tangdh's Blog_202307](https://tangdh.life/posts/database/duckdb-file/)
# docs
- DuckDB is a relational (table-oriented) DBMS that supports the Structured Query Language (SQL).
- DuckDB is designed to support analytical query workloads, also known as Online analytical processing (OLAP). 

## why duckdb

- To efficiently support this workload(olap), it is critical to reduce the amount of CPU cycles that are expended per individual value. 
  - The state of the art in data management to achieve this are either vectorized or just-in-time query execution engines. 
  - DuckDB contains a columnar-vectorized query execution engine, where queries are still interpreted, but a large batch of values (a “vector”) are processed in one operation.

- Simple Operation
  - DuckDB has no external dependencies, neither for compilation nor during run-time. 
  - DuckDB does not run as a separate process, but completely embedded within a host process. 
  - In some cases, DuckDB can process foreign data without copying. For example, the DuckDB Python package can run queries directly on Pandas data without ever importing or copying any data.
- Feature-Rich
  - DuckDB provides transactional guarantees (ACID properties) through our custom, bulk-optimized Multi-Version Concurrency Control (MVCC). 
  - Data can be stored in persistent, single-file databases. 
  - DuckDB supports secondary indexes to speed up queries trying to find a single table entry.
- Thorough Testing
  - DuckDB’s test suite currently contains millions of queries, and includes queries adapted from the test suites of SQLite, PostgreSQL and MonetDB
  - Every pull request is checked against the full test setup and only merged if it passes.
  - We run the TPC-H and TPC-DS benchmarks, and run various tests where DuckDB is used by many clients in parallel.
- Open Source under MIT
