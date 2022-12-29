---
title: lib-db-linvodb-community
tags: [community, linvodb, nedb]
created: 2022-12-17T13:59:53.477Z
modified: 2022-12-22T15:21:38.253Z
---

# lib-db-linvodb-community

# guide

- roadmap
  - [Remove should lock queries while happening](https://github.com/Ivshti/linvodb3/issues/34)
  - [use sift to drop code from lib/document](https://github.com/Ivshti/linvodb3/issues/30)
  - [Ability to disable in-memory indexes and only use levelup-based compound indexes](https://github.com/Ivshti/linvodb3/issues/18)
  - [`_id` index should just re-use LevelUp index on id, instead of building a separate binary-search-tree](https://github.com/Ivshti/linvodb3/issues/19)
  - [Imposible to save null to date prop like mongoose](https://github.com/Ivshti/linvodb3/issues/102)
# discuss
- ## 

- ## 


- ## [Why cursor is not an EventEmitter?](https://github.com/Ivshti/linvodb3/issues/26)
  - I think it may be useful, especially with live queries. For now, update of one live query invokes handlers of the same collection for other live queries. 
  - It's not good, because any handler can emit a re-render of different parts of the screen or make some hard computations.
- Probably good point. You can PR it. I think if you replace the constructor initialization with an EventEmitter (or extend object with event emitter on init) it would not break anything.
  - BTW, you should keep in mind linvodb emits events for live queries itself

- ## [Is it possible to preload db before quering? Like `nedb.loadDatabase` ?](https://github.com/Ivshti/linvodb3/issues/39)
- It doesn't need .loadDatabase, because the architecture is different
  - storage decides whether to pre-load key/value pairs
  - storage almost certainly preloads keys
  - as for in-memory indexes, they are built on demand
  - if you want to build all your indexes on demand, just specify `index: true` in your model for every queried property

- ## [Store HTML in LimvoDB](https://github.com/Ivshti/linvodb3/issues/44)
  - I want to make something like Sublime Text
  - when editing, all content inside is store in localStorage/IndexedDB/...
- an advantage with linvodb here is that it's abstract to the storage engine, and you can use anything compatible with leveldown
  - This means that localStorage/indexedDB/even raw files are all usable, depending on how the storage performs.
- In the case you're mentioning, I'd recommend being open-minded about storage
  - With LinvoDB, you can create a model called "TempFile" or directly "File" and use that.
  - You can have a `dirtyData` field on your object, which contains the last state of the data; this would be saved very often, like 1s after last keystroke.
  - Then, you can have a function, `flushToDisk()` , which flushes the file to disk when the user actually saves it, and removes dirtyData.
  - The benefit of this design is that you can call `.save()` as often as you want, and keep what the user is typing secure and saved (in localStorage, indexedDB or whatever you want), and call `.flushToDisk()` when the user actually saves to disk

- ## [group by equivalent? · Issue #54 · Ivshti/linvodb3](https://github.com/Ivshti/linvodb3/issues/54)
- You can use .reduce() to do it

```JS
db.reduce(function(cur, obj) {
  cur[obj.category] = cur[obj.category] || [];
  cur[obj.category].push(obj);
}, {})
```

- ## [memory usage of find({}).sort()](https://github.com/Ivshti/linvodb3/issues/65)
- depending on the indexing, it can consume high amounts of memory
- By default, linvodb makes an index for every key.

- ## [Is it normal that Doc.find({}) is that slow ?](https://github.com/Ivshti/linvodb3/issues/52)
- Yes, it would be. Which browser are you testing in? Safari is extremely slow with indexeddb, chrome are faster.

- ## [Specify Field Selection](https://github.com/Ivshti/linvodb3/issues/74)
- the way linvodb3 works is that it takes the objects out of any underlying storage and then JSON.parse-es them
  - this means that even if you want a subset of fields the whole object would still have to be retrieved and then parsed, which defeats the performance benefits
  - I suggest you utilize live queries and aggregation, that way the objects will be really retrieved only once at the loading of the app and afterwards the results will only be hot-updated when necessary
- 
Also if you are running into performance issues you should try changing your back-end store. 

- ## [feat-req: Capped collections](https://github.com/Ivshti/linvodb3/issues/3)
- [Capped Collections — MongoDB Manual](https://www.mongodb.com/docs/manual/core/capped-collections/)
  - Capped collections are fixed-size collections that support high-throughput operations that insert and retrieve documents based on insertion order. 
  - 👉🏻 Capped collections work in a way similar to circular buffers: once a collection fills its allocated space, it makes room for new documents by overwriting the oldest documents in the collection.

- ## [Several live queries whitin one Scheme and live query change?](https://github.com/Ivshti/linvodb3/issues/107)
  - Lets say i have Planets scheme and i have two live quersies one with .limit() and one just returning it all. is it possible?
- even though the API of this module is pretty convenient, the module itself is unfortunately unsupported

- ## [[Feature Request] Importing and Exporting](https://github.com/Ivshti/linvodb3/issues/15)
- LinvoDB itself does not support an API like this, and it doesn't sound like a feature that should be embedded in the DB to me. 
  - One benefit from having it integrated with the DB is to get the mapping in the schema itself - and then use `Model.schema` to translate the import format into JS properties - but that won't require patching LinvoDB itself.

- For importing you can use the `.save` method, which allows bulk save, and would account for re-saving (updating) objects, unlike insert which only does new inserts.

- As for exporting, the best approach would be a streaming cursor - which I'll implement, push and document in a little while.
  - Streaming cursors out in 3.10.0(201507)
  - cursor.stream(function(d) { /* document */ }, function(err, res) { /* query is finished, you can still use res */ }); 

- I agree that import/export should not be embedded into the DB, as tools like `mysqlimport`,  `mongoimport` are also external utility tools. Looks like having a separate utility tool is more appropriate.

- ## [linvodb: Any plans to rewrite on ES6? Check my work in c58/marsdb_201509](https://github.com/Ivshti/linvodb3/issues/24)
- I've decided to reimplement almost all things of the project with better decomposition, promises, ES6 and code linting. 
  - Indexes is removed, but should be implemented soon, after some storage implementations (just in-memory now)

- I was thinking of ways to do indexes better. 
  - Currently linvodb creates indexes for every key individually, on demand, and on queries makes an intersection of results from separate indexes.
- I like that approach very much, but intersections can become expensive. 
  - The other option is to put results in a bitmap and XOR/XAND according to the required logic, but that will get ugly quickly when exceeding a million records. 
- The other option is using compound indexes, but that can also get ugly quickly with many queries and etc. 
  - Maybe the DB can make compound indexes only in certain conditions and re-use them for several different queries, but I'm reluctant of trying to make a DB engine "smart". It's not a sustainable approach.
- Thinking to other DB engines, embedded or not, relational or not, I cannot think of a solution to this problem. Maybe Postgres / some MySQL storage engines have the answer within them, but unfortunately I do not have enough knowledge on the matter.

- I think we need to get some ideas from the original, likely it's open sourced (I mean MongoDB, ofc) :)
  - Also I found some mongo-like databases, like TingoDB, whose supports indexes, but I don't think it uses some better solution, then intersecting/XORing. (need to be checked)

- That's exactly the issue, the original doesn't solve the problem at all. 
  - 👉🏻 It relies on you to make your own indexes, which is totally ok, but then it picks which indexes to use in a totally mindless way - if you have a lot of indexes. 
  - Which leads to having to use `.hint()`, which kind of removes the whole advantage of it's promised ease of use. 
  - You can optimize queries greatly with .hint(), but if you have a more dynamic query (e.g. not always on the same properties), then you have to be smart about hints.
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

- Think I was wrong. It seems that a Key Value pair with an ID and a key get returned on each refresh only if I create an intended new entry before the refresh and it's inconsistent, it does not always happen. I hope I'm explaining well enough. Could create a small video with an example if you want to.
  - The results themselves are not returned by the find({}), but they're in Resources > IDBWrapper.

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
