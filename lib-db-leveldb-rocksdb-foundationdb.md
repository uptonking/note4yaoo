---
title: lib-db-leveldb-rocksdb-foundationdb
tags: [foundationdb, leveldb, rocksdb]
created: 2024-01-20T15:40:12.559Z
modified: 2024-01-20T15:40:37.064Z
---

# lib-db-leveldb-rocksdb-foundationdb

# guide

# leveldb

# rocksdb

# foundationdb
- pros
  - ?

- cons
  - ?

- features
  - ?

- who is using #foundationdb
  - Deno KV
  - SurrealDB
  - apple icloud
  - snowflake
  - Datadog
  - [Does anybody other than Apple use FoundationDB in production?](https://news.ycombinator.com/item?id=39029351)


- resources
  - ?

- [FoundationDB Architecture](https://apple.github.io/foundationdb/kv-architecture.html)
  - The ssd storage engine stores the data in a `b-tree`. 
  - The memory storage engine stores the data in memory with an append only log that is only read from disk if the process is rebooted.
  - [Architecture — FoundationDB](https://apple.github.io/foundationdb/architecture.html)
    - In the upcoming FoundationDB 7.0 release, the `B-tree` storage engine will be replaced with a brand new `Redwood` engine.
  - [Discussion thread for new storage engine ideas - Development - FoundationDB_201804](https://forums.foundationdb.org/t/discussion-thread-for-new-storage-engine-ideas/101)
    - Currently there are only two storage engines: The main SQLite-based one, and a “toy” one that works only for datasets that fit in memory. 
    - Many interesting ones could be built/integrated, for example, a log-structured engine for spinning disks, a better-optimized b-tree one, or even one that directly used some non-disk remote storage.
    - I’m excited to see Redwood, I also love the design of Bw-tree for both in-memory and disk engine.

## [limitations](https://apple.github.io/foundationdb/known-limitations.html)

- Design limitations: unlikely to change
- Large transactions
  - Transaction size cannot exceed 10, 000, 000 bytes of affected data.
  - Keys, values, and ranges that you write are included as affected data.
  - If any single transaction exceeds one megabyte of affected data, you should modify your design.
- Large keys and values
  - Keys cannot exceed 10, 000 bytes in size. 
  - Values cannot exceed 100, 000 bytes in size
- Key selectors with large offsets are slow
  - The current version of FoundationDB resolves key selectors with large offsets in O(offset) time. 
  - A common misusage of key selectors is using offsets to page through a large range of data (i.e. `reading ‘a’+0 to ‘a’+100`, then `‘a’+100 to ‘a’+200`, etc.)
  - An efficient alternative is to use the limit parameter with range reads, starting subsequent reads at the key after the last one returned.
- Not a security boundary
  - Anyone who can connect to a FoundationDB cluster can read and write every key in the database. 
  - There is no user-level access control. 
  - External protections must be put into place to protect your database.
- Spinning HDDs
  - FoundationDB is only designed for good performance with rotational disk drives when using the durable memory storage engine. 
  - It is not recommended that you run FoundationDB on rotational HDDs when using the ssd storage engine.

- Current limitations: likely to be resolved or mitigated in future
- Long running transactions
  - FoundationDB currently does not support transactions running for over five seconds.
- Cluster size
  - FoundationDB has undergone performance testing and tuning with clusters of up to 500 cores/processes.
- Database size
  - FoundationDB has been tested with databases up to 100 TB (total size of key-value pairs – required disk space will be significantly higher after replication and overhead).
- Limited read load balancing
  - FoundationDB load balances reads across the servers with replicas of the data being read. 
  - If data is accessed exceptionally frequently, an application could avoid this limitation by storing such data in multiple subspaces, effectively increasing its replication factor.

## [changelog](https://github.com/apple/foundationdb/tree/main/documentation/sphinx/source/release-notes)

### [v7.0.0_202112](https://github.com/apple/foundationdb/blob/main/documentation/sphinx/source/release-notes/release-notes-700.rst)

- First release of the Redwood Storage Engine, a BTree storage engine with higher throughput and lower write amplification than SQLite.
- Replaced committed version broadcast through proxy with centralizing live committed versions into master
- Introduced a new role called GRV proxy specialized for serving GRV requests to decrease GRV tail latency since we prioritize commit paths over GRV in the current proxy. 
- Tag-based throttling now also takes the write path into account

### [v6.0.0_201807](https://github.com/apple/foundationdb/blob/main/documentation/sphinx/source/release-notes/release-notes-600.rst)

#### [FoundationDB 6.0.15 Released_201811](https://www.foundationdb.org/blog/foundationdb-6-0-15-released/)

- FoundationDB 6.0.15, our first major release since open sourcing FoundationDB in April, is now officially available

- The FoundationDB 6.0 series features an architectural shift in the approach to cross-region replication, improving how FoundationDB can be managed as a production system
  - New multi-region support within single clusters
  - TLS improved for operational flexibility
  - Faster failure recovery in a number of situations
# more
