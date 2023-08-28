---
title: algs-data-structure-catalog
tags: [algorithms, data-structure]
created: 2020-12-20T15:20:40.311Z
modified: 2020-12-20T15:27:57.656Z
---

# algs-data-structure-catalog

# guide

# list

# map

# tree

# string
- [xi-editor: Rope science - Introduction](https://xi-editor.io/docs/rope_science_00.html)

- [Fleet: Data Structures in the Fleet Editor | Hacker News](https://news.ycombinator.com/item?id=30415868)
  - [Fleet Below Deck, Part II – Breaking down the editor: Ropes everywhere](https://blog.jetbrains.com/fleet/2022/02/fleet-below-deck-part-ii-breaking-down-the-editor/)
# patterns-for-data-structure
- https://github.com/tnfe/limu /ts
  - https://tnfe.github.io/limu
  - A fast immutable data js lib, based on shallow copy on read and mark modified on write mechanism
  - No freeze by default, faster than immer in different situations.
  - 默认支持Map、Set，兼容immer大部分接口
  - 更强的隐藏式代理机制，让用户像查看原生数据一样查看草稿数据任意节点
  - only run on JavaScript runtime that supports proxy

- https://github.com/Conaclos/cow-list /ts
  - Cow List provides a Copy-On-Write iterable list that supports logarithmic searches. 
  - It provides also a mutable iterable List with versioning capabilities.
  - Cow List naively supports lengthy values (objects with a length property). 
  - This makes Cow List a perfect fit to implement a `rope`.
  - Cow List uses a **partially persistent AVL tree**. This could change in the future in order to achieve better performances.

- https://github.com/RReverser/cow-utils-rs
  - Copy-on-write string utilities for Rust

- https://github.com/penberg/tihku /rust
  - Tihku is an work-in-progress, open-source implementation of the Hekaton multi-version concurrency control (MVCC) written in Rust. 
  - The project aims to provide a foundational building block for implementing database management systems.
  - One of the projects using Tihku is an experimental libSQL branch with MVCC that aims to implement `BEGIN CONCURRENT` with Tihku improve SQLite write concurrency.
  - Main memory architecture, rows are accessed via an index
  - Optimistic multi-version concurrency control
  - [Copy-on-write cloning](https://github.com/penberg/tihku/issues/21)
    - Many database management systems implement "branching", which allows users to create a copy-on-write clones of a database. 
    - With a row manager, we can make a copy of the in-memory index and bump the reference counts
    - For example, let's say we have a database A and we make a clone B. Initially, they both point to the same set of rows. If either one of them updates a row, the other one will not be affected because the updating clone just marks the shared row version as deleted, but the actual row is unchanged.
    - As a future optimization, we could also use a copy-on-write hash table to even share the index between clones.

- https://github.com/purpleprotocol/hashcow /rust
  - a Rust HashMap implementation with copy-on-write keys and values.
  - Originally built for optimizing the Purple Protocol, this library provides a way to link HashMaps in memory that have duplicate entries. 
  - Instead of the duplicate data, it is instead borrowed and it is only cloned when mutation is needed.
# discuss-data-structure
- ## 

- ## 

- ## 

- ## 

- ## 

- ## A persistent data structure is a data structure that always keeps a previous version of itself when modified, they are cloned very cheaply (in constant or logarithmic time)
- https://twitter.com/____abiodun____/status/1267925344079790081
  - The simplest example is a linked-list or `con` based list, removing the head of a linked-list is 0(1)...
  - Deleting the head is/can be 0(1) too, they are versionable as you just need the pointer to not point to the head or point to a new head, in case data are being added or deleted 
  - It also has structural sharing between which makes cloning cheap
- React Virtual DOM is effectively a tree data structure(trie), tree data structures support structural sharing, hence they can be used as a persistent data structure
  - However, I think LinkedList is a more easily accessible definition as they are easier to understand

# more-data-structure

## [一些不常见但是很重要的数据结构](https://www.cnblogs.com/sing1ee/archive/2012/10/12/2765064.html)

Trie树。应用比较多，一个比较cool的trie的应用TRASH-A dynamic LC-trie and hash data structure。
Bloom filter。wiki链接 删除某一项是不允许的，不过可以实现可计数的counting bloom filter
在BigTable，Cassandra中都有使用
可以用来快速检查是否拼写错误
Rope：rope 数据结构表示不能修改的字符序列，与 Java 的 String非常像。但是 ropes 效率奇高的字符串变换操作使得它与 String及其同一体系的可修改的 StringBuffer和 StringBuilder大不相同，非常适合那些执行繁重字符串操纵的应用程序，尤其在多线程环境下更是如此。ibm文章 包含java实现。
stl实现：http://www.sgi.com/tech/stl/Rope.html
 skip list：这里有一个演示：http://iamwww.unibe.ch/~wenger/DA/SkipList/
Cassandra的索引
redis的SortedSet
Spatial Indices：尤其是R-trees和KD-trees
Bit Array：压缩存储bit，支持快速的bit操作。
Zippers： 在函数式编程中非常有用。
Suffix tries: 字符串搜索非常有用。更酷的是suffix tree，可以O(n)的时间构建
Splay trees：非常酷的结构
非常小巧，仅需要类似二叉树的左右孩子指针
相对容易实现
性能良好，wiki地址
Heap-ordered search trees
邻接表：O(1)计算无向图的邻居节点
lock-free：
http://www.research.ibm.com/people/m/michael/podc-1996.pdf
http://www.cl.cam.ac.uk/research/srg/netos/lock-free/
http://www.boyet.com/Articles/LockfreeStack.html
http://stackoverflow.com/questions/2101789/implementation-of-a-work-stealing-queue-in-c-c
一个非常好的这方面的博客：Mike Acton‘s
并查集
fibonacci堆
 BSP Trees：应用在3D渲染领域
霍夫曼树：压缩
Finger Trees：在函数式结构中使用，wiki地址
Ring buffer
Merkle trees
Cukoo Hashing ：用来提升hash方法的空间利用，基本思想是利用多个hash函数，降低冲突。
 min-max heap：
缓存参数无关数据结构：Cache Oblivious datastructures
 Left learning Red-Back Trees： 论文
Bootstrapped skew-binomial heaps：
 O(1) size, union, insert, minimum
O(logn) deleteMin
Interval Trees: 在Cassandra中有应用
