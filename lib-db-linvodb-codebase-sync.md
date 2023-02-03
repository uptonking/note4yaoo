---
title: lib-db-linvodb-codebase-sync
tags: [codebase, linvodb, synchronization]
created: 2023-01-16T21:14:39.658Z
modified: 2023-01-16T21:14:55.049Z
---

# lib-db-linvodb-codebase-sync

# guide

- 同步功能需求
  - 👉🏻 同步所需的数据是所有changes-ops messages
  - 支持每个用户拥有多个设备，不用userId，考虑到org的同步而使用groupId/teamId
  - 考虑到客户端升级的问题，同步前一定要检查一个version/checkpointTime，参考indexeddb upgrade
  - 支持手动打开和关闭同步/协作，参考crdt-for-mortals的手动离线

- 在changes-ops表上需要执行的操作
  - getRowObjectById: 根据id获取 row object
  - getLatestHlcForColumn: 获取某个column最新的hlc

- hlc的使用
  - tinybase的hlc无依赖，方便测试
  - [x] tinysync去掉对tinybase的依赖，参考crdt-for-mortals
  - [x] tinysync改为c/s架构
  - [ ] 两阶段同步减少传输体积
  - tinysync的changes/ops数据迁移到表
  - 将crdt-for-mortals中apply对对象的修改改为对数据库的crud
  - ~~crdt的冲突处理由table-row-col改为kv结构~~，本身也适合字段级别的修改
# linvodb数据库同步的技术方案-v1
- 同步示例采用中心服务器的方式实现，参考crdt-for-mortals，便于以后支持p2p同步

- 当前方案缺点
  - 中心服务器每次都send全量的trie，因为采用中心服务器需要广播给多个客户端，客户端无需轮询

- 同步有2种方式
  - 每次客户端对db的crud都触发同步，类似crdt-for-mortals/linvo-sync，缺点是未实现服务端推送
    - client发送 op + trie
    - server响应 changes-new
  - 定期同步，类似setInterval轮询，便于实现伪实时效果
    - 两阶段同步

- 两阶段同步
  - 先请求远程元数据，类似文件列表、merkle-trie
  - 再diff计算出本地多的toPush、本地少的toPull

- 同步的防抖
  - 对于在同步的同时产生的新op，先缓存
  - 通过isDirty/isListening在同步完成前不会再次触发同步

- 同步使用插件架构，在数据库的crud中注入
  - 参考idbsidesync/linvo-sync

- 同步功能以接口约束，方便扩展
  - op数据同步的服务端实现不一定使用linvodb，支持sqlite
  - 两个linvodb相互同步时，提供便捷工具

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
