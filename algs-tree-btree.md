---
title: algs-tree-btree
tags: [algorithms, b-tree, tree]
created: 2023-04-20T08:12:41.106Z
modified: 2023-09-17T18:17:41.377Z
---

# algs-tree-btree

# guide

- who is using #b-tree
  - postgresql
  - sqlite
  - foundationdb
  - loro-crdt
  - bonsaidb/nebari

- who is using #b+tree
  - mongodb
  - couchdb

- foundationdb
  - [FoundationDB Architecture](https://apple.github.io/foundationdb/kv-architecture.html)
  - The ssd storage engine stores the data in a b-tree. 
  - The memory storage engine stores the data in memory with an append only log that is only read from disk if the process is rebooted.
  - [Architecture — FoundationDB](https://apple.github.io/foundationdb/architecture.html)
  - In the upcoming FoundationDB 7.0 release, the B-tree storage engine will be replaced with a brand new Redwood engine.
  - [Discussion thread for new storage engine ideas - Development - FoundationDB_201804](https://forums.foundationdb.org/t/discussion-thread-for-new-storage-engine-ideas/101)
    - Currently there are only two storage engines: The main SQLite-based one, and a “toy” one that works only for datasets that fit in memory. 
    - Many interesting ones could be built/integrated, for example, a log-structured engine for spinning disks, a better-optimized b-tree one, or even one that directly used some non-disk remote storage.
    - I’m excited to see Redwood, I also love the design of Bw-tree for both in-memory and disk engine.

- viz
  - [B-Tree Visualization](https://www.cs.usfca.edu/~galles/visualization/BTree.html)
# dev

# more
- Hackreels 这个动画效果真不错
  - https://twitter.com/Hooopo/status/1736743804810768784
