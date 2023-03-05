---
title: toc-database-columnar-arrow
tags: [apache-arrow, columnar, database, toc]
created: 2022-11-03T04:10:38.591Z
modified: 2022-11-03T04:43:06.880Z
---

# toc-database-columnar-arrow

# guide
- apache-arrow-js的使用示例可以在observablehq社区发现
# db-columnar
- https://github.com/apache/arrow/tree/master/js  /ts
  - Apache Arrow is a columnar memory layout specification for encoding vectors and table-like containers of flat and nested data. 
  - The Arrow spec aligns columnar data in memory to minimize cache misses and take advantage of the latest SIMD (Single input multiple data) and GPU operations on modern processors.
  - 👉🏻 Apache Arrow is the emerging standard for large in-memory columnar data (Spark, Pandas, Drill, Graphistry, ...). 
    - By standardizing on a common binary interchange format, big data systems can reduce the costs and friction associated with cross-system communication.

- https://github.com/steelbreeze/tilly /202201/js
  - a simple columnar database that can be used within the browser, or server-side in node.js
  - Stores the distinct values for each column and rows become integer indexes into the set of distinct values.
  - https://github.com/steelbreeze/pivot
    - A minimalist pivot table library for TypeScript/JavaScript.
    - It provides a minimalist pivot table capability, slicing data into cells defined by two dimensions. 
    - This is a spin-off(副产品，派生物) from the steelbreeze/landscape project
