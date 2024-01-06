---
title: toc-database-timeseries
tags: [database, timeseries, toc]
created: 2024-01-06T14:24:16.872Z
modified: 2024-01-06T14:24:45.338Z
---

# toc-database-timeseries

# guide

# popular
- influxdb /27kStar/MIT/202312/rust
  - https://github.com/influxdata/influxdb
  - https://influxdata.com/
  - InfluxDB is an open source time series database written in Rust, using Apache Arrow, Apache Parquet, and Apache DataFusion
  - This latest version (3.x) of InfluxDB focuses on providing a real-time buffer for observational data of all kinds (metrics, events, logs, traces, etc.) that is queryable via SQL or InfluxQL
  - Flux is the custom scripting and query language we developed as part of our effort on InfluxDB 2.0. it is noticeably absent from the description of InfluxDB 3.0.
  - For InfluxDB 3.0 we adopted Apache Arrow DataFusion, an existing query parser, planner, and executor as our core engine. 
  - With InfluxDB 3.0 being a ground-up rewrite of the database in a new language (from Go to Rust), we weren’t able to bring the Flux implementation along. 
  - [influxdb officially made the switch from Go => Rust : rust_202309](https://www.reddit.com/r/rust/comments/16v13l5/influxdb_officially_made_the_switch_from_go_rust/)
    - Cofounder and CTO of InfluxDB here, there are all the normal reasons: No garbage collector, Fearless concurrency (thanks Rust compiler), Performance, Error handling, Crates
  - [Meet the Founders Who Rewrote in Rust | InfluxData_202307](https://www.influxdata.com/blog/meet-founders-who-rewrote-in-rust/)
# examples

# more
