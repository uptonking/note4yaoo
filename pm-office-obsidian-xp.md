---
title: pm-office-obsidian-xp
tags: [dev-xp, obsidian]
favorited: true
created: 2026-06-30T17:32:22.808Z
modified: 2026-06-30T17:32:43.131Z
---

# pm-office-obsidian-xp

# guide
- pros
  - rich editor
  - backlinks: 双链基于[[]]语法, 同名文件的写法是相对路径
  - bases: 基于文件的多维表格
    - Convert CSV records to individual Markdown files and Bases.
    - 支持导出csv
  - publish
  - canvas
  - graph-view
  - slides
  - templates
  - sync

- cons
  - 不支持类似notion的 block-style dragging
  - bases
    - 不支持拖拽排序, 不能在指定位置插入行/列
    - 不支持拖拽导致不支持kanban
  - settings-sync 

- features(来自ob app里面的 core/community plugins)
  - filetree, file-properties, search, file-recovery, note-merge/split, quick switcher, workspaces-layout
  - backlinks, bases, bookmarks, outline, page-preview, footnotes, slash commands, outgoing-links, web viewer
  - canvas, slides, daily-notes, graph-view, tags view, 
  - templates
  - command-palette
  - publish
  - sync
# redmansion
- goals
  - publish/site
  - api
  - editing: web, app, obfm editor
  - compatible with obsidian: obfm, obsidian, config(attachment, .trash)

- 
- 
- 
- 
- 
- 
- 
- 

# draft
- architecture
  - 内容文件与配置文件分离的思路: 如表格内容与样式分离

- db-based-architecture
  - sync: file > db > webapp

- markdown-query
  - 2way sync of obsidian files and ~~wiki.js~~ 
  - 基于 agentfs 来bash files
  - 可参考 codebase-ast-wiki/graph 的思路来实现 markdown-databases
  - 🤔 实现原理是否与 经典rag流程 `chunking > vectordb ` 类似

- mermaid-chart + bases

- bases
  - export bundle: 将.base文件和相关文件一起导出
# pm
- 支持公开子目录作为site

- 部分内容需要加密的场景，如何解决
  - 需要在cli侧解决

- documentation-ideas
  - docusaurus
  - Starlight

- 类似wiki的场景
  - 可参考 books/library

- 生产力文档
  - 多语言文档, 自动翻译

- 如何支持外部文件

- ide和cli主流的ux都与启动文件夹相关联，而chat并不会自带文件夹而是需要上传文件
  - 可将vscode的文件书隐藏，将chat移到左边来实现目前主流chat的产品ux，没必要单独开发electron app for chat.
- 基于vscode的方案的优点
  - 直接使用基于git的同步

- multi-user/workspace的设计

## ob-bases

- database的技术方案可参考agentfs+just-bash, 以数据库作为数据源，到处markdown方便ai理解
# dev-xp
- 偏ui的plugin，在headless的场景下可能读不到配置，需要在vault中存一份配置，然后server运行时支持相关逻辑
  - headless方案可参考vscode-server

- 对markdown文件的import需求很少，因为可以手动复制粘贴内容

- ob-bases基于文件的设计，似乎很符合grist

- 
- 
- 
- 

# usage-workarounds
- 文件及文件夹不支持自定义排序, 可用带wikilink的文档来指定顺序, 类似 toc目录
# usage-tips
- 文件夹下的与文件夹同名的文件会在点击文件夹时显示, 类似于github的readme

- 
- 
- 
- 
- 

# more
