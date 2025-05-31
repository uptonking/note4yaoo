---
title: spec-format-apache-arrow-community
tags: [apache-arrow, community]
created: 2021-07-24T08:16:02.068Z
modified: 2021-07-24T08:16:41.076Z
---

# spec-format-apache-arrow-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-parquet
- ## 

- ## 

- ## ClickBench keeps me convinced that  Parquet can be quite fast. There is only a 2.3x performance difference vs @duckdb 's own format and unoptimized parquet
- https://x.com/andrewlamb1111/status/1925537738360504663
  - I am surprised that the (closed source) Umbra only reports 3.3x faster than DuckDB on parquet
  - BTW the delta between DuckDB and DataFusion is almost entirely explained by filter pushdown and late materialization, which we are working on
- Rather than twitter speculation, here is a fun project @MOVNTDQ filed about actually measuring how much better performance you can get using just parquet by simply sorting / clustering
- Agree. I believe it's possible to 2x or even 5x parquet or certain workloads, but 10x is impossible with an optimized parquet reader . Across all workloads even 3x is hard.

# discuss
- ## 

- ## 

- ## 

- ## Vortex is an Apache Arrow-compatible toolkit for working with compressed array data. 
- https://x.com/fredine/status/1803525967174049962
  - We are using Vortex to develop a next-generation columnar file format for multidimensional arrays.

- ## Arrow 每次发版都跳一个大版本
- https://twitter.com/OnlyXuanwo/status/1675803368856633345
- 但这样理论上你得对所有版本测试吧
- 主要问题是版本不同的话没法互相交互，比如 darabend 用 arrow 40，但是 ice lake 写了 arrow 42，那就寄了
- 本质是 arrow 太摆烂了，一点 API stability 都不愿意保证，永远是在 bump major version
  - 这可能部分也因为 ASF 项目每次发版都需要投票，不知道 OpenDAL 怎么解决这个问题
  - 这其实对别的库没啥问题，主要是arrow比较特殊，要被多个库跨版本用

- ## Streamlit is now more performant thanks to @ApacheArrow !
- https://twitter.com/streamlit/status/1418637045468000256
  - Using Arrow for data serialization helped us delete over 1, 000 lines of code 
- In general, the performance improvements come from reduced data serialization time (i.e. sending data from Python to the browser).
  - But pandas itself is also becoming faster due to Apache Arrow, so having both pandas and Streamlit using the same format should yield improvements
  - The app creator still needs to think about their workflow, use caching as appropriate, etc. **Apache Arrow can't fix algorithmic complexity of complex transformations**

# discuss-showcase
- ## 

- ## 看了一天的 datafuselabs/databend 代码才发现其节点间数据交换基于Apache Arrow Flight，和 apache/arrow-ballista 神似，不过后者README一目了然。不知道这个两个项目有啥关系
- https://twitter.com/yanchanglu/status/1578758012994433030
- https://github.com/apache/arrow-ballista
  - Ballista is a distributed SQL query engine powered by the Rust implementation of Apache Arrow and DataFusion.
  - Ballista implements a similar design to Apache Spark (particularly Spark SQL)
  - Ballista is designed from the ground up to use columnar data, enabling a number of efficiencies such as vectorized processing (SIMD) and efficient compression. Although Spark does have some columnar support, it is still largely row-based today.
  - The use of Apache Arrow as the memory model and network protocol means that data can be exchanged efficiently between executors using the Flight Protocol, and between clients and schedulers/executors using the Flight SQL Protocol

- ## "InfluxDB uses DataFusion for its Query Execution and Arrow as its internal data representation"
- https://twitter.com/gunnarmorling/status/1683184256011366400
  - Enjoyed reading this article about the system architecture of #InfluxDB 3.0
  - [InfluxDB 3.0: System Architecture](https://www.influxdata.com/blog/influxdb-3-0-system-architecture/)

- ## 用 Go 语言开发的开源时序型数据库 InfluxDB 宣布了未来的开发计划：InfluxDB IOx，用 Rust 语言开发，使用 Apache Arrow 和柱列式数据结构。
- https://twitter.com/wllcjd/status/1326999282105286656
  - InfluxDB 项目创始人 Paul Dix 称，Rust 能给予运行时行为和内存管理更细粒度控制，它带来的额外好处是并发编程更容易消除了数据竞争。

- ## [Apache Arrow, Parquet, Flight and Their Ecosystem are a Game Changer for OLAP | InfluxData_202004](https://www.influxdata.com/blog/apache-arrow-parquet-flight-and-their-ecosystem-are-a-game-changer-for-olap/)
  - Apache Arrow, a specification for an in-memory columnar data format, and associated projects: Parquet for compressed on-disk data, Flight for highly efficient RPC, and other projects for in-memory query processing will likely shape the future of OLAP and data warehousing systems.

# discuss-roadmap-changelog
- ## 

- ## 

- ## 🎯 [Apache Arrow 3.0 | Hacker News_202102](https://news.ycombinator.com/item?id=26018187)
- Arrow is the most important thing happening in the data ecosystem right now. 
  - It's going to allow you to run your choice of execution engine, on top of your choice of data store, as though they are designed to work together. 
  - It will mostly be invisible to users, the key thing that needs to happen is that all the producers and consumers of batch data need to adopt Arrow as the common interchange format.
- Google BigQuery recently implemented the storage API, which allows you to read BQ tables, in parallel, in Arrow format
  - Snowflake has adopted Arrow as the in-memory format for their JDBC driver, though to my knowledge there is still no way to access data in parallel from Snowflake, other than to export to S3.
  - As Arrow spreads across the ecosystem, users are going to start discovering that they can store data in one system and query it in another, at full speed, and it's going to be amazing.

- The premise around arrow is that when you want share data with another system, or even on the same machine between processes, most of the compute time spent is in serializing and deserializing data. 
  - Arrow removes that step by defining a common columnar format that can be used in many different programming languages. 
  - Theres more to arrow than just the file format that makes working with data even easier like better over the wire transfers (arrow flight). 
- 👉🏻 Not only in between processes, but also in between languages in a single process. In this POC I spun up a Python interpreter in a Go process and pass the Arrow data buffer between processes in constant time

- 🆚️ How is this any better than something like flatbuffers though?
  - For one, Arrow is columnar. 👉🏻 The idea of zero-copy serialization is shared between Arrow and FlatBuffers.
  - This is explained in the FAQS for Arrow, saying they use flatbuffers internally. Arrow supports more complex data types.
  - Only for IPC support - Arrow data format does not use flatbuffers.

- 🆚️ The big thing is that it is one of the first standardized, cross language binary data formats. 
  - CSV is an OK text format, but parsing it is really slow because of string escaping. The files it produces are also pretty big since it's text.
  - Arrow is really fast to parse (up to 1000x faster than CSV), supports data compression, enough data-types to be useful, and deals with metadata well. 
  - The closest competitor is probably protobuf, but protobuf is a total pain to parse.

- 😩 Until arrow has proper support for multidimensional arrays, its not really appropriate for many use cases.
  - FWIW, you can support tensors etc. natively today by using Arrow's structs
- Almost no database systems support multidimensional arrays. So they are not appropriate for many use cases?
  - * BigQuery: no * Redshift: no * Spark SQL: no * Snowflake: no * Clickhouse: no * Dremio: no * Impala: no * Presto: no ... list continues
  - We've invited developers to add the extension types for tensor data, but no one has contributed them yet. I'm not seeing a lot of tabular data with embedded tensors out in the wild.
- ClickHouse has support for multidimensional arrays with arbitrary types and number of dimensions. They are stored in tables in efficient column-oriented format.
- The only database I know of that natively supports multidimensional arrays is SciDB (one of Stonebraker's products)
- TileDB supports both sparse and dense multidimensional arrays. We support returning data in arrow arrays or an arrow table as one of many ways we interoperate with computational tools. You can also access the data directly via numpy array, pandas, R data.frames and a number of integrations with MariaDB, Presto, Spark, GDAL, PDAL and more.

- What are the use cases where multi-dimensional arrays are important and why?
  - R&D/manufacturing of consumer facing sensors, in my case.
  - Astronomy, seismology, microscopy. There's an interesting query language, SciQL, built to support such use cases. It can be used with MonetDB

- 
- 
- 
