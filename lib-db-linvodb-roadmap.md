---
title: lib-db-linvodb-roadmap
tags: [linvodb, roadmap]
created: 2023-01-09T18:00:07.337Z
modified: 2023-01-09T18:00:20.350Z
---

# lib-db-linvodb-roadmap

# guide

# dev-to
- linvodb-sync的实现原理
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

- 从callback迁移到async-await

- 参考tinybase基于checkpoints实现undo-redo

- 合并search-index和linvodb的存储层，修改search-index的获取全部对象逻辑
  - 非首次启动项目时，如何恢复search-idx的索引

- 迁移 原仓库功能，如sync/benchmark

- 支持延迟构建索引，而不是在构造函数中

- how to store images

- Mongoose driver for LinvoDB
  - https://github.com/aerys/mongoose-linvodb3
# later
- how to make filter/sort/group support extra data source?
# draft
