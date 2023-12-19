---
title: toc-lib-data-etl
tags: [data, etl, lib, toc]
created: 2020-10-05T09:34:33.467Z
modified: 2023-10-27T15:39:10.466Z
---

# toc-lib-data-etl

# popular

- https://github.com/alibaba/easyexcel /30kStar/apache2/202312/java
  - 简单且能避免OOM的java处理Excel工具
- https://github.com/mikedehaan/poi-test
  - Apache POI performance test application
- https://github.com/xresloader/xresloader
  - /147Star/MIT/202008
  - 跨平台Excel导表工具
  - Excel=>protobuf/msgpack/lua/javascript/json/xml
  - https://github.com/xresloader/xresconv-conf
    - 批量转表配置规范
  - https://github.com/xresloader/xresconv-gui
    - 跨平台GUI工具(Windows/Linux/macOS)
  - https://github.com/xresloader/xresconv-cli
    - 跨平台命令行工具，兼容python2和python3
# etl
- https://github.com/alibaba/DataX
  - /7.3kStar/Apache2/202009
  - 离线数据同步工具/平台，实现包括 MySQL、Oracle、Postgres、HDFS等各种异构数据源之间高效的数据同步功能

- https://github.com/Claviz/bellboy /202305/ts
  - Highly performant JavaScript data stream ETL engine.
  - Bellboy streams input data row by row. Every row, in turn, goes through user-defined function where it can be transformed.
  - When enough data is collected in batch, it is being loaded to destination.
  - A job in bellboy is a relationship link between processor and destinations
  - Each processor in bellboy is a class which has a single responsibility of processing data of specific type
  - **Every job can have as many destinations (outputs)** as needed. For example, one job can load processed data into a **database**, **log** this data to stdout and post it by **HTTP** simultaneously.
  - New processors and destinations can be made by extending existing ones.

- https://github.com/cloudquery/cloudquery /go
  - https://cloudquery.io/
  - high-performance data integration framework built for developers.
  - CloudQuery extracts, transforms, and loads configuration from cloud APIs to variety of supported destinations such as databases, data lakes, or streaming platforms for further analysis.
# query
- https://github.com/obi1kenobi/trustfall /apache2/rust
  - A query engine for any combination of data sources.
  - databases, APIs, file systems, anything else you can think of + any combination of them.
  - The easiest way to plug in a new data source is by implementing the BasicAdapter trait.
  - In the Playground, Trustfall is configured to run client-side as WASM, performing all aspects of query processing (parsing, compilation, and execution) within the browser. 
  - it is of course able to be used in a more traditional client-server context as well.
# data-platform
- https://github.com/infinyon/fluvio /rust
  - https://www.fluvio.io/
  - Fluvio is a high-performance distributed data streaming platform that's written in Rust, built to make it easy to run real-time applications.
  - Fluvio is an open source data pipeline project w/ plugin wasm modules for data transformations as "SmartModules". In our case we can run wasm plugins on frontend or backend (none of which require a browser). 
# infrastructure
- https://github.com/coollabsio/coolify
  - https://coollabs.io/coolify
  - An open-source, hassle-free, self-hostable Heroku & Netlify alternative
# more-tools
