---
title: toc-lib-list-grid-airtable-notion-database
tags: [airtable, grid, list, notion-database, table, toc]
created: '2022-01-30T19:35:55.709Z'
modified: '2022-03-14T19:55:47.081Z'
---

# toc-lib-list-grid-airtable-notion-database

# guide

- airtable-like的产品有2种方向
  - strapi 通过拖拽ui字段生成rest crud api
    - no code 平台，但此类产品应该偏向automation
  - airtable 通用的前端表格组件，提供各种后端的集成
# popular
- react-datasheet-grid /71Star/MIT/202202/ts
  - https://github.com/Equify/react-datasheet-grid
  - https://react-datasheet-grid.netlify.app/docs/features
  - 依赖react、react-window、react-resize-detector
  - more like Airtable or Notion and less like Excel in the sense that instead of dealing with individual cells it deals with entire rows, and each column is responsible for a single property of each row
  - features
    - Fast
      - can easily handle hundreds of thousands of rows thanks to its virtualized architecture.
      - Renders have been optimized to the strict minimum, follow the performance guides 
    - Customizable
      - Control every behavior of the spreadsheet, implement you own widgets, and customize the style of DSG to match your app.
    - Feature rich
      - Supports copy/pasting to and from Excel, Google-sheet, Notion
      - Keyboard navigation and shortcuts fully-supported

- https://github.com/rowyio/rowy
  - Manage Firestore data in a spreadsheet-like UI, write Cloud Functions effortlessly in the browser, 
  - https://demo.rowy.io/table/allFieldTypes
    - 给出了常用字段类型的示例
# notion database like
- focalboard
  - https://github.com/mattermost/focalboard
  - https://www.focalboard.com/
  - Focalboard comes in two main editions:
  - Personal Desktop: A stand-alone single-user Mac, Windows, or Linux desktop app for your todos and personal projects.
  - Mattermost Boards: A self-hosted or cloud server for your team to plan and collaborate.

- https://github.com/zadam/trilium
  - a hierarchical note taking application with focus on building large personal knowledge bases. 
  - 依赖 electron、express、jsdom、turndown、ckeditor、codemirror、fancytree、bootstrap
  - [Notion like database](https://github.com/zadam/trilium/issues/822)

- https://github.com/AppFlowy-IO/AppFlowy
  - [[FR] Databases](https://github.com/AppFlowy-IO/AppFlowy/issues/98)

- https://github.com/anytypeio/badger
  - https://anytype.io/en
# examples
- https://github.com/qwtel/sqlite-viewer-vscode
  - A quick and easy SQLite viewer for VSCode, inspired by DBBrowser for SQLite and Airtable.
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
- Note taking/knowledge base

RemNote: knowledge management, note taking, flashcards/spaced repetition; no offline mode

Trillium Notes: knowledge management, note taking; free and open source; fully offline; local storage

OneNote: note taking, checklists, web clipper; offline mode; local and cloud storage (depends on version)

Obsidian: knowledge management, note taking; fully offline; local storage

Joplin: knowledge management, note taking; free and open source; fully offline; local storage

Bear: knowledge management, note taking; offline mode; MacOS/iOS only

- Project management/task lists/kanban boards

ClickUp: goal tracking, tasks, spreadsheets/tables, docs/wikis; offline mode

Nimbus Note: goal tracking, tasks, spreadsheets/tables, docs/wikis; offline mode

Quire: tasks; Android app is only one listing offline mode

Asana: tasks; 100+ integrations; iOS app is only one listing offline mode

Trello: tasks

- Full on Notion replacement

AnyType: appears to be same as Notion, but not available yet; fully offline; local storage

Craft: knowledge management, note taking; offline mode; MacOS/iOS only

- ## Bangle.io - A fully local serverless Notion alternative
- https://www.reddit.com/r/selfhosted/comments/rnnj96/bangleio_a_fully_local_serverless_notion/
- some of the things that differentiate bangle from just a vanilla markdown editor:
  - WYSIWYG editor - countless editors force the user to look at a split view of raw and formatted markdown.
  - It support workspaces, tags, backlinks to name a few.
  - I am working hard to add an open API to make it extensible.
  - Is speedy and fast, not an electron bloatware.
  - No data hostage - allows you to edit your locally saved markdown notes write from the web app.
  - Has powerful vs-code like command palettes and keyboard shortcuts.
