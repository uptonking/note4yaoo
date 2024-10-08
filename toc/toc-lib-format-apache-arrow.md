---
title: toc-lib-format-apache-arrow
tags: [apache-arrow, format, toc]
created: 2023-01-08T16:27:30.419Z
modified: 2023-01-08T16:27:44.918Z
---

# toc-lib-format-apache-arrow

# guide
- apache-arrow-js的使用示例可以在observablehq社区发现
# popular
- polars /12.3kStar/MIT/202403/rust/NoDeps
  - https://github.com/pola-rs/polars
  - https://pola.rs/
  - Polars is a blazingly fast DataFrames library implemented in Rust using Apache Arrow Columnar Format as the memory model.
  - multi-threaded, hybrid-streaming DataFrame library in Rust | Python | Node.js
  - If you have data that does not fit into memory, polars lazy is able to process your query (or parts of your query) in a streaming fashion
  - In the TPCH benchmarks polars is orders of magnitudes faster than pandas, dask, modin and vaex on full queries (including IO).

- https://github.com/devinjdangelo/DataWeb /apache2/202401/rust
  - Virtual Data Integration Powered by Apache Arrow
  - DataWeb enables virtual integration of siloed data systems with minimal central coordination. 
  - DataWeb is designed for organizations which cannot effectively integrate all of their data in a single central data system (i.e. Data Warehouse, Data Lake, ...)
  - A Relay is a node in the DataWeb that has its own independent set of logical data models. Each Relay is connected to physical data sources and remote logical data sources (i.e. other Relays in the Web).
# examples
- https://github.com/vega/vega-loader-arrow
  - This package extends Vega's set of data format parsers to support the type "arrow" in Vega version 5.0 and higher.
  - You can try the Arrow loader in our Observable notebook examples for both Vega and Vega-Lite.
# parser-generator

# extension-superset

# arrow-impl

- https://github.com/kylebarron/arro3
  - a minimal Python implementation of @ApacheArrow based on the @rustlang Arrow crate.
  - This adds zero-copy data import from Numpy, so you can use numeric Numpy-backed arrays with Rust Arrow operations without copies
# utils
- https://github.com/kylebarron/arrow-js-ffi /rust
  - Zero-copy reading of Arrow data from WebAssembly

- https://github.com/geoarrow/geoarrow-rs /202311/rust
  - GeoArrow in Rust and WebAssembly with vectorized geometry operations
# more
