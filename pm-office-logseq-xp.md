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

- ## 

- ## 🤔🛢️ [Why the database version and how it's going? - Announcements - Logseq _20240429](https://discuss.logseq.com/t/why-the-database-version-and-how-its-going/26744)
- 
- 

- ## [Release backend source _202211](https://github.com/logseq/logseq/issues/7470)
- Does this mean there is no plan to make Logseq fully open source?
  - I think that's the case, although I'm not a member of the team.
  - However, another effort is underway, see discuss.logseq.com/t/building-a-self-hostable-sync-implementation/21850 and bcspragu/logseq-sync

- [Will Logseq remain fully open-source in the future and will the synchronization feature be self-hostable?  _202210](https://discuss.logseq.com/t/will-logseq-remain-fully-open-source-in-the-future-and-will-the-synchronization-feature-be-self-hostable/11951)
# discuss
- ## 

- ## 

- ## [LogSeq 为什么要推出数据库版本?「本地优先」的文本笔记该怎么办？ – 效率火箭，火箭君的新博客](https://xlrocket.blog/2024/05/19/logseq-%e4%b8%ba%e4%bb%80%e4%b9%88%e8%a6%81%e6%8e%a8%e5%87%ba%e6%95%b0%e6%8d%ae%e5%ba%93%e7%89%88%e6%9c%ac%e3%80%8c%e6%9c%ac%e5%9c%b0%e4%bc%98%e5%85%88%e3%80%8d%e7%9a%84%e6%96%87%e6%9c%ac%e7%ac%94/)
- 长久以来，LogSeq 和 Obsidian一样都是「本地优先」类笔记 App 的代表。 
  - 两者都是从最早的 类似 RoamResearch 的「本地存储版本」开始发力， 
  - 只不过， Obsidian 走向了一个「全功能」的双链笔记， LogSeq 则继续在树状结构的「节点笔记」上深耕。
  - LogSeq 的节点形式之上，另一家公司又带来了一个「非本地存储」的云端版，Tana。 
  - Tana 更深入地体现了 「节点笔记」的精髓，以节点为记录单位，而且彻底摒弃了「文件」的概念，自然也没有「本地存储」，一切都是云端数据库。Tana 的便利性和性能也因为这些改动而大幅提升，但是数据安全/数据所有权以及隐私保护，也受到了极大的挑战。

- 数据库版本是开源的吗？ 
  - 是的，可以在 GitHub 上找到：[WIP] 数据库版本 by tiensonqin – Pull Request #9858

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
