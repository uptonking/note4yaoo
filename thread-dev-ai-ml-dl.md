---
title: thread-dev-ai-ml-dl
tags: [ai, deep-learning, dev, machine-learning, thread]
created: 2021-05-18T19:33:16.251Z
modified: 2021-05-18T19:33:51.768Z
---

# thread-dev-ai-ml-dl

# guide

- read-books
  - [Interpretable Machine Learning_Christoph Molnar](https://christophm.github.io/interpretable-ml-book/)
# discuss
- ## 

- ## 一批 Vector Database 被 ChatGPT 带火了，官方推荐的有以下几个：Pinecone、Weaviate、Redis、Qdrant、Milvus 其实还有 Facebook 的 Faiss。
- https://twitter.com/nash_su/status/1638042474689220609
  - 另外 PostgreSQL 的 pgvector 拓展也可以让 PG 具有向量数据库的能力。
  - ChatGPT Embedding 后的内容相似度查询是用 Cosine算法
- Faiss其实不算database，只是一个索引的lib

- ## 向量数据库或许是好用的，但它本质是针对词或句子的embedding的比较，
- https://twitter.com/realrenmin/status/1638102005909471233
  - 我们在学术工作中已经做过评估，效果比传统的tfidf稍微好一点，但是tfidf可以非常轻量级的本地实现，所以有tradeoff。
  - 如果要引入语义索引，建议用专门的information retrival system (IRS)
- 如果有条件，自己部署一个neural-based IRS到云端，可以稳定高效的帮你完成query-document级别的搜索工作。 
  - 目前表现最强的的nerual irs是我前面推特提到的colbert。大家可以看一下。
- embedding 比tfidf 效果稍好的研究, 请问哪里看到的?
  - 指的是document级别的，我们自己就做过，差不了多少个百分点，事实上，tfidf依然广泛用在工业界，因为它的轻量级。

- ## 个人理解，这波AIGC浪潮，对db而言，向量数据库的地位会被又一次被推高😭
- https://twitter.com/cystokMsk/status/1637977243627704323
  - 因为以后肯定会有各种大模型私有化部署，一串串文本vector就需要存向量数据库里😭客户确实有需求，而且很有钱😭

- 唱反调，究竟有多少客户会强烈需求部署大模型。能部署大模型的用户也可自研
  - tob未来应该不少客户，不是通用大模型，而是专用大模型
  - 取决于成本能做多低吧，需求可能还挺广泛的。fine-tune反正需求很广泛，是不是自己部署不一定，但也可以是。

- 目前很多信息是runtime生成的，但一定会有很多查询或者说向量是重复度很高的，这个时候向量数据库就有用武之地了
- vector 少的话可以直接二进制存现有的 db 或者对象存储，需要时再拉出来在内存暴力计算，vector 多的话还得向量数据库🥲，部署成本有点高。
  - 不太一样的，向量需要相似度计算，就好像在吗，在咩和在不都是类似的语义，都存现有数据库不够用
- vector db主要是推荐系统用的吧，AIGC感觉用不上
  - 配合一下 llamaIndex 就可以用在 AIGC 上了
- 向量数据库可以做中间缓存，可以大大提高推理速度
- 个人觉得aigc这种文本需要的数据库的负载和传统数据库的设计还是挺不一样的，无论是读还是写的模式
- 做 CV 的时候就发现向量数据库可能是个大蓝海

- ## ChatPDF、ChatDoc 之类的服务都有页数限制，
- https://twitter.com/mybeky/status/1638087066130198529
  - 其实很好解决，写个 Python 脚本把每两页合并成一个长页就行了…不够的话对输出文件再执行一次
