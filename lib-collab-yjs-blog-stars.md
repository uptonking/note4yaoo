---
title: lib-collab-yjs-blog-stars
tags: [blog, collaboration, yjs]
created: 2022-10-22T18:45:04.054Z
modified: 2022-10-22T18:45:23.619Z
---

# lib-collab-yjs-blog-stars

# guide

# [探秘前端 CRDT 实时协作库 Yjs 工程实现 - 知乎](https://zhuanlan.zhihu.com/p/452980520)
- 本文会从 Yjs 的工程实现出发，介绍一个典型的工业级 CRDT 库是如何实现以下能力的：
  - 建模数据结构
  - 解决并发冲突
  - 回溯历史记录
  - 同步网络状态

- Yjs 的算法先进，但在实际应用中确存在下面的问题：
  1. fast search marker 不支持在 YXmlText 中使用
  2. 不支持移动操作，移动后的合并位置不符合预期
  3. ContentFormat 不支持同类型样式的嵌套或交错（不能还原 ProseMirror Mark 的特性）
  4. ProseMirror 的 Step 和 Yjs 的 insert/delete API 不匹配，y-prosemirror 采用了一套 diff 算法，导致用户意图丢失。也许与 Quilljs 结合没有这样的问题。
# [Syncing text files between browser and disk using Yjs and the File System Access API_202205](https://motif.land/blog/syncing-text-files-using-yjs-and-the-file-system-access-api)
- Wrote this blog post on how to sync files between browser and disk using Yjs and the File System Access API. It works really well! 
- https://twitter.com/michaelfester/status/1523698983117684736

- https://news.ycombinator.com/item?id=31315717
# [基于CRDT的一种文档冲突算法 YATA/yjs](https://juejin.cn/post/7064236095440961550)
- 本文我们主要介绍基于CRDT的一种文档合并算法-YATA。它有自己的开源实现Yjs

- [YATA：一种针对文本编辑优化的 CRDT 算法](https://hyrious.me/p/yata.html)

- [YATA线性数据插入算法](https://juejin.cn/post/7030327499829542942)

- [Near Real-Time Peer-to-Peer Shared Editing on Extensible Data Types](https://www.researchgate.net/publication/310212186_Near_Real-Time_Peer-to-Peer_Shared_Editing_on_Extensible_Data_Types)
# [Delta-state CRDTs: indexed sequences with YATA](https://bartoszsypytkowski.com/yata/)
- This time we'll cover YATA (Yet Another Transformation Approach): a delta-state based variant, introduced and popularized by Yjs framework used to build collaborative documents.
