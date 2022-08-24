---
title: lib-excel-spreadjs-dev
tags: [excel, spreadjs]
created: 2022-08-24T10:48:04.246Z
modified: 2022-08-24T10:48:29.318Z
---

# lib-excel-spreadjs-dev

# guide

- resources
  - [speadjs技术博客](https://www.grapecity.com.cn/blogs/categories/spread)
  - [SegmentFault D-Day 技术分享：葡萄城电子表格技术__202108](https://www.grapecity.com.cn/blogs/spreadjs-segmentfault-d-day)
# spreadjs-blog

## [葡萄城 SpreadJS 前端表格技术分享_202007](https://zhuanlan.zhihu.com/p/164731403)

- 针对前端表格开发的三大技术难点：性能、内存消耗和可靠性，SpreadJS分别提出了应对措施：
  - 基于双缓存画布绘制引擎，SpreadJS实现了极高的处理性能
  - 基于行模式的稀松矩阵存储策略，SpreadJS可大幅节省内存消耗
  - 基于计算引擎技术，SpreadJS可实现稳定可靠的应用系统
# blogs
- [简介：开发在线文档时，这个技术难点你解决了吗？ 多人协作](https://www.grapecity.com.cn/blogs/spreadjs-technical-difficulties-of-online-documentation)
- SpreadJS 采用了稀疏数组 (Sparse Array) 作为存储模型，相较于传统的链式存储或数组存储，稀疏数组只会对非空数据进行存储，而不需要对空数据开辟额外的内存空间。
  - 除了节省内存空间外，对于表格这类布局松散的数据类型，稀疏数组也更易于构建基于行索引的数据字典，以便随时替换或恢复整个存储结构中的任何一个级别的节点，
  - 借助这一特性，SpreadJS 在多人协同中实现了高效的数据回滚和数据恢复 (Redo/Undo)。

- [手把手教你用Canvas电子表格做电子签名](https://www.grapecity.com.cn/blogs/spreadjs-use-canvas-spreadsheet-for-electronic-signature)

- [详解Canvas优越性能和实际应用](https://www.grapecity.com.cn/blogs/spreadjs-advantages-and-practical-applications-of-canvas)
