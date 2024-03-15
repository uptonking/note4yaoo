---
title: lib-db-app-community-model-key-value
tags: [community, database, key-value]
created: 2023-10-26T15:02:34.035Z
modified: 2023-10-26T15:02:47.068Z
---

# lib-db-app-community-model-key-value

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## Cloudflare KV的更新时间大概要5~6秒啊。不知道是不是我用的有问题。
- https://twitter.com/PenngXiao/status/1768595444672905321
- 最终一致性

# discuss-redis
- ## 

- ## 

- ## 

- ## Why is Redis Fast? Redis is fast for in-memory data storage.
- https://twitter.com/sahnlam/status/1766345407045767559
  - Its speed has made it popular for caching, session storage, and real-time analytics.
- RAM-Based Storage
  - Redis primarily uses main memory for storing data. Accessing data from RAM is orders of magnitude faster than from disk. This is a major reason for Redis's speed.
  - To persist data, Redis supports disk snapshots and append-only file logging. This combines RAM's performance with disk's permanence.
  - There is a tradeoff though - recovery from disk is slow. If a Redis instance fails, restarting from disk can be slow compared to failing over to a replica instance fully in memory. So while Redis offers durability via disk, it comes at the cost of slower recovery.
  - A better solution is Redis replication. With a synchronized replica kept in memory, failover is instant with no rehydration. This maintains speed and near-instant recovery.
- IO Multiplexing & Single-threaded Read/Write
  - Redis uses an event-driven, single-threaded model for its core operations. A main event loop handles all client requests and data operations sequentially. 
  - This single-threaded execution avoids context switching and synchronization overhead typical of multi-threaded systems.
  - Redis uses non-blocking I/O to handle multiple connections asynchronously. This allows it to support many client connections with very low overhead, 
  - Redis also uses pipelining for high throughput. Clients pipeline commands without waiting for each response. 
- Redis does leverage threading in certain areas:
  - Background tasks like taking snapshots.
  - I/O threads are used for certain operations.
  - Modules can use threads.
  - Since Redis 6.0, it supports multi-threaded I/O for network communication, improving performance on multi-core systems.
- Redis supports various optimized data structures, from linked lists, zip lists, and skip lists to sets, hashes, and sorted sets, among others. 
  - Each is carefully designed for specific use cases for quick and efficient data access.

- ## Is Redis Data Persistence Useful in Practice?
- https://twitter.com/sahnlam/status/1760552420457980239
  - There are two ways to save Redis data to disk

- AOF (Append-Only File)
  - Unlike a write-ahead log, the Redis AOF log writes after commands run. 
  - Redis runs commands to change the data in memory first. Then it writes the commands to the log file. 
  - AOF logs the commands instead of the data. This simpler design makes recovering data easier. 
  - Additionally, AOF records commands after they have executed in memory. So it does not block current write operations.

- RDB (Redis Database)
  - The limitation of AOF is that it saves commands instead of data. 
  - When we use the AOF log to recover data, the whole log must be scanned. When the log size is large, Redis takes longer to recover. So Redis offers another way to save data - RDB.
  - RDB records snapshots of data at certain times. When the server needs recovery, the data snapshot can load directly into memory for fast recovery.
  - Step 1: The main thread forks the "bgsave" sub-process, which shares all the in-memory data. "bgsave" reads the data from the main thread and writes it to the RDB file.
  - Steps 2 and 3: If the main thread changes data, a copy is created.
  - Steps 4 and 5: The main thread then operates on the copy. Meanwhile, the "bgsave" sub-process continues writing data to the RDB file.

- redis supports BGREWRITEAOF, asynchronously rewrites the append-only file to disk

- ## Apache Kvrocks 在 RocksDB 上建构了一个 Redis 协议兼容的 NoSQL 系统，也实现了 Redis Cluster 兼容的集群方案（底层略有不同）。
- https://twitter.com/tison1096/status/1752177165146403150
  - 存在的最初原因是 Redis on Flash 一直拉胯 .. Kvrocks 也跟部分 Redis Client 系统做过兼容测试，目前有一些非常年轻的 C++ 开发者在做创新发展，不是个固守成规的项目。我 2022 年 mentor 这个项目进 Apache 孵化，去年成为 Apache 顶级项目

- ### 📝 [Apache Kvrocks 毕业随感 | 夜天之书 _20230628](https://www.tisonkun.org/2023/06/28/kvrocks-graduate/)
- Apache Kvrocks 是一个分布式 KV 数据库，使⽤ RocksDB 作为底层存储引擎并兼容 Redis 协议，旨在解决 Redis 内存成本⾼以及容量有限的问题，可以作为 Redis 的持久化变体做 drop-in 替换。
- Kvrocks 起初是美图内部研发的软件，于 2019 年对外开源并独立运营。2022 年 4 月，Kvrocks 在 Champion 陈亮的推动下进入 ASF 孵化器孵化。

- ## Redis is fast for in-memory data storage. 
- https://twitter.com/sahnlam/status/1741705354227163316
  - Its speed has made it popular for caching, session storage, and real-time analytics. But what gives Redis its blazing speed? 
- RAM-Based Storage
  - At its core, Redis primarily uses main memory for storing data. Accessing data from RAM is orders of magnitude faster than from disk. This is a major reason for Redis's speed.
  - However, RAM is volatile. To persist data, Redis supports disk snapshots and append-only file logging. This combines RAM's performance with disk's permanence.
  - There is a tradeoff though - recovery from disk is slow. 
- IO Multiplexing & Single-threaded Read/Write
  - Redis uses an event-driven, single-threaded model for its core operations. A main event loop handles all client requests and data operations sequentially. 
  - This single-threaded execution avoids context switching and synchronization overhead typical of multi-threaded systems.
  - Redis uses non-blocking I/O to handle multiple connections asynchronously. This allows it to support many client connections with very low overhead
- Efficient Data Structures
  - Redis supports various optimized data structures, from linked lists, zip lists, and skip lists to sets, hashes, and sorted sets, among others. Each is carefully designed for specific use cases for quick and efficient data access.

- Threads same as the CPU cores. I believe vertex does something similar.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [What is the best key-value store for Rust 2021 : rust_202201](https://www.reddit.com/r/rust/comments/s1cgof/what_is_the_best_keyvalue_store_for_rust_2021/)
- Depends on what you want to do. If you're solely in memory, use the std lib HashMap. That'll be plenty fast.

- ## 🔥 [What's the big deal about embedded key-value databases? | Hacker News_202208](https://news.ycombinator.com/item?id=32566851)
- 
- 

- ## [FoundationDB's Lesson: A Fast Key-Value Store Is Not Enough | Hacker News_201504](https://news.ycombinator.com/item?id=9306297)
- The underlying organization of a database is not about what can be expressed in theory, it is about what can be expressed efficiently. 
  - Not only is there a very rich set of data structure designs that can be used with varying tradeoffs, but most sophisticated databases use an ecosystem of different, tightly interwoven data structures that smooth over the sharp corners that any single data structure has.
- Efficient expressiveness follows from the relationships directly preserved in the organization. Generally from least-to-most expressive you have:
  - cardinality preserving (hash tables, most KV stores)
  - order preserving (LSM, btree, skiplist, space-filling curves*)
  - space preserving (space decomposition e.g. quad-tree, a zoo of exotics)
- SQL was designed for databases built on order-preserving structures. While you can implement it on a KV store, it will never be as efficient as a database organized in the more expressive organization that SQL assumes.
- KV stores are popular because they are relatively simple to design and implement, not because they are expressive. It is an architectural impedance(阻抗) mismatch to add query functionality that tacitly assumes a more expressive organization. It will never perform well against a database actually organized for the expressiveness of the query layer.
- Any database can only do a few things really well. It is inherent in the tradeoffs. You can add mediocre support for a laundry list of other "good enough" capabilities but you never want to market and position your product around those mediocre capabilities.

- In this case though FoundationDB's KV store was order preserving. The API supported (& efficiently implemented) ranged reads, not just individual get's.
  - Implementing layered architectures always looks good 'on paper' but the details often throw up performance issues that are hard to deal with without punching some holes in the abstractions.

- ## 🔥 [LevelDB: a fast and lightweight key/value database library | Hacker News_201105](https://news.ycombinator.com/item?id=2526032)
- 
- 
- 
