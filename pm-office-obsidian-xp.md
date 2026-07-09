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
    - bases 基于文件的设计 方便扩展每行的属性
    - 支持直接编辑单元格
    - Convert CSV records to individual Markdown files and Bases.
    - 支持 导入/导出 csv/excel, 提供独立的webapp
  - publish
  - canvas
  - graph-view
  - slides
  - templates
  - sync

- cons
  - 不支持类似notion的 block-style dragging
  - bases 基于文件的设计 难以获取页面内的内容
    - 给block添加properties/元数据
    - 页面内引用
  - bases
    - 文件架构限制，导致难以实现交换行列， 而benchmark场景有此需求
    - 不支持拖拽排序, 不能在指定位置插入行/列
    - 不支持拖拽导致不支持kanban
  - settings-sync 
  - 未提供统一的多语言切换方案

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
  - publish/site: github for obsidian bases
  - editing: web, app, obfm editor
  - api: md, bases
  - compatible with obsidian: obfm, bases, plugins, config(attachment, .trash)
    - 兼容和扩展plugins在bases方面的能力
  - 不要过于依赖ob的runtime, 充分利用文件系统的优势

- cms-platform
  - github for obsidian bases

- 
- 
- 
- 
- 
- 
- 

# draft
- architecture
  - reproducible-workspace: 数据/文件 + 配置 (+ 插件), 可在其他设备直接复用， 这一点上vscode的实现值得参考, 支持多级配置

- .base 的自定义后缀不够方便, 不如用 .base.yml

- bases auto converter: csv <> bases
- 用户手写table, 通过ui自动/手动转换成bases

- ob-cli alternative

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

- tasks
  - TaskNote优点: inline-task-auto-detect, workflow
  - use TaskNote/mdbase-spec as cms, not note
  - TaskNote 容易split， 考虑提供快速merge
  - 检查关系、验证

- multi-column
  - 社区有提供 css/js 插件方案
  - 临时方案可考虑 card view

- properties
  - hide empty properties
  - number类型的属性值， 禁止滚动来出发加减

- css-snippets
  - 调整bases左对齐是全局调整, 修改样式粒度太广, 如何部分左对齐、部分居中

## bases

- later
  - migrate popular notion-database to ob-bases
  - export bundle: 将.base文件和相关文件一起导出
  - 有时会显示过期数据

- group
  - 另一种显示方式是组名不显示在分组上方，而是作为合并单元格显示在左边，这样内容区就显示为连续的表格了

- frontmatter
  - 自动根据内容更新，是否有此需求 auto update from content

- cells
  - 单元格左中右对齐方式需要使用css, 这需要编辑器正确实现移动端的布局

### inline-bases

- later
  - 打开编辑器有时显示code block而不是视图， 或者视图显示的慢
    - read阅读模式此问题不严重，但仍然有明显的渲染闪烁(code快速变视图)

### list-view

- later
  - 不支持显示 property name
  - 大量内容时，实现 懒加载 + 虚拟渲染

### card-view

- later
  - 默认占满页面，ux不友好

- card view 比 list view 展示更友好
  - 支持显示 property name
  - 加大card的宽度到一行仅展示一个card，此时就可以作为list来使用了

### map-view

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

- bases-arch
  - bases 基于文件的设计 方便扩展每行的属性
  - 可考虑实现 基于block 来实现， 这样同一页面内的内容也可以实现动态引用/更新

- inline-bases
  - 实现思路类似在编辑内支持可执行的代码块

- bases list view
  - ✨ 需要支持分页
  - 使用场景: news-feed, 简单评论是否也可以采用list实现
  - 对于类似于 changelog 的场景， 支持查看列表，也支持查看指定日期

- 
- 
- 
- 
- 

- database的技术方案可参考agentfs+just-bash, 以数据库作为数据源，导出文件如markdown方便ai理解

## publish-quartz

- features
  - bases formula计算的列能正常渲染

- 对bases的支持度很低
  - properties默认不渲染
  - table/card/list 显示都是只读的，不能再次filter/sort
  - inline bases交互差
  - embed .base 文件有时未渲染， 因为相对路径解析失败了
  - bases的空内容渲染为 - , 很多cell的内容丢失了

- links
  - 部分 wikilink 404， 因为相对路径解析失败了， 似乎只能解析同级文件夹下的
# dev-xp
- 需要尽早决定 file/link path 的方案

- 加一个标签到 tags 方便用来快速生成bases

- column
  - 列名如何支持显示为link

- ob公开的 api 包含很多 codmeirror 相关的类型定义

- 偏ui的plugin，在headless的场景下可能读不到配置，需要在vault中存一份配置，然后server运行时支持相关逻辑
  - headless方案可参考vscode-server

- 
- 
- 
- 
- 
- 

- 对markdown文件的import需求很少，因为可以手动复制粘贴内容

- keyboard-shortcuts
  - use the keyboard shortcuts Ctrl/Cmd-Alt ←/→ to navigate back and forward.

## bases-xp

- 需要创建bases的note建议添加tags, 这样方便快速筛选

- 
- 
- 
- 

- ob-bases基于文件的设计，似乎很符合grist
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
