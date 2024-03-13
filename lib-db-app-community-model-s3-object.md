---
title: lib-db-app-community-model-s3-object
tags: [aws-s3, comunity, database, object-storage]
created: 2024-03-13T14:25:51.906Z
modified: 2024-03-13T14:26:26.220Z
---

# lib-db-app-community-model-s3-object

# guide

# discuss-stars
- ## 

- ## 

- ## 💡🆚️ Can anyone recommend something on the 'why' of object stores like S3? 
- https://twitter.com/LewisCTech/status/1767676201961922762
- The invariants imposed by a filesystem structure (graph) are very hard to maintain in a massively parallel/distributed system, compared to an ordered key space pointing to blobs.
  - OK I kind of get 'why not a file system'. But I don't understand 'why not a key value store'.
- I'm not sure I understand what distinction you're drawing between a key value store and an object store.
  - Implementations are going to be pretty different here for those. K/V is small objects with a spectrum of different R/W access patterns and possibly multi-key atomicity/transactions. Also probably geared toward low latency. 
  - Object storage is mostly create and read. Large objects
- 🆚️ I would say they are both key-value stores w/ diff performance tuning for the values. 
  - The assumption w/ object storage is the values may be v large, and shouldn't have any structure imposed on them (i.e., they are blobs). 
  - DB-like KV has structure, size limits, and low latency
  - DB-like KV has low latency and additional access patterns (like indexes) gained by imposing structure and size limits
- how does that translate to disk storage? the key data structures for KV stores are LSM Trees and B+ Trees. What are they for object stores?
  - Why does that matter for users of these services?

# discuss
- ## 

- ## 
