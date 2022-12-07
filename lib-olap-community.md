---
title: lib-olap-community
tags: [community, olap]
created: 2022-12-05T19:10:03.490Z
modified: 2022-12-05T19:10:15.451Z
---

# lib-olap-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## [ClickBench: A benchmark for analytical databases (Snowflake, Druid, Redshift) | Hacker News_202207](https://news.ycombinator.com/item?id=32084571)
- As a database author myself (I work on Apache Druid) I have really mixed feelings about publishing benchmarks. 
  - They're fun, especially when you win. 
  - But I always want to caution people not to put too much stock in them. 
  - We published one a few months ago showing Druid being faster than Clickhouse on a different workload
  - [Druid Nails Cost Efficiency Challenge Against ClickHouse & Rockset - Imply](https://imply.io/blog/druid-nails-cost-efficiency-challenge-against-clickhouse-and-rockset/)
  - It just seems wrong to take them too seriously.


- There are several existing benchmarks that test query optimisers with a lot of joins. It does not show performance of query engine, but more likely how good is your optimiser was tailored for this queries.


- It's possible the Druid configuration is suboptimal in some way. 
  - It appears that the ClickHouse tests were done using a local table, which there isn't an equivalent of in Druid. 
  - Druid treats every table like what ClickHouse would call a "distributed" table. 

- ## Metrics and benchmarks matter.
- https://twitter.com/ting_sun_cn/status/1600104343818031104
  - 李飞飞搞个ImageNet，Emery Berger搞个csrankings，一下子就对整个领域有了举足轻重的力量
- 确实，你看 clickbench 才上线多久，大家都已经开始在上面搞事情了
- 但是很多人搞过benchmark，最终也是消失在茫茫文献里
  - 说明设计合理的benchmark并推广它并不容易，比如ImageNet就是这样，不冲突
