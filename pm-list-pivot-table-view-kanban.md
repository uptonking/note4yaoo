---
title: pm-list-pivot-table-view-kanban
tags: [kanban, pivot-table, pm]
created: 2022-12-16T01:52:42.987Z
modified: 2023-01-22T18:45:58.936Z
---

# pm-list-pivot-table-view-kanban

# guide

# draft
- filter by select
  - 支持选择多个值来组成看板, 需要计算排列组合的方式
# blogs

## more-blogs

- [Building a Kanban Board With React](https://marmelab.com/blog/2023/07/28/create-a-kanban-board-in-react-admin.html)
# more

# discuss-kanban

- ## 

- ## 💫 Designing for Kanban Page
- https://x.com/barlydesign/status/1893294672564625461
  - 卡片内容出现动画

- ## [Nullboard: Kanban board in a single HTML file | Hacker News _202412](https://news.ycombinator.com/item?id=42461688)
- when developing single HTML file apps, instead of localStorage, one can use the HTML as the source of truth, so the user can just save/save-as to persist.
  - TiddlyWiki famously does this! It's a great system for what it needs to be

- I like urls as source of truth. It’s beautifully deterministic

- How would this work without manually editing the HTML file?
  - You write Javascript to read and write to HTML, like, develop a single page app that treats HTML as the view and the database, and restores state on DOMContentLoad from the HTML. Super easy and maintainable for micro apps.
  - You can also use the contenteditable attribute and use no JS, so you basically have a notepad.

- One major failing of WebDAV for these use cases is that the spec requires you to `PUT` the whole resource/file in order to save changes. This isn't too bad when the individual files are small, but as your single file apps grow, this means a lot of data transfer without the comforts of differential uploads.

- I feel GitHub gists are a very good store for data: writable, versioned, shareable and read-only for non authors, workable, support for arbitrary data including binary
  - I tried that. The problem is that you will always need a middle-end (a separate server between your stand-alone front end application and the GitHub server). You can't just distribute a stand-alone app and let it talk to GitHub directly. Or well you can but only if you get a token with *FULL* scope for all repositories. What I as a developer need is a scope for only one repository. That's how stand-alone and especially browser-based applications can remain safe. You don't want to store tokens with full permissions in multiple apps.

- SyncThing is my go-to for multi-device syncing.

- CouchDB + PouchDB
- dexieCloud too.

- Custom two way syncing is a nightmare to implement correctly, and it doesn't make sense for apps to have to keep reinventing the wheel 
  - It is a factor in why CRDT/OT posts and libraries get regularly upvoted on HN. A lot of us want a good, easy to use baseline. A lot of us are searching for that and/or thinking we can build that.
  - Part of why there's always some reinventing the wheel in this space, unfortunately is that this also seems to be one of the harder problems to generalize. There's always going to be domain specifics to your models or your users or users' idea of your models that is going to need some custom sync and conflict resolution work. Sync has a lot more application specifics than most of us want.
  - That said, yeah, if there was a good simple building block "base line" to start with that met a nice 80/20 rule plateau
  - (One such 80/20 place to start if the idea was just a simple KV store might be a basic "Last Write Wins" approach and a simple API to read older versions when necessary. You can build a lot of the cool CRDT/OT stuff on top of a store that simple. Many starting apps LWW is generally a good place to start for the basics. It doesn't solve all the syncing/conflict resolution problems, you'll still need to write app-specific code at some point, but that could be a place to start. It's basically the place most of the simplest NoSQL databases started.)

- ## [Show HN: Nullboard – Simple, light, locally-stored to-do lists | Hacker News _201906](https://news.ycombinator.com/item?id=20077177)
- It's a single html page, depends only on jQuery and a small webfont pack. It can be used completely offline, and it stores all data locally.

- Drag and drop doesn't work on mobile.
  - Yes, among other things. This is 100% desktop-oriented app.

- ## 我们团队近期不得不尝试寻找 Trello 替代品。
- https://twitter.com/DIGITALYCHEE/status/1773238652073881795
  - 一方面，未来新入职的员工下载 Trello App 的难度过大。另一方面，Trello 4月份会加大免费版的功能限制。
- Microsoft project online，用来分解复杂任务比较方便。
- 其实有个共享文档，就能做好协同了。

- ## 🪟✨ [如何评价 workflowy 新推出的 fractal boards (分形看板) 功能? - 知乎_202007](https://www.zhihu.com/question/404166572)
- 整个 workflowy 中的每一个节点全部可以在 (bullets / board) 这两种显示模式之间切换。
  - 无论选择哪种显示模式，原始数据都不会有任何改变，改变的只是展示形式。
  - 如果选择 bullets 模式(也就是过去的列表模式)，一棵子树会以一个列表的形式展示，
  - 而如果选择 board 模式，一棵子树就会以一个看板的形式来展示。

- 分形看板使用举例
- eg 1：将一个列表转化为看板
- eg 2：平铺显示多个看板, 
  - 同时平铺多个看板，trello 等传统看板工具是做不到的，而且分形看板还可以跨看板拖拽卡片
  - 上面两点 notion 也可以做到，但还有一点是 notion 也做不到的，那就是分形看板的跨看板拖拽卡片不仅仅是针对卡片，还可以跨看板拖拽整个竖排列表，或是跨看板直接拖拽卡片内部的列表元素
- eg 3：无限嵌套的分形看板

- workflowy 的大纲式数据本质上是以树状结构来组织的。

- trello 等传统看板
  - 优势：比起 trello 这样的传统看板，分形看板的最大优势就是可以平铺多个看板，而且可以跨看板直接拖拽任何元素
  - 劣势：workflowy 没有任何富文本特性；trello 有一大堆乱七八糟的功能，仅从看板这个维度来说，trello 的功能要丰富得多

- 桌面版滴答清单的看板, 从任务管理和时间管理的角度来比较：
  - 优势：滴答清单的看板模式只是提供了一种新的视图来组织任务，它依然没有实现无限层级子任务，而分形看板里可以添加无限层级的子任务
  - 劣势：清单软件可以设置精确到分钟的强制提醒和周期提醒，workflowy 只能做看板管理和简化版的 GTD

- notion
  - 优势：notion 的 database 打开比较慢，分形看板的各种操作要流畅得多，并且分形看板可以直接跨看板拖拽任意元素
  - 劣势：综合来说，如果仅仅比较看板的话，notion 的 database 功能更全更强

- 嘀嗒清单的TODO，workflowy的无限层级和evernote的文档、附件收藏结合下就好了

- 感觉 Reading Lists 用分形看板很方便（不过我的 Reading Notes 不在 Workflowy 里）
  - 悄悄吐槽左右滚动切换不大方便，所以每个看板最好不要超过 3 或 4 个 board

- ## 🪟 [Kanboard: free and open source Kanban project management software | Hacker News_202305](https://news.ycombinator.com/item?id=36047861)
- 
- 
- 
