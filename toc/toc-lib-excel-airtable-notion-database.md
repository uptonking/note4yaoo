---
title: toc-lib-excel-airtable-notion-database
tags: [airtable, grid, list, notion-database, table, toc]
created: 2022-01-30T19:35:55.709Z
modified: 2022-08-21T10:02:05.129Z
---

# toc-lib-excel-airtable-notion-database

# guide

- ali-LowCodeEngine目前仅支持生成React的前端代码
  - 开发成本固然低了，造出来的代码 **维护成本** 太高了
  - 这种东西，不会编程的人对他来说太复杂了，会编程的人来说太繁琐了。

- airtable-like的产品的方向
  - 偏后端，偏api，类似strapi通过拖拽ui字段生成rest crud api，即headless cms
  - 偏前端，类似airtable的通用表格组件，提供各种数据源的集成
  - 偏向automation

- 🆚️ table-builder vs page-builder/支持表格的页面编辑器  🤔有什么区别
  - nocodb支持现有的外部数据源，而页面编辑器的数据一般都是手动输入到系统内部数据库
  - 页面编辑器的功能更杂糅，特色功能点和优势不明显

- lowcode数据库层实现细节
  - 参考strapi实现table+audit-log
  - 参考apitable/directus实现以oplog为数据源的业务数据层
  - 基于oplog实现业务的案例: redux, event-store

- 🤔 难点
  - 动态修改数据类型、修改schema

- resources
  - https://github.com/topics/notion-database
  - [A More Human Approach To Databases](https://ccorcos.github.io/filing-cabinets/)
    - Notion 工程师 Chet 以警察信息管理系统为例，用普通人能理解的大白话，从文件、文件夹、文件柜逐步介绍关系型数据库的构成和实现原理
  - [Maybe some misunderstanding of how SQL DB indexes work?](https://github.com/ccorcos/tuple-database/issues/11)
  - [什么是比较好的低代码产品_Tw93](https://zhuanlan.zhihu.com/p/596474809): platform, baas, cms, workflow, airtable-like
# popular
- react-datasheet-grid /259Star/MIT/202305/ts
  - https://github.com/nick-keller/react-datasheet-grid
  - https://github.com/Equify/react-datasheet-grid
  - https://react-datasheet-grid.netlify.app/docs/features
  - more like Airtable or Notion and less like Excel in the sense that instead of dealing with individual cells it deals with entire rows, and each column is responsible for a single property of each row
  - 依赖react、tanstack-virtual、react-resize-detector
  - 默认可编辑单元格
  - 操作支持获取operation对象
  - Supports copy/pasting to and from Excel, Google-sheet...
  - Virtualized rows and columns, supports hundreds of thousands of rows
  - undo支持撤销编辑单元格，不支持撤销添加行
    - [Is there anyway I can implement Undo, Update button just after addRow button ?](https://github.com/nick-keller/react-datasheet-grid/discussions/221)
  - [V2 status update_202106](https://github.com/Equify/react-datasheet-grid/issues/37)
  - [Feature Roadmap_202106](https://github.com/Equify/react-datasheet-grid/issues/38)
  - Fast
    - can easily handle hundreds of thousands of rows thanks to its virtualized architecture.
    - Renders have been optimized to the strict minimum, follow the performance guides 
  - Customizable
    - Control every behavior of the spreadsheet, implement you own widgets, and customize the style of DSG to match your app.
  - Feature rich
    - Supports copy/pasting to and from Excel, Google-sheet, Notion
    - Keyboard navigation and shortcuts fully-supported

- https://github.com/archit-p/editable-react-table
  - React table built to resemble a database.

- obsidian dataview /5.8kStar/MIT/202312/ts
  - https://github.com/blacksmithgu/obsidian-dataview
  - https://blacksmithgu.github.io/obsidian-dataview/
  - A high-performance data index and query language over Markdown files, for obsidian
  - Treat your Obsidian Vault as a database which you can query from. 
  - Provides a JavaScript API and pipeline-based query language for filtering, sorting, and extracting data from Markdown pages.
  - **Dataview generates data from your vault by pulling information from Markdown frontmatter and Inline fields**.
  - Markdown frontmatter is arbitrary YAML enclosed by `---` at the top of a markdown document which can store metadata about that document.
  - Inline fields are a Dataview feature which allow you to write metadata directly inline in your markdown document via `Key:: Value` syntax.
  - [Obsidian Dataview: Turn Obsidian Vault into a database you can query from | Hacker News_202205](https://news.ycombinator.com/item?id=31407781)
  - https://github.com/obsidianmd/obsidian-releases
    - Obsidian is not open source software and this repo DOES NOT contain the source code of Obsidian. 
    - However, if you wish to contribute to Obsidian, you can easily do so with our extensive plugin system.
  - https://github.com/blacksmithgu/datacore /MIT
    - Datacore is a work-in-progress re-imagining of Dataview with a focus on 2-10x better query and rendering performance, as well as fully interactible views.
    - Datacore is fundamentally the same thing as dataview - an index over Markdown files that supports live-updating views and metadata. 
    - However, Datacore focuses on substantial index changes for performance, as well as a new sleek UI which completely replaces traditional Dataview queries. 
    - Datacore supports all query operations that Dataview does, with some extra functionality.
    - WYSIWYG Views: Datacore queries now use a responsive table view and can be manipulated with a table editor much more akin to what you would see in places like Notion and Airtable.
    - Live Editing: Values inside of table views can now be edited; task views include more nuanced rendering of metadata like due date and more operations for manipulating tasks directly.
    - Live Editing: Values inside of table views can now be edited; task views include more nuanced rendering of metadata like due date and more operations for manipulating tasks directly.
  - https://github.com/RafaelGB/obsidian-db-folder
    - Obsidian Plugin to Allow Notion like database based on folders

- undb /20Star/AGPLv3/202304/ts/参考前端后端
  - https://github.com/undb-xyz/undb
  - https://www.undb.xyz/
  - https://docs.undb.xyz/
  - Private first, unified, self-hosted no code database.
  - Open-source Airtable alternative
  - 可在redux-devtools中查看数据结构
  - 前端依赖 tanstack-table、dnd-kit、redux-toolkit、emotion、@loadable/component、jotai、react-hook-form、trpc
  - 后端依赖 nestjs、mikro-orm、trpc、undb
  - 示例使用sqlite
  - 用户在界面上创建表时，数据库层也会添加一张新表
  - [feature/frontend next_20230503(v0.3), 前端迁移到svelte](https://github.com/undb-xyz/undb/pull/908)
    - 41fa03d9bfbc9b5072266ad94c9532ccdcf25a68

- nocodb /33kStar/AGPLv3/202212/ts/vue/参考后端/多视图
  - https://github.com/nocodb/nocodb
  - https://nocodb.com/
  - [Development Setup](https://docs.nocodb.com/engineering/development-setup/)
  - The Open Source Airtable Alternative
  - Turns any MySQL, PostgreSQL, SQL Server, SQLite & MariaDB into a smart-spreadsheet
  - 后端依赖 express、knex、ioredis、passport、request
  - 前端依赖 nuxt3、ant-design-vue.v3、vueuse、vue-flow(chart)、monaco-editor、d3-scale、dayjs、vuedraggable、xlsx
  - 示例使用sqlite
  - 用户在界面上创建表时，数据库层也会添加一张新表
  - 支持提供返回表中数据的api
  - 支持现有数据库，不需要导入数据: We transform any existing databases MySQL, Postgres, SQL Server & SQLite databases into a spreadsheet.
  - 主要功能模块
    - 多种视图ui
    - 管理后台、仪表板
    - 团队管理
    - 支持外部数据源
    - 表格数据自动生成api
    - 支持公式、rollup
  - Search, sort, filter, hide columns with uber ease
  - Create Views : Grid, Gallery, Kanban, Form
  - Database: Any SQL (postgres, mysql, sqlite, maria DB, SQL server)
  - API: REST and graphql
  - [Show HN: NocoDB – Open-Source Airtable Alternative | Hacker News _202105](https://news.ycombinator.com/item?id=27303783)
  - [Nocodb with MongoDB _202205](https://github.com/nocodb/nocodb/discussions/2072)
    - Sorry, not at the moment
  - [Feature : NoSQL DB support 暂不支持 _202105](https://github.com/nocodb/nocodb/issues/184)
  - [Feature : Import data from external source _202205](https://github.com/nocodb/nocodb/issues/2052)

- locokit /47Star/MIT🌹/202301/ts/vue/参考后端/后端依赖pg的schema特性
  - https://github.com/locokit/locokit
  - https://locokit.io/
  - LocoKit is an AirTable alternative, providing database management as a spreadsheet and an app builder.
  - 不支持除表格外的其他视图
  - 后端依赖feathers4、knex.v0.21.5旧版
  - 前端依赖vue2、turf、mapbox-gl.v1、monaco-editor、xlsx、marked
  - 示例使用postgresql
  - 用户在界面上创建workspace1时，pg数据库会创建一个新的名为workspace1的schema
  - 用户在界面上创建表T1时，会在public schema的`table_row`表上插入数据，并在workspace1 schema下创建名为T1的view
  - 添加表格定义和数据的入口在workspace名称右上角的设置按钮，可设置数据源、page-builder、cms页面与结构、自动化流程、权限、用户与组、workspace配置
  - 主要功能模块
    - 数据库设计与数据录入
    - 前端cms页面与视图
    - workspace管理
    - 成员与权限
    - Processes/Workflows with a webhook mechanism
  - [[roadmap] API over SQL / Nuxt 3 / Feathers 5 / Pinia](https://github.com/locokit/locokit/issues/151)
    - 正在迁移到nuxt3+pinia(vue store)+feathers5

- teable /80Star/AGPLv3/202403/ts
  - https://github.com/teableio/teable
  - https://teable.io/
  - https://app.teable.io/share/shrVgdLiOvNQABtW0yX/view
  - fast, Real-time, Professional, Developer friendly, No code database built on Postgres
  - uses a spreadsheet-like interface to create complex enterprise-level database applications. 
  - 表格基于canvas实现
  - 后端依赖nestjs、@keyv/sqlite、sharedb、passport、opentelemetry、prisma、knex、next、ts-pattern、zod
  - 前端依赖nextjs、zustand、shadcn-ui、codemirror6、g6、dnd-kit、emoji-mart、tanstack-table.v8、echarts5、knex、react-grid-layout、react-hook-form、react-markdown、remark-gfm
  - Formula Support: Input mathematical and logical formulas to auto-calculate values.
  - Aggregation Function: Automatically summarize statistics for each column, providing instant calculations like sum, average, count, max, and min for streamlined data analysis.
  - Multiple Views
    - Grid
    - Form
    - wip: Kanban, Calendar,Gallery,Gantt,Timeline
  - wip
    - Undo/Redo
    - Bring your own database
    - Support for multiple databases
    - Row Styling & Conditional Formatting
    - Charts & Visualization Tools
    - Comments & Annotations
    - Find & Replace
    - Extensions
    - Automation

- nocobase /3.7kStar/apache2(core)🌹 + AGPL(plugin)/202212/ts/国内
  - https://github.com/nocobase/nocobase
  - https://www.nocobase.com/
  - [源码安装](https://docs-cn.nocobase.com/welcome/getting-started/installation/git-clone)
  - 易扩展的开源无代码开发平台
  - NocoBase is a scalability-first, open-source no-code/low-code development platform.
  - 后端依赖 koa、sequelize.v6
  - 前端依赖 umi、antd、g2plot、ahooks、dnd-kit、formily、marked、react-iframe、react-quill、react-router5
  - 示例使用sqlite
  - 用户在界面上创建表时，数据库层也会添加一张新表
  - 提供了tree结构的4种存储方式，邻接表、闭包表、路径枚举、嵌套集
  - 支持应用层的插件系统，安装后需要刷新页面
  - 不直接支持输出表格的crud api，但提供了sdk文档，自己实现比较方便
  - 可配置表格工具条菜单项、添加行，也可配置页面菜单
    - 从这个角度看，headless cms更灵活
  - 采用数据结构与使用界面分离的设计思路
    - 可以为数据表创建任意数量、任意形态的区块（数据视图），
    - 每个区块里可以定义不同的样式、文案、操作
  - you can configure the user interface directly with WYSIWYG operations.
  - Everything is a plugin, all new features can be implemented by developing and installing plugins
  - [change license of plugins-AGPLv3_20230111, v0.8.1 > v0.9.0](https://github.com/nocobase/nocobase/pull/1350)

- focalboard /10.3kStar/AGPL-src + MIT-bin/202203/ts/go/偏看板/参考前端/squirrel-sql-builder
  - https://github.com/mattermost/focalboard
  - https://www.focalboard.com/
  - an open source, multilingual, self-hosted project management tool that's an alternative to Trello, Notion, and Asana.
  - 前端依赖 @reduxjs/toolkit、@tippyjs/react、draft-js、@fullcalendar/react、imagemin-svgo、marked、moment、nanoevents、react-dnd.v14、react-hot-keys、react-intl、react-router-dom.v5
  - 示例使用sqlite
  - Focalboard comes in two main editions:
    - Personal Desktop: A stand-alone single-user Mac, Windows, or Linux desktop app for your todos and personal projects.
    - Mattermost Boards: A self-hosted or cloud server for your team to plan and collaborate.
  - [Focalboard Personal and Plugin Editions Announcement_20230430](https://github.com/mattermost/focalboard/discussions/4645)
    - we won’t be adding any new enhancements

- rowy /4kStar/apache2🌹/202212/ts/firebase/示例丰富/参考前端
  - https://github.com/rowyio/rowy
  - http://rowy.io/
  - https://demo.rowy.io/
  - Rowy is an open-source low-code platform for Firebase and Firestore.
  - 前端依赖mui5、tanstack-table、tinymce5、monaco-editor、jotai、swr、react-dnd
  - 后端依赖firebase
  - 不支持firebase外的其他数据库、数据源，但在开发中
  - 不支持除表格外的其他视图
  - Airtable-like UI with cloud functions workflows in JS/TS, all in your browser.
  - Manage Firestore data in a spreadsheet-like UI, write Cloud Functions effortlessly in the browser
  - Powerful spreadsheet interface for Firestore
  - 30+ fields supported
  - [Firetable is now Rowy_202110](https://news.ycombinator.com/item?id=28768261)
  - [When will MySQL be supported](https://github.com/rowyio/rowy/discussions/1051)
    - we're currently(202301) working on the support for PostgreSQL with Rowy
  - [Abstracting the UI to be compatible with any database](https://github.com/rowyio/rowy/issues/228)
    - long term
  - [[Offtop] Supporting Supabase](https://github.com/rowyio/rowy/discussions/806)
    - I am aware that Supabase provides a builtin CMS, Interested to know which parts of Rowy you miss the most?
    - I think supporting postgres directly doesn't make sense, as we have nocodb for that, who've done a lot of stuff already. So supporting supabase will bring a bigger benefit, as they're no solutions on the market for this problem atm.
  - https://demo.rowy.io/table/allFieldTypes
    - 给出了常用字段类型的示例
  - firetable /36Star/apache2/202108/ts
    - https://github.com/Antler-VC/firetable
    - Excel/Google Sheets like UI for Firebase/Firestore. No more admin portals!
    - https://github.com/FiretableProject/firetable

- grist-core /5.3kStar/apache2🌹/202311/ts/参考后端
  - https://github.com/gristlabs/grist-core
  - https://support.getgrist.com/
  - https://docs.getgrist.com/
  - Grist is a modern relational spreadsheet. 
  - 表格不支持视图切换，支持各种widgets，类似dashboard
  - 前端依赖backbone-model/events、knockout-observable、jquery、bootstrap3、ace-builds、exceljs
  - 后端依赖typeorm、express、grain-rpc
  - 示例使用sqlite
  - 用户在界面上创建表T1时，server会在主数据库会添加数据元信息记录，表T1的实际数据在本地`grist-core/docs`文件夹，🧐 用户创建的每个document对应一个sqlite格式的`.grist`文件，用户创建的每张表对应.grist数据库中的一张表，.grist数据库中还包含视图、权限、action等业务数据和元数据
  - It combines the flexibility of a spreadsheet with the robustness of a database to organize your data and make you more productive.
  - Columns work like they do in databases.
  - Columns can be filled by formula
  - A portable, self-contained format. Based on SQLite
  - Full Python syntax is supported, and the standard library.
  - `grist-core` has what you need to run a powerful spreadsheet hosting server. 
  - And to show Grist spreadsheets on a website without any special back-end support, your options include `grist-static`.
  - Grist spreadsheets by default store a lot of history in the `.grist` file. You can prune that history by building grist-core
  - [Offline first support_202212](https://github.com/gristlabs/grist-core/issues/380)
    - we tried Grist as a conventional SaaS app, and that is when we started accumulating users.
    - Grist has two levels. There's a "home" database, which keeps track of users/sites/workspaces/documents, and that uses postgresql/sqlite via `typeorm`. Then, each individual document has its own database, which is sqlite accessed directly via `node-sqlite3`.
  - [How to make snapshots work on self-hosted ?_202211](https://github.com/gristlabs/grist-core/issues/359)
    - we don't have an implementation of snapshots that works directly on a plain file system, so snapshots don't do anything useful in grist-core. 
    - For our SaaS, we have an implementation for managing document versions in AWS S3. Grist Enterprise includes that implementation
  - [Grist is a modern, relational spreadsheet | Hacker News_202311](https://news.ycombinator.com/item?id=38080951)
  - https://github.com/gristlabs/grist-static /apache2/ts
    - https://gristlabs.github.io/grist-static/
    - Showing Grist spreadsheets on a static website, without a special backend.
    - Use Grist as the PDF of data
    - Changes aren't stored. Changes are not shared with other viewers.
    - No specific access control.
    - No special server is needed for grist-static, it works straight from a CDN or any standard web server.
    - Grist spreadsheets by default store a lot of history in the `.grist` file. You can prune that history
  - https://github.com/gristlabs/grist-ee
    - The source code for self-managed Grist Enterprise.
  - https://github.com/gristlabs/grist-electron /apache2/ts
    - Desktop Grist, packaged with Electron

- irelia /18Star/apache2/202301/ts/python/inactive
  - https://github.com/IreliaTable/irelia
  - https://ireliatable.github.io/irelia-web/
  - 依赖 gristlabs/grist-core、backbone、knockout、jquery
  - Irelia is a modern relational spreadsheet. 
  - Python formulas. Full Python syntax is supported, and the standard library.
  - A portable, self-contained format based on SQLite
  - Irelia formulas in documents will be run using Python executed directly on your machine.

- apitable /2.3kStar/AGPLv3/202301/ts/java/维格表团队
  - https://github.com/apitable/apitable
  - https://apitable.com/
  - [developer-guide](https://github.com/apitable/apitable/blob/develop/docs/readme/zh-CN/docs/contribute/developer-guide.md)
  - [Developer Quick Start](https://apitable.getoutline.com/s/751b142b-866f-4174-a5f1-a2975f85ad41/doc/developer-quick-start-zofpBpXg9A)
  - API-oriented low-code platform for building collaborative apps and better than all other Airtable open-source alternatives
  - 后端依赖 spring-boot、mybatis、easyexcel、grpc、protobuf、nestjs
  - 前端依赖 antd、ahooks、redux、exceljs、konva、markdown-it、react-quill、react-dnd、slate
  - 示例使用mysql
  - 用户的所有操作都记录在`datasheet_changeset`这张表，该表的`operations`字段存储了用户操作的元信息和用户输入的数据如AddRecords/SetRecords/SetFieldAttr/DeleteField，业务表和view数据会据此计算得到
  - 默认管理员 By default the admin account is `admin@apitable.com` and `Apitable2022`.
  - 主要功能模块
    - 基于canvas渲染的表格ui
    - 实时协作
    - 数据库本地架构：变更集/操作/动作/快照等
    - 跨表关联
    - 自动生成api，一键式API面板
    - 表单
    - 强大的行/列权限
    - Shareable and embeddable page
  - APITable 将提供一个数据表查询语言(DQL)来查询您的数据库电子表格内容。
  - Realtime collaboration allows multiple users to edit together in real time, or simultaneously with the Operational Transformation (OT) Algorithm.
  - 7 View Types: Grid View (Datasheet) / Gallery View / Mindmap View / Kanban View / Full-Feature Gantt View / Calendar View
  - [APITable: open-source Airtable alternative | Hacker News_202212](https://news.ycombinator.com/item?id=34127804&ref=upstract.com)
  - super-fast database-spreadsheet interface in `<canvas>` Rendering Engine.
  - Database native architecture: Changeset / Operation / Action / Snapshot and so on.
  - Full-stack API access, from Data to Metadata.
  - One-direction / Bi-direction Table Link and Infinite Cross Links
  - Embed-friendly: Share your datasheet table or folder. Embed them by copying and pasting HTML scripts.
  - Community-friendly programming languages and framework, TypeScript (NextJS + NestJS) and Java (Spring Boot)
  - APITable will provides a Datasheet Query Language (DQL) to query your database-spreadsheet contents.
  - 落地页glassmorphism风格
  - [apitable 和 vika.cn 是有啥关系吗？怎么两个产品看起来一模一样？](https://discord.com/channels/1016320471010115666/1062551587718959224/1062555700246618193)
    - APITable is the open-source and community version of Vika.
    - Vika is a SaaS distribution for China mainland built on APITable open-source core
  - [chore: update BSL license by mr-kelly](https://github.com/apitable/apitable/pull/1428)

- S2 /1.1kStar/MIT/202302/ts/纯前端
  - https://github.com/antvis/S2
  - https://s2.antv.antgroup.com/examples
  - S2是多维交叉分析领域的表格解决方案，数据驱动视图，提供底层核心库、基础组件库、业务场景库
  - 依赖 @antv/g-canvas、g-gesture、d3-interpolate

- baserow /1.3kStar/MIT/202212/python/django/js/vue/多视图
  - https://github.com/bram2w/baserow
  - https://baserow.io/
  - Baserow is an open source no-code database tool and Airtable alternative. 
  - Open-core with all non-premium features under the MIT License allowing commercial and private use.
  - 前端依赖nuxt2、chartjs2、markdown-it、moment、antlr4
  - 后端依赖django3
  - 免费版支持视图grid、form、gallery
    - kanban view is restricted to the premium version only
    - 但企业版源码也是公开的
  - Headless and API first.
  - Uses popular frameworks and tools like Django, Vue.js and PostgreSQL.
  - Baserow is not completely open source, there are features they reserve for premium users (like kanban view).

- mathesar /2kStar/GPLv3/202312/python/django/svelte
  - https://github.com/mathesar-foundation/mathesar
  - https://mathesar.org/
  - open source tool that provides a spreadsheet-like interface to a PostgreSQL database.
  - You can use Mathesar to build data models, enter data, and even build reports. 

- quadratic /1.5kStar/MIT > Custom/202402/rust/ts
  - https://github.com/quadratichq/quadratic
  - https://www.quadratichq.com/
  - Quadratic is a Web-based spreadsheet application that runs in the browser and as a native app (via Electron).
  - Our goal is to build a spreadsheet that enables you to pull your data from its source (SaaS, Database, CSV, API, etc) and then work with that data using the most popular data science tools today (Python, Pandas, SQL, JS, Excel Formulas, etc).
  - WebGL Grid (pinch and zoom grid)
  - Python, Pandas Support (WASM)
  - [Update LICENSE _20230826](https://github.com/quadratichq/quadratic/pull/661)
  - [Is this open source? _202311](https://github.com/quadratichq/quadratic/issues/824)
    - Quadratic's source code is available publicly in this repo. However, we do not provide any license to use, modify, or distribute our code.
  - [Show HN: Quadratic – Open-Source Spreadsheet with Python, AI (WASM and WebGL) | Hacker News_202304](https://news.ycombinator.com/item?id=35456509)

- refine /6.5kStar/MIT/202212/ts
  - https://github.com/refinedev/refine
  - https://refine.dev/
  - headless web application framework developed with flexibility in mind.
  - 非典型cms
  - It eliminates repetitive tasks demanded by CRUD operations and provides industry standard solutions for critical parts like authentication, access control, routing, networking, state management, and i18n.
  - Connectors for 15+ backend services including REST API

- https://github.com/baastronaut/baastronaut /202304/ts/inactive
  - open-source Airtable alternative built on PostgREST
  - 依赖nestjs、typeorm、mantine.v6、mobx、nextjs
  - [Show HN: Baastronaut – open-source Airtable alternative built on PostgREST | Hacker News_202303](https://news.ycombinator.com/item?id=35356736)
    - the most essential features of Airtable are: filtering, grouping, and views. Without that it's a nonstarter. I don't see that here.

- https://github.com/coderinblack08/graspable /202207/ts/inactive
  - A realtime, powerful, lightweight alternative to Airtable/Excel
  - 依赖firebase-admin、supabase、trpc、prisma、tiptap、next-auth、zustand
# notion-database-like
- https://github.com/mukulchugh/kanboard-notion-kanban-react /js
  - https://notion-kanboard-mukul.netlify.app/
  - 暂不支持表格视图

- https://github.com/qwtel/sqlite-viewer-vscode /202304/ts/vscode
  - A quick and easy SQLite viewer for VSCode, inspired by DBBrowser for SQLite and Airtable.
  - [SQLite Viewer Web App](https://sqliteviewer.app/) /未开源

- https://github.com/NotionX/react-notion-x
  - https://react-notion-x-demo.transitivebullsh.it/
  - Fast and accurate React renderer for Notion. TS batteries included.
  - Notion seems to publicly refers to collections as Notion databases, whereas their API and implementation consistently refers to them as collections and collection views.
  - 提供了Notion中各种blocks的渲染器，但不是可切换视图的database，组件有一定的参考价值

- trilium /17.1kStar/AGPLv3/202208/js
  - https://github.com/zadam/trilium
  - https://github.com/zadam/trilium/wiki/
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - 依赖electron、express、jsdom、turndown、ckeditor.v5、codemirror5、jsplumb、fancytree、bootstrap
  - [Notion like database request](https://github.com/zadam/trilium/issues/822)
    - https://github.com/mabeyj/trilium-collection-views
    - An extension for Trilium Notes that implements different ways of viewing collections of notes.
    - 样式过于简单

- AppFlowy /25.8kStar/AGPLv3/202208/rust/dart
  - https://github.com/AppFlowy-IO/AppFlowy
  - https://www.appflowy.io/
  - [[FR] Databases](https://github.com/AppFlowy-IO/AppFlowy/issues/98)
  - AppFlowy is an open-source alternative to Notion. You are in charge of your data and customizations. 
  - Built with Flutter and Rust.

- anytype /需注册登录才能使用
  - https://github.com/anytypeio/badger
  - https://anytype.io/en
  - 暂时未将项目全部开源
  - 已开源的项目大多是go写的玩具

- https://github.com/souvikinator/notion-to-md /MIT/202307/ts
  - Convert notion pages, block and list of blocks to markdown (supports nesting) using notion-sdk-js
# airtable-like
- https://github.com/chanchalguptaa/db-dash /202303/js
  - This is walkover product based on airtable clone
  - 用户数据存放在mongodb/mongoose, 表格数据存放在postgresql/pg
  - https://github.com/tanishjain510/db_dash_frontend /202303/js
    - 依赖firebase、@reduxjs/toolkit、react-table.v7

- https://github.com/ielmar/airtable-clone-typescript-nodejs-jest-tailwind /202211/ts/ejs
  - node后端以纯内存数据作为数据源渲染的简单表格，非常简洁

- https://github.com/medadeshreyas/Airtable.com-Clone /202210/js/仅前端无后端
  - easy-to-use online platform for creating and sharing relational databases
  - allows anyone to spin up a database in minutes
  - built in 6 days by a team of 5 developers
  - https://github.com/manshikumari12/Airtable-Clone /202312/js
  - https://github.com/SunilHooda/Airtable.com-Clone /202302/js
  - https://github.com/misprachi023/Airtable /202311/js
  - https://github.com/ramsarraf11/Airtable-Clone /202212/js
  - https://github.com/Bipin579/Airtable.com-clone-
  - https://github.com/Avneesh002/Airtable
  - https://github.com/Sachintewatia-tech/Airtable_clone

- https://github.com/shreyasmanolkar/notion-browser-client /MIT/202308/ts
  - https://www.notion-s.co/
  - develop a comprehensive clone resembling the popular platform Notion.
  - 依赖tiptap、reduxjs/toolkit、firebase
  - https://github.com/shreyasmanolkar/notion-api /ts
    - Notion Clone API built with TypeScript and MongoDB, using TDD
    - 依赖mongodb、express
  - [Building Notion Clone: Part 1 — Planning the Architecture | by Shreyas manolkar | Medium _202307](https://medium.com/@shreyasmanolkar123/building-notion-clone-part-1-planning-the-architecture-f50342e58019)
  - [Building Notion Clone: Part 2 — Crafting the Front-end Experience | by Shreyas manolkar | Medium _202307](https://medium.com/@shreyasmanolkar123/building-notion-clone-part-2-crafting-the-front-end-experience-cb194c1d132c)

- https://github.com/Mabloq/mabloq-notion /apache2/202304/ts
  - An implementation of the popular Workspace App: Notion.
  - 依赖 nestjs、mongoose、passport、rxjs
  - [Minimalist Notion Implementation: Part 1-Everything Is a Block_202203](https://medium.com/@arcilamatt/minimalist-notion-implementation-part-1-everything-is-a-block-debda338b61a)

- https://github.com/linyows/notionate
  - https://notionate.linyo.ws/
  - React components that uses the Notion API to display the Notion's database and page.

- https://github.com/Arro/airtable-json /202202/js
  - A clean way to get Airtable data into JavaScript.
  - If your records have references to other tables in the same base, you can get a nice clean json blob with that data included.

- https://github.com/Arro/mongo-airtable /MIT/202008/js
  - Keep Airtable tables synced with local MongoDB collections
  - This tool allows you to get and set your data to a MongoDB database, whether or not you have internet access, and then sync whenever is convenient. That way, Airtable is still your ultimate source of truth, but your app's proxy source of truth is MongoDB.

- https://github.com/ThinkAM/typeairtable /MIT/202310/ts
  - an ORM that can run in NodeJS, Browser, Cordova, PhoneGap, Ionic, React Native, NativeScript, Expo, and Electron platforms and can be used with TypeScript
  - TypeAirtable is highly influenced by other ORMs, such as TypeORM and Entity Framework.
  - Using multiple database instances.
  - Supports Airtable.

- https://github.com/markusand/painless-airtable /MIT/202401/ts
  - Easily interact with the Airtable API
- https://github.com/simonw/airtable-export /apache2/202309/python
  - Export Airtable data to YAML, JSON or SQLite files on disk
  - If you run this command against an existing SQLite database records with matching primary keys will be over-written by new records from the export.
# table-solutions
- https://github.com/vikadata/vika.js
  - Vika JavaScript SDK 是对维格表 Fusion API 的官方封装，可以很方便的对你的维格表中的数据进行增删改查操作。
  - 你可以轻松的将维格表中的数据集成到你自己的应用中

- https://github.com/teableio/airtable2teable /MIT/202311/ts
  - https://teable.io/
  - The data pipeline from airtable to teable.

- https://github.com/whitebrick/whitebrick /202202/ts/deprecated/未完成
  - Open Source Airtable Alternative (No Code DB)
  - Whitebrick is a lightweight No Code Database with 3 points of difference:
  - The front end uses a Gatsby static Jamstack client for dead easy customization and deployment.
  - The back end is a set of Serverless functions for making DDL calls to PostgreSQL and configuring Hasura GraphQL server.
  - The PostgreSQL database schemas can be accessed directly with psql for data import/export and integrations with other tools.

- https://github.com/seatable/seatable /未开源
  - SeaTable is a spreadsheet/database like Airtable.
  - SeaTable is originally built by the Seafile team (haiwen/seafile). 
  - The source code will be uploaded to GitHub later. 
  - https://github.com/seatable/dtable-ui-component

- https://github.com/yatharth1706/FormVibe /202310/js
  - Create Forms With Ease. Alternative of typeform and airtable
  - 依赖Appwrite、NextJS、React DND、Formik
# examples
- https://github.com/1657744680/obsidian-yaml-database /ts
  - 像notion database一样浏览编辑文档的YAML属性
  - 注意：这个表格编辑YAML它是只能编辑一个文件夹下的”子“文档，意思就是这个文件夹的子文件夹下的文档并不会被索引。

- https://github.com/jdan/notes /js/类似渲染表格数据的其他视图
  - Turn a Notion database into a deck of cards
# more
