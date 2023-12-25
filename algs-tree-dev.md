---
title: algs-tree-dev
tags: [algorithms, tree]
created: 2023-04-20T08:05:12.746Z
modified: 2023-04-20T08:05:25.098Z
---

# algs-tree-dev

# guide

# dev

# blogs

- [线段树（segment tree)、区间树(interval tree) - 知乎](https://zhuanlan.zhihu.com/p/105368572)

- [Hash Array Mapped Trie（HAMT）简介 - 雪球球 - 博客园](https://www.cnblogs.com/xueqiuqiu/articles/8648853.html)
  - Hash Table 和 List 的一个区别在于 Hash Table 当中保存的元素是散列和稀疏的，不像 List 那样从下标 0 一直排列到 n。
  - 只要把 List 当中下标必须连续的限制条件去掉，Vector Trie 本身就变成了一种相对传统 Array 更好的容器
# more

# discuss

- ## 

- ## 

- ## 

- ## 🆚️ [What are the differences between segment trees, interval trees, binary indexed trees and range trees? - Stack Overflow](https://stackoverflow.com/questions/17466218/what-are-the-differences-between-segment-trees-interval-trees-binary-indexed-t)
- Segment tree 线段树 存储区间，查询哪些区间包含给定的点
  - O(k+logn) 查询，O(n logn) 空间
- Interval tree 区间树 存储区间，查询哪些区间与给定区间相交，也支持点查询（Segment tree）
  - O(k+logn) 查询，O(n) 空间
- Range tree 范围树 存储点，查询哪些点落在了给定区间
  - O(k+logn) 查询，O(n) 空间
- Binary indexed tree 二叉索引树 存储每个索引的项目数，查询索引 m 和 n 之间有多少个项目
  - O(logn) 查询，O(n) 空间

- 
- 
- 
