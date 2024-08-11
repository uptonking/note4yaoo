---
title: dev-log-repeat-solutions
tags: [dev, pm, repeat, solutions]
favorited: true
created: 2021-01-08T00:10:18.987Z
modified: 2021-07-20T13:50:23.433Z
---

# dev-log-repeat-solutions

# guide

- tips
  - ~~paas/rendering/web~~ may be the future
  - 涉猎saas解决方案，积累算法、库、框架、模版项目、生态
    - 尝试将算法和技术转化为可复用的产品, 参考yjs+hocuspocus
    - 工具型框架离商业化应用太远, 直接从主流cms/saas中寻找参考
  - 🌰 深入一个项目，开发需要精力，建立生态更需要精力
    - 视图+持久化，前端分析model/view/dataflow, 后端分析数据库设计和优化
    - 分析api的设计，包括扩展ui、api，插件开发，热加载
    - src-code, issues, pr, forks, extensions, most-commented-issues
    - roadmap, open-issues, alternatives
    - 开放能力: extensions, scripts, marketplace
    - pref: 索引、缓存、分库分表、读写分离
    - 文档产品: editor + fileTree + workbenchLayout + search + cmdKeys + settings
  - 💠 architecture-early 需要尽早考虑的架构问题，没有完美的架构
    - 核心架构考虑 server/db/network-socket
    - 早期不要将系统架构设计得过于复杂，会影响开发进度, 甚至产品终止都用不上
    - collaborative的数据结构，冲突处理算法，客户端中心还是服务端中心
    - scale水平扩展/多实例/多租户; http更适合scale; 配置、缓存
    - 数据通信，http/websocket
    - 读多？ 写多？
    - sqlite的流行表明scaling要考虑场景, zulip/jupyterhub私有部署默认支持几千用户但不scale
    - 没有完美的架构，优先支持迭代，不要执着于当下的问题，也许以后就突然想清楚了
    - 先实现业务核心功能， 再考虑如何以sdk/paas的方式提供给使用方，再优化性能
  - 抽空在线体验，工作专注代码
  - data-app
    - specification for pivot table
    - 输入数据input-data-table, 开放数据api，开放应用app-builder
    - 产品方向: 偏设计布局， 偏业务逻辑

- 技术方向js: 前端版/流式版/oplog; 编辑器/ide，多维表格/excel，协作/gitdb; dnd，floating
- 技术扩展js/py: 可拖拽的页面编辑器/lowcode, Excel/kanban, 图表
- 技术产品: client/server版; cms/wiki, airtable/table, db
- 技术可选1: 画板, pdf/ppt-editor, 图形编辑器
- 技术可选2: olap-bi, 大数据系统, 数据库
- 技术可选3: vscode，可参考架构 extensions、capabilities
- 技术可选4: 侧重版本控制的数据库，如dolt, SirixDB, git-like-db
- 玩具尝试1: git+crdt+table+branch/version, 参考类似ckan的data-portal
- roadmap: 
  - 📝 虚拟渲染, 分支版本, 协作冲突, undo/redo
  - 🔀🛢️ crdt版本历史, partial-replica、ivm, delta-db, dynamic-schema/eav, 实时架构
- file-first: notable, hexo
- db-first: joplin, siyuan, nocodb

- 🚀 产品落地
  - 表格类cms, 内容创作与管理
  - 运营数据仪表板
  - sharing table/data pieces/snippets
  - 个人数据管理，开放api，允许其他app获取，参考ckan
  - tags

- 生态与集成, 业务方向考虑实时市场，不要凭空想象
  - office365，从 word/excel 复制粘贴的表格，如果其中有合并的单元格，也能支持正常展示
  - jupyter-notebook, observable-notebook

- marketplace: vscode/jupyter
  - browser-extensions
  - table-capture/shot
  - figma
  - ocr

- 团队版/企业版-features
  - 表单/投票收集与统计，如features
  - 编辑器内的时间变化动态表格
  - 类似多个图表facet的多个表格
  - table in table
  - 移动端优化的表格

## techstacks: rich-editor/builder

- design-system
  - themeable; unstyled/headless; a11y/keyboard-ux
- 💎 editor/WYSIWYG
  - collaborative, block-style, virtualized-render
  - modular/extensible; collaborative; easy-pivotable
  - 📌 prosemirror/tiptap/rich-md, quill/typewriter, slate/wang, lexical; cms/outline
  - block-editor with slash-menu/backlinks
  - pdf
- 💎 excel/data-grid
  - editing, group/pivot, multi-views
  - pivotable; collaborative; formulas
  - 📌 tanstack-table, ag-grid, handsontable, luckysheet/univer, ospreadsheet ; undb/nocodb/ethercalc
  - stream-updates/server-side-infinite-row-model
  - scripting/themeable/canvas/viztable/apache-arrow
  - ~~excel-like~~/~~headless~~
- 💎 collab
  - crdt: yjs, automerge, logux, rga, fluid-framework, hlc
  - log-based: p/couchdb, powersync, kappa-db, event-sourcing
  - eav: triplitdb

## solutions: inter(re)active knowledge-base/wiki

- ✨ cms(content-mgmt)
  - 👉🏻 outline (apache2/sequelize+prosemirror)
  - 👉🏻 strapi      (MIT/knex+slate)
  - 👉🏻 directus   (AGPL/knex+vue3+tinymce5)
  - nocobase   (apache2/sequelize+umi)
  - payloadcms     (MIT/mongoose+slate)
- ✨ airtable-like(data-mgmt)
  - 👉🏻 nocodb     (AGPL/knex+nuxt3)
  - 👉🏻 ethercalc   (MIT/nodejs+redis)
  - locokit        (MIT/knex+vue2)
  - undb          (AGPL/nestjs+mikro-orm+dnd-kit/table)
  - apitable      (AGPL/spring-mybatis+canvas)
  - focalboard    (AGPL/go+react-dnd)
  - rowy       (apache2/firebase+tinymce5)
  - baserow        (MIT/django+nuxt2)
  - ckan/datapian
- ✨ ~~workflow~~ > directus
  - n8n           (AGPL/typeorm+vue2+jsplumb)
  - budibase      (AGPL/knex+svelte)
  - automatisch   (AGPL/knex+graphql+slate)
- ✨ bi
  - 👉🏻 lightdash   (MIT/knex+echarts)
  - superset   (apache2/flask+echarts)
- more
  - notion/confluence/outline
  - airtable/nocodb
  - trello/kanban/jira/linear/asana
  - dropbox/google-drive
  - chat, forum

- ✨ admin-dashboard > strapi
  - react-admin
  - tremor
- ✨ editor-wiki(web+pc)
  - outline
  - notesnook
  - mdSilo

- features
  - local-first/offlineable/localizable
  - collaborative
  - easy pivot table in document
  - interactive-contents: variable, attachment, viz
  - backlinks/bidirectional: [[Wikilinks(stub)]], providing more context around backlink reference
  - relations: trilium-relation-map, trilium-link-map, dendron-hierarchical
  - scientific writing: latex, bibtex, citation，data
  - rich-ui: collapsible, floating, emoji
  - portable format: text format; no vendor lock in; partially export cuz mobile
  - templates
  - es search-ui experience, algolia-docsearch/autocomplete

- byproduct-apps
  - live/reactive-notebook
    - cell-style/nonlinear; reproducible/computational; math
  - dashboard/spaces
    - themeable/configurable/widgets-blocks

- integrations/connections
  - wechat-miniapp、公众号、实时通知
  - github/gitee
  - 腾讯文档
  - 类似outline集成slack
  - 类似superset支持各种数据源

- to-try
  - kibana for meilisearch
# collab
- 多文件的app, 或多或少有点类似知识库
  - 可以参考给普通数据库表添加crdt支持的场景

- version-history
  - 不仅是文档级别的history，还支持项目级别的history，采用branch+merge策略

- collab-framework
  - 所有的操作可由用户执行，也可由ai执行

- high-availability / horizontal-scaling
2  - yjs-hocuspocus, y-redis, fluid-routerlicious 🤔 使用websocket通信是否是错误的架构
  - strapi, nocobase
  - fwk: nestjs, feathers-sync
  - manual: zulip
  - more: overleaf

- 协同类产品要考虑数据和配置是否都要同步的问题
  - 表格的过滤条件
  - 回放操作的进度
  - 搜索
# editor
- tips
  - live edit
  - 随意搭建ui的需求过于灵活，而基于controls的在线配置编辑更实用; 有限定制组件+专题场景

- leading
  - 微软 office/word/excel
  - 腾讯 文档
  - 字节 飞书

- prosemirror
  - atlassian editor
  - rich-markdown-editor + outline
  - milkdown

- react-markdown-editor-lite
  - 基于textarea和React的markdown编辑器，实现简单且清晰，非所见即所得

- more-editor
  - google-docs-like-editor
  - monaco-editor
    - code editor that powers desktop vscode
    - not supported in mobile browsers. not for IE

- 支持多种前端框架的实现
  - tanstack-table/virtual
  - slate-editor, wangEditor, editablejs
  - tiptap-editor, prosekit
# excel
- tips

- react-table /tannerlinsley

- ag-grid /ag-grid

- luckysheet

- more-list-grid
  - x-spreadsheet
  - tabulator 
  - frappe-datatable /frappe
# creators
- marijn /prosemirror/codemirror
  - forum

- Tanner Linsley /tanstack-table
    - https://twitter.com/tannerlinsley
    - https://github.com/tannerlinsley
    - https://github.com/tannerlinsley/react-table

- 胡文召
  - https://x.com/wzhudev

- davidbrochart /jupyter
  - https://x.com/davidbrochart

- Kevin Jahns /yjs
  - https://x.com/kevin_jahns

- Bartosz Sypytkowski /yjs
  - https://x.com/Horusiath

- mweidner037 /fugue
  - https://github.com/mweidner037
  - https://x.com/MatthewWeidner3

- Geoffrey Litt /peritext
  - https://x.com/geoffreylitt

- powersync-partial
  - discord

- Matt Wonlaw /cr-sqlite
  - https://x.com/tantaman
  - https://github.com/tantaman

- tinybase-crdt
  - discord

- triplitdb-eav
  - discord

- 
- 
- 

- watching
  - notion
  - linear
# wishlist
- charting-viz
  - leading
    - echarts
    - d3
    - vega
  - more-charting
    - antvis

- faves
  - design: adobe-spectrum, tailwind
  - editor: prosemirror, codemirror, gutenberg
  - geomapping:mapbox-gl, leaflet
  - geoviz:deck.gl
  - geoprocessing:turfjs, mapnik
  - geo: gdal, esri，计算工具大部分都基于cpp

- design-system
  - tips
  - material
  - carbon
  - spectrum
  - ui: material-ui, ant design, atlaskit , theme-ui, bootstrap
  - design-tokens: polaris-tokens

- dashboard
  - tips
    - 实际仪表板常与业务紧密相关，建议结合window-layout和drag实现
  - coreui
  - creativetim
  - olap(js intensive)

- layout/window-manager
  - tips
    - 常作为app的基础组件
  - golden-layout: 场景丰富功能全面的window
  - elara: demo示例非常酷，特别是layer，dashboard, shell, pic-viewer
  - ventus: 快速切换到窗口平铺预览
  - rc-dock: 类似ide的拖拽停靠效果
# fundamentals
- format
  - excel/csv/office open xml
  - markdown
  - pdf
  - json

- rendering
  - canvas
  - webgl
  - animation
    - FLIP
# dev-xp
- 针对具体业务的前端开发流程
  - 分析需求的主要属性和状态变化临界点
  - 定义数据结构和updateState方法，可以使用主流第三方库提供的api结构
  - 设置初始值
  - 设计action/op/cmd来触发updateState
  - 更新视图
# pm
- ai的能力擅长在翻译 语言 转换
# more
- 20240406: 想做的事情有 灵活的cms、协作系统、支持大量数据的编辑器
  - cms需要在架构层支持配置和存储表和字段元数据
  - 协作系统需要对文本使用特殊的数据结构，还要考虑版本历史/yjs/权限
  - 编辑器在模型层要考虑db架构和更新op采用ot/crdt, 系统中编辑器大多可替换
  - 协作只有部分文本需要YText这类复杂的crdt，表格使用llw-map足够
  - 富文本编辑器和页面编辑器的区别，主要在是否使用conetenteditable、选区

- 视图层的实现可参考: wangeditor/typewriter/autocomplete, 库和应用层不同在于ajax
- 架构参考
  - immutable: prosemirror, slate, wangeditor, typewriter, ospreadsheet, maxgraph
  - functional: wangeditor, typewriter
  - 数据层: ivm-crsqlite
# topic-replay/playback
- usecase
  - replayable workspace
- solutions
  - redux
  - event-sourcing
# topic-collab
- usecase
  - meetings-whiteboard
- solutions
  - ot
  - crdt

- why crdt is hard
- u not need crdt
# topic-collab-git
- usecase
  - branching
- solutions
  - fossil
# topic-db-airtable
- usecase
  - cms/lowcode
  - notion

- 树形数据结构的4种表示
# topic-pm
- 飞书功能的子集
