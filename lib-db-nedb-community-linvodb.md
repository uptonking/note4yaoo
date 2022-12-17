---
title: lib-db-nedb-community-linvodb
tags: [community, linvodb, nedb]
created: 2022-12-17T13:59:53.477Z
modified: 2022-12-17T14:00:22.252Z
---

# lib-db-nedb-community-linvodb

# guide

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
# discuss
- ## 

- ## 

- ## 

- ## [when using level-js , LinvoDB.dbPath setting not work，is that correct？](https://github.com/Ivshti/linvodb3/issues/55)
- This is absolutely correct behaviour. 
  - Level-js is an abstraction on top of IndexedDB, which does not allow you to change paths. The path here is considered, but on a higher level than an actual path. 
  - If you open the indexeddb inside your browser debugger, you'll see that the values are indeed beginning with the path, but it won't reflect the actual real FS path
