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
# discuss-btree
- ## 

- ## 

- ## When explaining database B+ trees, so many resources focus solely on keys, but fail to discuss what the actual values are. 
- https://x.com/gunnarmorling/status/1994711292309864667
  - Does the tree store the actual row contents, or only references to rows stored elsewhere?
  - Turns out, it can be both! 
  - Some databases do the former, for instance MySQL with the InnoDB storage engine. The B+ tree _is_ the table in this case, storing the row contents in its leaf nodes.
  - Other databases don't support clustered indexes, e.g. Postgres. Instead, data is laid out sequentially in an array-like structure (the "heap"). In this model, the primary key index is a B+ tree with pointers to row locations on the heap.
  - B+ trees are also used for secondary indexes, allowing you to find data efficiently based on row contents other than the primary key. What's stored in such a secondary index B+ tree differs between the two models: either it's the key of the clustered index, or it's a heap reference.
  - Finally, some databases also support both models. As an example, tables are heap-organized by default in Oracle. But it also lets you create index-organized tables, which essentially is a clustered index.

- In Postgres you can include data in the index
  - Yepp. That's in addition to the data on the heap, though. I.e. you can't have _only_ a B+ tree with the data.
- fair enough ; ) just wanted to note you can avoid going to the heap.

- So true. Many talk about the great O(log N) without realizing that their range scan has to get the rows scattered in a large table, for each index entry, and must do it one after the other if they want to preserve the order

- ## Want to understand B-trees better?
- https://x.com/BenjDicken/status/1986098285875261766
  - Try http://btree.app and http://bplustree.app
  - These are standalone sandboxes of the visuals I built for my "B-trees and database indexes" article.
  - [B-trees and database indexes — PlanetScale](https://planetscale.com/blog/btrees-and-database-indexes)
