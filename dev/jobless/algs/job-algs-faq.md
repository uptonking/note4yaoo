---
title: job-algs-faq
tags: [algorithms, faq, job]
created: 2021-09-21T19:41:58.469Z
modified: 2021-09-23T08:26:55.811Z
---

# job-algs-faq  

# guide

# tree
- [bst: Are duplicate keys allowed in the definition of binary search trees?](https://stackoverflow.com/questions/300935/are-duplicate-keys-allowed-in-the-definition-of-binary-search-trees)
  - Many algorithms will specify that duplicates are excluded
  - It is fairly trivial to implement duplicates (either as a list at the node, or in one particular direction.)
  - a BST which allows either of the right or left children to be equal to the root node, will require extra computational steps to finish a search where duplicate nodes are allowed.
  - It is best to utilize a list at the node to store duplicates, as inserting an '=' value to one side of a node requires rewriting the tree 
# array

# list

## [既然已经有数组了, 为什么还要链表](https://juejin.cn/post/6844903946222321671)

- 链表(linked list)这种数据结构既熟悉又陌生, 熟悉是因为它确实是非常基础的数据结构, 陌生的原因是我们在业务开发中用到它的几率的确不大
- 相同点是都是线性数据结构
- 不同之处在于数组是一块连续的内存，而链表可以不是连续内存
  - 非连续内存的特性导致链表非常适用于频繁插入、删除的场景，而不见长于读取场景，这跟数组的特性恰好形成互补
  - 数组利用下标定位，时间复杂度为O(1)，链表定位元素时间复杂度O(n); 
  - 数组插入或删除元素的时间复杂度O(n)，链表的时间复杂度O(1); 
