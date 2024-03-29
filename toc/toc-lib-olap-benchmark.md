---
title: toc-lib-olap-benchmark
tags: [benchmark, olap]
created: 2022-12-06T16:15:49.736Z
modified: 2022-12-06T16:16:00.262Z
---

# toc-lib-olap-benchmark

# guide

# olap-benchmark
- https://github.com/ClickHouse/ClickBench /CC-NC-SA/202402
  - https://benchmark.clickhouse.com/
  - ClickBench: a Benchmark For Analytical Databases
  - It covers the typical queries in ad-hoc analytics and real-time dashboards.
  - 比较了很多数据库，包括clickhouse、sqlite、mysql、pg、duckdb、doris、druid、mongodb、es
  - 提供了很多 Similar Projects/alternatives
  - This benchmark represents typical workload in the following areas: clickstream and traffic analysis, web analytics, machine-generated data, structured logs, and events data. 
  - The dataset from this benchmark was obtained from the actual traffic recording of one of the world's largest web analytics platforms.
  - The dataset is available in CSV, TSV, JSONlines and Parquet formats
  - [Show HN: A benchmark for analytical databases (Snowflake, Druid, Redshift) | Hacker News_202207](https://news.ycombinator.com/item?id=32084571)
  - 🍴 forks
  - https://github.com/hydradatabase/ClickBench
# data

# utils
# clickhouse
- https://github.com/clickvisual/clickvisual
  - lightweight log analytic and data visualize platform built on clickhouse.

# more
- https://github.com/Kyligence/ssb-kylin
  - Star Schema Benchmark Tool for Apache Kylin
  - The schema for SSB is based on the TPC-H benchmark, but in a modified form. 
  - The queries are also based on the TPC-H queries, but the number of queries is reduced to make it easy for individuals to run SSB on different platforms.

- https://github.com/vadimtk/ssb-dbgen
  - SSBM is based on TPC-H dbgen source. The coding style and architecture follows the TPCH dbgen. 
