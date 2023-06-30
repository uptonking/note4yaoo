---
title: lib-olap-benchmark-tpc
tags: [benchmark, olap, tpc]
created: 2022-12-05T16:02:35.575Z
modified: 2022-12-05T16:05:40.690Z
---

# lib-olap-benchmark-tpc

# guide

- [TPC-H in MongoDB_2013](https://www.slideshare.net/aungthurhahein/tpch-in-mongodb)
# Star Schema Benchmark
- https://github.com/ClickHouse/ClickBench
  - https://benchmark.clickhouse.com/
  - ClickBench: a Benchmark For Analytical Databases
  - It covers the typical queries in ad-hoc analytics and real-time dashboards.
  - The dataset is available in CSV, TSV, JSONlines and Parquet formats
  - 比较了很多数据库，包括clickhouse、sqlite、mysql、pg、duckdb、doris、druid、mongodb、es

- ref
  - [ssb.pdf](https://www.cs.umb.edu/~poneil/StarSchemaB.PDF)
  - [《Star Schema Benchmark》阅读笔记_202012](https://andrewei1316.github.io/2020/12/12/star-schema-benchmark/)
  - [数据库】Star Schema Benchmark 标准测试集优化（一）_202209](https://www.jianshu.com/p/271cb880c0b5)
  - [【数据库】Star Schema Benchmark 标准测试集优化（二） - 简书](https://www.jianshu.com/p/c804d4c21c70)
  - [【数据库】Star Schema Benchmark 标准测试集优化（三） - 简书](https://www.jianshu.com/p/acacce2a7293)

- [ClickHouse: Star Schema Benchmark](https://clickhouse.com/docs/en/getting-started/example-datasets/star-schema/)

- [Oracle: Sample Star Schema Benchmark (SSB) Queries and Analytic Views](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/sample-queries.html)

- [Apache Doris: Star-Schema-Benchmark](https://doris.apache.org/zh-CN/docs/benchmark/ssb/)
  - SSB 基于 TPC-H 提供了一个简化版的星型模型数据集，主要用于测试在星型模型下，多表关联查询的性能表现。
  - 业界内通常也会将 SSB 打平为宽表模型（以下简称：SSB flat），来测试查询引擎的性能，参考Clickhouse。
# tpc-benchmarks

## TPC-C 侧重OLTP

- [OLTP](https://www.tpc.org/tpc-bm-categories/oltp5.asp)

- Typical transactional workloads include order-entry (sales), stock-trading (financial), package management (logistics) and manufacturing. 
  - These workloads represent the core operations of many business models.

- The TPC has developed four OLTP benchmarks; 
  - TPC-A, TPC-B, TPC-C and TPC-E, which reflect the evolution of transaction processing requirements over the past three decades.
  - The first two, now obsolete, focused on a system's ability to process simple database transactions concurrently from multiple user or batch sessions. 
  - TPC-C and TPC-E are the current OLTP benchmarks offered by the TPC.
- TPC-C implements an order-entry workload, with more complex real-time and batch transactions, and introduced the notion of a client/server model with response time constraints. 
- TPC-E implements a stock-trading workload, with multi-stage trading transactions and a significant body of read-only transactions, representing a shift towards mixed environments. 
- TPC-E requires RAID protection of the entire disk subsystem, TPC-C requires RAID protection of the database logs only. 
  - In addition, TPC-E requires test sponsors to report how long recovery takes following catastrophic failures. 
- TPC-E implements a richer database schema and transactions. 
  - TPC-E has 33 tables and 10 transactions with tables populated with pseudo-real data instead of random numbers and string fragments. 
  - TPC-C has nine database tables and five transactions. 
  - **The primary metrics of TPC-E and TPC-C are similar**. 
  - Both performance metrics report transactions per time unit and both price performance metrics report price per performance. 
  - TPC-E’s performance metric is tpsE, and price performance metric is $/tpsE while the corresponding metrics in TPC-C are tpmC and $/tpmC.

## TPC-H 侧重ad-hoc queries

- TPC-H用于评测数据库的分析型查询能力。
  - TPC-H 查询包含 8 张数据表、22 条复杂的 SQL 查询，大多数查询包含若干表 Join、子查询和 Group-by 聚合等。
  - 简单来说，TPC-H就是通过22个复杂SQL查询来评估数据库OLAP的性能。

### tpc-h intro

- [TPC-H Homepage](https://www.tpc.org/tpch/default5.asp)
- [TPC Current Specs/Source](https://www.tpc.org/tpc_documents_current_versions/current_specifications5.asp)

- TPC-H is a decision support benchmark. 
  - It consists of a suite of business oriented ad-hoc queries and concurrent data modifications. 
  - The queries and the data populating the database have been chosen to have broad industry-wide relevance. 
  - The performance metric reported by TPC-H is called the TPC-H Composite Query-per-Hour Performance Metric (QphH@Size), and reflects multiple aspects of the capability of the system to process queries.
  - The TPC-H Price/Performance metric is expressed as Price/QphH@Size for Version 2 and Price/kQphH@Size for Version 3.

- [如何理解 大数据、数据仓库领域的ad-hoc这个词？ - 知乎](https://www.zhihu.com/question/48734970)
  - Ad hoc 查询（即席查询）是信息学的一个术语。
  - 许多应用软件系统都有一个潜在的、只能通过有限的请求和报告才能访问的数据库
  - 与其对照的是 "ad hoc" 报告系统（又作“专案报告系统”）。这个系统允许终端用户自己去建立特定的、自定义的查询请求。
  - 偏向于“临时的、将就的”的意思。比如说有个术语叫 ad hoc testing，就是指的是在没有测试指导手册或测试case的前提下，进行临时将就的测试。

- The TPC is introducing V3.0 of the TPC-H Benchmark to accommodate these trends and maintain the relevance of the Price/Performance metric.
  - The primary change in this major revision is to adjust the Price/Performance metric by a multiplier of 1, 000.

## TPC-DS 侧重查询+维护

### tpc-ds intro

- [TPC-DS Homepage](https://www.tpc.org/tpcds/default5.asp)

- TPC-DS is a decision support benchmark that models several generally applicable aspects of a decision support system, including queries and data maintenance. 
  - The benchmark provides a representative evaluation of performance as a general purpose decision support system. 
  - A benchmark result measures query response time in single user mode, query throughput in multi user mode and data maintenance performance for a given hardware, operating system, and data processing system configuration under a controlled, complex, multi-user decision support workload.

## TPC-DI 侧重ETL

- TPC-DI is a benchmark for Data Integration
  - Historically, the process of synchronizing a decision support system with data from operational systems has been referred to as Extract, Transform, Load (ETL) and the tools supporting such process have been referred to as ETL tools. 
  - Recently, ETL was replaced by the more comprehensive acronym, data integration (DI). 
  - DI describes the process of extracting and combining data from a variety of data source formats, transforming that data into a unified data model representation and loading it into a data store. 
  - The TPC-DI benchmark combines and transforms data extracted from an On-Line Transaction Processing (OLTP) system along with other sources of data, and loads it into a data warehouse. 
  - The source and destination data models, data transformations and implementation rules have been designed to be broadly representative of modern data integration requirements.
# discuss
- ## 

- ## 

- ## Snowflake has a pre-built TPCH SF100 dataset, and when you run tpch query 1 in an XSMALL configuration, you'll be amazed, oh my god, it's less than 100ms. 
- https://twitter.com/DreaMer31004339/status/1674323207980208129
  - Then, if you turn off the result cache: `ALTER SESSION SET USE_CACHED_RESULT = FALSE;` things change and the time becomes 15s.
  - 15 second is spectacular when using only 8 cores

- Seriously, results cache vs running from disc vs running from remote storage, I don't understand your point
  - And that was not my experience, first run of ❄️ is from remote storage, they don't pre cache stuff. Are U sure U didn't run it before
- Maybe a colleague, Snowflake keep result cache from other users

- cold run 12 second
  - hot run 9 second
  - result cache 106 ms

- Benchmark became much meaningless especially for a fully managed cloud service. It’s a blackbox that you won’t know the detail about how your queries are executed and the spec of their cluster. The only thing users would care about is typing their query and click the big button.
  - If you find that the performance of your query is not as expected, they have a query acceleration service for you. Just pay for better performance then.

- ## This week, I'll focus on generating a TPC-H-like dataset with @faker_js.
- https://twitter.com/ghalimi/status/1609981590125543426
  - TPC-H synthetic data generated by DBGEN is the golden standard, but it does not look like real data. 
  - In 2023, we can probably do better, using a library such as @faker_js . 
  - I'll generate data in both CSV and Parquet formats, for the 1, 10, 100, 1000, 10000, and 100000 scale factors. 

# more
- [MongoDB TPC-H Queries - Factors Influencing NoSQL Adoption](https://alronz.github.io/Factors-Influencing-NoSQL-Adoption/site/MongoDB/Examples/TPC-H%20Queries/)
