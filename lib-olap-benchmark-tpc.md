---
title: lib-olap-benchmark-tpc
tags: [benchmark, olap, tpc]
created: 2022-12-05T16:02:35.575Z
modified: 2022-12-05T16:05:40.690Z
---

# lib-olap-benchmark-tpc

# guide

- [MongoDB TPC-H Queries - Factors Influencing NoSQL Adoption](https://alronz.github.io/Factors-Influencing-NoSQL-Adoption/site/MongoDB/Examples/TPC-H%20Queries/)

- [TPC-H in MongoDB_2013](https://www.slideshare.net/aungthurhahein/tpch-in-mongodb)
# TPC-H 侧重ad-hoc queres
- TPC-H用于评测数据库的分析型查询能力。
  - TPC-H 查询包含 8 张数据表、22 条复杂的 SQL 查询，大多数查询包含若干表 Join、子查询和 Group-by 聚合等。
  - 简单来说，TPC-H就是通过22个复杂SQL查询来评估数据库OLAP的性能。

## tpc-h intro

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
# tpc-examples

# tpc-utils

# TPC-DS 侧重查询+维护

## tpc-ds intro

- [TPC-DS Homepage](https://www.tpc.org/tpcds/default5.asp)

- TPC-DS is a decision support benchmark that models several generally applicable aspects of a decision support system, including queries and data maintenance. 
  - The benchmark provides a representative evaluation of performance as a general purpose decision support system. 
  - A benchmark result measures query response time in single user mode, query throughput in multi user mode and data maintenance performance for a given hardware, operating system, and data processing system configuration under a controlled, complex, multi-user decision support workload.
# TPC-DI 侧重ETL
- TPC-DI is a benchmark for Data Integration
  - Historically, the process of synchronizing a decision support system with data from operational systems has been referred to as Extract, Transform, Load (ETL) and the tools supporting such process have been referred to as ETL tools. 
  - Recently, ETL was replaced by the more comprehensive acronym, data integration (DI). 
  - DI describes the process of extracting and combining data from a variety of data source formats, transforming that data into a unified data model representation and loading it into a data store. 
  - The TPC-DI benchmark combines and transforms data extracted from an On-Line Transaction Processing (OLTP) system along with other sources of data, and loads it into a data warehouse. 
  - The source and destination data models, data transformations and implementation rules have been designed to be broadly representative of modern data integration requirements.
