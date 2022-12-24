---
title: lib-db-nedb-dev
tags: [database, nedb]
created: 2022-11-27T19:20:09.883Z
modified: 2022-11-27T19:20:24.273Z
---

# lib-db-nedb-dev

# guide

# lab
- nedb启动后执行insert/ensureIndex会造成持久化文件中间出现索引行
  - 但每次compact或reload都会压缩持久化文件，都会将索引放在最后，去掉旧的行
# faq
- insert方法插入`_id`相同的对象时，如从序列化字符串中拷贝出对象，能正常插入吗
  - nedb不能正常插入 Can't insert key xxx, it violates the unique constraint

- 每个索引都包含全量数据？
  - 不一定。只会对非空值创建索引
  - [sql server - Will index be fully loaded into memory_201011](https://stackoverflow.com/questions/4296027)
  - No, it's treated like any other data stored on disk. It's loaded into memory disk page by disk page. And a page stays in memory as long as it's regularly accessed.

- [How to make a field value is required(not empty)?](https://github.com/louischatriot/nedb/issues/670)

- [The first find function takes time](https://github.com/louischatriot/nedb/issues/621)

- 在已有数据的基础上createIndex然后insert，那么index的数据会保存在数据中间还是最后
  - 提问不明确，执行持久化会先序列化数据，再序列化索引，分析清楚数据结构更重要
  - 索引序列化输出时会放在所有数据的后面
