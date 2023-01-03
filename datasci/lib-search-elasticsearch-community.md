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

- ## 

- ## 

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
