---
title: toc-db-benchmark
tags: [benchmark, db, toc]
created: 2022-11-25T16:16:25.906Z
modified: 2022-11-25T16:16:52.713Z
---

# toc-db-benchmark

# guide

- common
  - oltp
    - tpc-c
  - olap
    - tpc-h

- [数据库压测模型TPC-C/TPC-H - HunterHuang - 博客园](https://www.cnblogs.com/hunterhuang8888/p/14237903.html)
  - TPC , Transaction Processing Performance Council, 是一个非盈利组织，成立于1988年，这个组织主要的功能是定义事务处理、数据库的基准，这个基准用于评估服务器的性能，并且把服务器评估的结果发布在TPC的官方网站上。
  - 绝大部分数据库产品在发布时都会进行TPC压力测试，阿里OceanBase在2019年10月的TPC-C测试中，跑出6000万+的测试成绩，成为TPC-C榜单第一名。
- TPC-C用于评测数据库的联机交易处理（OLTP）能力。
  - 主要涉及10张表，包含五类业务事务模型（NewOrder–新订单的生成、Payment–订单付款、OrderStatus–最近订单查询、Delivery–配送、StockLevel–库存缺货状态分析）。
  - TPC-C通过tpmC值（Transactions per Minute）来衡量系统最大有效吞吐量（MQTh，Max Qualified Throughput），其中Transactions以NewOrder Transaction为准，即最终衡量单位为每分钟处理的新订单数
- TPC-H用于评测数据库的分析型查询能力。
  - TPC-H 查询包含 8 张数据表、22 条复杂的 SQL 查询，大多数查询包含若干表 Join、子查询和 Group-by 聚合等。
  - 简单来说，TPC-H就是通过22个复杂SQL查询来评估数据库OLAP的性能。
# benchmarks
- https://github.com/ClickHouse/ClickBench
  - https://benchmark.clickhouse.com/
  - ClickBench: a Benchmark For Analytical Databases
  - It covers the typical queries in ad-hoc analytics and real-time dashboards.
  - 比较了很多数据库，包括clickhouse、sqlite、mysql、pg、duckdb、doris、druid、mongodb、es
  - 提供了很多 Similar Projects/alternatives
  - This benchmark represents typical workload in the following areas: clickstream and traffic analysis, web analytics, machine-generated data, structured logs, and events data. 
  - The dataset from this benchmark was obtained from the actual traffic recording of one of the world's largest web analytics platforms. 
  - The dataset is available in CSV, TSV, JSONlines and Parquet formats
  - [Show HN: A benchmark for analytical databases (Snowflake, Druid, Redshift) | Hacker News_202207](https://news.ycombinator.com/item?id=32084571)

- https://github.com/pubkey/client-side-databases
  - https://pubkey.github.io/client-side-databases/database-comparison/index.html
  - I have implemented the exact same chat application with different database technologies.
  - The chat app is a web based angular application, with functionality similar to Whatsapp Web.
  - PouchDB with IndexedDB adapter & CouchDB replication
  - RxDB PouchDB with PouchDB Storage & GraphQL replication
  - RxDB LokiJS with LokiJS Storage & GraphQL replication
  - RxDB Dexie.js with Dexie.js Storage & GraphQL replication
  - WatermelonDB with LokiJS adapter (no backend sync atm)

- https://github.com/Level/bench
  - Benchmark `abstract-level` databases. 
  - Currently only suitable for use in Node.js.
# tpc
- https://github.com/abz53378/tpch-json /201905/json
  - 导入json输入到mongodb

- https://github.com/DBYardstick/TPC-C /201506/ts
  - TPC-C benchmark implementation in NodeJS
  - The TPC-C benchmark has been implemented. It is currently capable of running 100, 000 clients against an infinitely fast database (implemented as NullDB in code), while consuming just one CPU.
  - The architecture of this implementation allows one to easily port this benchmark application to another database, without any changes to the application itself. 

- https://github.com/Juliiii/TPC-Hdatatojson
  - TPC-H的测试数据转成json格式的nodejs代码

- https://github.com/Mahan3340/TPC-benchmark
  - TPC-H Benchmark on Spark (Avro, Parquet, ORC formats) , PostgreSQL , Flink (Avro Format)

- https://github.com/trinodb/tpch
  - Port of TPC-H dbgen to Java

- https://github.com/dhuny/tpch
  - TPC-H Benchmark helper for MySQL and MariaDB

- https://github.com/lucasgiutavares/MongoDB-TPC-H-Translation
  - Python script for MongoDB TPC-H translation.

- https://github.com/mongodb-labs/py-tpcc /202207
  - an experimental variant of Python TPC-C implementation
  - https://github.com/apavlo/py-tpcc /201901

- https://github.com/xv500i/TPC-H-Benchmark-NOSQL /201306/java
  - We're testing oracle, node4j and mongodb with TPC-H benchmark in order learn its pros and cons

- https://github.com/alronz/B2C-Database-Selection-Implementations
  - created to show how to use NoSQL databases such as Redis, MongoDB, Neo4j and Cassandra to implement a real life data model of a B2C application and try to check how is the query expressiveness for each database. 
  - The data model used for this experiment is the TPCH benchmark data model
  - [TPC-H Queries - Factors Influencing NoSQL Adoption](https://alronz.github.io/Factors-Influencing-NoSQL-Adoption/site/MongoDB/Examples/TPC-H%20Queries/)
# mongo-sql
- https://github.com/scsinha/benchmark_mongo_postgres /202003/js
  - Benchmarking Postgres and MongoDb aggregate queries on 1 million records

- https://github.com/parse-community/benchmark /apache2/201908/js
  - https://benchmark.parseplatform.org/
  - a continuous integration tool that runs benchmarks on every commit to Parse server.
  - 比较了mongo/pg，指标包括get/post/cpu/ram

- https://github.com/kennethjiang/pg-mongo-benchmark /201504/js
  - The goal of this challenge is to measure the read and write performance for a sample dataset of Postgres and MongoDB

- https://github.com/dtim-upc/MongoDBTests /202005/java
  - A set of test cases to evaluate cache performance of MongoDB with different document counts and sizes
  - I have disabled the compression and limited the cache to 0.25GB to get the cache saturated faster.

- https://github.com/monorkin/mongo-vs-pg-large-table-performance /MIT/202308/ruby
  - a simple benchmark that tests how quick Postgres and MongoDB can concurrently read and write records to a table/collection that has at least 100M records in it.
  - This kind of benchmark is important to show which DB performs better as an event log store - think thermostat readings, or when a user (dis)connected to a chat room, and similar events that just get logged and never updated.
# timeseries
- https://github.com/timescale/tsbs /MIT/202309/go
  - This repo contains code for benchmarking several time series databases, including TimescaleDB, MongoDB, InfluxDB, CrateDB and Cassandra. 
  - This code is based on a fork of work initially made public by InfluxDB at https://github.com/influxdata/influxdb-comparisons.

- https://github.com/tsdbbench/Ultimate-TSDB-Comparison /202003/未找到代码
  - https://tsdbbench.github.io/Ultimate-TSDB-Comparison/
  - Feature comparison of open source Time Series Databases (TSDBs)
# utils

# more
- https://github.com/nolanlawson/database-comparison /202102/js
  - http://nolanlawson.github.io/database-comparison/
  - Compare DOM-blocking in browser databases
  - Demo app to test different browser databases (memory, LocalStorage, IndexedDB, WebSQL) and in particular see whether or not they block the DOM.
