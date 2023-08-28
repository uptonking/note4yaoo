---
title: toc-lib-excel-airtable-notion-database
tags: [airtable, grid, list, notion-database, table, toc]
created: 2022-01-30T19:35:55.709Z
modified: 2022-08-21T10:02:05.129Z
---

# toc-lib-excel-airtable-notion-database

# guide

- ali-LowCodeEngine目前仅支持生成React的前端代码
  - 制作成本固然低了，造出来的代码维护成本太高了
  - 这种东西，不会编程的人对他来说太复杂了，会编程的人来说太繁琐了。

- airtable-like的产品的方向
  - 偏后端，偏api，类似strapi通过拖拽ui字段生成rest crud api，即headless cms
  - 偏前端，类似airtable的通用表格组件，提供各种数据源的集成
  - 偏向automation

- [什么是比较好的低代码产品_Tw93](https://zhuanlan.zhihu.com/p/596474809)
  - platform, baas, cms, workflow, airtable-like
  - 流程自动化

- [A More Human Approach To Databases](https://ccorcos.github.io/filing-cabinets/)
  - Notion 工程师 Chet 以警察信息管理系统为例，用普通人能理解的大白话，从文件、文件夹、文件柜逐步介绍关系型数据库的构成和实现原理
  - [Maybe some misunderstanding of how SQL DB indexes work?](https://github.com/ccorcos/tuple-database/issues/11)
# popular
- react-datasheet-grid /259Star/MIT/202305/ts
  - https://github.com/nick-keller/react-datasheet-grid
  - https://github.com/Equify/react-datasheet-grid
  - https://react-datasheet-grid.netlify.app/docs/features
  - 依赖react、tanstack-virtual、react-resize-detector
  - more like Airtable or Notion and less like Excel in the sense that instead of dealing with individual cells it deals with entire rows, and each column is responsible for a single property of each row
  - 默认可编辑单元格
  - 操作支持获取operation对象
  - Supports copy / pasting to and from Excel, Google-sheet...
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
- https://github.com/RafaelGB/obsidian-db-folder
  - Obsidian Plugin to Allow Notion like database based on folders
  - https://github.com/blacksmithgu/datacore
    - Datacore is a work-in-progress re-imagining of Dataview with a focus on 2-10x better query and rendering performance, as well as fully interactible views.

- https://github.com/linyows/notionate
  - https://notionate.linyo.ws/
  - React components that uses the Notion API to display the Notion's database and page.

- undb /20Star/AGPLv3/202304/ts
  - https://github.com/undb-xyz/undb
  - https://www.undb.xyz/
  - https://docs.undb.xyz/
  - Private first, unified, self-hosted no code database.
  - 前端依赖 undb, dnd-kit、tanstack-table, redux-toolkit, emotion, @loadable/component, jotai, react-hook-form, trpc
    - 可在redux-devtools中查看数据结构
  - 后端依赖 nestjs、mikro-orm、trpc、undb
  - [feature/frontend next_20230503(v0.3), 前端迁移到svelte](https://github.com/undb-xyz/undb/pull/908)
    - 41fa03d9bfbc9b5072266ad94c9532ccdcf25a68
- https://github.com/baastronaut/baastronaut /ts
  - Open-source Airtable alternative
  - 依赖 nestjs、reactgrid、@mui/x-data-grid、mantine.v6、next

- nocodb /33kStar/AGPLv3/202212/ts/vue/重后端/多视图
  - https://github.com/nocodb/nocodb
  - https://nocodb.com/
  - [Development Setup](https://docs.nocodb.com/engineering/development-setup/)
  - The Open Source Airtable Alternative
  - Turns any MySQL, PostgreSQL, SQL Server, SQLite & MariaDB into a smart-spreadsheet
  - 后端依赖 express、knex、ioredis、passport、request
  - 前端依赖 nuxt3、ant-design-vue.v3、vueuse、vue-flow(chart)、monaco-editor、d3-scale、dayjs、vuedraggable、xlsx
  - 支持提供返回表中数据的api
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

- locokit /47Star/MIT/202301/ts
  - https://github.com/locokit/locokit
  - https://locokit.io/
  - LocoKit is an AirTable alternative, providing database management as a spreadsheet and an app builder.
  - 后端依赖feathers4、knex.v旧版
  - 前端依赖vue2、turf、mapbox-gl.v1、monaco-editor、xlsx、marked
  - 不支持除表格外的其他视图
  - 主要功能模块
    - 数据库设计与数据录入
    - 前端视图
    - workspace管理
    - 成员与权限
    - Processes/Workflows with a webhook mechanism
  - [[roadmap] API over SQL / Nuxt 3 / Feathers 5 / Pinia](https://github.com/locokit/locokit/issues/151)
    - 正在迁移到nuxt3+pinia(vue store)+feathers5

- apitable /2.3kStar/AGPLv3/202301/ts/java/维格表团队
  - https://github.com/apitable/apitable
  - https://apitable.com/
  - [开发者指南](https://github.com/apitable/apitable/blob/develop/docs/readme/zh-CN/docs/contribute/developer-guide.md)
  - API-oriented low-code platform for building collaborative apps and better than all other Airtable open-source alternatives
  - 后端依赖 spring-boot、mybatis、easyexcel、grpc、protobuf、nestjs
  - 前端依赖 antd、ahooks、redux、exceljs、konva、markdown-it、react-quill、react-dnd、slate
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

- nocobase /3.7kStar/apache2/202212/ts/国内
  - https://github.com/nocobase/nocobase
  - https://www.nocobase.com/
  - [源码安装](https://docs-cn.nocobase.com/welcome/getting-started/installation/git-clone)
  - 易扩展的开源无代码开发平台。
  - NocoBase is a scalability-first, open-source no-code/low-code development platform.
  - 后端依赖 koa、sequelize.v6
  - 前端依赖 umi、antd、g2plot、ahooks、dnd-kit、formily、marked、react-iframe、react-quill、react-router5
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

- focalboard /10.3kStar/src-AGPL & bin-MIT/202203/ts/go
  - https://github.com/mattermost/focalboard
  - https://www.focalboard.com/
  - 前端webapp依赖 @reduxjs/toolkit、@tippyjs/react、draft-js、@fullcalendar/react、imagemin-svgo、marked、moment、nanoevents、react-dnd.v14、react-hot-keys、react-intl、react-router-dom.v5
  - an open source, multilingual, self-hosted project management tool that's an alternative to Trello, Notion, and Asana.
  - Focalboard comes in two main editions:
    - Personal Desktop: A stand-alone single-user Mac, Windows, or Linux desktop app for your todos and personal projects.
    - Mattermost Boards: A self-hosted or cloud server for your team to plan and collaborate.
  - [Focalboard Personal and Plugin Editions Announcement_20230430](https://github.com/mattermost/focalboard/discussions/4645)
    - we won’t be adding any new enhancements

- rowy /4kStar/apache2/202212/ts/firebase/示例丰富
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

- S2 /1.1kStar/MIT/202302/ts
  - https://github.com/antvis/S2
  - https://s2.antv.antgroup.com/examples
  - S2是多维交叉分析领域的表格解决方案，数据驱动视图，提供底层核心库、基础组件库、业务场景库
  - 依赖 @antv/g-canvas、g-gesture、d3-interpolate

- baserow /1.3kStar/MIT/202212/python/js/vue/多视图
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

- grist-core /3.4kStar/apache2/202211/ts/python
  - https://github.com/gristlabs/grist-core
  - https://support.getgrist.com/
  - 表格不支持视图切换，支持各种widgets，类似dashboard
  - 前端基于backbone、jquery
  - Grist is a modern relational spreadsheet. 
  - It combines the flexibility of a spreadsheet with the robustness of a database to organize your data and make you more productive.
  - Columns work like they do in databases.
  - Columns can be filled by formula
  - A portable, self-contained format. Based on SQLite
  - Full Python syntax is supported, and the standard library.
- irelia /18Star/apache2/202211/ts/python
  - https://github.com/IreliaTable/irelia
  - https://ireliatable.github.io/irelia-web/
  - 依赖 gristlabs/grist-core、backbone、knockout、jquery
  - Irelia is a modern relational spreadsheet. 
  - Python formulas. Full Python syntax is supported, and the standard library.
  - A portable, self-contained format based on SQLite

- quadratic /1.5kStar/MIT/202304/python
  - https://github.com/quadratichq/quadratic
  - https://quadratichq.com/
  - Quadratic is a Web-based spreadsheet application that runs in the browser and as a native app (via Electron).
  - Our goal is to build a spreadsheet that enables you to pull your data from its source (SaaS, Database, CSV, API, etc) and then work with that data using the most popular data science tools today (Python, Pandas, SQL, JS, Excel Formulas, etc).

- refine /6.5kStar/MIT/202212/ts
  - https://github.com/refinedev/refine
  - https://refine.dev/
  - headless web application framework developed with flexibility in mind.
  - 非典型cms
  - It eliminates repetitive tasks demanded by CRUD operations and provides industry standard solutions for critical parts like authentication, access control, routing, networking, state management, and i18n.
  - Connectors for 15+ backend services including REST API

- https://github.com/mukulchugh/kanboard-notion-kanban-react /js
  - https://notion-kanboard-mukul.netlify.app/
  - 暂不支持表格视图
# notion-database-like
- https://github.com/NotionX/react-notion-x
  - https://react-notion-x-demo.transitivebullsh.it/
  - Fast and accurate React renderer for Notion. TS batteries included.
  - Notion seems to publicly refers to collections as Notion databases, whereas their API and implementation consistently refers to them as collections and collection views.
  - 提供了Notion中各种blocks的渲染器，但不是可切换视图的database，组件有一定的参考价值

- obsidian dataview
  - https://github.com/blacksmithgu/obsidian-dataview
  - Treat your Obsidian Vault as a database which you can query from. 
    - Provides a JavaScript API and pipeline-based query language for filtering, sorting, and extracting data from Markdown pages.
    - Dataview generates data from your vault by pulling information from Markdown frontmatter and Inline fields.
    - Markdown frontmatter is arbitrary YAML enclosed by --- at the top of a markdown document which can store metadata about that document.
    - Inline fields are a Dataview feature which allow you to write metadata directly inline in your markdown document via Key:: Value syntax.
  - https://github.com/obsidianmd/obsidian-releases
    - Obsidian is not open source software and this repo DOES NOT contain the source code of Obsidian. 
    - However, if you wish to contribute to Obsidian, you can easily do so with our extensive plugin system.

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

- anytype
  - https://github.com/anytypeio/badger
  - https://anytype.io/en
  - 暂时未将项目全部开源
  - 已开源的项目大多是go写的玩具

- https://github.com/souvikinator/notion-to-md
  - Convert notion pages, block and list of blocks to markdown (supports nesting) using notion-sdk-js
# table-like
- https://github.com/vikadata/vika.js
  - Vika JavaScript SDK 是对维格表 Fusion API 的官方封装，可以很方便的对你的维格表中的数据进行增删改查操作。
  - 你可以轻松的将维格表中的数据集成到你自己的应用中

- https://github.com/coderinblack08/graspable
  - A realtime, powerful, lightweight alternative to Airtable/Excel
  - 依赖firebase/supabase

- https://github.com/whitebrick/whitebrick /202202/ts/deprecated/未完成
  - Open Source Airtable Alternative (No Code DB)
  - Whitebrick is a lightweight No Code Database with 3 points of difference:
  - The front end uses a Gatsby static Jamstack client for dead easy customization and deployment.
  - The back end is a set of Serverless functions for making DDL calls to PostgreSQL and configuring Hasura GraphQL server.
  - The PostgreSQL database schemas can be accessed directly with psql for data import/export and integrations with other tools.

- https://github.com/qwtel/sqlite-viewer-vscode
  - A quick and easy SQLite viewer for VSCode, inspired by DBBrowser for SQLite and Airtable.

- https://github.com/seatable/seatable /未开源
  - SeaTable is a spreadsheet/database like Airtable.
  - SeaTable is originally built by the Seafile team (haiwen/seafile). 
  - The source code will be uploaded to GitHub later. 
  - https://github.com/seatable/dtable-ui-component
# more
