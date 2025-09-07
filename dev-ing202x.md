---
title: dev-ing202x
tags: [dev, draft]
created: 2023-02-26T15:28:56.959Z
modified: 2023-02-26T15:30:04.261Z
---

# dev-ing202x

# guide
- 数学复习
  - 线性代数矩阵分解: 数据降维
  - 统计概念: 标准差、协方差
# dev-log

# dev-to

# dev-later
- mergeable-table
  - insertAbove能执行，inertBelow不能执行
  - Cannot resolve a Slate point from DOM point

- crdt-hlc 
  - merkle 如何在op-log中找到上次相等的timestamp

- idb-side-sync
  - storage adapter: indexeddb/memory/sqlite-opfs
  - 系统预置数据如待办类型合并时可能出现名称相同的情况，用户添加数据时也可能出现

- url-as-state-management
  - [Storing state in the URL with React](https://pierrehedkvist.com/posts/react-state-url?boolean=false)

- docker打包前端

- eg-prosemirror-examples+collab
  - 重写collab示例，在一个页面展示多个编辑器且支持实时协作
  - [x] 用websocket替换轮询，可基于socket.io
  - 分析协作时官方的undo-redo和yjs的undo-redo
- eg-tiptap-examples
  - eg-migrate-atlaskit-examples
  - 重写ckeditor的丰富示例
  - tiptap-yjs-server-src
- eg-block-editor
  - BlockNote
  - plate

- dev-later
  - crdt tutorials
  - 默认 last-write-win, 出现冲突时，提示用户选择版本
  - 离屏渲染, keep-alive
  - 分层渲染
  - 测试文档系统未登录的流程和mock
# maybe
- 参考atlaskit-editor实现collab，服务端未开源，但yjs提供了示例，支持切换docs

- sqlite-web
  - evolu(hlc+worker)
  - absurd-sql-ts: read ArrayBuffer
  - kikko

- dev-starter
  - css: open-props, glass-ui, 渐变字体
  - patterns: react, typescript
- list-grid-starter
  - no sort/filter/group
  - no reorder
  - no column width resize
  - custom cell renderer
  - searchable
  - virtualizable
- list-grid-solutions
  - checkbox
  - draggable/reorder list
  - fields menu - filter/groupable
  - inline editing
  - orm integration
  - sortable-filterable-groupable-table
  - dropdown-menu & tabs switcher
- 产品日历组件: headless-date-picker
# dev-log
- cms 功能融合及模块化
  - outline, strapi, undb, nocobase, 将undb的多维表格加入strapi-admin
  - business-features, 盈利支持自身
  - 不必执着于engine如db/excel-dataflow, 产品的形式大多cms
- slate-wangeditor
  - model, view, sync, collab
  - slate-docs-examples
  - general-editing-backend: ActionText, cms-payload
- eg-pivot-views/focalboard
  - table view
  - kanban view, specification
  - **结合tanstack-table的pivot和ospreadsheet的edit/architecture**

- dev-gap202209
  - apps-wiki-knowledge-base--0904
  - dashboard/webapp-template--0901
  - ui: ariakit, zag/ark, radix-ui/base-ui, mantine
  - apps: cms+crdt
