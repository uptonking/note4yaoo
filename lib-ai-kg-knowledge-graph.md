---
title: lib-ai-kg-knowledge-graph
tags: [knowledge-graph, rdf]
created: 2023-02-07T09:22:11.767Z
modified: 2023-02-07T09:23:32.856Z
---

# lib-ai-kg-knowledge-graph

# guide

# blogs

## [知识图谱基础之RDF，RDFS与OWL - 知乎](https://zhuanlan.zhihu.com/p/32122644)

- RDF(Resource Description Framework)，即资源描述框架，其本质是一个数据模型（Data Model）。
  - 它提供了一个统一的标准，用于描述实体/资源。
  - 简单来说，就是表示事物的一种方法和手段。
  - RDF形式上表示为SPO三元组，有时候也称为一条语句（statement），知识图谱中我们也称其为一条知识
- RDF由节点和边组成，节点表示实体/资源、属性，边则表示了实体和实体之间的关系以及实体和属性的关系。
- 如何创建RDF数据集，将其序列化（Serialization）呢？换句话说，就是我们怎么存储和传输RDF数据。
  - 目前，RDF序列化的方式主要有：RDF/XML，N-Triples，Turtle，RDFa，JSON-LD等几种。

- RDF/XML，顾名思义，就是用XML的格式来表示RDF数据。
  - 之所以提出这个方法，是因为XML的技术比较成熟，有许多现成的工具来存储和解析XML。
  - 然而，对于RDF来说，XML的格式太冗长，也不便于阅读，通常我们不会使用这种方式来处理RDF数据。
- N-Triples，即用多个三元组来表示RDF数据集，是最直观的表示方法。
  - 在文件中，每一行表示一个三元组，方便机器解析和处理。
  - 开放领域知识图谱DBpedia通常是用这种格式来发布数据的。
- Turtle, 应该是使用得最多的一种RDF序列化方式了。
  - 它比RDF/XML紧凑，且可读性比N-Triples好。
- RDFa, 即“The Resource Description Framework in Attributes”，是HTML5的一个扩展，在不改变任何显示效果的情况下，让网站构建者能够在页面中标记实体，像人物、地点、时间、评论等等。
  - 也就是说，将RDF数据嵌入到网页中，搜索引擎能够更好的解析非结构化页面，获取一些有用的结构化信息。
  - 可以去这个页面感受一下RDFa，其直观展示了普通用户看到的页面，浏览器看到的页面和搜索引擎解析出来的结构化信息。
  - [RDFa / Play](https://rdfa.info/play/)
- JSON-LD，即“JSON for Linking Data”，用键值对的方式来存储RDF数据。
  - [JSON-LD - JSON for Linking Data](https://json-ld.org/)

- RDFS/OWL本质上是一些预定义词汇（vocabulary）构成的集合，用于对RDF进行类似的类定义及其属性的定义。
  - 通常我们用小写开头的单词或词组来表示属性，大写开头的表示类。

- RDFS，即“Resource Description Framework Schema”，是最基础的模式语言
  - RDFS本质上是RDF词汇的一个扩展。后来人们发现RDFS的表达能力还是相当有限，因此提出了OWL。
  - 我们也可以把OWL当做是RDFS的一个扩展，其添加了额外的预定义词汇。

- OWL，即“Web Ontology Language”，语义网技术栈的核心之一
  - OWL的最新版本是OWL 2，在兼容OWL的基础上添加了新的功能
  - OWL 2包含了三个标准，或者三种配置（Profile），它们是OWL 2完整标准（OWL 2/Full）的一个子集。
# more
- [DDIA 读书笔记（二）：数据模型和查询语言 | 木鸟杂记](https://www.qtmuniao.com/2022/04/16/ddia-reading-chapter2/)
