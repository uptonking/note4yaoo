---
title: toc-lib-olap-mapreduce
tags: [lib, mapreduce, olap, toc]
created: 2020-10-05T09:11:36.186Z
modified: 2020-10-05T09:12:01.565Z
---

# toc-lib-olap-mapreduce

# guide

# popular
- https://github.com/chdb-io/chdb /cpp
  - https://clickhouse.com/blog/chdb-embedded-clickhouse-rocket-engine-on-a-bicycle
  - an embedded SQL OLAP Engine powered by ClickHouse
  - In-process SQL OLAP Engine, powered by ClickHouse
  - Minimized data copy from C++ to Python with python memoryview
  - Input&Output support Parquet, CSV, JSON, Arrow, ORC and 60+more formats, samples
# rust
- https://github.com/apache/arrow-datafusion /rust
  - extensible query engine for building high-quality data-centric systems in Rust, using the Apache Arrow in-memory format. 
  - Python Bindings are also available.
  - DataFusion offers SQL and Dataframe APIs, excellent performance, built-in support for CSV, Parquet, JSON, and Avro, extensive customization, and a great community.
  - https://github.com/apache/arrow-datafusion/tree/main/datafusion-examples

- https://github.com/apache/arrow-ballista /rust
  - Ballista is a distributed SQL query engine powered by the Rust implementation of Apache Arrow and DataFusion.
  - Ballista implements a similar design to Apache Spark (particularly Spark SQL)
  - Ballista is designed from the ground up to use columnar data, enabling a number of efficiencies such as vectorized processing (SIMD) and efficient compression. Although Spark does have some columnar support, it is still largely row-based today.
  - The use of Apache Arrow as the memory model and network protocol means that data can be exchanged efficiently between executors using the Flight Protocol, and between clients and schedulers/executors using the Flight SQL Protocol
  - Supports HDFS as well as cloud object stores. S3 is supported today and GCS and Azure support is planned.
  - Clients can connect to a Ballista cluster using Flight SQL.

- https://github.com/hetudb/hetu /rust/inactive
  - https://www.hetudb.com/
  - a real-time OLAP database management system in the cloud
  - Apache Arrow memory model and compute kernels for efficient processing of data.
  - DataFusion Query Engine for query execution
  - Apache Arrow Flight Protocol for efficient data transfer between processes.
  - Google Protocol Buffers for serializing query plans

- https://github.com/kaskada-ai/kaskada /apache2/rust
  - https://kaskada.io/
  - Kaskada is a unified event processing engine that provides all the power of stateful stream processing in a high-level, declarative query language designed specifically for reasoning about events in bulk and in real time.
  - Kaskada's query language builds on the best features of SQL to provide a more expressive way to compute over events
  - Unlike SQL, they are also concise, composable, and designed for processing events
  - Written in Rust and built on Apache Arrow, Kaskada can compute most workloads without the complexity and overhead of distributed execution.
  - Event-based windowing: Collect events as you move through time
# olap
- druid /10.1kStar/Apache2/202009
  - https://github.com/apache/druid
  - https://druid.apache.org/
  - a high performance real-time analytics database. 
  - Druid's main value add is to reduce time to insight and action.

- querybook /1.3kStar/apache2/202301/ts/python
  - https://github.com/pinterest/querybook
  - https://www.querybook.org/
  - Querybook is a Big Data Querying UI, combining collocated table metadata and a simple notebook interface.
  - 依赖flask
  - 依赖chart.js, codemirror5, draftjs, redux, react-dnd
  - 支持 mysql、postgresql、sqlite、hive、druid、presto

- quix /202Star/MIT/202105
  - https://github.com/wix/quix
  - https://wix.github.io/quix/
  - an easy-to-use notebook manager with support for Presto, Athena, BigQuery, MySQL, PostgreSQL, ClickHouse, Amazon Redshift and more.
