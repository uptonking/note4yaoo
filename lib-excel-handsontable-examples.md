---
title: lib-excel-handsontable-examples
tags: [data-grid, examples, handsontable]
created: 2023-12-21T20:05:53.059Z
modified: 2023-12-21T20:06:13.700Z
---

# lib-excel-handsontable-examples

# guide

# popular
- handsontable v6.2.2 /13.8kStar/MIT > Free4NonCommercial/201903/js
  - https://github.com/handsontable/handsontable
  - https://handsontable.com/
  - 基于table标签实现
  - 依赖numbro、moment、pikaday
  - a JS HTML5 data grid with spreadsheet look & feel.
  - free for all non-commercial purposes since 7.0
  - 不支持协作
  - 支持undo，[Q: Possible to combine multiple actions into single undo/redo step? _202010](https://github.com/handsontable/handsontable/issues/7324)
  - [Handsontable drops open source for a non-commercial license_201903](https://github.com/handsontable/handsontable/issues/5831)
    - https://github.com/handsontable/handsontable/releases/tag/7.0.0
    - [Handsontable v7 and later versions are fully commercial so it really depends on your case](https://twitter.com/handsontable/status/1164198101726433282). 
    - If you want to fully integrate it with your software while maintaining the OSS license, then your only option is to use v6.2.2 - the last one released under the MIT license.
  - https://github.com/handsontable/react-handsontable/tree/2.1.0 /MIT/201812/ts
    - the official wrapper 
  - 🍴 forks
    - https://github.com/firm-app/opentable /202201/js/from-jacksontable/move walkontable back
      - https://github.com/swsvindland/opentable-react
    - https://github.com/rathbone-labs/jacksontable /201907/js/inactive
    - https://github.com/lbobylev/jacksontable
    - https://github.com/dreamsavior/mitontable /2commits
    - https://github.com/janisdd/handsontable /202304/v6/ts-d/fork for https://github.com/janisdd/vscode-edit-csv
      - https://edit-csv.net/
      - vs code extension to edit csv files with an excel like table ui
    - https://github.com/nzzdev/handsontable /v6/fix-excel-copy-paste
      - used by Q-editor
    - https://github.com/KonstantinMilovanovDSR/handsontable /202210/v6/fix
    - https://github.com/rayzeller/handsontable /202209/v6/Auto row size
    - https://github.com/sylcdev/handsontable /202207/v6/3fix
    - https://github.com/plusone-masaki/handsontable-simple /202111/v6/rename
    - https://github.com/jeremy-smith-maco/handsontable /202104/v6/from 2018/Added afterAutofill hook
    - https://github.com/tho-asterist/handsontable-custom /202110/v6/1fix
    - https://github.com/Codypinto23/handsontable /v6/1fix
    - https://github.com/dataiku/handsontable /202309/from v0.17.0/Remove moment
    - https://github.com/skillstampllc/handsontable /202309/from v8
    - https://github.com/naymkazp/handsontable /202009/from v8
    - https://github.com/jansiegel/handsontable /202211/from v12
    - https://github.com/iLoveBug/handsontable /202305/v12
    - https://github.com/pingyuanChen/handsontable /201611/js/inactive
    - https://github.com/pingyuanChen/Spreadsheet /201606/js
  - repos
  - https://github.com/warpech/walkontable /MIT/201304/js
    - This is a playground for next table view engine that will enable virtual rendering in Handsontable.
    - This project is currently not maintained in this repo, but as part of Handsontable
    - [Refactor Walkontable Selection rendering module_202304](https://github.com/handsontable/handsontable/pull/10265)
      - The PR refactors and extends the Walkontable Selection rendering module for the ability to highlight the table's headers. The work presented here will be the basis for the navigation in headers

- https://github.com/laomu1988/handsontable /201910/js/inactive
  - https://laomu1988.github.io/handsontable/
  - 在线表格编辑，可编辑公式、添加Object对象

- https://github.com/moregorenine/handsontable-example /202110/ts
  - handsontable 6.2.2 MIT version example

- https://github.com/hand-dot/table2md /201906/js
  - https://hand-dot.github.io/table2md/
  - Convert from Excel-like table to markdown table.

- https://github.com/handsontable/performance-lab
  - JavaScript performance tests for Handsontable

- https://github.com/bgrins/data-ui-tests /202303/js
  - https://bgrins.github.io/data-ui-tests/
  - benchmarks with vanilla-table/handsontable, revo-grid

- https://github.com/WranglHQ/handsontable_vs_reactdatagrid
  - a website to compare the performance of two excel-type React spreadsheet components: react-data-grid and handsontable

- https://github.com/hh54188/hansontable-react-performance /201908/js
  - web_worker_demo

- https://github.com/project-kit/handsontable-select2 /201905/ts
  - Handsontable editor and cell based on select2
  - 依赖select2, jquery
  - https://github.com/TheGr8Nik/Handsontable-key-value-select /201907/ts
    - defines a Key-Value selector and a relative Renderer. The code is an extension for base Select editor and Renderer.

- https://github.com/plusone-masaki/csv-plus /202310/ts/vue3
  - CSV editor that gives you a great experience with simple operations.
  - 依赖hot.v6、electron、vuedraggable

- https://github.com/implerhq/impler.io /MIT/202401/ts/Nestjs
  - https://impler.io/
  - Open source CSV & Excel file Import Experience
  - Built With Nestjs Typescript Nx Pnpm
  - 依赖handsontable.v13

- https://github.com/DTStack/dt-react-component /202312/ts
  - https://dtstack.github.io/dt-react-component/
  - React UI component library based on antd package
  - 依赖handsontable.v6

- https://github.com/tinper-acs/ac-hand-table /201911/js/inactive
  - https://tinper-acs.github.io/ac-hand-table/
  - ac-hand-table 是基于 handsontable.v7 的适用于 React 框架的电子表格，它提供了数据绑定、数据验证、行过滤、列排序、表格多选、表格样式、表头交互、表头拖拽、行高拖拽、行交换等操作
- https://github.com/tinper-acs/ac-spreadsheet /201905/js/v5
  - https://tinper-acs.github.io/ac-spreadsheet
  - 在线电子表格组件, 依赖于handsontable. 该组件提供了列宽拖拽、列交换、排序、在线编辑、增减行、动态获取焦点行数据等操作。

- https://gitee.com/bomwu/xlsx2handson /202205/js/inactive
  - 一个将XLSX文件转换为Handsontable配置的工具, 可参考dist/index.html
  - 依赖Luckyexcel

- https://github.com/zayscue/websheets /MIT/201811/js
  - a test for importing an excel sheet into a web page using react.js, react dropzone, sheet.js, and handsontable

- https://github.com/handsontable/formula-parser /MIT/202101/js/archived
  - Javascript Library parsing Excel Formulas and more
  - https://github.com/formulajs/formulajs /500Star/MIT/202403/js
  - https://github.com/handsontable/formula.js /MIT/202001/js/archived
  - 🧮 [Handsontable 9.0.0: New formula plugin _202106](https://handsontable.com/blog/handsontable-9.0.0-new-formula-plugin)
    - It integrates our powerful calculation engine – HyperFormula®
    - Up to version 8.4.0 there was a formula plugin that was built by us based on two other projects: our own formula parser, and an external library of spreadsheet functions, called formula.js.
  - https://github.com/PascalKeukInovia/hot-formula-parser /202205/js/inactive
    - Library provides a Parser class that evaluates excel and mathematical formulas.
    - All excel formulas defined in formula.js;

- https://github.com/tdjun/handsontable.webpack /MIT/201805/js
  - Custom Hansontable+ es6
  - handsontable formula
  - Merge handsontable Grid implementation
# utils
- https://github.com/Yinger/ts-excel-compare /202009/ts
  - https://yinger.github.io/ts-excel-compare/
  - 🆚 Diff Tool to Compare Two Excel Spreadsheet Files 
  - 依赖handsontable、sheetjs、daff、antd
  - 借鉴了diff符号，+++(-:1) 表示新增行, `(1:-) 表示删除行

- https://github.com/21epub/xlsx /201908/js
  - xlsx table data module

- https://github.com/mydea/handsontable-chosen-editor /201901/js
  - http://mydea.github.io/handsontable-chosen-editor/
  - select field

- https://github.com/orestisrodriguez/handsontable-multi-select /202007/js/v7
  - Editor for handsontable that allows multiple select cells. Based on jshjohnson/Choices

- https://github.com/kpi-intelligence/handsontable-key-value /201906/js
  - Handstontable plugin to handle key-value pair data type.
  - It's built upon the builtin autocomplete feature with some small tweaks
  - https://github.com/npm-moregorenine/handsontable-6.2.2-celltype-key-value /202110/js

- https://github.com/burnash/dataimport
  - Simple JavaScript CSV Importer

- https://github.com/handsontable/pikaday /202312/js/NoDeps
  - A refreshing JavaScript Datepicker — lightweight, no dependencies, modular CSS
  - No dependencies (but plays well with Moment.js)
  - https://github.com/Pikaday/Pikaday /202109/js/inactive

- https://github.com/shuttlethread/hodf /202009/js/v7
  - A wrapper around handsontable spreadsheet for collecting data.frame objects with a dynamic number of columns/rows.

- https://github.com/omid/formula /MIT/202211/rust/inactive
  - A parser and evaluator of spreadsheet-like formulas
  - Add this library to your project with npm install formula-wasm
  - At the moment, we don't support table data. It means you need to extract table data and pass theirs values to this library
  - We still do not support parentheses to change the order of operations, but you can use our F. function
  - Inspired by formulajs
# examples
- https://github.com/hughfenghen/spreadsheet-demo /202003/js/inactive
  - 电子表格从调研到demo的杂乱记录 Handsontable vs SpreadJS
  - SpreadJS时间较长，基本上对标Excel，功能比Hot丰富。比如对公式（Hot 处于alpha版，不支持自定义）、分组（Hot不支持）、图表（Hot需要继承第三方图表）的支持。

- https://github.com/xuehongyanL/SetLite /MIT/201901/js
  - lightweight electron app for data processing & visualization
  - 依赖handsontable.v6、react-katex、react-bootstrap
  - I have used miniblink as alternative for electron built-in browser kernel

- https://github.com/ONSdigital/dp-table-builder-ui /202207/js
  - react component ui for table builder
  - 依赖handsontable.v0.33

- https://github.com/White-Canary-Team/Google-Docs /201710/js
  - Cloned Google Docs with react | redux | nodeJS | Socket. IO | QuillJS | JSpreadsheets | MaterialUI.
  - 依赖handsontable.v0.34、material-ui.v0.19、react-quill、react-redux、socket.io

- https://github.com/bloodstrawberry/react-project /202404/js
  - https://bloodstrawberry.github.io/react-project/myHandsTable
  - 玩具合集: hot/tui/file-browser/chat

- https://github.com/GeordiIGT/grids /202207/js
  - For FuturMaster: handsontable, ag-grid

- https://github.com/geoffreylitt/wildcard /202104/ts/inactive
  - https://www.geoffreylitt.com/wildcard/
  - A browser extension for customizing web apps with a spreadsheet view
  - 依赖hot.v7
  - Wildcard is a platform that empowers anyone to build browser extensions and modify websites to meet their own specific needs.
  - Wildcard shows a simplified view of the data in a web page as a familiar table view. People can directly manipulate the table to sort/filter content, add annotations, and even use spreadsheet-style formulas to pull in data from other websites.

- https://github.com/artbels/mongo-table-admin /201801/js
  - Work with mongo collection as a table. Inline edit or pivot. Filter documents with json query.
  - Integrates Handsontable - great inline edit tool, and Pivottable - data discovery and analysis tool.

- https://github.com/dataspread/dataspread-web /202105/后端java/js/inactive
  - http://dataspread.github.io/
  - DataSpread is a spreadsheet-database hybrid system, with a spreadsheet frontend, and a database backend. 
  - Thus, DataSpread inherits the flexibility and ease-of-use of spreadsheets, as well as the scalability and power of databases.
  - A flexible hybrid data model to represent spreadsheet data within a database
  - 前端依赖handsontable.v6

- https://github.com/apogeejs/apogeejs-admin /202112/js
  - http://www.apogeejs.com/
  - Apogee is a tool for quick coding tasks, like munging data or prototyping an algorithm
  - a javascript programming environment for iterative programming
  - inspired by the spreadsheet and notebooks
  - The Apogee web application runs completely in the browser
  - 依赖handsontable.v6

- https://github.com/prose/prose /BSD/202401/js
  - http://prose.io/
  - It's a web-based interface for managing content on GitHub. 
  - Use it to create, edit, and delete files, and save your changes directly to GitHub.
  - 依赖backbone.v1、codemirror5、handsontable.v0.23

- https://github.com/unep-grid/mapx /GPLv3/202311/js
  - https://app.mapx.org/
  - an online platform for managing geospatial data on natural resources, developed by UNEP/GRID-Geneva
  - 依赖handsontable.v6

- https://github.com/statsim/app /202012/js/vue
  - open-source web application for statistical simulations and bayesian inference.
  - Made with VueJS and WebPPL

- https://github.com/qcif/data-curator /MIT/202111/js/vue
  - a simple desktop data editor to help describe, validate and share usable open data.
  - 依赖rxjs、vue2、xlsx、handsontable.v3

- https://github.com/OpenDataRepository/data-publisher /202401/php/js
  - aims to create a simple tool for publishing data to the web.

- https://github.com/decisive-wizard/GridHub /201412/js/inactive
  - Desktop spreadsheet editor with version history

- https://github.com/thanhlevu/excel-alike-editor /202401/ts/HyperFormula
  - client + server

- https://github.com/willchenko7/sheets-ai /202307/js/inactive
  - The goal of this repo is to create a natural language interface to perform spreadsheet tasks.
  - This code uses prompt engineering to generate code from a given request that will then interact with the spreadsheet.
  - The approach to this app is to leverage GPT to take a user's request, convert it into a piece of code that is then executed with eval.

- https://github.com/liuwei2016/file-viewer /202301/js/vue/inactive
  - 一个客户端压缩包和文件预览系统
  - 依赖vue2、jszip、handsontable.v11

- https://github.com/bloodstrawberry/csv-editor-with-handsontable /202208/js
  - 依赖hot.v12
# collab
- https://github.com/liddiard/project-linteum /201703/js
  - Concept for a Handsontable+Node.js+Websockets collaborative editing tool that publicly exposes sheet data via an API. 
  -  Didn't get very far because https://github.com/liddiard/google-sheet-s3 solved my use case

- https://github.com/BrotherJing/scalable-ot /MIT/201911/ts/inactive
  - A scalable concurrent collaboration framework based on Operational Transformation (OT).
  - 后端依赖 ot-json0、ot-text、google-protobuf、mongodb、ws、express
  - 前端依赖handsontable.v7、text-diff-binding、protobuf
  - Clients send operations through API.
  - Operations are pushed into MQ, partitioned by document id.
  - OT server receives operations of same document sequentially and performs conflict solving.
  - Broadcast server sends conflict-free operations to clients.
  - Conflict-free operations are pushed into another MQ(or db stream), trigger a consumer which apply them on document snapshot sequentially.

- https://github.com/khalilgharbaoui/realtime_spreadsheet /201906/ruby
  - Realtime spreadsheet like google docs using Rails, RethinkDB (nobrainer)
# integrations
- https://gitlab.com/thanhhuu09/superset-handsontable-plugin /202308/ts/v13
  - This is the Superset Handsontable Plugin Superset Chart Plugin.

- https://github.com/kintone-samples/kintone-spreadsheet /202401/ts
  - You can view and edit the kintone list screen with the look of a spreadsheet like Excel.
  - 依赖handsontable.v6、kintone-ui-component
# more
- https://github.com/owid/owid-grapher /MIT/202404/ts
  - https://ourworldindata.org/owid-grapher
  - A platform for creating interactive data visualizations
  - This is the project we use at Our World in Data to create embeddable visualizations
  - This repo is currently not well-designed for reuse as a visualization library, as our tools are tightly coupled with our database structure.
