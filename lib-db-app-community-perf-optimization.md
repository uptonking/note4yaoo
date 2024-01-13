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

- ## 

- ## 

- ## ⚡️ 公司搞优化，讨论如何优化 SQL 和业务。我实在忍不住，跟他们说，先做读写分离，之后把能迁走的表都迁走。
- https://twitter.com/yfractal/status/1745979462615982578
  - 我司虽然量大，但没多大难度。后端难度大的一个现象是用折腾存储，比如上家公司折腾了 5、6 种存储。
  - 所以现在读写分离，加迁表可以苟活很久了。迁移的另一个好处是，责任清晰，好优化。

- 读写分离，数据归档，慢SQL和索引优化基本可以解决大部分问题。很多时候迁移和拆分的难点，不在技术而在人，配合度不高，推责
  - 读写分离也要看业务规模和人力分配，大部分时候，数据归档，慢查询优化，应用缓存可以解决问题。

- 迁表是什么？把其他服务的表迁移到单独的数据库？
  - 恩，是的。

- 请问啥是读写分离？
  - 主库再加几个从库，然后读流量去从库。牺牲一点点一致性，换读流量可拓展。

- 之前我就只推这个，效果很好。我选型的倾向是用最糙猛且 proved 的办法来解决行业里已经解决过的问题，把最无聊的落地工作推下去，很多花拳绣腿的办法烂尾风险都很高
  - well-defined/resolved的问题其实最适合用那种烂大街且boring的方案。搞工程不是艺术表演，用可控的成本赶紧把事儿做好是最重要的。工作越久经历的情况越多越觉得沉迷/陷入纯粹技术对engineer来说是一种病

- 
- 
- 

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
