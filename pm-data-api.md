---
title: pm-data-api
tags: [api, data, pm]
created: 2022-08-28T10:28:13.057Z
modified: 2022-08-28T10:28:34.791Z
---

# pm-data-api

# guide

# wikidata
- features
  - 数据国际化
# api

# community

## [维基数据 (Wikidata) 是一个怎样的项目？](https://www.zhihu.com/question/20151850/answers/updated)

- 这个产品的目的是将维基百科大量的信息结构化，增加利用价值。为什么这么做：
  - 结构化的数据便于机器识别，有更高的利用价值；（可以参考为SIRI提供信息的Wolfram Alpha，以及google收购的freebase。
  - 内容结构化需要大量“有序”的数据，维基百科的几千万词条显然能够满足；
  - 内容结构化需要强大的算法支持，但目前的技术方案都不够完美，因此以UGC见长的维基百科就能通过人肉方式搞定；
- 这个玩意不是刚刚开始做，维基百科有一种很常用的模版叫infobox，这个模版就是对词条中的信息做深度挖掘并结构化，维基百科的社区也在有意识地组织用户建设这种结构化内容。
  - 内容的价值除了其本身质量，还有一个重要的指标就是流动性，而内容的流动性主要看其是否能够适应新的媒介。
  - 一本书，在互联网上传播的价值一定比纸张媒介更大。
  - 新的传播媒介大多基于人工智能，而结构化内容恰能很好地提供便于索引计算的素材，这也是内容自身在不断顺应信息行业发展所做的努力。

- Wikidata是一个知识库，但可以看做是一个庞大的知识图谱，并且非常好玩。
  - Wikidata提供有检索服务，可以用SPARQL语句进行各种有意思的查询。
  - Wikidata的图谱中包含的语言有100多种。这个大型的多语言知识库是完全开源的——基于CC0——其中的数据可以自由复制、修改、分发或商用。
- 普通人要把问题翻译成这些SPARQL太难了吧，大概也是因为这个才没有广泛应用
  - 把自然语言翻译成查询语句，这个在智能问答领域做得比较多了。Wikidata如果能加上这个功能就完美了。

- 和其他的维基项目一样，Wikidata 是人人可编辑的。但它又是一个知识库（knowledge base），收录的是结构化数据
- Wikidata 的一个核心概念是 entity，可以指一个现实中的对象或一个抽象概念。
  - 而这个对象或概念可以对应 Wikidata 中的一个 item。比如上图就是一个 item，对应的 entity 是一个现实中的城市（柏林）。
  - 每个 item 都有标签（label）、描述（description）、别名（aliases），使不同的 item 得以区分。
  - item 中的具体数据被称为 statement，一个 item 可以有许多 statement，上图显示的就是其中一条关于人口的 statement。statement 的具体结构图中已经表示的很明白了，由属性（property）、数值（value）、修饰成分（qualifier）、参考资料（reference）等部分组成。每个属性（比如图中的 population）又对应一个专门的属性页。
  - entity 除了可以是 item 外，还可以是 query（查询）。比如可以有一条 query 表示「人口100万以上的城市」，就是一个包含许多符合条件的 item 的搜索结果。
- Wikidata 中的数据以后将会被用于 Wikipedia，另外还可以供第三方研究使用。不过现在 Wikidata 才刚刚正式启动，具体数据内容（statement、query）都还没有，目前的目标是先建立 item（完善各语言的标签、描述、别名的信息），并收集整理与每个 item 对应的各语言 Wikipedia 的条目名称。
