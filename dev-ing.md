---
title: dev-ing
tags: [dev]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# dev-2023
- 分析核心需求和问题，拆分问题，梳理任务、子任务，排期开发

金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-xp
- my-next
  - dev-starter
    - react patterns
    - typescript patterns
    - mvc dev pattern(for app/data-grid)
  - readonly-list-grid
    - plain
      - no sort/filter/group
      - no reorder
      - no column width resize
      - custom cell renderer
    - searchable
    - virtualizable
  - crud-list-grid
    - checkbox
    - draggable/reorder list
    - fields menu - filter/groupable
    - inline editing
    - orm integration
  - sortable-filterable-groupable-table
- 产品日历组件
  - headless-date-picker
- module/fwk/server
  - 灵活的tag/bookmark系统
- 编辑器参考
  - atlassian-editor
    - https://atlaskit.atlassian.com/packages/editor/editor-core
    - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
    - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html
  - more-editor
    - https://demo.grammarly.com/

```JS
console.log(';; r1-user-spaces ', pathname, user, userSpaces, currentSpaceId);
```

```shell
DEBUG=* npm install --legacy-peer-deps --loglevel silly
```

# dev-review
- dev-goals
  - rich-editor: text/code/block
  - pivot-table
  - collaboration
  - local-first-database
  - annotation/comment/whiteboard/pdf
  - 事项--截止日期(0730+休整)--重要性(hml/s1-s3)
  - *mirror-based-editor-vanillajs--0825--hl
  - pivot-table/grid--0828--hl
    - dropdown-menu vs tabs
  - app-wiki-knowledge-base--0904
  - dashboard/webapp-template--0901

- dev-to/log/xp

- later
  - crdt-hlc 
    - merkle 如何在op-log中找到上次相等的timestamp
  - idb-side-sync
    - storage adapter: indexeddb/memory/sqlite-opfs
    - 系统预置数据如待办类型合并时可能出现名称相同的情况，用户添加数据时也可能出现
  - url-as-state-management
  - 灵活的tag/bookmark系统
  - docker打包前端
# dev-2023
- eg-prosemirror-examples+collab
  - 重写collab示例的交互，参考blocky-editor在一个页面展示多个编辑器且支持实时协作
  - [x] 用websocket替换轮询，可基于socket.io
  - 参考atlaskit-editor实现collab，服务端未开源，但yjs提供了示例，支持切换docs
  - 分析协作时官方的undo-redo和yjs的undo-redo
- eg-tiptap-examples
  - 重写atlaskit或ckeditor的丰富示例
  - tiptap-yjs-server-src
- eg-BlockNote
- eg-focalboard
  - olap-cube-js
- 👉🏻 eg-tanstack-table-v8
  - tuple-database
  - [x] 数据全内存: nedb, blinkdb
  - 数据全持久: linvodb, tingodb

- sync-collab
  - [ ] ddp/ejson/minimongo
  - collab-data-structure: hlc/lww
  - undo/redo
  - remoteStorage: google-drive、网盘、七牛对象存储
- sqlite-web
  - evolu
  - kikko
  - [ ] absurd-sql-ts: read ArrayBuffer

- 内容的存储与更新如何与数据库集成
  - 编辑器内容自动保存一般通过在onChange方法中执行saveToDB
    - ❌ 也可以在onChange方法中创建内存db、更新索引，通过索引提高计算效率； 应该避免维护2份数据
  - 将编辑器的计算密集部分的数据模型不使用普通json对象，而用类似数据库模型的设计

- log2022 数据同步、冲突处理、本地存储
  - 07-focalboard-views
  - 08-block-editor-tiny-write
  - 09-prosemirror-examples
  - 10-prosemirror-collab - otjs - crdt
  - 11-idb-sync
  - 12-nedb-linvodb
# dev-01

## 010

## 0101

- dev-to
  - crdt tutorials
