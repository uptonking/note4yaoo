---
title: pm-office-logseq-xp
tags: [logseq, note-taking, pm, xp]
created: 2022-06-02T04:32:59.545Z
modified: 2022-06-02T06:11:16.758Z
---

# pm-office-logseq-xp

# guide

- pros
  - 编辑器类似typora，支持即时预览和编辑文本
    - 即时预览的切换预览和源码文本经常导致页面重排layout

- cons
  - not open source: backend and sync
  - 支持浏览器直接打开本地文件夹
  - 不支持 database

- features
  - No data lock-in, no proprietary formats
    - you can edit the same Markdown/Org-mode file with any tools
  - 支持用 [[]] 引用任何page，自动生成文档关系图
  - 任务管理很方便
    - 支持 deadline，支持优先级
  - pdf阅读批注很方便
    - 支持分屏查看
    - 支持复制后链接到pdf位置
  - 支持多设备，包括网页版、移动端

- user-xp
  - 每一行前面都有类似无序列表的小点
    - 优点是点击小点时，每一行都可以作为单独的page打开
    - 缺点是左边的小点和竖线使得页面看起来有点乱
  - 配置文件格式是 config.edn
    - 类似json，支持注释

- who is using #logseq
  - https://note.xuanwo.io/#/all-pages
# discuss-stars
- ## 

- ## 

- ## [Release backend source _202211](https://github.com/logseq/logseq/issues/7470)
- Does this mean there is no plan to make Logseq fully open source?
  - I think that's the case, although I'm not a member of the team.
  - However, another effort is underway, see discuss.logseq.com/t/building-a-self-hostable-sync-implementation/21850 and bcspragu/logseq-sync

- [Will Logseq remain fully open-source in the future and will the synchronization feature be self-hostable?  _202210](https://discuss.logseq.com/t/will-logseq-remain-fully-open-source-in-the-future-and-will-the-synchronization-feature-be-self-hostable/11951)
# discuss
- ## 

- ## 

- ## 

- ## [[WIP] Database version](https://github.com/logseq/logseq/pull/9858)

- ### @logseq DB / Database version on the way?_20230715
- https://twitter.com/ednico_/status/1680134195484434432
  - There's not a switch. Two storage methods (file, DB) will be in parallel.
  - DB storage is for users looking for good outliner performance and structured data support. Also, there will be a full graph markdown export with automatic refreshing to cover the local-first demands.
- benefits
  - Performance +++
  - No more re-index required
  - No more structural parsing required
  - Reliable page & block timestamp
  - Reliable page & block history
  - Reliable sync & RTC
  - Reliable & snappy multi-window
  - Enabling more features on web app"

- How will it compare to other database products on the market?

- ### A nice little update on the @logseq db / database version  - getting closer and closer
- https://twitter.com/ednico_/status/1674111439173189660
- Easy converting between MD and db will make this a winner for sure. Seems to be going in a similar direction to @notesnook

- Imo this defeats the purpose completely of using logseq, which is to have markdown as the source of truth
