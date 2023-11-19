---
title: lib-db-app-community-model-columnar-arrow
tags: [apache-arrow, columnar, community, database]
created: 2023-10-26T15:02:54.334Z
modified: 2023-10-26T15:03:56.115Z
---

# lib-db-app-community-model-columnar-arrow

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🔥 [The design and implementation of modern column-oriented database systems | Hacker News_201809](https://news.ycombinator.com/item?id=18076547)
- 
- 
- 

# discuss-vector-db
- ## 

- ## 

- ## pgvector is the de facto standard for vectorized processing in Postgres. 
- https://twitter.com/denismagda/status/1726071145235874059
  - But its dominance can be challenged soon by http://pgvecto.rs - a Postgres extension for vector similarity search written in Rust. 
- I doubt that... pgvector has won all the approvals for all the public clouds. This is a cool project but the go-to-market is nearly impossible compared to pgvector

- ## Vector Databases clearly explained!
- https://twitter.com/Sumanth_077/status/1719362859879285022

- ## 🔥 [Rewriting a high performance vector database in Rust | Hacker News_202210](https://news.ycombinator.com/item?id=33252137)
- 
- 
- 

- ## 🔥 [Which vector database should I use? A comparison cheatsheet | Hacker News_202307](https://news.ycombinator.com/item?id=36943318)
- 
- 
- 

- ## 🔥 [A gentle introduction to vector databases | Hacker News_202202](https://news.ycombinator.com/item?id=30425599)

- ## 🔥 [Do we really need a specialized vector database? | Hacker News_202308](https://news.ycombinator.com/item?id=37097004)
- 
- 
- 

- ## 🔥 [Vector databases: analyzing the trade-offs | Hacker News_202308](https://news.ycombinator.com/item?id=37193599)
- 
- 
- 

- ## 🔥 [Vector database built for scalable similarity search | Hacker News_202303](https://news.ycombinator.com/item?id=35308551)
- 
- 
- 

- ## 🔥 [Choosing vector database: a side-by-side comparison | Hacker News_202310](https://news.ycombinator.com/item?id=37764489)
- 
- 
- 

- ## 🔥 [Do you need a vector database? | Hacker News_202304](https://news.ycombinator.com/item?id=35550567)
- 
- 
- 

- ## 🔥 [Every database will become a vector database sooner or later | Hacker News_202310](https://news.ycombinator.com/item?id=37747534)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Most discussions of row vs columnar layout I see are pretty abstract.
- https://twitter.com/eatonphil/status/1720453837566197947
  - The impact really only clicked for me when I tried some benchmarks of workloads on in memory data: sort data stored row and column wise, add all cells of one columns stored row and column wise.
- Think about the (1) branches, (2) data dependencies, and (3) memory overhead that row representation creates on loops processing the records. CPUs hate 1, 2, and 3.

- 💡 Column layout = compression. Thats the key feature. Columns are all the same type! For instance parquet format. **Uncompressing can be cheaper than reading uncompressed data as CPU are fast** and cache misses (both disk pages and cache lines) kill performance.
  - From my tests, you don't even need compression to get the wins (of most likely: cache locality) on analytics workloads like summing a column. But yes compression is another thing made feasible in columnar layouts.
- Absolutely! Columnar storage basically feel like a disk resident ECS

- I like browsing InnoDB (typical row-oriented db) vs. Kudu (column-oriented, with per-column disk structures, but with a row-wise memrowset ("insert buffer") to see differences. 

- ## 🤔 [Why do database columns have a character length of 191? | Hacker News_202105](https://news.ycombinator.com/item?id=27186385)
- 
- 
- 

- ## 🤔🔥 [Why are column oriented databases so much faster than row oriented databases? | Hacker News_201201](https://news.ycombinator.com/item?id=3524437)
- 
- 
- 

- ## 🔥 [Building columnar compression in a row-oriented database | Hacker News_201910](https://news.ycombinator.com/item?id=21412596)
- 
- 
- 

- ## Database File Format Optimization: Per Column Dictionary
- https://twitter.com/gunnarmorling/status/1717552810370167253
  - Nice write-up about @mixpanel 's internal columnar database and some optimizations they did
  - [Database File Format Optimization: Per Column Dictionary_202310](https://engineering.mixpanel.com/database-file-format-optimization-per-column-dictionary-2e108df1d706)
