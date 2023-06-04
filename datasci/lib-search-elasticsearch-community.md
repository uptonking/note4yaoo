---
title: lib-search-elasticsearch-community
tags: [community, elasticsearch]
created: 2023-01-02T08:49:27.078Z
modified: 2023-01-02T08:49:39.114Z
---

# lib-search-elasticsearch-community

# guide

# discuss
- ## 

- ## 

- ## [请教一个问题，搜索词的生成应该怎么做。 - V2EX](https://www.v2ex.com/t/888629)
  - 例如在 Google 中输入：Java google 会生成: javascript, java binary search, java 教程等一些列
  - 搜索日志，只能优化排序，原生的搜索词生成是基于系统的关键字检索出来的，系统在冷启动时，排序可以是随机的，随着使用情况，逐步优化。当然也可以初始化一些排序。


- 一般都不是算法生成的。suggest 数据都会有以下一些来源：
  1. 搜索数据本身的一些 title 、tag 属性等
  2. 用户的搜索词(如用户可能会搜索 java ，还可能会搜索 javascript)
  3. 爬虫抓取
- 最简单的直接基于 Trie 做，query 的权重要加到 TrieNode 里，Trie 树里召回一堆词以后再加入一些提前处理好的非前缀词，比如和召回 query 强相关的中缀、后缀，最后排序
- 如果只是前缀匹配，那非常简单，像楼上说的 trie 树或者直接数据库前缀匹配都可以获得一些推荐，难的是怎么做权重和关联性
- 没有序列的概念，每个 suggestion 都是整体，比如 "javascript" / "java orm"，在数据挖掘时 "java orm" 是从日志中挖掘出的用户 query ，如果很多人搜了 "java orm"，这个 query 的权重就比较高。虽然在搜索时引擎内部会分词做召回，但是实际上用户想搜索的是个整体 "java orm"，所以这个 query 就是个 suggestion ，不需要再分词单独计算权重。
- 最关键是能够持续学习，随着持续的使用，能够学习到用户的使用习惯。

- ## 前天的推有人问为什么不用 elasticsearch，这是回复，看内存占用，数据量两万。对小应用来说 elasticsearch 太重了。
- https://twitter.com/chloerei/status/1641790933946740738
- 感觉还是 postgres 十项全能
  - 要装分词插件就要自己维护数据库，不能用托管的，这是我不想在 pg 做全文搜索的原因。
- 前段时间看到 supabase 这个产品好像不错，内置了很多扩展在 pg 里
  - 也调研过，还不支持中文分词插件。

- ## [Elasticsearch, the server_201608](https://www.elastic.co/blog/elasticsearch-the-server#_embedded_elasticsearch_not_supported)
- Some users run Elasticsearch as embedded. We are not going to stop them from doing so, but we cannot support it. 
  - Embedding Elasticsearch bypasses the security manager, the Jar Hell checks, the bootstrap checks, and plugin loading. 
  - It is inherently unsafe and not recommended for production. 
  - For the sanity of our developers and support team, we cannot support users who disable all of the safety mechanisms which we have added for good reasons. 

- ## [ElasticSearch in-memory for testing - Stack Overflow](https://stackoverflow.com/questions/31400491)
- As of 2016 embedded elasticsearch is no-longer supported

- ## Who will be the first one to submit an OpenSearch plugin to logstash?
- https://twitter.com/roidelapluie/status/1398678850490535937
- We might fork the other components as necessary, but honestly people should move away from LogStash towards @fluentd or eventually @opentelemetry

- ## [可否完全使用ElasticSearch代替数据库存储？](https://www.zhihu.com/question/45510463/answers/updated)
- 目前公司的项目就是用的es做的数据储存，暂时发现的几个问题： 
  - 无事务，不具备ACID的特性（大概率会出现脏数据的问题） 
  - 非关系型数据库，无法join操作 
  - mapping类型无法修改
  - 如果是为了性能做数据储存完全可以被分库分表替代
- 我之前的项目，业务数据没有用RMDB存储，而是用的Bleve+BoltDB自己搞了个“数据库”。用了有两三年时间吧，写入性能不行，查询性能还行（使用SSD+内存管够的情况下）。但是
  - 没有事务，导致我们需要自己实现保证完整性的代码。
  - 这个“数据库”垂直扩展性不错，但是没有水平扩展能力，不做分库不敢正式上线。
  - 出了问题只能自己解决，没人帮你，因为没人这么搞过。
  - 现在天天悔不该当初。所以，题主，建议你老老实实用业内方案。
- ES是倒排索引，数据库是Btree索引。
  - 所以ES是写入慢，读取快。数据库是写入快，读取慢。
  - 我觉得写入要求高的用redis，不高的全用ES，感觉挺方便的。没有了数据同步流程，爽
