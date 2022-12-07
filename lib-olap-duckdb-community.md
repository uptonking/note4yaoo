---
title: lib-olap-duckdb-community
tags: [community, duckdb, olap]
created: 2022-12-05T16:01:07.929Z
modified: 2022-12-05T16:01:25.243Z
---

# lib-olap-duckdb-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## DuckDB can query parquet data that's hosted on GitHub without needing to fully download the files! Presumably using HTTP range headers?
- https://twitter.com/simonw/status/1571140256052969482
- Indeed we use Range requests to surgically read Parquet metadata first, then only the row groups / columns relevant to the query
- Correct! And it works in DuckDB WASM as well - you can query anything on GitHub just by heading to the shell (on a non-mobile browser)! https://shell.duckdb.org/
- Oh! Is DuckDB WASM able to do glob expansion on remote http files?
  - Not yet I don't think!
  - Nice! In the Python world, it should be possible with the HTTP filesystem abstraction and Arrow.
- Any reason mobile browsers don't work with that? My iPhone runs WASM quite happily
- Bandwidth is magnitude cheaper than storage.
