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
- I would point out that calling put is not equivalent to SQL update. 
  - When putting a new object into a store, if another object with the same keypath (id) already exists, that existing object will be replaced, entirely. indexedDB does not modify the existing object in the store, a property at a time, instead it completely replaces the old object with a new object.
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
