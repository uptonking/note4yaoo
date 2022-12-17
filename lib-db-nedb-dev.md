---
title: lib-db-nedb-dev
tags: [database, nedb]
created: 2022-11-27T19:20:09.883Z
modified: 2022-11-27T19:20:24.273Z
---

# lib-db-nedb-dev

# guide

- 基于idb的数据存取不使用字符串，使用arraybuffer
# faq
- 每个索引都包含全量数据？
  - 错误。只会对非空值创建索引

- [How to make a field value is required(not empty)?](https://github.com/louischatriot/nedb/issues/670)

- [The first find function takes time](https://github.com/louischatriot/nedb/issues/621)

- 在已有数据的基础上createIndex然后insert，那么index的数据会保存在数据中间还是最后
  - 提问不明确，执行持久化会先序列化数据，再序列化索引，分析清楚数据结构更重要
  - 索引序列化输出时会放在所有数据的后面
