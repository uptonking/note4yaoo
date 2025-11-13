---
title: algs-text-string
tags: [algorithms, string, text]
created: 2025-11-13T14:44:41.191Z
modified: 2025-11-13T14:44:54.946Z
---

# algs-text-string

# guide

# dev-xp
- ai生成的文本或代码有时需要较高的准确度，一种方案是采用 Levenshtein 距离来计算生成文本与目标文本的距离，若距离小于某个阈值，则认为生成文本是可接受的
# examples

## utils

# blogs

## [浅谈Levenshtein Distance莱文斯坦距离算法 - 知乎](https://zhuanlan.zhihu.com/p/507830576)

- Levenshtein Distance莱文斯坦距离，属于编辑距离的一种。由苏联数学家Vladimir Levenshtein于1965年提出
- 两个字符串之间的Levenshtein Distance莱文斯坦距离指的是将一个字符串变为另一个字符串需要进行编辑操作最少的次数。
  - 可用于衡量两个字符串之间的差异，故被广泛应用于拼写纠错检查、DNA分析、语音识别等领域
- 一般来说，编辑距离越小，两个串的相似度越大。
- 其中，允许的编辑操作有以下三种。
  - 「替换」：将一个字符替换成另一个字符
  - 「插入」：插入一个字符
  - 「删除」：删除一个字符

- [Levenshtein Distance算法（编辑距离算法） - 熊仔其人 - 博客园](https://www.cnblogs.com/xiongzaiqiren/p/4997947.html)
- 编辑距离是测量一个字符串转换成另外一个字符串需要操作（操作包括： 插入    删除    置换）的最小次数。 
- 编辑距离可以用来计算两字符串的相似度，另外也可以通过余弦方法来计算两字符串的相似度
- 算法实现采用动态规划算法，其求解过程类似于求两字符串的最长公共序列（LCS）

- 

# discuss
- ## 

- ## 

- ## 

- ## [什么是莱文斯坦距离(Levenshtein distance)，它在计算机科学中有什么应用？ - 知乎](https://www.zhihu.com/question/315634571)
- 从四种操作我们可以看出来，四种操作都可以被分解为多个重叠子问题。对于重叠子问题，我们一般会采用动态规划的方案。
