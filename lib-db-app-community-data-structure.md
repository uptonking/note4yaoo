---
title: lib-db-app-community-data-structure
tags: [b-tree, community, data-structure, database, LSM-Tree]
created: 2023-09-17T17:44:07.206Z
modified: 2023-09-17T18:17:41.377Z
---

# lib-db-app-community-data-structure

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-lsm-tree
- ## 

- ## 

- ## 

- ## 
# discuss-b-tree
- ## 

- ## 

- ## 

- ## 

- ## This document from ScyllaDB makes a strong case why B-trees make a good choice for in-memory collections as well
- https://twitter.com/debasishg/status/1688551567044251648
  - B-trees are usually used for disk based storage. 
  - [The Taming(驯服) of the B-Trees - ScyllaDB](https://www.scylladb.com/2021/11/23/the-taming-of-the-b-trees/)
- Also TIL: Google has implemented a C++ template library that implements B-tree containers with an analogous interface to the standard STL map, set, multimap, and multiset containers
- I tested several B-tree implementations on the JVM in https://github.com/szeiger/forest/tree/master/main/src/main/scala/forest/mutable. 
  - I don't remember the exact benchmark results but there was no conclusive case to use them instead of the red-black trees in Scala's TreeMaps.

- Obvious in retrospect, but I just realized that if you use prolly trees for your DB indices, you can run queries against any historical state of your DB (by simply not GC'ing old data). And in fact, @DoltHub supports that
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 今天发现 在 DB 里面对于 时间/空间或者多维的数据操作 , 用 R tree 来减少工作量似乎是个冷知识了.
- https://twitter.com/fuergaosi/status/1658470145109680132
- 已经见过好几次有老哥为了计算时间区间, 把数据拉到内存里面 For loop 计算了
- 当年 LBS 跟现在的 AIGC 一样火的时候，R tree 都可以写到简历上来吹牛逼了。
