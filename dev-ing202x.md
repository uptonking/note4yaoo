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

## 0613

- dev-log
  - 整理了执行计划的代码，在ui层mock计划op做了简单实现，提交了pr
- dev-to
  - 尝试将执行计划的op转换到paas中对编辑器的操作

- 每周分享-大数据中台 /黄茂俊/20240613
  - 从你的经历中，处理过的大数据的数据量有多大tb级别，文本、二进制数据
  - 运营商的书仓，pb级别的数据，日常的日志是1-2tb
    - 数据源较复杂，使用了第三方工具和平台
    - 还有些excel文件，使用python解析入库
  - 数据清理的工作量大
    - 主动对接和采集几百家停车场的数据，提供api和文档
    - 对不同业务域建模
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
# maybe
- 参考atlaskit-editor实现collab，服务端未开源，但yjs提供了示例，支持切换docs
