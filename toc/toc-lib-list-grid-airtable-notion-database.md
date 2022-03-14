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
- https://github.com/mattermost/focalboard
  - https://www.focalboard.com/
  - Focalboard comes in two main editions:
  - Personal Desktop: A stand-alone single-user Mac, Windows, or Linux desktop app for your todos and personal projects.
  - Mattermost Boards: A self-hosted or cloud server for your team to plan and collaborate.
# examples
- https://github.com/qwtel/sqlite-viewer-vscode
  - A quick and easy SQLite viewer for VSCode, inspired by DBBrowser for SQLite and Airtable.
