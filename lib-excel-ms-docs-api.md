---
title: lib-excel-ms-docs-api
tags: [api, docs, excel, microsoft]
created: 2023-08-17T08:27:02.980Z
modified: 2023-08-17T08:28:11.799Z
---

# lib-excel-ms-docs-api

# guide

- roadmap
  - open-office-ext-store

- ext vs scripts
  - 扩展的设置可保存与恢复，脚本每次重新执行
  - 扩展适合打包较复杂的包含外部依赖的逻辑，脚本的逻辑不适合包含外部依赖，否则难以实现在线打包和执行

- ext的实现
  - 参考编辑器插件扩展
  - 支持本地/私有/中立仓库，如openvsx

- scripts的实现
  - 难点
    - 在线导入并打包依赖如react/xlsx的能力，可通过预构建的扩展变通解决
  - 参考react-live/mdx-live/script-lab，每次将数据对象和解析后的代码传进去
  - 类似vscode像codepen的实时预览扩展
  - [Announcing Python in Excel](https://techcommunity.microsoft.com/t5/excel-blog/announcing-python-in-excel-combining-the-power-of-python-and-the/ba-p/3893439)
# docs

## Excel JavaScript API

- [精读《Excel JS API》 - 知乎](https://zhuanlan.zhihu.com/p/455298252)

- [Excel JavaScript API overview](https://learn.microsoft.com/en-us/office/dev/add-ins/reference/overview/excel-add-ins-reference-overview)
  - These are the application-specific APIs for Excel. 
  - Introduced with Office 2016, the Excel JavaScript API provides strongly-typed objects that you can use to access worksheets, ranges, tables, charts, and more.

- [Explore Office JavaScript API using Script Lab](https://learn.microsoft.com/en-us/office/dev/add-ins/overview/explore-with-script-lab)
  - [Build an Excel task pane add-in](https://learn.microsoft.com/en-us/office/dev/add-ins/quickstarts/excel-quickstart-jquery?tabs=yeomangenerator)

- [Using the application-specific API model](https://learn.microsoft.com/en-us/office/dev/add-ins/develop/application-specific-api-model)
  - [Work with workbooks using the Excel JavaScript API](https://learn.microsoft.com/en-us/office/dev/add-ins/excel/excel-add-ins-workbooks)
  - [Excel. Workbook class](https://learn.microsoft.com/en-us/javascript/api/excel/excel.workbook?view=excel-js-preview)

- https://github.com/OfficeDev/script-lab /MIT/202311/ts
  - https://script-lab.azureedge.net/
  - Create, run and share your code directly from Office
  - Experiment with the Office JavaScript API without ever leaving Excel, Outlook, Word, or PowerPoint

- https://github.com/OfficeDev/office-js-snippets
  - A collection of code snippets built with Script Lab

- [excel package](https://learn.microsoft.com/en-us/javascript/api/excel?view=excel-js-preview)

### examples-excel-js-api

- https://github.com/honey-grapes/excel-link-manager-dashboard /js
  - a tool for financial analysts to navigate the dependencies in complex financial models. 
  - Built with React and Excel Javascript API.

- https://github.com/OfficeDev/Excel-Add-in-WoodGrove-Expense-Trends /js
  - A compelling Excel add-in that demonstrates how you can use the new JavaScript API for Excel 2016. 
  - Comes in two flavors - task pane and add-in commands.

- https://github.com/areed1192/excel-custom-function-add-in
  - A tutorial on how to build an Excel Custom Function Add-In using the new Office JavaScript API.
  - https://github.com/parkers116/excel_add_in_javascrpit_test

- https://github.com/OfficeDev/Excel-Content-Add-in-Humongous-Insurance /js
  - shows how you can use the new JavaScript API for Microsoft Excel 2016 to create a compelling Excel add-in.
  - This add-in shows how you can embed rich, interactive objects into Office documents. 

- https://github.com/odwyersoftware/sheet2api-js /js
  - JavaScript Library for Google Sheets/Microsoft Excel Online through [sheet2api](https://sheet2api.com/).
# office-app-store
- open office extensions store
  - 扩展示例1: chatgpt, drawio, calendar, formula-editor
  - 扩展示例2: wikipedia, stock-connector, jira

- [microsoft appsource](https://appsource.microsoft.com/en-us/marketplace/apps?product=office)
# discuss
- ## 

- ## 

- ## 

- ## 
# more
