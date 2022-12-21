---
title: lib-db-nedb-community-linvodb
tags: [community, linvodb, nedb]
created: 2022-12-17T13:59:53.477Z
modified: 2022-12-17T14:00:22.252Z
---

# lib-db-nedb-community-linvodb

# guide
- doc是单个Model对象

- Yes, you have to set both index/unique in the model or ensureIndex

- 依赖level-js-v2
  - chrome-linux的idb本地位置: ~/.config/google-chrome/Default/IndexedDB/
# roadmap
- full-text-search
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

- ## [[Feature Request] Importing and Exporting · Issue #15 · Ivshti/linvodb3](https://github.com/Ivshti/linvodb3/issues/15)
- For importing you can use the .save method, which allows bulk save, and would account for re-saving (updating) objects, unlike insert which only does new inserts.

- As for exporting, the best approach would be a streaming cursor - which I'll implement, push and document in a little while.

- ## [Any plans to rewrite on ES6?](https://github.com/Ivshti/linvodb3/issues/24)
- I've decided to reimplement almost all things of the project with better decomposition, promises, ES6 and code linting. Check my work in c58/marsdb
  - Indexes is removed, but should be implemented soon, after some storage implementations (just in-memory now)

- Currently linvodb creates indexes for every key individually, on demand, and on queries makes an intersection of results from separate indexes.
- I like that approach very much, but intersections can become expensive. The other option is to put results in a bitmap and XOR / XAND according to the required logic, but that will get ugly quickly when exceeding a million records. 

- I think we need to get some ideas from the original, likely it's open sourced (I mean MongoDB, ofc) :)
Also I found some mongo-like databases, like TingoDB, whose supports indexes, but I don't think it uses some better solution, then intersecting/XORing. (need to be checked)

- MongoDB is also built to do one index lookup for a query. I'm not entirely sure if today it still follows that, but I'm sure it does a lot of scanning if you haven't optimized the queries.
  - 👉🏻 That's why linvodb is entirely scan-less, except of course the first time when indexes are built.
- Maybe some manual intervention should be allowed, but instead of building indexes prematurely, just give them as .hint()'s and then the DB first lookups this index, no matter if compound or not, and then applies XOR/XAND with the other matches for other properties if there are any.

- ## [Preloading db](https://github.com/Ivshti/linvodb3/issues/39)
- It doesn't need .loadDatabase, because the architecture is different
  - storage decides whether to pre-load key/value pairs
  - storage almost certainly preloads keys
  - as for in-memory indexes, they are built on demand

- ## [Benchmarks too bad at the first query](https://github.com/Ivshti/linvodb3/issues/106)
- yeah, that's totally normal
  - the reason for this is that it takes a while to build the index; there's no way around it
  - I guess if you can build the index in advance (rather than using autoIndex), it will be fast on the first query too

- ## [DB cannot be accessed by multiple processes](https://github.com/Ivshti/linvodb3/issues/23)
- linvodb runs over a key/value store as a backend, so it's an issue in the store rather than linvodb itself.
  - Most stores like level and Medea do not allow access from multiple processes, but there may be some store that can - but that brings all kinds of other issues, like keeping the indexes in sync.
- look into medea-clusterify and also multilevel, etc. It seems that a lot of folks are running multiprocess level databases, just takes a little extra configuration. 'level compatible' leaves open a lot of options!
- https://github.com/juliangruber/multilevel
  - Expose a LevelDB over the network

- ## [Persistent Indexes?](https://github.com/Ivshti/linvodb3/issues/35)
- Are there any plans for persistent indexes stored in leveldb?
  - Yep, there are plans for those. However, they cannot be automatic like the in-memory indexes, and to be truly useful, compound indexes must be implemented. But it's a great feature, since it could allow larger datasets and remote access/replication without waste of resource

- currently indexes are created automatically for every looked-up property; if we do this for persistent indexes, the user may accidentally polute everything with indexes

- I didn't realize linvodb3 created an index for each queried property.
- If I understand correctly I'd use {autoindex: false} to turn that off and use Doc.ensureIndex() to explicitly create just the indexes I want.
- they've added support for secondary indexes to PouchDB. 
  - [Secondary indexes have landed in PouchDB_201405](https://pouchdb.com/2014/05/01/secondary-indexes-have-landed-in-pouchdb.html)
- There are also some levelup libs such as juliangruber/level-secondary and eugeneware/jsonquery-engine which implement secondary indexes which could be worth looking at.
  - I'll look forward to seeing you future release with persistent + secondary + compound indexes.

- ## [Database files not deleting?](https://github.com/Ivshti/linvodb3/issues/36)
 
- dbPath may still be used I think because it should be passed as a prefix to the indexeddb keys. Use it to avoid conflicts.

- Do the entries actually stay in the database? Or only on the filesystem?
  - If it's only on the FS, it's pretty normal, as medea won't delete the entries unless you call compact ( can't remember how it was called ).

- ## [is there any way to encryption and decryption](https://github.com/Ivshti/linvodb3/issues/64)
- since linvodb3 is only a middleware, so you can use an encrypted back-end store (key-value store) and you would achieve the goal
  - look for encrypted leveldown stores, as linvodb works with levelup

- I think the most viable option is with encryptdown

- ## [File path does not store or generate anything](https://github.com/Ivshti/linvodb3/issues/68)
- I think using level-js as the store options means that under the hood indexedDB is being used, 
  - so probably you can find the data files somewhere in the default appdata location, on windows that is something like `%APPDATA%/Local/name-of-your-app/UserData/Default/IndexedDb`

- ## [when using level-js , LinvoDB.dbPath setting not work，is that correct？](https://github.com/Ivshti/linvodb3/issues/55)
- path实参 对应于 idb的objectStore名称

- This is absolutely correct behaviour. 
  - Level-js is an abstraction on top of IndexedDB, which does not allow you to change paths. The path here is considered, but on a higher level than an actual path. 
  - If you open the indexeddb inside your browser debugger, you'll see that the values are indeed beginning with the path, but it won't reflect the actual real FS path
