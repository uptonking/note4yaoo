---
title: lib-db-indexeddb-community
tags: [community, indexeddb]
created: 2022-06-13T02:56:38.743Z
modified: 2022-06-13T02:56:51.029Z
---

# lib-db-indexeddb-community

# guide

# discuss-stars
- ## [How to update in indexeddb instead of override all the data?](https://stackoverflow.com/questions/49846187)
- I would point out that calling `put` is not equivalent to SQL update. 
  - When putting a new object into a store, if another object with the same keypath (id) already exists, that existing object will be replaced, entirely. 
  - indexedDB does not modify the existing object in the store, a property at a time, instead it completely replaces the old object with a new object.
- If you want to only replace some properties of an object, use two requests. 
  - One request to get the existing object in the store, 
  - and a second request to store the modified object. 
  - In between the get and put, make changes to the object.
- This behavior forces the dev to consider idb store design carefully. 
  - Imagine wanting to update a single prop with a true/false on 50 objs, each obs has other props with very large strings. 
  - You have to read those large objs out, update your true/false prop and write them back. 
  - This is not efficient.

- ## [Dexie.js: Update nested object via dynamic id](https://stackoverflow.com/questions/69967027)
- You're updating the entire object just to update one entry in an array. 
  - Perhaps it is easier to store each nested object as its own object in an object store? 
  - Then you can add, remove, edit, and reorder as you see fit. 
- You can store the parent object's details redundantly within each subobject. 
  - Store parent id within each child object, then create an index on the parent id, 
  - then do getAll on the child object store using the parent id index to load all of the child objects (and sort).

- ## [Using indexeddb as a versioned database with multiple versions](https://stackoverflow.com/questions/60400573)
- IDB uses versioning as a way to let you change the structure. You can only modify object stores when the version changes.
- So you are barking up the wrong tree here, using versioning as a way of partitioning data. I think your solution of an archive table actually makes much more sense.
# discuss
- ## 

- ## I really can't wait for IndexedDBv3 to come out. V2 is just so damn slow and file storage API is just not widely support enough to use yet
- https://twitter.com/matthew_linkous/status/1749521680198705269
- How will v3 improve performance?
  - Durability hints should allow writes be a lot faster with "relaxed" mode
  - Which actually seems to be already launched everywhere except on Firefox

- ## 如果把 IndexedDB 当成一个 KV 缓存，如何实现过期一个月自动清除呢？ 有什么思路吗？
- https://twitter.com/hamsterbase/status/1679479640753340418
- 可参考支持过期失效的localStorage
- Value头部带过期时间，懒删除+定时删除

- ## [Indexing array values in an object in an IndexedDB - Stack Overflow](https://stackoverflow.com/questions/36921561/indexing-array-values-in-an-object-in-an-indexeddb)
- the missing of the possibility to index object values in arrays, makes using indexedDB really unneeded complicated. It's a failure in design. This forces the developer to do things like in relational DBs, while lacking all the possibilities of SQL. 

- ## [IndexedDB - Is keyPath already an Index? - Stack Overflow](https://stackoverflow.com/questions/31908605/indexeddb-is-keypath-already-an-index)
- It doesn't technically create an index, but it's basically the same thing. 
  - Every object in the database is associated with a key. 
  - If you set a key path, then they key is whatever the key path evaluates to. 
  - Then you can query with for that key (e.g. IDBObjectStore.get), no index needed.
- Indexes only come into play when you want to efficiently query your database for something besides the key.

- ## ios supports indexeddb?
- https://stackoverflow.com/questions/25818860
- To sum up, indexedDB would run on android 4.4+ and iOS8+.
