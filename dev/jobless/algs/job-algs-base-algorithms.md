---
title: job-algs-base-algorithms
tags: [algorithms, job]
created: 2021-09-25T19:40:11.839Z
modified: 2021-09-25T19:40:33.814Z
---

# job-algs-base-algorithms

# guide

- O(1) < O(logn) < O(n) < O(nlogn) < O(n^2)

# 动态规划
- 最大正方形
  - https://leetcode-cn.com/problems/maximal-square/
# discuss

## [如何分析、统计算法的执行效率和资源消耗](https://github.com/sisterAn/JavaScript-Algorithms/issues/1)

- 大O时间复杂度表示法。
- 大O时间复杂度实际上并不具体表示代码真正的执行时间，而是表示代码执行时间随数据规模增长的变化趋势，
  - 所以，也叫作渐进时间复杂度（asymptotic time complexity），简称时间复杂度。
  - 当 n 无限大时，时间复杂度 T(n) 受 n 的最高数量级影响最大，与f(n) 中的常量、低阶、系数关系就不那么大了。
  - 所以我们分析代码的时间复杂度时，仅仅关注代码执行次数最多的那段就可以了。
