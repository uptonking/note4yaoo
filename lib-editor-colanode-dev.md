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
  - subpage/sub-doc
  - 支持计算存储空间

- cons
  - version-history不支持
  - export不支持
  - ~~docs中的图片需要手动点击才会下载和显示~~
  - docs不支持分享，每个doc没有单独的url
  - 多tab的设计，没有自动关闭tab很烦
  - database支持inline和fullPage, ~~不支持查看和编辑，需要在单独tab操作~~
    - table不支持在中间位置插入row/column
    - 不支持拖拽改变行顺序, 首列的最小宽度过大
    - 列较多时，表格不会水平滚动导致可见数据太少
    - 列数据类型不支持修改
    - 添加row时默认会打开新tab，体验不流畅
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
- 🛢️✅ 应用层数据库的设计非常简洁且弱耦合，表之间外键都很少用

- build/run
  - 顶层的npm run build执行时可能出现部分子包未正确打包构建的问题，可收到执行子包的构建
  - vite访问站点出现import path not found时，发现由于网络问题部分node_modules下的包只下载了一部分不完整

## editor-dev

- image
  - png图片默认显示的url为blob格式如 `blob:http://localhost:4000/d1dabae6-52bb-44a5-967f-a18fbc70d7c1`, 这种方案每次刷新页面图片的url都会变化
  - 跨浏览器显示图片存在问题，firefox/edge正常显示图片，但safari无法显示图片而url也是blob

- 
- 
- 
- 
- 

# more
