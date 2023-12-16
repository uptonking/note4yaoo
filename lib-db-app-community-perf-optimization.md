---
title: lib-db-app-community-perf-optimization
tags: [database, perf]
created: 2023-10-26T18:59:45.214Z
modified: 2023-10-26T19:00:02.186Z
---

# lib-db-app-community-perf-optimization

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-vendors
- ## 

- ## 

- ## 🔥 [Techniques for Microsoft SQL database design and optimization | Hacker News_201612](https://news.ycombinator.com/item?id=13277061)
- 
- 
- 

# discuss
- ## 

- ## Parquet Row Group Skipping with Bloom Filter in Apache Hudi 
- https://twitter.com/Dipankartnt/status/1735715073409106056
  - Parquet filter pushdown is a performance optimization method that prunes irrelevant data from a parquet file to reduce the amount of data scanned by a query engine

- You can skip row groups using 3 ways:
  - column min/max statistics. Column min/max stats are simple. Based on the min/max stats, you can filter out values that are not in the range.
  - dictionary filter. With dictionary, you can filter out values that are between min & max but not in the dictionary. Problem with dictionary is that it can consume more space with higher cardinality columns.
  - bloom filter. 
- A bloom filter is a probabilistic data structure that allows you to identify whether an item belong to a data set or not. 
  - It either outputs: "definitely not present" or "maybe present" for every data search.
  - By using Bloom filters, you can efficiently skip over large portions of the Parquet file that are irrelevant to your query, reducing the amount of data that needs to be read and processed.
- With the 0.14 release of @apachehudi , you can use this bloom filter to skip non-relevant row groups. This can be very valuable for improving query performance & reducing I/O operations when dealing with large-scale data.

- ## 🔥 [Demystifying Database Performance for Developers | Hacker News_202205](https://news.ycombinator.com/item?id=31287442)
- 
- 
- 

- ## 🔥 [Database Performance at Scale – A free book | Hacker News_202310](https://news.ycombinator.com/item?id=37778069)
- 
- 
- 
