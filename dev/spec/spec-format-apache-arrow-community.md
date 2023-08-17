---
title: spec-format-apache-arrow-community
tags: [apache-arrow, community]
created: 2021-07-24T08:16:02.068Z
modified: 2021-07-24T08:16:41.076Z
---

# spec-format-apache-arrow-community

# discuss

- ## 

- ## 

- ## 

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
