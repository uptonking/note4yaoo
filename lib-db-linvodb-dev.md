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

- Yes, you have to set both index/unique in the model or ensureIndex

- 依赖level-js-v2
  - chrome-linux的idb本地位置: ~/.config/google-chrome/Default/IndexedDB/
# roadmap
- full-text-search
# codebase
- 为什么使用 bagpipe+async，是否双重异步
# not-yet
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
