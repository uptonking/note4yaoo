---
title: lib-db-linvodb-codebase-sync
tags: [codebase, linvodb, synchronization]
created: 2023-01-16T21:14:39.658Z
modified: 2023-01-16T21:14:55.049Z
---

# lib-db-linvodb-codebase-sync




# guide


# hlc-sync

- 难点
  - 与数据集关联的change-tree的构建
  - 2棵change-tree的diff

- from 数据集D1  to 数据集D2 的协作流程
  - 在D1/D2日常的crud中构建 change-tree
  - 获取D1的change-tree相对于D2的最小diff-tree
  - 根据diff-tree更新D2

- 🤔 代码疑问，在使用中心服务器的前提下
  - 是否有必要每次发送完整的change-tree?
  - TREE_DEPTH = 3 为什么这么设计
  - latestHlcsByCell 似乎无用，可删除
  - change-tree `{ time1: { time2: {counter: {clientId:changeObj} } } }`

# linvo-sync

- linvodb的思路是在DataModel的inserted/updated钩子函数中执行 `triggerSync()`，即每个dml操作都执行
- 每次 triggerSync 的逻辑
  1. ensure_indexes，构建本地索引
  2. retrieve_remote，请求远程变更元数据，{ id: datetime }
  3. compile_changes，遍历本地id比较并对应远程变更元数据id比较，将所有ids分类 toPull/toPush
  4. push_remote，将本地toPush数据发送到远程
  5. pull_local，将远程toPull数据请求到本地，然后insert/save到本地数据库
  6. finalize，完成后emit syncEnd事件
- 依赖3个服务端api，API.request 
  - datastoreMeta
  - datastorePut
  - datastoreGet
