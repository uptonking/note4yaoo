---
title: lib-editor-colanode-dev
tags: [chat, colanode, knowledge-base, notion-database, notion-like]
created: 2025-06-21T19:10:23.145Z
modified: 2025-06-21T19:10:57.709Z
---

# lib-editor-colanode-dev

# guide

- pros
  - local-first: background syncing, web前端及后端server及minio全停止时web也可正常使用
    - 由于使用WebWorker，可在断网时使用
  - collab editing by yjs, undo/redo by yjs
  - all-in-one: 📈 database + 💬 chat + 📝 doc + 📁 files
  - blocky data model: flexible building blocks
  - 👾 AI assistant built in

- cons
  - export不支持
  - docs中的图片需要手动点击才会下载和显示
  - docs不支持分享，每个doc没有单独的url
  - database支持inline和fullPage, ~~不支持查看和编辑，需要在单独tab操作~~
    - table不支持拖拽改变行顺序
    - kanban不支持拖拽改变列顺序
  - editor
    - table不支持，只实现了database
  - SubPage 的名称需要手动指定而不会自动显示第一行内容
    - 还不会显示在文件树
  - collab
    - 文档分享未实现，协同编辑待开发
  - chat impl is too simple

- features
  - docs支持多tab
# draft
- editor
  - 如何将database的数据结构提取为适配多种编辑器的通用结构
# dev-xp
- 应用层数据库的设计非常简洁且弱耦合，表之间外键都很少用

- build/run
  - 顶层的npm run build执行时可能出现部分子包未正确打包构建的问题，可收到执行子包的构建
  - vite访问站点出现import path not found时，发现由于网络问题部分node_modules下的包只下载了一部分不完整
# more
