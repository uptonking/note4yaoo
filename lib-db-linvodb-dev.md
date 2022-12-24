---
title: lib-db-linvodb-dev
created: 2022-12-22T15:21:49.223Z
modified: 2022-12-22T15:22:15.191Z
---

# lib-db-linvodb-dev

# guide

- nedb与linvodb的区别
  - nedb是内存优先，dml操作会同时持久化op，也提供了全量持久化的方法
  - linvodb是存储优先，没有全量持久化的方法，所以dml操作要持久化，要从代码上确认下❓

- find方法是异步，要放在insert/save的回调函数里面，不能写在顶层或同层

- Yes, you have to set both index/unique in the model or ensureIndex

- 依赖level-js-v2
  - chrome-linux的idb本地位置: ~/.config/google-chrome/Default/IndexedDB/
  - 在idb里面key是_id字符串，value是一个document对象序列化后的字符串，符合leveldb的设计
# roadmap
- full-text-search
# codebase

- 在insert和find的过程中，都有  Cursor.getMatchesStream

- 

- save方法的callback是在insert-cb和find-cb之后执行的

## indexes 索引avl-tree
- 使用旧版构造函数初始化时传入数据，buildIndexes得到的单节点avl
  - 为什么根节点为空，且高度为2
  - root(data=[])
    - left(null)
    - right(data=key=_id)
      - left=null
      - right=null



## crud

- insert方法插入`_id`相同的对象时，如从序列化字符串中拷贝出对象，能正常插入吗
  - nedb不能正常插入 Can't insert key xxx, it violates the unique constraint
  - linvodb未测试
# not-yet

- 为什么使用 bagpipe+async，是否双重异步
  - bagpipe的push方法执行时都是setTimeout


- ## 4个测试用例未通过
- TypeError: db is not a function
  - Cursor: "before each" hook for "Without query, an empty query or a simple query and no skip or limit":
  - Database: "before each" hook for "Able to insert a document in the database, setting an _id if none provided, and retrieve it even after a reload"
  - Schema: "before each" hook for "Create indexes specified in schema, auto-indexing does not override them"
- AssertionError: expected [Function] to throw an error
  - Document - Modifying documents: Throw an error if a modifier is used with a non-object argument
# issues
- ## [`_id` index should just re-use LevelUp index on id, instead of building a separate binary-search-tree](https://github.com/Ivshti/linvodb3/issues/19)

- ## [A doc can be written to index w/o being saved](https://github.com/Ivshti/linvodb3/issues/16)
  - The way to fix this is actually simple
  - Upon the _persist function, write to a cache saving[]. When the doc is committed to levelup, delete it from that cache.
  - Modify cursor.getMatchesStream to use this cache if the doc is there

- ## [use sift to drop code from lib/document](https://github.com/Ivshti/linvodb3/issues/30)
