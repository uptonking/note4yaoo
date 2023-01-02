---
title: lib-search-elasticsearch-dev
tags: [changelog, elasticsearch, search]
created: 2020-03-29T15:38:04.974Z
modified: 2021-05-13T03:18:43.412Z
---

# lib-search-elasticsearch-dev

# faq

- elasticsearch vs solr
  - 当实时建立索引的时候，solr会产生IO阻塞，而es则不会，所以es查询性能要高于solr
  - 在不断动态添加数据的时候，solr的检索效率会变低，而es则没有什么变化
  - 集群中节点发现，solr利用zookeeper进行分布式管理，而es自身带有分布式系统管理功能
  - solr一般部署到web服务器上，比如tomcat，solr的本质是一个动态web项目
  - solr支持更多的格式数据【xml、json、csv】，而es仅支持json文件格式
  - solr是传统搜索应用的有力解决方案，但是es更适合用于新兴的实时搜索应用
  - 单纯对已有数据进行检索的时候，solr效率高，但实时搜索的时候es效率高
  - solr官网提供的功能更多，而es本身更注重于核心功能，高级功能有多个第三方插件
  - ref
    - https://zhuanlan.zhihu.com/p/61257030
# discuss
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

- ## Who will be the first one to submit an OpenSearch plugin to logstash?
- https://twitter.com/roidelapluie/status/1398678850490535937
- We might fork the other components as necessary, but honestly people should move away from LogStash towards @fluentd or eventually @opentelemetry
# docs
- ref
  - https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html
  - https://juejin.im/post/5d921442e51d4578364f6fd3
# changelog
- [license change in 202101](https://www.elastic.co/blog/licensing-change)
  - 7.10及以前采用Apache2, 7.11及以后采用SSPL or ElasticLic
  - We are moving our Apache 2.0-licensed source code in Elasticsearch and Kibana to be dual licensed under Server Side Public License (SSPL) and the Elastic License, giving users the choice of which license to apply.
  - It is similar to those made by many other open source companies over these years, including MongoDB, which developed the SSPL. 
    - The SSPL allows free and unrestricted use, as well as modification, 
    - with the simple requirement that if you provide the product as a service, you must also publicly release any modifications as well as the source code of your management layers under SSPL.
  - ref
    - Our license change is aimed at preventing companies from taking our Elasticsearch and Kibana products and providing them directly as a service without collaborating with us.
    - [license faq](https://www.elastic.co/pricing/faq/licensing)
    - [License Change Clarification](https://www.elastic.co/blog/license-change-clarification)
    - [license change tweet](https://twitter.com/kimchy/status/1351534442993446917)

- changelog
- 7.0.0-201904
  - 7.1开始，Security功能免费使用
  - 集群连接变化：TransportClient被废弃，es7的java代码只能使用rest client，建议采用RestHighLevelClient的方式操作ES集群
  - Zen2是Elasticsearch的全新集群协调层，提高了性能，并更易于使用
  - ES程序包默认打包jdk： 以至于7.x版本的程序包大小突然边300MB+ 对比6.x发现，包大了200MB+， 正是JDK的大小
  - Lucene9.0的支持
  - 正式废除单个索引下多Type的支持，在es7中使用默认的_doc作为type，官方会在8.x版本会彻底移除type
  - 兼容性：es 7.0 can read indices created in version 6.0 or above. 
    - An es 7.0 node will not start in the presence of indices created in a version of es before 6.0.
    - Indices created in es 5.x or before will need to be reindexed with es 6.x in order to be readable by es 7.x.
  - Index creation no longer defaults to five shards
    - Previous versions of Elasticsearch defaulted to creating five shards per index.
    - Starting with 7.0.0, the default is now one shard per index.
  - 查询相关性速度优化：Weak-AND算法，原理是取TOP N结果集，估算命中记录数
- 6.0.0-201708
  - 无缝滚动升级
  - Index sorting，即索引阶段的排序
  - 顺序号的支持，每个es的操作都有一个顺序编号（类似增量设计）
  - Load aware shard routing，基于负载的请求路由，目前的搜索请求是全节点轮询，那么性能最慢的节点往往会造成整体的延迟增加，新的实现方式将基于队列的耗费时间自动调节队列长度，负载高的节点的队列长度将减少，让其他节点分摊更多的压力，搜索和索引都将基于这种机制
  - 已经关闭的索引将也支持replica的自动处理，确保数据可靠
- 5.0.0-201610
  - Lucene 6.x的支持，磁盘空间少一半；索引时间少一半；查询性能提升25%；
  - Internal engine级别移除了用于避免同一文档并发更新的竞争锁，带来15%-20%的性能提升
  - 新增Sliced Scroll类型，现在Scroll接口可以并发来进行数据遍历了。每个Scroll请求，可以分成多个Slice请求
  - 新增了Profile API，新增了Rollover API，新增Reindex
  - 限制索引请求大小，避免大量并发请求压垮 ES
  - 限制单个请求的shards数量，默认1000个
- 2.0.0-201510
  - 增加了pipleline Aggregations
  - query/filter查询合并，都合并到query中，根据不同的上下文执行不同的查询
  - 存储压缩可配置
  - Rivers模块被移除
  - Multicast组播发现被移除，成为一个插件，生产环境必须配置单播地址
- 1.0.0-201402
  - 支持Aggregations聚合分析
  - Snapshot/Restore API 备份恢复API
  - CAT API 支持
  - 支持联盟查询
  - 断路器支持
  - Doc values 引入
- 0.7.0-201005
  - es集群自动发现模块Zen Discovery
  - 简单的插件管理机制
  - 更好支持ICU分词器
  - 更多的管理API
