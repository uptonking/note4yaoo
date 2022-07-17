---
title: lib-olap-apache-druid
tags: [apache-druid, olap]
created: 2020-03-29T15:40:17.360Z
modified: 2021-05-13T03:15:22.261Z
---

# lib-olap-apache-druid

# faq

- druid vs pinot vs clickhouse
# discuss
- ## clickhouse到底有哪些吊炸天的优化？
- https://www.zhihu.com/question/446288242/answers/updated
- 利益相关: OLAP查询引擎开发者，TPC-H 30TB榜单排名第一的系统的开发者之一。
  - 先放结论: Clickhouse没有任何吊炸天的优化，它只是把论文和社区中大家都讨论过的那些优化技巧，很好地实现了一下而已。(本回答只讨论查询链路)
- 谈起数据库查询引擎或者大数据执行引擎，你一定听说过这些关键词：向量化、列式执行、SIMD、LLVM等等等。每个人都会讨论这些，但是很少有人能够把这些东西讲的很透彻。
  - Clickhouse做的无非就是把这些技术一个一个地进行工程优化、实现到生产系统中。这不是我说的，这是clickhouse自己的文档说的
  - 实际上，只需要招一些有性能优化、HPC经验的工程师做些简单分析，就能找到查询引擎的性能瓶颈，然后照着之前大家讨论过的那些概念去实现就好了。
  - 但是**这东西不能上PPT、也不能发论文**，所以在意的人不多。
- Clickhouse的性能，就是大量类似的工程优化堆积起来的。
  - 比如clickhouse的hash agg，用模板实现了30多个版本，覆盖了最常见的group key的类型。这么做的目的就是为了减少一些类型判断的时间。
- 当然clickhouse也有缺陷。
  - 从我自己做过的测试来看，clickhouse主要关注单表优化，不能很好地处理复杂表达式和多表join的场景，而且在需要落盘的场景clickhouse也没有做过很好的优化。
  - 有些原因是clickhouse没有在这个点上花太多功夫，有些原因则是clickhouse的列式架构本身的限制。

- ## An interesting aspect of this comparison between Clickhouse and Apache Pinot is C++ is assumed to be faster than Java. If this is true today, will it be true in 5 years time?
- https://twitter.com/richardstartin/status/1440382771730411520
- Reminds me Apache Cassandra vs ScyllaDB a bit. I’d say it’s rather a question of how close Java and C++ could end up in terms of performance in certain use cases.

- ## Clickhouse and Apache Pinot
- https://www.reddit.com/r/bigdata/comments/pse4gb/clickhouse_and_apache_pinot/
