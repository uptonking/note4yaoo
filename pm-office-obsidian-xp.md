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
  - free to use but not open source
  - local file based, friendly to human and ai
  - 🔗 backlinks: 双链基于[[]]语法, 同名文件的写法是相对路径
  - 📈 bases: 基于文件的多维表格
    - bases 基于文件的设计 方便扩展每行的属性
    - 支持直接编辑单元格
    - Convert CSV records to individual Markdown files and Bases.
    - 支持 导入/导出 csv/excel, 提供独立的webapp
  - graph-view
  - 🔌 plugins
  - rich editor
  - publish
  - sync: version-history, collab
  - canvas
  - slides
  - templates
  - web clipper

- cons
  - 不支持打开单个外部markdown文件， 将外部md拖到ob时默认行为是复制，如果拖到bases默认会增加一行
  - 不支持打开多个vault
  - 不支持类似notion的 block-style dragging
  - publish/webapp 视图层不开源
  - bases 基于文件的设计 难以获取页面内的内容
    - 给block添加properties/元数据, 变通方式是embed file
    - 页面内引用
  - bases
    - 文件架构限制，导致难以实现交换行列， 而benchmark场景有此需求
    - 不支持拖拽排序, 不能在指定位置插入行/列
    - 不支持拖拽导致不支持kanban
  - css-snippets的样式设置是 per-page 的, 同一页面内的元素/bases难以实现不同样式
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
# 🌸 redmansion

> local file based workspace, like notion but with files, bases, backlinks.

- features: productivity > ux
  - embedded-companion-files(ECF): 当使用ofm embed语法嵌入支持的源文件格式时, 会自动创建对应的ECF文件, 并支持切换显示源文件预览视图和方便编辑的ECF视图
    - pdf/image/ocr>md(单向), csv>bases, xlsx>bases, docx>md, pptx>jsoncanvas
    - ❓ 是不是可以embed sqlite
  - bases: formula, schema-change
    - embed csv as bases
  - editing with pagination, unifying markdown/pdf xp
  - pdf backlink/citation/preview
  - file-editor: 不改变原文件的格式, 可利用全局LRU缓存
  - offline-editing
  - sync
  - collab with agent

- goals
  - publish/site: github for obsidian bases
  - editing: web, app, obfm editor
  - api + cli + sdk: md, bases
  - compatible with obsidian: obfm, bases, plugins, config(attachment, .trash)
    - 兼容和扩展plugins在bases方面的能力
  - 不要过于依赖ob的runtime, 充分利用文件系统的优势
  - 类似cloudflare-drop的快速分享
  - offline-capable: 仅本地能工作， 还支持开启云端同步

- ✨ 内置RAG的优点
  - 快速处理用户上传的pdf/docx
  - web search 的结果能快速处理
- 内置coding的优点
  - 方便操作用户本地环境的文件、软件
  - 方便生成动态ui/操作界面

- non-goals
  - 支持md但不支持mdx, mdx 一定不放在core实现， 可能会放在extension， 也可能不支持
  - 非代码优先, 不支持react组建作为内容，如 page.tsx
  - 前端交互相关的功能都是不重要的，包括协作
  - 市面上可用的开源编辑器足够了，不要花过多时间做没人用的细节，集中精力做特色
  - 优先web/desktop, cli不重要

- DRMN主要为本地设计, designed for markdown/bases files
  - 同步方案a: ~~local-file <> local-db <> remote-db~~ , 先操作本地db，再由db同步
    - local-db-client <> remote-db-server, local-db-client <> local-files
    - 优点是思路清晰， 统一的单向数据流
    - 缺点是本地作为数据源，始终拥有全量数据， 可能速度慢且不scale
    - 降低sync复杂度的思路, 本地作为数据源, 自动执行到本地的新增, 到本地的删除需要确认并且默认进回收站
    - 🤔 如果产品主要为本地设计，此方案可行性高
  - 🐛 其他方案b: 在线时连接remote-server/db, 离线时才使用local-server/db，将remote作为数据源能简化同步, 
    - 在线时本地db只做为cache/backup, ui操作全部基于db实现， 本地文件的外部操作由chokidar监控进程通知
    - 架构较为复杂, ui操作需要更新remote-db+local-db+local-files, 本地外部操作需要更新remote-db+local-db
    - 此方案在离线场景下edit，仍然需要实现方案a的 local-file <> local-db <> remote-db, 其中 local-db <> remote-db 的复杂度并没有降低
  - 还可以将 desktop-app/webapp 分开实现
    - 复杂度变高
  - 参考joplin: 支持配置 sync target 如filesystem/joplin-cloud/onedrive, 这样本地的db修改就可以自动同步到files/cloud

- infra-针对本产品的优先级(什么是必须做的, 似乎只有离线编辑)
  - ✨ offline editing
  - partial sync: 必需实现吗
    - 采用snapshot方案的时候也可以通过delta结构+时间戳的方式来实现partial sync
    - 甚至full sync的问题也不大， git 仓库就是这个设计
    - text-sync first, 附件lazy, 很多项目都是类似设计
  - collab with conflict resolution: 简单替代就是LLW, 或提供ui让用户解决冲突或选版本
  - realtime sync

- features-maybe
  - sync daemon
- features-nice
  - bulk renaming

- cms-platform
  - github for obsidian bases, like gitea

- 架构采用client/server模式， 方便实现saas, 
  - web必做，desktop必做，cli非必要， 如何复用架构或数据，降低复杂度
  - desktop app 使用本地文件作为数据源 或 使用db作为数据源 都能实现需求， 但为了方便实现saas，放弃使用本地文件作为数据源的方案
  - 🤔 采用db作为数据源时，要考虑如何支持使用本地db, 使用云端db，计算逻辑在本地，仅数据在云端？
    - 梳理 本地文件 <> 本地db <> 云端db 的同步流程

- cms-cli的参考
  - nocobase

- 
- 
- 
- 
- 
- 
- 

- maybe
  - 实现类似git commit history 的历史记录ux
  - file-metadata as database
  - text-first chat history

- 
- 
- 
- 

## draft-ai

- harness
  - harness工具越来越多, 每个都有自己的配置、特性, 统一管理的难度大、更新维护的复杂度高
  - 🤔 可考虑不做agent的管理, 只做 context 的共享、产物的共享、skills的共享

## draft-rdmn

- dev-to
  - 基础层工作db-schema: replace-editor + pdf-ECF 
  - 2way sync for bases
  - backlink

- chat-as-files
  - every chat is a folder, every message is a file
    - workbuddy采用了此设计, 方便放产物、版本、多AI协作， 以日期为文件夹名
  - 聊天会保存为本地文件, 用bases视图来保存元数据和信息

- 
- 
- 
- 
- 

- later
  - mobile doc agent

- 
- 
- 
- 
- 
- 

## embeddable-companion-files(ECF)

- features
  - portable files
  - easy to read for human/agent
  - ECF is easy to edit as markdown files(before chatting with agent)
  - rich metadata for doc/image/chart
  - fast model switching: 同时支持本地model和api

- 支持各种ocr模型的输出与pdf对比展示
  - 手动创建ECF
  - 代码自动创建ECF
  - 支持自定义ocr的模版如table/chart/image
  - 典型场景: pdf->md, docx->md, xlsx->md, image->md

- 当使用ofm embed语法嵌入支持的源文件格式时, 会自动创建/更新对应的ECF文件, 并支持切换显示源文件预览视图和方便编辑的ECF视图(类似embed bases), ~~甚至bases card view~~ 
  - ECF文件默认保存为文件夹, 默认放在源文件的相同目录, 默认名称为`源文件名[xxx]_ecf`, 为了资料整洁，也可统一放在指定目录, ~~同时也会放在全剧缓存~~ ， 目录内采用 assets/main/.backupYYYYMMddHHmmss 的结构, 其中main内是主内容, .backupN采用assets/main的结构且作为备份会自动删除, 可使用.backupN 的内容替换顶层主文件
  - 一个源文件可以生成多个版本的ECF文件， 依次默认打开`源文件名_ecf`下的顶层main 或 最新日期的 `.backupN/main`
  - 也可以手动创建ECF文件， 就是普通markdown文件
  - 首次打开嵌入了ECF的父文件时，会尝试创建源文件和ECF文件的内容关系, 最好能建立更细粒度的元数据关系，如标题、双链, 具体关联信息可在属性面板查看/编辑
  - 自动更新文本: 修改源文件也会自动更新ECF文件, ~~修改ECF文件会自动更新源文件~~ 
    - 格式转换会丢失少数内容
    - ❓ 双向更新源文件和ECF的复杂度高, 源文件 > 目标文件的单向更新在产品逻辑上更简单、实现也更简单

- goals
  - 兼容性: bases, ofm-embed
  - 同步更新文本
  - 🤔 是不是可以embed sqlite

- non-goals
  - 不会同步更新样式， 因为部分样式在转换时会丢失

- tips
  - 适合embed的是 pdf/docx/xlsx/csv 符合现有bases的心智模型和产品设计
  - 嵌入ECF的父文件还适合记录更新的内容, 但更多的是提供给用户熟悉的pdf视图

- ECF与bases的相同点
  - 支持手动创建bases/ECF文件、通过代码创建
  - 都支持embed使用, 也支持单独打开
  - bases/ECF文件的内容与 一个或多个源文件 关联, ECF的内容会尝试与源文件建立块与块的对应关系
  - excel内容样式与markdown的转换存在损失, 都尝试同步尽可能多的文本内容
  - 在界面上修改ECF视图内容时，也会修改源文件

- ECF与bases的不同点
  - bases的视图内容完全由源文件计算得到因而总是同步变化， 而ECF的内容有自己的数据源所以允许存在数据不一致的问题

- ECF文件和源文件的更新
  - pdf/image/ocr>md, 单向编辑， 就像编辑普通markdown文件
  - csv>bases, 双向
  - xlsx>bases, 双向
  - docx>md, 双向
  - pptx>jsoncanvas/xml
  - sqlite>sql, 双向
  - sqlite只是作为一种参考实现，可以由它更新源文件和ecf

- 冲突处理(ECF由外部更新后)
  - 源文件与ECF的文本内容通常是一致的， 不一致时需要用户处理，支持由用户选择 (docx/xlsx/pdf)生成新的ECF-md 或 ECF-md生成新的源文件(docx/xlsx), 生成新文件后旧的文件(夹)会自动被重命名
  - 参考bases.yaml文件可能失效

- 
- 
- 
- 
- 

### faq-ECF

- 数据丢失问题
  - xlsx 和 markdown 的转换也有损失, 如列宽
  - docx 和 markdown 的转换有损失

- 必需要手动创建ECF文件吗
  - 不是必需, embeddable, embed is not required
  - 产品设计上, 打开pdf/docx/xlsx/image时, 可以手动打开ECF视图模式, 程序会自动在全局临时缓存目录, 但此时的ECF文件编辑时会提示保存到源文件目录否则编辑会丢失, 源文件更新时ECF会自动更新， 缓存的内容始终是最新版不含旧版本
  - 需要手动开启视图， 开启后打开源文件时会自动打开ECF

- 何时使用全局临时缓存，何时使用本地ECF文件
  - 非embed的场景会使用全局临时缓存
  - embed+auto会使用全局临时缓存
  - 明确的embed会使用指定的本地

- 
- 
- 

### later-ECF

- new-split-view
  - markdown and webpage

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
    - 临时方案是 per-page

## sync

- markdown <-> db 的转换可参考 notty/joplin
- markdown/yaml的解析可参考 quartz

## openbases spec

- mdbase

## bases

> a base file is a live query language for the stateful(persisted) markdown files.

- 实现方式3种
  - ❌1 在ssg阶段提前持久化base的结果，在前端仅展示静态数据
    - 维护成本低， 但体验差， 不支持修改, 
    - 不支持大量数据, 对图片支持不好
  - 📌2 server通过解析文件动态计算, 由server来计算， 甚至可支持修改数据/文件
    - 完整的server能力，功能强， 但运营成本高，
    - 支持大量数据，对本地图片支持友好
    - 本地运行时需要设备提供计算能力， 计算大量数据的逻辑不适合放在本地，要考虑低性能移动端
    - 方便基于本地server实现sync/edit
    - free user 支持查看但不可编辑的成本不高， 这样避免方案3为了实现查看引入复杂的数据转换/缓存方案
  - ❌ 3 将数据轻量获取到本地后，存入memorydb/jsondb, 直接在浏览器内存或indexdb计算， 不依赖server(所以 ~~不能~~ 难以修改数据)
    - 🐛 实现复杂度太高, 但能支持动态filter， 低性能移动端的计算能力差
    - 可在浏览器持久化变更数据，然后再手动/自动同步， 此方案可与方案2结合，支持切换数据源/server-url
    - 此方案可结合多MPA多文件webapp拆分数据、懒加载来实现
    - 甚至可引入高级数据操作方案， 如 sqlite-wasm/apache-arrow/duckdb
    - 🛢️ 类似jsonnl的db也方便使用cdn静态化低成本提供
    - 支持大量数据需要优化很多细节
    - 对图片的支持需要单独的方案， 只做缓存的场景可以直接用base64
    - 但本方案适合低成本托管db
    - 本地client的实现没必要搞这么复杂，因为本地client/server逻辑更简单清晰

- later
  - migrate popular notion-database to ob-bases
  - 有时会显示过期数据
- export bundle: 将.base文件和相关文件一起导出
- export view result: 可参考dataview的serializer

- bases-arch
  - bases 基于文件的设计 方便扩展每行的属性
  - 可考虑实现 基于block 来实现， 这样同一页面内的内容也可以实现动态引用/更新

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
- 🤔 产品形态是 markdown sdk？
  - 付费点: bases api, cloud rag for big pdf

- 部分内容需要加密的场景，如何解决
  - 需要在cli侧解决

- wikilinks扩展: pdf-bbox, 支持preview, 甚至可以显示为截图内容
  - 引用pdf内容的场景都可以使用类似wikilinks的设计 + preview
  - 还可以优化图片pdf的搜索体验

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

- 支持公开子目录作为site
  - obsidian vault支持任意文件夹， 注意 此目标需要配置link使用 相对路径 来减少坏链

## ob-bases

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

## maybe

- 类似postman/scalar, 但基于md

- 
- 
- 
- 
- 

# dev-xp
- 需要尽早决定 file/link path 的方案
  - 推荐使用 relative path， 方便将子目录作为vault打开或分享

- 加一个标签到 tags 方便用来快速生成bases

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

- column
  - 列名如何支持显示为link， 一般无此需求， 点击列名一般用来排序

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
