---
title: lib-db-pouch-couch-blog
tags: [blog, couchbase, couchdb]
created: 2024-01-04T06:21:43.569Z
modified: 2024-01-04T06:34:57.448Z
---

# lib-db-pouch-couch-blog

# guide

- resources
  - [couchdb blog](https://blog.couchdb.org/)
# blogs-couch-internals

## 📕 [ForestDB - Boosting Compaction in B-Tree Based Key-Value Store by Exploiting Parallel Reads in Flash SSDs_202104](https://www.researchgate.net/publication/350825598_Boosting_Compaction_in_B-Tree_Based_Key-Value_Store_by_Exploiting_Parallel_Reads_in_Flash_SSDs)

- Append-only B-tree based key-value stores provide superior search and update performance based on their structural characteristics; 
  - however, they periodically require the compaction task that incurs significant I/O overhead. 
- In this paper, we present that the compaction’s degraded(降低…质量；使恶化) read performance deteriorates(变坏；变质；恶化) the overall performance in ForestDB, a representative append-only B-tree engine.
- this paper proposes a novel compaction method that improves the compaction’s read performance by exploiting SSD’s internal parallelism by requesting multiple read operations in a batch using the asynchronous I/O technique.

## 📕 [ForestDB: A Fast Key-Value Storage System for Variable-Length String Keys_201501](https://www.researchgate.net/publication/277950163_ForestDB_A_Fast_Key-Value_Storage_System_for_Variable-Length_String_Keys)

- https://github.com/couchbase/forestdb /201904/cpp/inactive

- ForestDB uses a new hybrid indexing scheme called HB+-trie, which is a disk-based trie-like structure combined with B+-trees. It allows for efficient indexing and retrieval of arbitrary length string keys with relatively low disk accesses over tree-like structures
- Our evaluation results show that ForestDB significantly outperforms the current key-value storage engine of Couchbase Server, LevelDB, and RocksDB, in terms of both the number of operations per second and the amount of disk writes per update operation

## 📕 [Couchbase Under the Hood](https://info.couchbase.com/rs/302-GJY-034/images/Couchbase_Under_The_Hood_WP.pdf)

- The original multi-model NoSQL database Couchbase was originally founded through the merger of two open source database companies, CouchOne and Membase.
  - CouchOne employed developers of Apache CouchDB, an original, highly-reliable, document database, while Membase employed developers of memcached, a high- performance, memory-first, key-value database. 
  - The merger of these teams led to the design of Couchbase, a reliable, scalable, fast in-memory, key-value database with document-based access and storage. 
  - In this model, document identification “keys” store “value” data as a JSON document. 
- Couchbase was the first of its kind, dual model access database, setting the standard for advancing consolidation(联合或合并) of single-access NoSQL datastores. 
  - Couchbase further distanced itself from its origin sources by adding support for SQL++ (aka N1QL) as its primary query language.

- Couchbase is a pioneer in offering multiple data access methods to gain, read, and update access to its foundational JSON and Key/Value storage structures. 
  - This type of NoSQL database is referred to as “multimodel” because many NoSQL systems have only one access method which is bound to their physical storage design structures on disk to minimize access latency.
- While many developers may confuse the two, Couchbase and CouchDB are not the same

- Couchbase has also introduced a new storage engine format which is defined as buckets are created
- Magma combines the performance of a log-structured merge trees (LSM) with the compaction, reorganizability, and immutability of sorted string tables (SSTables) to provide a high performance in a well organized, low latency engine that suits write-heavy, low latency point lookup workloads. 
  - This design minimizes disk space increases, called “storage amplifications, ” and the accompanying complexity which occurs when documents are heavily mutated without being reorganized.

## 📕🌲 [Magma: a high data density storage engine used in couchbase: Proceedings of the VLDB Endowment_202208](https://dl.acm.org/doi/abs/10.14778/3554821.3554839)

- https://github.com/couchbase/kv_engine/tree/master/engines/ep/src/kvstore/magma-kvstore /BSL/202312/cpp

- Our current generation storage engine, Couchstore is based on a log-structured append-only copy-on-write B+Tree architecture. To make substantial improvements to support higher data density and write throughput, we needed a storage engine architecture that lowers write amplification and avoids compaction operations that rewrite the whole database files periodically.
- We introduce Magma, a hybrid key-value storage engine that combines LSM Trees and a segmented log approach from log-structured file systems. 
  - We present a novel approach to performing garbage collection of stale document versions avoiding index lookup during log segment compaction. 
  - This is the key to achieving storage efficiency for Magma and eliminates the need for random I/Os during compaction. 
  - Magma offers significantly lower write amplification, scalable incremental compaction, and lower space amplification while not regressing the read amplification. 
  - Through the efficiency improvements, we improved the single machine data density supported by the Couchbase Server by 3.3x and lowered the memory requirement by 10x, thereby reducing the total cost of ownership up to 10x. 
  - Our evaluation results show that Magma outperforms Couchstore and RocksDB in write-heavy workloads.

- Couchstore is the current generation storage engine of Couchbase Server for document storage.
  - The overall architecture inherits from the storage model of Apache CouchDB
  - This storage engine is battle-hardened in production and has been serving Couchbase customers for almost 10 years. 
- Couchstore is based on copy-on-write (COW) B+Tree and it follows a log-structured append-only storage model. Each vBucket maintains a couchstore file and stores the documents belonging to the vBucket
  - A copy-on-write B+Tree is an adaptation of B+Tree for the log-structured storage model. 
  - Compared to update in-place B+trees, the COW B+Trees can achieve higher write throughput as it performs writes in a sequential access pattern

- LSM Tree is a write-optimized persistent index data structure. 
  - LSM Trees achieve high write throughput by utilizing superior sequential write bandwidth of SSDs and spinning disks compared to the random I/O access pattern. 
  - The large sequential writes are achieved by batching a large number of mutations in memory before writing the index structure. 
  - LSM Trees is a hierarchical data structure that consists of a memory component and multiple levels of persistent immutable index components. 
  - For the persistent components, it uses the append-only B+Tree index. The on-disk components are organized as levels with exponentially increasing sizes.

- Magma is the next-generation single node document storage engine of Couchbase Server designed for improving write performance and data density per node.
  - The core idea is to separate index and document data to minimize write amplification. 
  - Magma also builds a scalable and incremental compaction method to maintain stable space amplification.

- The idea of separating key and value for LSM Tree based key-value store has been proposed by Wisckey

- Finally, we compare and evaluate the performance of Magma through microbenchmarks and YCSB full system tests to demonstrate that it outperforms other engines in write-heavy workloads.

## [Magma, a new storage engine for Couchbase_202209](https://smalldatum.blogspot.com/2022/09/magma-new-storage-engine-for-couchbase.html)

- Many years ago I sat next to a Couchbase exec at a VLDB event and was explained on how awesome their new storage engine was especially when compared to RocksDB. That new engine was based on ForestDB and while the idea was interesting the engine was never finished. 
- At last, Couchbase has a new storage named Magma. 
  - The rest of this post explains Magma based on the paper and a few other posts. 
  - The Magma engine is an example of the index+log index structure and looks like a great upgrade from the previous engine (Couchstore).
- Magma should eventually replace Couchstore as the Couchbase storage engine. 
- Couchstore is a copy-on-write B-Tree (CoW-S). Compaction (GC) for Couchstore is single-threaded and not incremental (a database file is read & fully rewritten). 
  - Couchstore does not do block compression. Couchstore writes are done by appending the modified pages (from leaf to root) to the end of the database file. That is a lot of write-amp.

- A summary of the implementation:
  - writes are persisted to a WAL and then added to the write cache. I assume each document gets a unique seqno at that time.
  - the write cache (RocksDB memtable) buffers KV pairs with 2 skiplists. 
    - The paper first describes them as the active and immutable lists. Later it states one skiplist orders by PK and the other by seqno. I believe the later description. When full the documents are appended to the tail of the open log segment and the (key,seqno, doc size) tuples are flushed to the LSM index.
  - an LSM tree index stores (key, seqno, doc size) tuples to map a document PK to a seqno
  - the Log Structured Object Store is composed of log segments. Per-segment metadata includes the min and max seqno in that segment and the seqno values do not overlap between segments.
  - there is a document cache and index block cache. The index block cache caches blocks from the LSM index and from the per-segment B-tree indexes. 

- 👥 [Magma, a new storage engine for Couchbase | Hacker News_202210](https://news.ycombinator.com/item?id=33048469)
  - > Modern RocksDB also has an option to do key-value separation via Integrated BlobDB.
  - The gist(主旨；要点) being, as I understand it, that WiscKey showed how you can improve both read and write performance if you store values outside of the main LSM tree. (Only store keys in the LSM tree with a pointer to the value.)

## [Magma Storage Engine: Couchstore and Magma Comparison_202210](https://www.couchbase.com/blog/magma-next-gen-document-storage-engine/)

- The Couchbase database platform supports two storage mechanisms: Couchstore, the default, and Magma, the recently released engine.

- Couchstore is a mature storage engine that is optimized for high performance with large datasets, particularly ones that can fit in memory. 
  - The minimum bucket size for Couchstore is 100MB. 
  - It’s ideal for caching use cases and situations where data compression is not a primary deciding factor. 
- Magma is a new storage engine that is designed to be highly performant even with very large datasets that do not fit in memory.
  - Magma is optimized to run on very low amounts of memory even with very large datasets

- The performance evaluation results showed that Magma outperformed both Couchstore and RocksDB engines in write-heavy YCSB workloads with datasets that were too large for memory.

## [CouchDB on ZFS_201006](https://letsgetdugg.com/2010/06/25/couchdb-on-zfs/)

- CouchDB was made for next generation filesystems such as ZFS and BTRFS. 
  - First off, unlike PostgreSQL or MySQL, CouchDB can be snapshot while in production without any flushing or locking trickery since it uses an append only B-Tree storage approach. That alone makes it a compelling database choice on ZFS/BTRFS.
  - Second, CouchDB works hand-in-hand with ZFS’s block level compression. ZFS can compress blocks of data as they are being written out to the disk. However, it only does it for new blocks and not retroactively. Now, the awesome part, CouchDB on compaction writes out a brand new database file which can utilize the new gzip compression settings on ZFS. This means you can try out different gzip compression settings just by compacting your CouchDB.
# blogs-couchdb

## [10 Common Misconceptions about Apache CouchDB - Speaker Deck_201311](https://speakerdeck.com/wohali/10-common-misconceptions-about-apache-couchdb)

### [Another 10 Common Misconceptions about Apache CouchDB - Speaker Deck_201809](https://speakerdeck.com/wohali/another-10-common-misconceptions-about-apache-couchdb)

## [Upscaling LinkedIn's Profile Datastore While Reducing Costs | LinkedIn Engineering_202305](https://engineering.linkedin.com/blog/2023/upscaling-profile-datastore-while-reducing-costs)

- Instead, we chose to introduce Couchbase as a centralized storage tier cache for read scaling. 
  - This solution achieved a cache hit rate of over 99%, reduced tail latencies by more than 60%, and trimmed the cost to serve by 10% annually. 

### [How LinkedIn Serves 5 Million User Profiles per Second](https://blog.quastor.org/p/linkedin-serves-5-million-user-profiles-per-second)

- Couchbase is a combination of ideas from Membase and CouchDB, where you have the highly scalable caching layer of Membase and the flexible data model of CouchDB.
  - It’s both a key/value store and a document store, so you can perform Create/Read/Update/Delete (CRUD) operations using the simple API of a key/value store (add, set, get, etc.) but the value can be represented as a JSON document.
  - With this, you can access your data with the primary key (like you would with a key/value store), or you can use N1QL (pronounced nickel). This is an SQL-like query language for Couchbase that allows you to retrieve your data arbitrarily and also do joins and aggregation.

## 🆚️ [Couchbase vs. MongoDB: NoSQL Misconceptions Part 1 - What about SQL?_202206](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-1/)

- [Couchbase vs. MongoDB: Part 2 - Is Couchbase just a Key-Value Store? _202206](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-2/)
- [Is NoSQL Database Secure? Couchbase vs. MongoDB (Part 3)_202207](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-3/)
- [Are NoSQL Databases Scalable? Couchbase vs. MongoDB (Part 4)_202207](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-4/)
- [Memory Usage in Databases: Buffering & Caching (Part 5)_202207](https://www.couchbase.com/blog/couchbase-mongodb-nosql-misconceptions-5/)

- [NoSQL Document Database Replication - MongoDB vs. Couchbase_202003](https://www.couchbase.com/blog/replication-in-nosql-document-databases-mongo-db-vs-couchbase/)

## 🆚️ [CouchDB and MongoDB Compared](https://www.mongodb.com/compare/couchdb-vs-mongodb)

- Although MongoDB and CouchDB share a similar concept of a document-oriented database, there are some key advantages to MongoDB over CouchDB technology as well as some key differences we should address.

- MongoDB is a document database built for general-purpose usage. 
  - It stores data in an optimized JSON format called BSON (Binary JSON). 
    - This allows the MongoDB document model to benefit from the flexibility of JSON documents stored in logical groups called collections. 
    - The document model supports many different data types, including strings, dates, numbers, arrays, decimals, nested objects, geo data, and binary data.
  - MongoDB uses replication and data partitioning called sharding to distribute data for high availability and scalability purposes
  - Additionally, MongoDB Enterprise and MongoDB Atlas offer enterprise-grade security features like authentication, authorization, and LDAP support as well as end-to-end encryption.

- CouchDB is a NoSQL document-oriented database implemented in Erlang. 
  - CouchDB documents are JSON-based and stored in databases. 
  - The database software can be installed as a single instance or a cluster of instances for durability and high availability. 
    - CouchDB’s overall design favors availability over consistency, and is considered eventually consistent in many read scenarios.
  - CouchDB is designed on the concept of “optimistic concurrency, ” which places an added burden on the application for handling data consistency. 
  - The query system does not lock database objects on writes, meaning any conflict resolution or locking mechanisms for consistency need to be implemented by the application developer.
  - CouchDB uses an HTTP Rest API to perform database access and document manipulation, rather than native drivers using a unified query language like many other modern databases. It supports basic types of authentication like session cookies/users and TLS/SSL for the Rest API traffic.

- comparison table
- Data Model
  - couchdb data formats are limited to: strings, numbers, arrays, objects, boolean.
  - mongodb: strings, numbers, geo data, dates, arrays, decimal, nested objects, binary data.
- Indexing
  - couchdb: Indexing of documents is limited. For some workloads, indexing requires a special “Design Document” definition.
  - mongodb: Secondary indexes on any field are available and supported in different types: Compound, Text, Geo, TTL
- Query Language
  - couchdb: If you require more complex queries, you will need to use views and map-reduce aggregations to filter and query your documents.
- Transactions
  - 😩 CouchDB does not support transactions.
- Concurrency
  - CouchDB is eventually consistent and uses optimistic locking as part of its database operations. Write operations do not lock database objects and conflict errors need to be resolved by the application developer.
  - MongoDB uses document level locking so writes to a single document occur either in full or not at all, and clients always see consistent data.
  - MongoDB supports different read and write concerns for distributed clusters and retryable reads and writes.
- High Availability and Scalability
  - CouchDB supports a concept of a replication factor as well as a sharding setting on a global or per database basis.
  - MongoDB was built from the ground up to support distribution of data using replication and sharding mechanisms. Replica sets host an identical copy of the data and elect a primary which receives all the writes, while other nodes are secondaries replicating all the data. Sharding allows you to easily scale your collections across multiple replica sets.
- Security
  - CouchDB security is built for simple website backend requirements
  - mongodb: Authentication and authorization using built-in SCRAM or certificates
- Mobile Support
  - PouchDB: Conflict resolution needs to be solved by the developer.
  - Realm is a lightweight reactive object-store designed to work seamlessly with mobile frameworks.

## 🆚️ [Couchbase vs CouchDB NoSQL Systems: Difference Between Them](https://www.couchbase.com/comparing-couchbase-vs-couchdb/)

- both use Append-only B-Tree

- couchbase supports SQL++ (SQL for JSON)	
  - couchdb uses a limited find API derived from MongoDB

## 🆚️🛋️🌵 [Persistent Trees in git, Clojure and CouchDB_200912](https://eclipsesource.com/blogs/2009/12/13/persistent-trees-in-git-clojure-and-couchdb-data-structure-convergence/)

- Immutable, recycling trees
  - All three systems have these immutable trees in some way way or form that allow sharing structure. 
  - In git these are tree objects, in Clojure they are called persistent data structures, and in CouchDB they are part of the internal index tree.
- Mutable references
  - To allow for changes in an otherwise immutable world, all systems allow for mutable reference constructs. 
  - All change is encapsulated in these references, which are called exactly that in both git and Clojure. 
  - In CouchDB the story is a little different. Here the “reference” to the latest tree is simply the end of the database file
# more
- [Pragmatic Programming Techniques: CouchDB Implementation_200810](https://horicky.blogspot.com/2008/10/couchdb-implementation.html)

- [Database Deep Dives: CouchDB - IBM Blog_201907](https://www.ibm.com/blog/database-deep-dives-couchdb/)
