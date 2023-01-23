---
title: lib-db-linvodb-codebase-sync
tags: [codebase, linvodb, synchronization]
created: 2023-01-16T21:14:39.658Z
modified: 2023-01-16T21:14:55.049Z
---

# lib-db-linvodb-codebase-sync

# guide

# linvodb数据库同步的技术方案-v1
- 同步示例采用中心服务器的方式实现，但同时支持p2p

- 同步逻辑分两阶段
  - 先请求远程元数据，类似文件列表、merkle-trie
  - 再diff计算出本地多的toPush、本地少的toPull

- 同步使用插件架构，在数据库的crud中注入
  - 参考idbsidesync
- 同步功能以接口约束，方便扩展
  - op数据同步的服务端实现不一定要是linvodb，支持sqlite
  - 两个linvodb相互同步时，提供便捷工具

- hlc的使用
  - tinybase的hlc无依赖，方便测试

- @deprecated
  - 计算两设备的最小变更树比较后决定采取的方案是数据库查询，而不使用merkle-trie或patricia-trie来计算最小变更节点，因为理解较难，考虑到当一个用户有多个设备时，本地需要维护多颗树，不如用数据库直观
# hlc-sync
- 难点
  - 与数据表关联的change-tree的构建
  - 两棵change-tree的diff，目标是计算出最小变更节点

- from 数据集D1  to 数据集D2 的协作流程
  - 在D1/D2日常的crud中构建 change-tree
  - 获取D1的change-tree相对于D2的最小diff-tree
  - 根据diff-tree更新D2

- 🤔 代码疑问，在使用中心服务器的前提下
  - 是否有必要每次发送完整的change-tree?
    - 若是2阶段同步，则无必要
  - change-tree的结构设计 `{ time1: { time2: {counter: {clientId:changeObj} } } }`, 为何将hlc分为4部分，为何用3+4而不是4+3/2+5
  - latestHlcsByCell 似乎无用，可删除
  - TREE_DEPTH = 3 为什么这么设计
# ✨ linvo-sync
- linvodb的思路是在DataModel的inserted/updated钩子函数中执行 `triggerSync()`，即每个dml操作都执行

- linvodb的同步逻辑分两阶段
  - 先请求远程元数据，类似文件列表、merkle-trie
  - 再diff计算出本地多的toPush、本地少的toPull

- 每次 triggerSync 的逻辑
  1. ensure_indexes，构建本地索引
  2. retrieve_remote_meta，请求远程变更元数据，`{ id: datetime }` 集合
  3. compile_changes，遍历本地id比较并对应远程变更元数据id比较，将所有ids分类 toPull/toPush
  4. push_remote，将本地toPush数据发送到远程
  5. pull_local，将远程toPull数据请求到本地，然后insert/save到本地数据库
  6. finalize，完成后emit syncEnd事件
- 依赖3个服务端api，API.request 
  - datastoreMeta
  - datastorePut
  - datastoreGet
