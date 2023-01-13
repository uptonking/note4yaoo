---
title: spec-format-parquet-blogs
tags: [blog, columnar, parquet]
created: 2023-01-13T14:53:11.013Z
modified: 2023-01-13T14:53:39.692Z
---

# spec-format-parquet-blogs

# guide

# blogs

## [一文讲透大数据列存标准格式 - Parquet](https://helloyoubeautifulthing.net/blog/2021/01/03/parquet-format/)

- 列式存储（Column-oriented Storage）是大数据场景面向分析型数据的主流存储方式。
  - 与行式存储相比，列存由于可以只提取部分数据列、同列同质数据拥有更好的编码及压缩方式，因此在 OLAP 场景下能提供更好的 IO 性能。
- Apache Parquet 是由 Twitter 和 Cloudera 最先发起并合作开发的列存项目，也是 2010 年 Google 发表的 Dremel 论文中描述的内部列存格式的开源实现。
  - 和一些传统的列式存储（C-Store、MonetDB 等）系统相比，Dremel/Parquet 最大的贡献是支持嵌套格式数据（Nested Data）的列式存储。
  - Parquet 的设计与计算框架、数据模型以及编程语言无关，可以与任意项目集成，因此应用广泛。目前已经是 Hadoop 大数据生态圈列式存储的事实标准。

- Parquet 采用了一个类似 Google Protobuf 的协议来描述存储数据的 schema。
  - schema 的最上层是 message，里面可以包含一系列字段。每个字段都拥有 3 个属性：重复性（repetition）、类型（type）以及名称（name）。
- 为了使数据能够按列存储，对于一条记录（Record），首先要将其按列（Column）进行拆分。
  - Dremel/Parquet 中，提出以树状层级的形式组织 schema 中的字段（Field），树的叶子结点对应一个原子类型字段，这样这个模型能同时覆盖扁平结构和嵌套结构数据（扁平结构只是嵌套结构的一种特例）。
  - 嵌套字段的完整路径使用简单的点分符号表示，如，contacts. name。
- 列存连续的存储一个字段的值，以便进行高效的编码压缩及快速的读取。

- Parquet 文件格式是自解析的，采用 thrift 格式定义的文件 schema 以及其他元数据信息一起存储在文件的末尾。
# more
- [Why parquet files are my preferred API for bulk open data_201301](https://www.robinlinacre.com/parquet_api/)

- [两种列式存储格式：Parquet和ORC-云社区-华为云](https://bbs.huaweicloud.com/blogs/282511)

- [Parquet 和 ORC：高性能列式存储 - 掘金](https://juejin.cn/post/7135096619543822344)
- [Parquet 与 ORC：高性能列式存储 | 青训营笔记 - 掘金](https://juejin.cn/post/7130640919400808479)
