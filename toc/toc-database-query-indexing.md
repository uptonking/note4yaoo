---
title: toc-database-query-indexing
tags: [database, indexing, query-engine]
created: 2023-10-30T14:21:26.882Z
modified: 2023-10-30T14:22:08.767Z
---

# toc-database-query-indexing

# guide

- tips
  - 可以分析现有数据库的模块霍扩展是如何实现和使用kdtree的
# excel
- https://github.com/taco-org/taco /202308/java
  - a library for analyzing the dependency and formula structure of a spreadsheet
  - [Efficient and Compact Spreadsheet Formula Graphs](https://arxiv.org/abs/2302.05482v1)
  - [Efficient and Compact Spreadsheet Formula Graphs | Hacker News_202302](https://news.ycombinator.com/item?id=34800138)
    - cool! The authors exploit the fact that neighboring cells often have similar formulas to compress the evaluation graph.
    - This seems odd to me. This is basically just ways of finding database-esque tables in spreadsheets to then leverage for vector/matrix operations.
  - https://github.com/taco-org/tacolens
    - an Excel plugin that is based on TACO framework
    - In TACO-Lens, users can visually inspect formula graphs

- https://github.com/dataspread/dataspread-web /后端java/js
  - http://dataspread.github.io/
  - a spreadsheet-database hybrid system, with a spreadsheet frontend, and a database backend
  - DataSpread v0.1 is built using PostgreSQL and ZKSpreadsheet
  - The current version of DataSpread (what we're calling DataSpread 2.0) is being developed by a team of undergraduate and graduate students at UC Berkeley
  - https://github.com/dataspread/spreadsheet-benchmark
    - We developed an exhaustive benchmark, sheetperf, to evaluate the performance of spreadsheet systems.
  - https://github.com/dataspread/sheetanalyzer /java
    - a library for analyzing the dependency and formula structure of a spreadsheet
# multidimensional
- https://github.com/mikolalysenko/static-kdtree /js/inactive
  - A static kdtree data structure
  - kd-trees are a compact data structure for answering orthogonal range and nearest neighbor queries on higher dimensional point data in linear time
  - While they are not as efficient at answering orthogonal range queries as range trees - especially in low dimensions - kdtrees consume exponentially less space, support k-nearest neighbor queries and are relatively cheap to construct. 
  - This makes them useful in small to medium dimensions for achieving a modest speed up over a linear scan.
  - Note that kd-trees are not the best data structure in all circumstances like range searching / nearest neighbor searching

- https://github.com/0x0539/kdtree /js/inactive
  - Node.js KDTree implementation with lazy indexing for sparse object collision detection
  - This KDTree implementation indexes axis-aligned bounding boxes (AABB's) in any number of dimensions. 
  - It is meant to do real-time indexing with many updates per second (think collision detection of sparse objects like bullets in a fast-paced game).
  - This implementation really benefits from object stability meaning that the less your objects move, the faster index updates will be. For rapidly moving objects (like objects that teleport across the space every timestep), this is a poor choice of index.
  - The index is actually computed at query time, which is what is meant by 'lazy indexing'. And only the necessary parts are computed. 

- https://github.com/gvinciguerra/PGM-index /apache2/cpp
  - The Piecewise Geometric Model index (PGM-index) is a data structure that enables fast lookup, predecessor, range searches and updates in arrays of billions of items using orders of magnitude less space than traditional indexes while providing the same worst-case query time guarantees.
  - This is a header-only library. It does not need to be installed.

- https://gitlab.com/mdds/mdds /cpp
  - A collection of multi-dimensional data structures and indexing algorithms.
  - [Performance benchmark on mdds R-tree](https://kohei.us/2019/02/15/performance-benchmark-on-mdds-rtree/)

- https://github.com/DanielJDufour/xdim /ts
  - Create, Query, and Transform Multi-Dimensional Data.
  - I work a lot with satellite imagery. In theory, most satellite imagery has three dimensions: (1) band, (2) row, and (3) column. 
  - However, for practical reasons, this data is often structured in a flat array, like ImageData.data or a two-dimensional array where each subarray holds all the values for a specific band in row-major order. 
  - This library was created for two main purposes: (1) to provide a unified interface for querying this data regardless of its practical structure and (2) converting this data between different array layouts.

- https://github.com/danakt/multi-array-view /ts
  - small JavaScript library for efficient work with multidimensional arrays
  - When working with a large data, (for example, in 3d-graphics), working with nested arrays in JavaScript can affect the performance of the code. 
  - The more productive analogy(类似；类推) of nested arrays is strided(跨过) arrays—multidimensional data placed in the plane of a one-dimensional array. 
  - Unfortunately, working with strided arrays can lead to code repetition, complex operations, and syntactic noise in the code. 
  - The MultiArrayView library serves to simplify the work with strided arrays as if it were an ordinary multidimensional array.

- https://github.com/stdlib-js/ndarray-array /js
  - Create a multidimensional array
  - https://github.com/stdlib-js/ndarray-base-ctor
  - https://github.com/stdlib-js/ndarray-base-ind2sub

- https://github.com/TileDB-Inc/TileDB /MIT/202310/cpp
  - https://tiledb.com/
  - The Universal Storage Engine
  - a powerful engine for storing and accessing dense and sparse multi-dimensional arrays, which can help you model any complex data efficiently. 
  - It is an embeddable C++ library that works on Linux, macOS, and Windows
  - The power of TileDB stems from the fact that any data can be modeled efficiently as either a dense or a sparse multi-dimensional array, which is the format used internally by most data science tooling. 

- https://github.com/BrandonHaynes/scidb /AGPL/201502/cpp
  - http://scidb.cs.washington.edu/
  - a new open source DBMS that is organized around multidimensional array data model, a generalization of relational model that can provide orders of magnitude better performance. 
  - SciDB is designed to store petabytes of data spread over large number of machines. 
  - High performance, high-availability, fault tolerance, and scalability are the main goals considered in the design of SciDB
# spatial-indexing
- https://github.com/kylebarron/geo-index /MIT/202403/rust
  - A Rust crate for packed, static, zero-copy spatial indexes.
  - An R-tree and k-d tree written in safe rust.
  - Memory-efficient. The index is fully packed, meaning that all nodes are at full capacity (except for the last node at each tree level). 
  - Multiple R-tree sorting methods. Currently, hilbert and sort-tile-recursive (STR) sorting methods
  - Being ABI-stable means that the spatial index can be shared zero-copy between Rust and another program like Python.
  - Drawbacks
    - Trees are static. After creating the index, items can no longer be added or removed.
    - Only two-dimensional data is supported. 
    - Only the set of coordinate types that exist in JavaScript are allowed, to maintain FFI compatibility 
    - Nearest-neighbor queries on the R-tree. This is implemented in the original JS version but hasn't been ported yet.
  - Inspiration: @mourner's amazing flatbush and kdbush libraries are the fastest JavaScript libraries for static R-trees and k-d trees.
  - `GeoArrow` defines a language-independent, ABI-stable memory layout. 
    - Currently, this library is used under the hood in `geoarrow-rs` to speed up boolean operations and spatial joins

- https://github.com/tzaeschke/tinspin-indexes /apache2/java
  - Spatial index library with R*Tree, STR-Tree, Quadtree, CritBit, KD-Tree, CoverTree and PH-Tree
  - This is a library of in-memory indexes. They are used in the TinSpin TinSpin project. 
  - https://github.com/tzaeschke/TinSpin
    - TinSpin is a framework for benchmarking in-memory spatial indexes.

- https://github.com/HactarCE/NDCell /apache2/202108/rust/inactive
  - feature-rich interactive multidimensional cellular automaton simulator written in Rust
# examples

# utils

- https://github.com/bdezonia/zorbage /bsd/java
  - algebraic data types and algorithms for use in numeric processing
  - provide a framework for reusable numeric algorithms
  - support very large data sets: arrays, virtual files, sparse structures, JDBC storage
  - Zorbage has an excellent abstraction for multi- dimensional data
# more
- https://github.com/solzimer/skmeans /MIT/202001/js/inactive
  - Super fast simple k-means and k-means++ implementation for unidimiensional and multidimensional data.
  - Works on nodejs and browser.

- https://github.com/solzimer/sdbscan /MIT/201707/js/inactive
  - Super fast density based spatial clustering DBSCAN implementation for unidimiensional and multidimensional data. 
  - Works on nodejs and browser.
