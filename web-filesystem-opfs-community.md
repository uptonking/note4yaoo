---
title: web-filesystem-opfs-community
tags: [community, opfs]
created: 2023-01-13T10:47:22.203Z
modified: 2023-01-13T10:47:36.755Z
---

# web-filesystem-opfs-community




# guide

# discuss

- ## 

- ## 

- ## 

- ## 

- ## Do you know what persistence is like in Chrome? 
- https://twitter.com/tomayac/status/1613605318407094275
  - Say my website dumps 1 GB of data in an OPFS SQLite database. Does that get persisted similar to IndexedDB? Like will it get evicted(驱逐，赶出) due to low disk space, or deleted if the user clears their browser cache?
- When it hits your origin, _all_ quota-managed storage mechanisms get purged. The way if it hits your origin gets decided is by looking at all quota-managed storage mechanisms of all origins and then purging by LRU.
  - Quota-managed storage mechanisms are: cache storage, IDB, service worker, media license, OPFS, Web SQL (the last is of course soon history).
- The library uses the OPFS, the origin private file system, and requires a web worker context.
- 
- 
- 

