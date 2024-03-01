---
title: toc-lib-olap-mapreduce
tags: [lib, mapreduce, olap, toc]
created: 2020-10-05T09:11:36.186Z
modified: 2020-10-05T09:12:01.565Z
---

# toc-lib-olap-mapreduce

# guide

# popular
- https://github.com/chdb-io/chdb /apache2/202312/cpp
  - https://doc.chdb.io/
  - https://clickhouse.com/blog/chdb-embedded-clickhouse-rocket-engine-on-a-bicycle
  - an embedded SQL OLAP Engine powered by ClickHouse
  - In-process SQL OLAP Engine, powered by ClickHouse
  - Minimized data copy from C++ to Python with python memoryview
  - Input&Output support Parquet, CSV, JSON, Arrow, ORC and 60+more formats, samples
  - https://twitter.com/ohmypy/status/1734189799521812615
    - What's the difference between this and clickhouse-local?
    - Bindings for major languages + some additional features 
    - A true competitor to duckdb
# rust
- https://github.com/apache/arrow-datafusion /4.7kStar/apache2/202403/rust
  - https://arrow.apache.org/datafusion
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

- https://github.com/tensorbase/tensorbase /apache2/202112/rust/inactive
  - https://tensorbase.io/
  - TensorBase is a new big data warehousing with modern efforts.
  - TensorBase is building on top of Rust, Apache Arrow and Arrow DataFusion.
  - The world's first ClickHouse compatible open-source implementation.
  - First no-LSM, write and read optimized storage layer proposed.
  - TensorBase hopes the open source not become a copy game. After thoughts, we decided to temporarily leave the general data warehousing field.

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
- druid /13.1kStar/apache2/202403/java
  - https://github.com/apache/druid
  - https://druid.apache.org/
  - https://druid.apache.org/docs/latest/design/architecture/
  - a high performance real-time analytics database. 
  - Druid's main value add is to reduce time to insight and action.
  - Druid is designed for workflows where fast queries and ingest really matter. 
  - Druid excels at powering UIs, running operational (ad-hoc) queries, or handling high concurrency. 
  - 🏘️ Druid has a distributed architecture that is designed to be cloud-friendly and easy to operate. This design includes enhanced fault tolerance: an outage of one component does not immediately affect other components.
    - A Master server manages data ingestion and availability
    - Coordinator services watch over the Historical services on the Data servers
    - A Query server provides the endpoints that users and client applications interact with, routing queries to Data servers or other Query servers (and optionally proxied Master server requests).
    - Router services provide a unified API gateway in front of Brokers, Overlords, and Coordinators.
  - 🏘️ Druid has three external dependencies.
  - Druid uses deep storage to store any data that has been ingested into the system. 
    - Deep storage is shared file storage accessible by every Druid server.
    - In a clustered deployment, this is typically a distributed object store like S3 or HDFS, or a network mounted filesystem. 
    - In a single-server deployment, this is typically local disk.
  - The metadata storage holds various shared system metadata such as segment usage information and task information. 
    - In a clustered deployment, this is typically a traditional RDBMS like PostgreSQL or MySQL. 
    - In a single-server deployment, it is typically a locally-stored Apache Derby database.
  - ZooKeeper is used for internal service discovery, coordination, and leader election.
  - [Druid vs Pinot: Choosing the best database for Real-Time Analytics - Imply _202312](https://imply.io/blog/choosing-a-database-for-real-time-analytics-druid-and-pinot/)
    - The key differences are indexing, ingestion, mixed workloads, and maturity.
  - [Apache Druid vs. Apache Pinot - Imply](https://imply.io/lp/apache-druid-vs-apache-pinot/)

- pinot /5kStar/apache2/202403/java
  - https://github.com/apache/pinot
  - https://pinot.apache.org/
  - https://docs.pinot.apache.org/basics/architecture
  - a real-time distributed OLAP datastore, built to deliver scalable real-time analytics with low latency
  - Pinot is designed to execute real-time OLAP queries with low latency on massive amounts of data and events. 
  - It can ingest from batch data sources (such as Hadoop HDFS, Amazon S3, Azure ADLS, Google Cloud Storage) as well as stream data sources (such as Apache Kafka).
  - Pinot was built by engineers at LinkedIn and Uber and is designed to scale up and out with no upper bound.
  - Column-oriented: a column-oriented database with various compression schemes such as Run Length, Fixed Bit Length.
  - Pluggable indexing: pluggable indexing technologies Sorted Index, Bitmap Index, Inverted Index.
  - Query optimization: ability to optimize query/execution plan based on query and segment metadata.
  - Stream and batch ingest: near real time ingestion from streams and batch ingestion from Hadoop.
  - Query: SQL based query execution engine.
  - Multi-valued fields: support for multi-valued fields, allowing you to query fields as comma separated values.
  - Pinot also provides Kubernetes integrations with the interactive query engine, Trino Presto, and the data visualization tool, Apache Superset.
  - Pinot™ is a distributed OLAP database designed to serve real-time, user-facing use cases
  - 🏘️ 
  - Helix was designed by the original creators of Pinot for Pinot's own cluster management purposes. 
    - It uses Apache ZooKeeper as a fault-tolerant, strongly consistent, durable state store.
    - Helix maintains a picture of the intended state of the cluster, including the number of servers and brokers, the configuration and schema of all tables, connections to streaming ingest sources, currently executing batch ingestion jobs
  - The Pinot controller schedules and re-schedules resources in a Pinot cluster when metadata changes or a node fails
  - The broker's responsibility is to route queries to the appropriate server instances
  - Servers host segments on locally attached storage and process queries on those segments.
  - A Pinot minion is an optional cluster component that executes background tasks on table data apart from the query processes performed by brokers and servers

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
# more
