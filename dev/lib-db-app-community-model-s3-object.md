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

# discuss-slatedb-news
- ## 

- ## 

- ## 

- ## SlateDB now has clones _202502
- https://x.com/criccomini/status/1886490144049651867
  - Clone an existing DB's data to a new location. Clones reference the data from the old bucket rather than copying. Writes to the clone update the new location. Compaction merges old data into new directory.

# discuss-s3-tools
- ## 

- ## 

- ## Let's say I have a 1GB+ JSON file on AWS S3 for a day's worth of data.
- https://x.com/arvidkahl/status/1910713079123366065
  - I want to combine these files into per-week, per-month, and per-year files, but I don't want to download, combine, and upload the merged file(s). That feels wasteful.
  - How would you do this economically?

- How’s the data structure of the per day week year file differ from the days worth of data? Is it an aggregate with summary statistics? Or just an append?
  - It's all just JSON arrays, so it would be a big append (but unfortunately not just a file append because of JSON syntax)
- quick tip: use JSONL! You still get the structure of json but you can append!
- Jsonl should be your choice of format because of lower memory usage during processing. Most of the time, you don't need to load the files into the memory.
- you absolutely should use jsonl in the future. But if this is a json array, you can technically still stream parse it, just a bit trickier.
- Actually jor jsonl files it is a file append. Each line is one row.

- compress each file, use jsonl, and use a streaming reader/writer

- 
- 

# discuss
- ## 

- ## 

- ## 

- ## Last year, it was S3 Express One Zone. This year, it’s S3 Tables. These features indicate three key trends:
- https://x.com/YingjunWu/status/1864411659336552753
  - Lakehouses are the new norm. The days of traditional data warehouses are numbered!
  - Apache Iceberg’s leadership in the open table format space has been reaffirmed by a major cloud provider.
  - Every data infrastructure vendor must now seriously consider their Apache Iceberg strategy.

- ## Justin, CTO of Docker, share my post on implementing "Delta Lake" from scratch in a talk at kubecon. "Object Storage Is All You Need"
- https://x.com/eatonphil/status/1857807099851395336
  - [Build a serverless ACID database with this one neat trick (atomic PutIfAbsent) | notes.eatonphil.com _202409](https://notes.eatonphil.com/2024-09-29-build-a-serverless-acid-database-with-this-one-neat-trick.html)

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
