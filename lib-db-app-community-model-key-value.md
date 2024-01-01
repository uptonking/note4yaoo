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

- ## 
# discuss-redis
- ## 

- ## 

- ## 

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
