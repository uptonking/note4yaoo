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

- ## To optimize performance, We( @DatabendLabs )’ve done: 
- https://x.com/BohuTANG/status/1862364484100399594
  - 1. Adopted efficient compression like zstd. 
  - 2. Optimized warehouse processor scheduling to hit S3 max bandwidth. 
  - 3. Merged S3 requests to minimize API call overhead.

- ## 正在做一个web应用，数据库某个表可能会有100w量级的数据，假如单纯使用nextjs + supabase 方案，问题大吗？
- https://twitter.com/wsygc/status/1775093291165634871
- 当说到数据库使用的时候，要分是不是存多查少？如果查多且多维度查询，可能得再跑一个ES，如果只是简单查询，单表可以撑很久
- pg 100w 肯定没问题，supabase 是完整的 pg 100w 肯定也没问题，但是 supabase 的定价真的到了 100w 那么钱包可能会有问题

- pq 百万数据查询很快，我把某公链的索引存在 supabase, 其中一张表的数据有 6000W+，依然可以在一秒内响应，不过我是本地部署的 supabase，购买服务的话，会慢一些

- 百万在数据库领域是个小数目，做好索引即可
- 100w数据量，都不叫数据，随便折腾，mysql也算是千万级的，更高就上clickhouse
- 100G 也不算多，MySQL 一把梭，查询很轻松，只要做好索引就好了, 实在多了就分区分表。

- 没用过supabase，以mysql好久之前的版本为基准，没索引的情况下，全表扫描1s在100w~200w数据，魔改版应该会快，索引做好，就没啥事
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

- ## Database Caching is a million-dollar technique you can’t ignore.
- https://twitter.com/ProgressiveCod2/status/1765333907522916465
- Cache-Aside Strategy
- Read-Through Strategy
- Write-Around Strategy
- Write-Through Strategy
- Write-Back Strategy

- ## 🌰 Many tutorials give you tips to improve your Database performance using only single-column Indexes.
- https://twitter.com/deisbel/status/1761384992775500055
  - Using 4 examples, I’ll teach you 3 new tips to create great Composite Indexes.

- ## 💡 Data skipping is one of the common techniques used with large volumes of data to achieve better query performances.
- https://twitter.com/Dipankartnt/status/1759054983029203240
  - The whole idea is simple - read as less data as possible
  - What that means is that as a compute engine paired with a data lake table format like @apachehudi , it should read only the data files that are needed to satisfy the query from the storage. Data skipping reduces the volume of data that needs to be scanned and processed.
  - Of course this is made possible because of the metadata information provided by file formats like Parquet. Basically, each Parquet file contains the min/max values of each column along with other useful info: num of NULL values. These min/max values are 'column statistics'.
  - Now, although, we could directly leverage these stats for data skipping, this could affect the query performance because the engine still has to go through each file to read the footer. 

- What's Hudi's approach?
  - it adds a next level of pruning. basically it takes all these stats & collates the info in the form of an INDEX.
  - Indexes such as this are incorporated into Hudi's internal metadata table so engines can just get the files where the data is stored.
  - Therefore, instead of reading individual Parquet footers, compute engines can directly go to the metadata table's index & fetch the required files. Way faster.
  - [Hudi’s Column Stats Index and Data Skipping feature help speed up queries by an orders of magnitude _202206](https://www.onehouse.ai/blog/hudis-column-stats-index-and-data-skipping-feature-help-speed-up-queries-by-an-orders-of-magnitude)

- ## [Understanding Connections and Pools | Hacker News _202101](https://news.ycombinator.com/item?id=25644656)
- 
- 
- 

- ## you can delete old data very efficiently if you partition your table by time ranges and drop one of them.
- https://twitter.com/tobias_petry/status/1748340608849072602
  - [Delete Old Rows with Partitions - Database Tip](https://sqlfordevs.com/partition-delete-old-rows)
- Can this be applied to previously created tables?  A clients MySQL database has grown so large there isn't enough disk space to run OPTIMIZE TABLE after deleting table records.  This seems like a good trick to free up disk space.
  - You would have to create a new table and insert the rows there again.
- Have any tricks to free up disk space on a MySQL 5.6.3 database when the host doesn't have enough disk space to run OPTIMIZE TABLE?

- What would you use to maintain the partitions, events, or external cron?
  - I would use a cron

- ## ⚡️ 我司搞数据库优化，我没忍住，说我们先把读写分离搞了。因为至少能搞出来 10x 的性能，还好操作，不用考虑细节。
- https://twitter.com/yfractal/status/1757276270457770225
  - 但到执行上，又是各种细节优化。比如我说把后台任务都丢到 read replica 上，变成了挑流量大的。然后还有忙着加 cache 的。

- 最蛋疼的是搞个半天，费尽口舌，最后 PM 过来说：你给的方案怎么做了这么久？怎么到现在问题还好多？

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
