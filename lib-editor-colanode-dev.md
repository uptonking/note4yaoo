---
title: lib-editor-colanode-dev
tags: [chat, colanode, knowledge-base, notion-database, notion-like]
created: 2025-06-21T19:10:23.145Z
modified: 2025-06-21T19:10:57.709Z
---

# lib-editor-colanode-dev

# guide

- pros
  - local-first: background syncing
    - 由于使用WebWorker，可在断网时使用
  - collab editing by yjs
  - all-in-one: chat + doc + files + database
  - blocky data model: flexible building blocks
  - docs支持多tab

- cons
  - docs中的图片需要手动点击才会下载和显示
  - docs不支持分享，每个doc没有单独的url
  - database在编辑器不支持查看和编辑，需要在单独tab操作
  - chat impl is too simple

- features
  - Colanode comes with an AI assistant built in
# draft
- editor
  - 如何将database的数据结构提取为适配多种编辑器的通用结构
# dev-xp
- build/run
  - 顶层的npm run build执行时可能出现部分子包未正确打包构建的问题，可收到执行子包的构建
  - vite访问站点出现import path not found时，发现由于网络问题部分node_modules下的包只下载了一部分不完整
# more
