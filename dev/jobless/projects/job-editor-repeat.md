---
title: job-editor-repeat
tags: [editor, job, repeat]
created: 2021-10-10T09:46:03.711Z
modified: 2021-10-10T09:46:16.058Z
---

# job-editor-repeat

# guide

# [如何在画布中实现对齐吸附](https://zhuanlan.zhihu.com/p/92469406)
- 当我们总结出自由画布中组件对齐吸附的能力之后，就可以考虑如何实现它。涉及到对齐吸附，一定就涉及到”移动组件“和”目标组件“
  - 一个组件可以看做是由 6 条线构成的，组件移动过程中的吸附就是这些线之间的对齐关系。所以，首先要做的就是对组件进行线的存储
  - 一个组件有 6 条线，且冗余存储其 node 及组件实例信息 instance
  - 线的存储可以考虑使用二叉树
