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

- ## 

- ## Why are Object Databases not mainstream and we still waste gigawatts of electricity to convert to tables and relations back and forth?
- https://x.com/bercut2000/status/1809141678013387080
- Because modern SQL adopted NOSQL features, we can store and index JSONs in SQLite.

- Normalisation is a core capability of the relational model. The good parts of object databases were integrated in SQL's ORDBMS extensions, just like the good parts of XML and JSON dbs were integrated in SQL/XML and SQL/JSON.

- ## Are there any databases which use S3 / S3 Express One Zone as primary storage?
- https://x.com/iavins/status/1801799034455396669
- TiDB Serverless uses S3 as its primary storage.
  - Are there any details available on you store the pages, indexed and kept it all cost efficient?
- It has a custom LSM implementation., unlike TiKV which uses RocksDB. The SST files are stored on S3.
  - It has a custom LSM implementation., unlike TiKV which uses RocksDB. The SST files are stored on S3.

- @DatabendLabs relies solely on S3 for its primary storage, which means there's no need for tiered storage or intermediate disk caching. 
  - With a stateless query engine that’s production-ready, DatabendLabs is well-equipped to handle both batch processing and streaming data tasks seamlessly.

- EBS is a replicated and scalable system. What is the practical benefit of processing data on/from S3(like why not use directly use EBS)?
  - S3 is cheap for storage, expensive for individual requests. 
  - EBS is expensive to store but cheap for individual requests. 
  - If we did all reads directly from S3 it would be very expensive.
- Makes sense. I am guessing the database runs totally from EBS. Is there a situation where a warmed up database node needs to pull data from S3? I guess compacted files, etc?
  - Starting up a new compute node will initially read from S3, cold start just like any other database. This architecture makes it very easy to startup new compute nodes against S3 and scale compute or other background services. Since it’s a cache and more expensive than S3, we want to keep the minimum amount of data in the EBS cache. Also, the architecture has a distributed file system abstraction at the storage layer. This allows adding any type of caching between S3 and the compute node. Eg., we could write some type of distributed shared memory layer as another cache type to reduce latency further and  reduce the cost by sharing this cache, we don’t do this but it’s possible.

- here it is RisingWave Streaming Database with Yingjun Wu
