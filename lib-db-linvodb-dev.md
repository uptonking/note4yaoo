---
title: lib-db-linvodb-dev
created: 2022-12-22T15:21:49.223Z
modified: 2022-12-22T15:22:15.191Z
---

# lib-db-linvodb-dev

# guide

- nedb与linvodb的区别
  - nedb是内存优先，dml操作会同时持久化op，也提供了全量持久化的方法
  - linvodb是存储优先，没有全量持久化的方法，所以每个dml操作要持久化，要从代码上确认下❓

- find方法是异步，要放在insert/save的回调函数里面，不能写在顶层或同层

- Yes, you have to set both index/unique in the model or ensureIndex

- 依赖level-js-v2
  - chrome-linux的idb本地位置: `~/.config/google-chrome/Default/IndexedDB/`, 每个domain对应一个本地文件夹，典型的leveldb格式
  - 在idb里面key是_id字符串，value是一个document对象序列化后的字符串，符合leveldb的设计
# roadmap
- fix-tests db.test.ts, Can't insert key **, it violates the unique constraint

- 从callback迁移到async-await

- 合并search-index和linvodb的存储层
  - 非首次启动项目时，如何恢复search-idx的索引

- 迁移 full-text-search
  - 基本思路，textSearch.index + textSearch.query

- 迁移 原仓库功能，如sync/benchmark

- 支持延迟构建索引，而不是在构造函数中

- how to store images

- Mongoose driver for LinvoDB
  - https://github.com/aerys/mongoose-linvodb3
# codebase
- not-yet
  - update是基于insert实现，作者表示wonky ?

- 较大的源码改动
  - 去掉了 construct 事件，因为每个doc对象都是普通js对象，而不是Model对象，与nedb一致

- schema的作用
  - 在初始化Model时，生成构建索引的options

- 从db查找对象时，会先在Model的dml方法中注册ids/data/ready事件，然后在Cursor.getMatchesStream中触发相应的事件
  - 在Cursor.getMatchesStream中触发ids，在Cursor.retriever取完数据触发data
  - data/ready都在ids事件内部
  - 在Model的dml方法中注册ids/data/ready事件
    - cursor.exec中注册了ids/data/ready
  - 在Cursor中触发相应的事件
    - 触发ids
      - 在Cursor.getMatchesStream中Cursor.getIdsForQuery找到ids
      - 在Cursor.getMatchesStream中buildIndexes完成后的回调找到ids
      - 在Cursor.getMatchesStream的最后注册ids事件
    - Cursor.retriever触发data
    - 触发ready
      - 在Cursor.getMatchesStream的参数收到ids
      - 在Cursor.retriever的cb

- ❓ 怪异的执行顺序
  - 代码中update操作然后remove，实际上update操作的cb比remove操作的cb后执行
  - 代码中先 insert>update, 但cb顺序update>insert
  - save方法的callback是在insert-cb和find-cb之后执行的

- 在insert和find的过程中，都有  Cursor.getMatchesStream

- ？ insert只插入了一个对象(是否1次)，但get能返回2个对象
  - 分析错了，上次保存的数据未及时清理

## indexes 索引 avl-tree

- 使用旧版构造函数初始化时传入数据，buildIndexes得到的单节点avl
  - 为什么根节点为空，且高度为2
  - root(data=[])
    - left(null)
    - right(data=key=_id)
      - left=null
      - right=null
# faq
- 为什么使用 bagpipe+async，是否双重异步
  - bagpipe的push方法执行时都是setTimeout

- 如何存储图片，可参考[pr: added support for Buffers (BLOB) to nedb_201408](https://github.com/louischatriot/nedb/pull/167)
  - I think buffers don't have their place in nedb. 
  - There is already a quite simple way to store a BLOB, and that is to serialize it (as your code does in hex format). 
  - Also, buffers are Node only and don't work in node webkit or the browser

- insert方法插入`_id`相同的对象时，如从序列化字符串中拷贝出对象，能正常插入吗
  - nedb不能正常插入 Can't insert key xxx, it violates the unique constraint
  - linvodb未测试
