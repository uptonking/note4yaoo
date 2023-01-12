---
title: algs-data-structure-catalog
tags: [algorithms, data-structure]
created: 2020-12-20T15:20:40.311Z
modified: 2020-12-20T15:27:57.656Z
---

# algs-data-structure-catalog

# List

# Map

# Tree

# String
- [xi-editor: Rope science - Introduction](https://xi-editor.io/docs/rope_science_00.html)

- [Fleet: Data Structures in the Fleet Editor | Hacker News](https://news.ycombinator.com/item?id=30415868)
  - [Fleet Below Deck, Part II – Breaking down the editor: Ropes everywhere](https://blog.jetbrains.com/fleet/2022/02/fleet-below-deck-part-ii-breaking-down-the-editor/)
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
