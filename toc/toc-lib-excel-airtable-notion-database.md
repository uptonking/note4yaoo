---
title: toc-lib-excel-airtable-notion-database
tags: [airtable, grid, list, notion-database, table, toc]
created: 2022-01-30T19:35:55.709Z
modified: 2022-08-21T10:02:05.129Z
---

# toc-lib-excel-airtable-notion-database

# guide

- airtable-like的产品有2种方向
  - strapi 通过拖拽ui字段生成rest crud api
    - no code 平台，但此类产品应该偏向automation
  - airtable 通用的前端表格组件，提供各种后端的集成

- [A More Human Approach To Databases](https://ccorcos.github.io/filing-cabinets/)
  - Notion 工程师 Chet 以警察信息管理系统为例，用普通人能理解的大白话，从文件、文件夹、文件柜逐步介绍关系型数据库的构成和实现原理
  - [Maybe some misunderstanding of how SQL DB indexes work?](https://github.com/ccorcos/tuple-database/issues/11)
# popular
- react-datasheet-grid /133Star/MIT/202205/ts
  - https://github.com/nick-keller/react-datasheet-grid
  - https://github.com/Equify/react-datasheet-grid
  - https://github.com/nick-keller/react-datasheet-grid
  - https://react-datasheet-grid.netlify.app/docs/features
  - 依赖react、react-window、react-resize-detector
  - more like Airtable or Notion and less like Excel in the sense that instead of dealing with individual cells it deals with entire rows, and each column is responsible for a single property of each row
  - [V2 status update_202106](https://github.com/Equify/react-datasheet-grid/issues/37)
  - [Feature Roadmap_202106](https://github.com/Equify/react-datasheet-grid/issues/38)
  - features
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
  - 未完成
  - https://github.com/RafaelGB/obsidian-db-folder
    - Obsidian Plugin to Allow Notion like database based on folders

- https://github.com/linyows/notionate
  - React components that uses the Notion API to display the Notion's database and page.

- rowy /4kStar/apache2/202212/ts
  - https://github.com/rowyio/rowy
  - http://rowy.io/
  - https://demo.rowy.io/
  - Rowy is an open-source low-code platform for Firebase and Firestore.
  - 依赖firebase、mui5、tanstack-table、tinymce5、monaco-editor、jotai、swr、react-dnd
  - Airtable-like UI with cloud functions workflows in JS/TS, all in your browser.
  - Manage Firestore data in a spreadsheet-like UI, write Cloud Functions effortlessly in the browser
  - Powerful spreadsheet interface for Firestore
  - 30+ fields supported
  - [Firetable is now Rowy_202110](https://news.ycombinator.com/item?id=28768261)
  - [Abstracting the UI to be compatible with any database](https://github.com/rowyio/rowy/issues/228)
    - long term
  - https://demo.rowy.io/table/allFieldTypes
    - 给出了常用字段类型的示例
- firetable /36Star/apache2/202108/ts
  - https://github.com/Antler-VC/firetable
  - Excel/Google Sheets like UI for Firebase/Firestore. No more admin portals!
  - https://github.com/FiretableProject/firetable

- nocodb /33kStar/AGPLv3/202212/ts/vue
  - https://github.com/nocodb/nocodb
  - https://nocodb.com/
  - The Open Source Airtable Alternative
  - Turns any MySQL, PostgreSQL, SQL Server, SQLite & MariaDB into a smart-spreadsheet
  - 依赖monaco-editor、vueuse、antd-vue、monaco-editor、sortablejs、vuedraggable
  - Search, sort, filter, hide columns with uber ease
  - Create Views : Grid, Gallery, Kanban, Form
  - Frontend: Vue.js
  - Backend: express.js, knex, 
  - Database: Any SQL (postgres, mysql, sqlite, maria DB, SQL server)
  - API: REST and graphql

- grist-core /3.4kStar/apache2/202211/ts/python
  - https://github.com/gristlabs/grist-core
  - https://support.getgrist.com/
  - 不直接支持视图切换，但支持各种widgets
  - 前端基于backbone、jquery
  - Grist is a modern relational spreadsheet. It combines the flexibility of a spreadsheet with the robustness of a database to organize your data and make you more productive.
  - Columns work like they do in databases.
  - Columns can be filled by formula
  - A portable, self-contained format. Based on SQLite
  - Full Python syntax is supported, and the standard library.

- refine /6.5kStar/MIT/202212/ts
  - https://github.com/refinedev/refine
  - https://refine.dev/
  - headless web application framework developed with flexibility in mind.
  - It eliminates repetitive tasks demanded by CRUD operations and provides industry standard solutions for critical parts like authentication, access control, routing, networking, state management, and i18n.
  - Connectors for 15+ backend services including REST API

- https://github.com/mukulchugh/kanboard-notion-kanban-react
  - https://notion-kanboard-mukul.netlify.app/
  - 暂不支持视图切换
# notion database like
- focalboard /10.3kStar/MIT-like/202203/ts+go
  - https://github.com/mattermost/focalboard
  - https://www.focalboard.com/
  - 前端webapp依赖 @reduxjs/toolkit、react-redux.v7、@tippyjs/react、draft-js、@fullcalendar/react、imagemin-svgo、marked、moment、nanoevents、react-dnd.v14、react-hot-keys、react-intl、react-router-dom.v5
  - an open source, multilingual, self-hosted project management tool that's an alternative to Trello, Notion, and Asana.
  - Focalboard comes in two main editions:
    - Personal Desktop: A stand-alone single-user Mac, Windows, or Linux desktop app for your todos and personal projects.
    - Mattermost Boards: A self-hosted or cloud server for your team to plan and collaborate.

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

- trilium /17.1kStar/AGPL.v3/202208/js
  - https://github.com/zadam/trilium
  - https://github.com/zadam/trilium/wiki/
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - 依赖 electron、express、jsdom、turndown、ckeditor、codemirror、fancytree、bootstrap
  - [Notion like database request](https://github.com/zadam/trilium/issues/822)
    - https://github.com/mabeyj/trilium-collection-views
      - An extension for Trilium Notes that implements different ways of viewing collections of notes.
      - 样式过于简单

- AppFlowy /25.8kStar/AGPL.v3/202208/rust/dart
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
# airtable-like
- baserow /1.3kStar/MIT/202212/python/js/vue
  - https://github.com/bram2w/baserow
  - https://baserow.io/
  - Baserow is an open source no-code database tool and Airtable alternative. 
  - Open-core with all non-premium features under the MIT License allowing commercial and private use.
  - Headless and API first.
  - Uses popular frameworks and tools like Django, Vue.js and PostgreSQL.

- nocobase /3.7kStar/apache2/202212/ts/国内
  - https://github.com/nocobase/nocobase
  - https://www.nocobase.com/
  - NocoBase is a scalability-first, open-source no-code/low-code development platform. 开源无代码开发平台
  - server依赖koa
  - client依赖antd、g2plot、ahooks、dnd-kit、formily、marked、react-iframe、react-quill、react-router5
  - 采用数据结构与使用界面分离的设计思路，可以为数据表创建任意数量、任意形态的区块（数据视图），每个区块里可以定义不同的样式、文案、操作
  - you can configure the user interface directly with WYSIWYG operations.
  - Everything is a plugin, all new features can be implemented by developing and installing plugins

- https://github.com/seatable/seatable
  - SeaTable is a spreadsheet/database like Airtable.
  - SeaTable is originally built by the Seafile team (haiwen/seafile). 
  - The source code will be uploaded to GitHub later. 
  - https://github.com/seatable/dtable-ui-component
# examples
- https://github.com/qwtel/sqlite-viewer-vscode
  - A quick and easy SQLite viewer for VSCode, inspired by DBBrowser for SQLite and Airtable.

- https://github.com/vikadata/vika.js
  - Vika JavaScript SDK 是对维格表 Fusion API 的官方封装，可以很方便的对你的维格表中的数据进行增删改查操作。
  - 你可以轻松的将维格表中的数据集成到你自己的应用中
# discuss
- ## Alternative for Notion
- https://www.reddit.com/r/selfhosted/comments/qhm1v2/alternative_for_notion/
- The best alternative to notion is actually trilium. 
  - Gallery view like notion via book note
  - tables nt databases, but over notion, tables in trilium support embedding of images directly
  - What it does not have
    - notion like database sorting of tables
    - notion like filters for tables
    - notion like backlinks again not sure about this
    - notion like kanban

- ## Privacy-forward notion alternative with databases?
- https://www.reddit.com/r/Notion/comments/sl5kiu/privacyforward_notion_alternative_with_databases/
- There are two pieces of software I'm eagerly waiting for. 
  - Anytype who someone already mentioned, and Appflowy.

- ## List of Notion alternatives
- https://www.reddit.com/r/Notion/comments/lijien/list_of_notion_alternatives/

### Note taking/knowledge base

- RemNote: knowledge management, note taking, flashcards/spaced repetition; no offline mode
- Trillium Notes: knowledge management, note taking; free and open source; fully offline; local storage
- OneNote: note taking, checklists, web clipper; offline mode; local and cloud storage (depends on version)
- Obsidian: knowledge management, note taking; fully offline; local storage
- Joplin: knowledge management, note taking; free and open source; fully offline; local storage
- Bear: knowledge management, note taking; offline mode; MacOS/iOS only

### Project management/task lists/kanban boards

- ClickUp: goal tracking, tasks, spreadsheets/tables, docs/wikis; offline mode
- Nimbus Note: goal tracking, tasks, spreadsheets/tables, docs/wikis; offline mode
- Quire: tasks; Android app is only one listing offline mode
- Asana: tasks; 100+ integrations; iOS app is only one listing offline mode
- Trello: tasks

### Full on Notion replacement

- AnyType
  - appears to be same as Notion, but not available yet; fully offline; local storage
- Craft
  - knowledge management, note taking; offline mode; MacOS/iOS only

- ## Notion alternatives? And why I want to switch.
- https://www.reddit.com/r/Notion/comments/ser139/notion_alternatives_and_why_i_want_to_switch/
- Specific grievances that influence my opinion are:
  - No offline support: flaky UX anywhere there is a flaky connection, including at my home
  - Second class mobile experience: no multitasking on iOS / Android, no zoom, and if you use mobile, the website has a banner you can’t X out of
  - No on-premises data support: I can’t have custody of my data in case I want to, say, store sensitive data in Notion. I must trust the probably great but possibly flawed Notion team I’ve never met.
  - Search is buggy: sometimes pages don’t show up, and I have no idea why. Search is slow. I generally don’t trust it.
  - Flaky handling of uploads: I can’t tell you how often I’ve thought I stored an important image, only to find out the upload silently failed.

- The only thing I wasn't able to replace was Notion's highly featured database system, but I found a better workaround.
- Notes
  - I used Obsidian and then switched to Craft. 
  - Obsidian was nice because it was free and all your data was yours. Uses markdown formatting, supports backlinks, and a whole slew of potential with third party extensions. 
  - I eventually switched to Craft because it did what I needed to do in a more fluent manner. 
  - Craft required less adjustments and was a much more opinionated software.

- Task/Project Management
  - I use Asana for my big project management now. It's a premium/subscription service for some of the better features, but it gets the job done and has offline support.

- Basic todo list
  - I use Things 3 for my basic every day tasks. Sure it's pricey but the app does not disappoint.

- Calendar: I use Fantastical. 
  - People hate on it ever since it switched to a subscription model but it is undeniably the best calendar app out there, especially if you manage multiple calendars across different services (Google Calendar + Outlook Calendar). And it has this magical feature where if I drag a task from Things 3 over to Fantastical, it makes a calendar event!

- Task Management + to do + calendar
  - For a while I used Ticktick and realized it was the closest I ever got to an all-in-one workspace that had offline support
  - Filters, tags, kanban view, calendar view, Eisenhower view, etc. Ticktick had it all! And when life slowed down and I only needed simple to-do lists, Ticktick did that too. 
  - The only issue I had when I used Ticktick two years ago was that the iOS/iPadOS app received updates much sooner than macOS app, which made using it on both platforms very difficult as I could see everything on my phone, but not on my laptop. 
  - Hopefully this has been fixed, but I just don't need an all-in-one workspace anymore.

- Breaking everything down into their separate apps has made the experience doing each thing much better. 
  - Notion was nice to use because everything was in one place. It was the jack of all trades, master of none, but it was never better than any master of one. 

- I’ve tried out a lot of recommended Notion alternatives, and no apps really come close to touching the full-fat feature set, aesthetics, functionality and community of Notion. 
  - As others have mentioned, apps such as Obsidian, Logseq and Roam and are great at what they do, which is essentially pure notetaking, but they do not contain database features 
  - (although it is worth mentioning that Obsidian with its DataView plugin can replicate most functions of a Notion database, albeit in a manner that’s very user unfriendly. Still, it’s amazing what can be achieved with Obsidian, a few plugins, and plain markdown files).
- Some other alternatives that do **include database features** include Coda, Airtable, MS Excel, ClickUp and a few new upstarts like Appflowy, which looks promising but is in a very early stage of development. 
  - Focalboard also looks decent, and so does Microsoft Loop, which while probably not be self-hosted or open source, will likely be widely adopted across Microsoft 365 companies.

- I tried switching to Obsidian initially - and I was able to recreate my Notion database heavy workflow within the Dataview plugin. 
  - However, sync just got too tedious to manage, and using YAML frontmatter was not a great experience for managing Notion-like “databases”. 
  - The lack of block-based editing was also a significant con

- ## Anyone has an *offline* alternative for Notion in terms of database?
- https://www.reddit.com/r/Notion/comments/jzgrk2/anyone_has_an_offline_alternative_for_notion_in/
- Try Trilium. It's open source, self hosted, free, and pretty damn good.
- The ease of putting pages in database rows still makes Notion a better option, but clicking through data surely isn't as fast as my old spreadsheet.

- ## How to share a filtered view of a table to a guest user, and prevent them to check the full table by changing views / accesing the source database?
- https://www.reddit.com/r/Notion/comments/dk1vys/how_to_share_a_filtered_view_of_a_table_to_a/
- 2 years later I am having the same issue. 
- I found a solution to show an empty database if the recipient would click on the title of a database I had specifically filtered for them.
  - I made my original mother-database completely empty by putting a condition that is always false. In my case I chose to put a delivery date to a date where nothing happened (before I used Notion).

- ## Bangle.io - A fully local serverless Notion alternative
- https://www.reddit.com/r/selfhosted/comments/rnnj96/bangleio_a_fully_local_serverless_notion/
- some of the things that differentiate bangle from just a vanilla markdown editor:
  - WYSIWYG editor - countless editors force the user to look at a split view of raw and formatted markdown.
  - It support workspaces, tags, backlinks to name a few.
  - I am working hard to add an open API to make it extensible.
  - Is speedy and fast, not an electron bloatware.
  - No data hostage - allows you to edit your locally saved markdown notes write from the web app.
  - Has powerful vs-code like command palettes and keyboard shortcuts.
# ref
- [How to Connect a React App to a Notion Database](https://dev.to/alexeagleson/how-to-connect-a-react-app-to-a-notion-database-51mc)
