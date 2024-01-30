---
title: lib-excel-handsontable-examples
tags: [data-grid, examples, handsontable]
created: 2023-12-21T20:05:53.059Z
modified: 2023-12-21T20:06:13.700Z
---

# lib-excel-handsontable-examples

# guide

# popular
- handsontable v6.2.2 /13.8kStar/MIT~Paid/201903/js
  - https://github.com/handsontable/handsontable
  - https://handsontable.com/
  - 基于table标签实现
  - 依赖numbro, moment, pikaday
  - a JS HTML5 data grid with spreadsheet look & feel.
  - free for all non-commercial purposes since 7.0
  - 不支持协作
  - 支持undo，[Q: Possible to combine multiple actions into single undo/redo step?](https://github.com/handsontable/handsontable/issues/7324)
  - [Handsontable drops open source for a non-commercial license_201903](https://github.com/handsontable/handsontable/issues/5831)
    - https://github.com/handsontable/handsontable/releases/tag/7.0.0
    - [Handsontable v7 and later versions are fully commercial so it really depends on your case](https://twitter.com/handsontable/status/1164198101726433282). 
    - If you want to fully integrate it with your software while maintaining the OSS license, then your only option is to use v6.2.2 - the last one released under the MIT license.
  - 🍴 forks
    - https://github.com/swsvindland/opentable /202201/js/from-jacksontable/move walkontable back
      - https://github.com/swsvindland/opentable-react
    - https://github.com/rathbone-labs/jacksontable /201907/js/inactive
    - https://github.com/lbobylev/jacksontable
    - https://github.com/dreamsavior/mitontable /2commits
    - https://github.com/janisdd/handsontable /202304/v6/ts-d/fork for https://github.com/janisdd/vscode-edit-csv
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
  - repos
  - https://github.com/warpech/walkontable /MIT/201304/js
    - This is a playground for next table view engine that will enable virtual rendering in Handsontable.
    - This project is currently not maintained in this repo, but as part of Handsontable
    - [Refactor Walkontable Selection rendering module_202304](https://github.com/handsontable/handsontable/pull/10265)
      - The PR refactors and extends the Walkontable Selection rendering module for the ability to highlight the table's headers. The work presented here will be the basis for the navigation in headers

- https://github.com/moregorenine/handsontable-example /202110/ts
  - handsontable 6.2.2 MIT version example

- https://github.com/laomu1988/handsontable /201910/js/inactive
  - https://laomu1988.github.io/handsontable/
  - 在线表格编辑，可编辑公式、添加Object对象

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

- https://github.com/project-kit/handsontable-select2 /201905/ts
  - Handsontable editor and cell based on select2
  - 依赖select2, jquery
  - https://github.com/TheGr8Nik/Handsontable-key-value-select /201907/ts
    - defines a Key-Value selector and a relative Renderer. The code is an extension for base Select editor and Renderer.

- https://github.com/plusone-masaki/csv-plus /202310/ts/vue3
  - CSV editor that gives you a great experience with simple operations.
  - 依赖hot.v6、electron、vuedraggable

- https://github.com/implerhq/impler.io /MIT/202401/ts
  - https://impler.io/
  - Open source CSV & Excel file Import Experience
  - Built With Nestjs Typescript Nx Pnpm
  - 依赖handsontable.v13

- https://github.com/DTStack/dt-react-component /202312/ts
  - https://dtstack.github.io/dt-react-component/
  - React UI component library based on antd package
  - 依赖handsontable.v6

- https://gitee.com/bomwu/xlsx2handson /202205/js/inactive
  - 一个将XLSX文件转换为Handsontable配置的工具, 可参考dist/index.html
  - 依赖Luckyexcel

- https://github.com/zayscue/websheets /MIT/201811/js
  - a test for importing an excel sheet into a web page using react.js, react dropzone, sheet.js, and handsontable
# utils
- https://github.com/Yinger/ts-excel-compare /202009/ts
  - https://yinger.github.io/ts-excel-compare/
  - Diff Tool to Compare Two Excel Spreadsheet Files 
  - 依赖handsontable、sheetjs、daff、antd

- https://github.com/21epub/xlsx /201908/js
  - xlsx table data module

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
  - A wrapper around handsontable spreadsheet for collecting data.frame objects with a dynamic number of columns / rows.
# examples
- https://github.com/hughfenghen/spreadsheet-demo /202003/js
  - 电子表格从调研到demo的杂乱记录 Handsontable vs SpreadJS
  - SpreadJS时间较长，基本上对标Excel，功能比Hot丰富。比如对公式（Hot 处于alpha版，不支持自定义）、分组（Hot不支持）、图表（Hot需要继承第三方图表）的支持。

- https://github.com/xuehongyanL/SetLite /MIT/201901/js
  - lightweight electron app for data processing & visualization
  - 依赖handsontable.v6、katex

- https://github.com/ONSdigital/dp-table-builder-ui /202207/js
  - react component ui for table builder
  - 依赖handsontable.v0.33

- https://github.com/tinper-acs/ac-spreadsheet /201905/js/v5
  - https://tinper-acs.github.io/ac-spreadsheet
  - 在线电子表格组件, 依赖于handsontable. 该组件提供了列宽拖拽、列交换、排序、在线编辑、增减行、动态获取焦点行数据等操作。

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
# integrations
- https://gitlab.com/thanhhuu09/superset-handsontable-plugin /202308/ts/v13
  - This is the Superset Handsontable Plugin Superset Chart Plugin.

- https://github.com/kintone-samples/kintone-spreadsheet /202401/ts
  - You can view and edit the kintone list screen with the look of a spreadsheet like Excel.
  - 依赖handsontable.v6、kintone-ui-component
# more
