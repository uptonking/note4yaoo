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
  - ~~paas/rendering/web/benefit~~ may be the future
  - 抽空在线体验(demo/bookmarks/github-latest)，工作专注代码
  - 涉猎saas解决方案，积累算法、库、框架、模版项目、生态
    - 尝试将算法和技术转化为可复用的产品, 参考yjs+hocuspocus
    - 工具型框架离商业化应用太远, 可直接从主流cms/saas产品中寻找架构或框架参考
    - 好用的开源产品通常license都很严格，如esearch/joplin/drawio(minified)/reader
  - 🌰 深入一个项目，开发需要精力，建立生态更需要精力
    - 视图+持久化，前端分析model/view/dataflow, 后端分析数据库设计和优化
    - 分析api的设计，包括扩展ui、api，插件开发，热加载
    - src-code, issues, pr, forks, extensions, most-commented-issues
    - roadmap, open-issues, alternatives, 竞品
    - 开放能力: extensions, scripts, marketplace
    - pref: 索引、缓存、分库分表、读写分离
    - 典型产品: editor + fileTree + workbenchLayout + search + cmdKeys + settings
  - 🏘️ architecture-early 需要尽早考虑的架构问题，没有完美的架构
    - 核心架构考虑 server/db/network-socket
    - feature-flag: strapi
    - 早期不要将系统架构设计得过于复杂，会影响开发进度, 甚至产品终止都用不上
    - 没有完美的架构，优先支持迭代，不要执着于当下的问题，也许以后就突然想清楚了
    - 先实现业务核心功能， 再考虑如何以sdk/paas的方式提供给使用方，再优化性能
    - 重前端还是重服务端的设计
    - collaborative的数据结构，冲突处理算法，客户端中心还是服务端中心
    - scale水平扩展/多实例/多租户; http更适合scale; shared配置、缓存
    - 数据通信，http/websocket
    - 偏实时系统的断连恢复如何实现
    - 读多？ 写多？
    - api/接口 冪等调用
    - 系统解耦: vscode在扩展崩溃时仍可编辑， clacky保证ai断联/LSP断联/未激活时仍可编辑
    - sqlite的流行表明scaling要考虑场景, zulip/jupyterhub私有部署默认支持几千用户但不scale
    - 系统的性能受第三方资源如github的fetch api的限制，设计初期要想办法避免
    - 计算密集型的feature可尝试多层架构，如大模型llm/ocr
    - 重技术的业务开发时灵活性兼容性比性能更重要, Compatibility, Flexibility, Perf
    - frontend: animation, 多标签, 刷新页面是否恢复状态, 换设备是否恢复状态
    - backend: orm vs sql
    - 采用第三方包前期开发快，后期跟随升级及处理breaking changes的工作量会增加，要做取舍
  - data-app
    - specification for pivot table
    - 输入数据input-data-table, 开放数据api，开放应用app-builder
    - 产品方向: 偏设计布局， 偏业务逻辑
    - 网盘: 数据展示和回收站，经典使用场景，大多数cms都有且用来存储资源

- lts-tech-stack 可协作/同步(离线)、版本历史、自动化
  - 选择技术栈时，多问自己，是否愿意，是否有条件持续维护/轻度封装/仅使用
  - techstacks: editor, excel, workflow/ai, drive, whiteboard
  - products: knowledgebase + workflow, 卖工具(铲子)比卖产品更长久
  - 🌰 lts: vscode/ide/ ~~office~~ , git/vcs(history/sync), LSP/MCP(backlink)/auto
    - 20230630: editor/slate  + table   + collab
    - 20250129: editor/vscode + triplit + sync(powersync/zerosync)
  - vscode: 🏘️ 支持BS/CS架构, monaco-editor + electron, coder-server
  - codemirror/prosemirror: state + view + commands + transform/ot/collab + virtualized
    - 对内容的块级抽象，可参考colanode
  - version-history: rrweb, diff, format(.fodt), video-but-auto-update
  - collab: room-playground❓, 非auth版本的简易测试环境
  - automation/workflow/scheduler: n8n, activepieces, lowcode
  - format parser/generator: json, markdown
  - office: suite-docs, outline, handsontable, xlsx, revealjs-ts+PPTist, pdf-lib
  - plugin/extension: sandbox, e2b
  - rspack: js plugin; rspack/rolldown-wasm
  - ai: 擅长text-gen
  - 考虑维护/fork旧版项目: codemirror5-lang/demo, atlaskit-editor-eg, mxgraph-demo
  - 考虑port主流项目: codemirror-go/rust
  - ~~animation: motion(dom/svg)~~ 

- 技术细节(editor): virtualized, draggable, table(eav)
- 技术产品(reuse):  cm-devtools, noseditor, collab-hocuspocus
  - 做合并功能如llm支持vlm/asr/tts, claude自己做plugins/skills, vsocode内置部分插件, 或者做闭源功能的开放版
- 技术方向js: 协作/ver-`gitdb`/partial-sync, 编辑器/ide, 多维表格/excel; scaling/HA-socket; dnd, floating; 前端版/流式版/oplog; 
  - 纯前端/客户端的产品其实商业化的能力不强，付费特性一般是存储(回放)、计算(后台、并发、自动化)
- 技术扩展js/py: 可拖拽的页面编辑器/lowcode, Excel/kanban, 图表
- 通用能力: collab, version-history+sync+replay, automation, search
  - ai-chat, auth, payment
- ai能力: rag, search, vector, 知识库搜索与对话
- 技术业务: client/server版; cms/wiki, airtable/table, db
- 技术可选1: 画板, pdf/ppt-editor, 图形编辑器
- 技术可选2: olap-bi, 大数据系统, 数据库
- 技术可选3: vscode, 可参考架构 extensions、capabilities
- 技术可选4: 侧重版本控制的数据库，如dolt, SirixDB, git-like-db
- 玩具尝试1: git+crdt+table+branch/version, 参考类似ckan的data-portal
- 🎯 roadmap: virtualized-draggable-table, cm-devtools, cm-noseditor, cm-hocus
  - 📝 编辑器，协作同步，版本分支， ~~虚拟渲染, 分支版本, 协作冲突, undo/redo~~ 
  - 🔀🛢️ crdt版本历史, partial-replica、ivm, delta-db, 实时架构
  - version-history+sync(for table/pdf), replay, motion/live-photo(标准)
  - replay(editor+tree+layout), reproducible
  - dynamic-schema/eav
  - 基于ast的架构: reka, tango-lowcode, ast优化常使用bytecode(data+logic)
  - sourcegraph
  - 支持输出canvas，为了分享或安全
- 🛢️ 数据存储架构
  - file-first
    - usecases: vscode, obsidian, notable, ssg(hexo), llamaindex, claude-code
    - pros: open and portable, agent-memory
    - cons: not scale well, conflicts, large-file-read/write
  - db-first
    - usecases: RAG, git, joplin, siyuan, 多维表格/nocodb, logseq
    - pros: advanced-query, collab/sync, easier history, client/server-arch, auth, validate, graph-relations
    - cons: complex-infra
  - hybrid-file-db
    - git
    - hive, iceberg, deltalake
  - 代码文件与数据库紧密结合的方案示例，可参考git/docx-zip
  - 代码与数据库结合来更新应用程序(app/webapp)的方案，可参考aquameta/couchapp/reka/sourcegraph
- server-first
  - vscode/cline-cli(从客户端重构为c/s架构) 都从本地计算迁移到了服务端计算
  - codesandbox从nodebox(纯浏览器客户端)转向devbox(服务端)
  - apitable(前同事liuyi告知从浏览器转向服务端), affine(server-native-rafactor)
  - lmstudio-v0.4: core of the LM Studio packaged to be server-native
  - powersync
  - replicache/zerosync
- client-first
  - usecases: webcontainer/nodebox
  - claude-code, codex
  - client-first对于多实例的场景，注意处理database-lock, 比如chrome/edge访问访问网站的场景
    - 还对协作冲突处理不友好
- cli-first
  - 很多项目都迁移到了cli, 如lmstudio, claude-cowork, codex-app

- 🚀 产品落地
  - 侧重表格的cms, 内容创作与管理
  - 运营数据仪表板(bi)
  - sharing table/data pieces/snippets
  - 个人数据管理, 开放api，允许其他app获取，参考ckan
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
  - 移动端优化的表格
  - 表单/投票收集与统计，如features
  - 编辑器内的时间变化动态表格
  - 类似多个图表facet的多个表格
  - table in table

## techstacks: rich-editor/builder

- design-system
  - themeable; unstyled/headless; a11y/keyboard-ux
- 💎 editor/WYSIWYG
  - collaborative, block-style, virtualized-render
  - modular/extensible; collaborative; easy-pivotable
  - 📌 prosemirror/tiptap/rich-md, quill/typewriter, slate/wang, lexical; cms/outline
  - block-editor with slash-menu/backlinks
  - pdf
  - edit-image: 虽然不是编辑器的核心，但很实用且难做好
- 💎 excel/data-grid
  - editing, group/pivot, multi-views
  - pivotable; collaborative; formulas
  - 📌 tanstack-table, ag-grid, handsontable, luckysheet/univer, ospreadsheet; undb/nocodb/ethercalc
  - stream-updates/server-side-infinite-row-model
  - scripting/themeable/canvas/viztable/apache-arrow
  - ~~excel-like~~/~~headless~~ 
- 💎 collab
  - crdt: yjs, automerge, logux, rga, fluid-framework, hlc
  - log-based: ~~p/couchdb~~ , powersync, kappa-db, event-sourcing
  - eav: triplitdb

- 通用能力/features
  - collab, realtime
  - version-history + sync
  - 操作与回放, time travel，倍速播放
  - automation
  - ai

## solutions: inter(re)active knowledgebase/wiki

- ✨ cms(content-mgmt)
  - 👉 suite-docs  (MIT/django+blocknote)
  - 👉🏻 strapi      (MIT/knex+slate)
  - directus      (AGPL/knex+vue3+tinymce5)
  - odoo          (LGPL/python+owl)
  - huly-platform  (EPL/tiptap/svelte//🐞jira)
  - zulip      (apache2/django)
  - outline    (apache2/sequelize+prosemirror)
  - think          (MIT/typeorm+tiptap)
  - nocobase   (apache2/sequelize+umi)
  - payloadcms     (MIT/drizzle+slate)
- ✨ airtable-like(data-mgmt)
  - 👉 colanode(apache2/kysely🛢️+tiptap)
  - 👉🏻 grist   (apache2/typeorm+backbone)
  - 👉🏻 nocodb     (AGPL/knex+nuxt3)
  - ethercalc      (MIT/nodejs+redis)
  - baserow        (MIT/django+nuxt2)
  - rowy       (apache2/firebase+tinymce5)
  - locokit        (MIT/knex+vue2)
  - undb          (AGPL/nestjs+mikro-orm+dnd-kit/table)
  - apitable      (AGPL/spring-mybatis+canvas)
  - focalboard    (AGPL/go+react-dnd)
  - ckan/datapian
- ✨ workflow/automation (eg, directus)
  - 👉🏻 activepieces(MIT/typeorm)
  - 👉🏻 n8n        (AGPL/typeorm+vue2+jsplumb)
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

- reusable
- ✨ admin/dashboard > strapi
  - react-admin
  - tremor
  - fwk: react, nextjs, tanstack
- ✨ editor-wiki(web+pc)
  - outline
  - notesnook
  - mdSilo
- file-manager
  - vscode-like
  - jupyter

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

- 视图层的实现可参考: wangeditor/typewriter/autocomplete, 库和应用层不同在于ajax

- 架构参考
- immutable: prosemirror, slate, wangeditor, typewriter, ospreadsheet, maxgraph
- functional: wangeditor, typewriter, tanstack-table
  - ?: dexie
  - date-fns
  - feathersjs
- 数据层: ivm-crsqlite/zero-sync

### solutions-cases 💡

- partial-sync
  - 实现方案可参考成熟数据库的streaming，一般与业务表相关
  - zerosync: query-based sync
  - powersync
  - triplit
  - sqlsync/Graft(rust)
  - evolu
  - garden-co/jazz

- ivm/incremental-view-maintenance
  - zero-sync
  - electric-sql/d2ts
  - web前端的reactive实现
  - 数据库的materialized view
  - event sourcing
  - bundler的热加载，如turbopack
  - 编译器的热更新

- event-sourcing
  - livestore

- 系统提供很多配置项的设计
  - webpack
  - vscode settings
  - npmrc
  - 手机系统的设置

- replay
  - 回放时可与执行时显示不同的视图，如将edit显示为diff，显示debug信息
  - 基于代码的回放能解决视频难以实时更新的问题, video-but-auto-update

- playground
  - monaco-editor
  - https://electric-ai-chat.examples.electric-sql.com/

- 重前端架构的优点
  - 无需服务器，或对服务器要求低
  - 容易快速响应用户交互
- 重前端架构的缺点
  - 刷新页面或关闭页面容易导致数据丢失或数据不一致

- 大量小文件的存储方式
  - 可参考github的方案
# collab
- 多文件的app, 或多或少有点类似知识库
  - 可以参考给普通数据库表添加crdt支持的场景

- version-history
  - 不仅是文档级别的history，还支持项目级别的history，采用branch+merge策略
  - 另一种思路: agent执行action后，整个repo都能回到指定action的时刻，类似git回到某个commit的状态

- collab-framework
  - 采用基于事件的架构，所有的操作可由用户执行，也可由ai执行

- high-availability / horizontal-scaling
  - 实现参考: yjs-hocuspocus, y-redis, fluid-routerlicious 🤔 使用websocket通信是否是错误的架构(mq更好)
  - strapi, nocobase
  - fwk: nestjs, feathers-sync
  - manual-ha: zulip
  - more: overleaf(pro-only)

- 协同类产品要考虑数据和配置是否都要同步的问题
  - 表格的过滤条件
  - 回放操作的进度
  - 搜索关键词
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

- 使用preact做前端也支持其他框架: 
  - blocky-editor, tui.grid, gridjs, logicFlow, autocomplete
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

- 胡文召 /univer
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
- job-hunting
  - codemirror / prosemirror
  - jupyter
  - 协同 ot算法 开发 yjs 协同编辑
  - 低代码(易商业化，技术框架很难商业化) automation/rpa
  - 知识库 文档

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

## rewrite-to 🛝👾

- prosemirror
  - columns
  - code-diff
- codemirror
  - monaco-diff
- vscode 
  - obsidian

- handsontable: database, grist
- grist: ember to agnostic/react

- pptist: vue to agnostic/react

- papermerge
  - paperless-ngx: nested tags, ai

- bentopdf backport
- PyMuPDF

- pdf-proofreading
  - word
  - excel

- janai
  - lmstudio-cli

- web-clipper

- git-graph

- timeline

- 
- 
- 
- 

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

- 维护现有系统时修改与添加特性
  - 添加属性不如添加方法，可以让使用方自定义方法的内容与具体逻辑，
    - 一般可以分别提供get/set方法
    - 提供配置方法可以让使用方随时随地调用方法，而提供配置属性的方案一般只在初始化时
  - 添加属性或方法后要注意提供清理方法或实现自动清理
# pm
- ai的能力擅长在翻译 语言 转换
# marketing
- 用户留存分析
  - 总体用户情况4x3x2: 4个场景nodejs/python/ruby/go, 3个规模大/中/小, 2大类别toB/toC(实测这种方式效果不好，大规模用户案例一直为空, 按用户使用场景分类更实用)
# more-work-xp
- 20240406: 想做的事情有 灵活的cms、协作系统、支持大量数据的编辑器
  - cms需要在架构层支持 配置和存储 表和字段 的元数据, 可参考directus/nocodb
  - 协作系统需要对文本使用特殊的数据结构，还要考虑版本历史/权限/yjs
  - 编辑器在模型层要考虑db架构和更新op采用ot/crdt, 系统中编辑器大多可替换
  - 协作只有部分文本需要YText这类复杂的crdt，表格使用llw-map足够
  - 富文本编辑器和页面编辑器的区别，主要在是否使用conetenteditable、选区
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
