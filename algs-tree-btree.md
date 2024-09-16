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
  - couchstore-legacy

- foundationdb
  - v7_202112: First release of the Redwood Storage Engine, a BTree storage engine with higher throughput and lower write amplification than SQLite.

- redis
  - [Redis Internal Data Structure : Skiplist, sds/Simple Dynamic Strings, dictionary, adlist/Doubly Linked List](https://blog.wjin.org/archive.html)
    - Skip List gets O(log n) time complexity on average. And it is easy to implement compared to AVL tree or Red-Black tree. So Redis uses it to implement ordered set.
    - Redis provides SDS because it supports efficient functions to get the string length and append another string to the end without allocating memory each time.
    - dictionary is implemented by means of hash table and there are two hash tables in dictionary to implement incremental rehashing.

- resources
  - [B-Tree Visualization](https://www.cs.usfca.edu/~galles/visualization/BTree.html)
# dev
- https://github.com/postgres/postgres/tree/master/src/backend/access/nbtree /clang
  - This directory contains a correct implementation of Lehman and Yao's
high-concurrency B-tree management algorithm 

# blogs

## [B-trees and database indexes _202409](https://planetscale.com/blog/btrees-and-database-indexes)

- 
- 
- 

### [This piece not only *describes* how B-trees and database indexes work, but gives you the opportunity to interact with them](https://x.com/BenjDicken/status/1833173334953234628)

- 
- 

## [How does B-tree make your queries fast?_202311](https://blog.allegro.tech/2023/11/how-does-btree-make-your-queries-fast.html)

# more
- Hackreels 这个动画效果真不错
  - https://twitter.com/Hooopo/status/1736743804810768784
