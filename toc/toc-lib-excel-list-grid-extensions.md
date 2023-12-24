---
title: toc-lib-excel-list-grid-extensions
tags: [extensions, grid, list, toc]
created: 2021-05-23T16:31:14.208Z
modified: 2022-08-21T10:03:57.063Z
---

# toc-lib-excel-list-grid-extensions

# react-list-keyboard
- react-window默认显示滚动条，但可通过css隐藏滚动条同时使内容支持滚动
  - [Add option to FixedSizeList for hiding scrollbar](https://github.com/bvaughn/react-window/issues/375)
    - scrollbar-color: transparent transparent;
- mui默认的list就支持键盘操作
- [Hide scroll bar, but while still being able to scroll](https://stackoverflow.com/questions/16670931)

- https://github.com/lukasbach/react-accessible-menu
  - https://lukasbach.github.io/react-accessible-menu/storybook/
  - 只依赖uuid
  - Accessible keyboard-friendly interactive list/menu component
  - 提供了丰富的示例，包括 vertical、horizontal、grid、imperative、virtualized
  - 长列表的示例支持向下方向键自动滚动
  - virtualized的示例基于 react-virtualized

- https://github.com/dzucconi/use-keyboard-list-navigation
  - A React hook to navigate through lists with your keyboard.
# tabulator-extensions
- https://github.com/ngduc/react-tabulator
  - React Cell Editors: DateEditor, MultiSelectEditor, etc.
  - React Cell Formatters: MultiValueFormatter, etc.
- https://github.com/surveyjs/survey-analytics
  - SurveyJS Analytics library allows to render survey results as charts or tables
  - 依赖tabulator-tables、datatables.net
- https://github.com/orgenic/orgenic-ui
  - create strong user interfaces with high quality web components.
  - 依赖stencil、tabulator-tables.v4
# excel-utils
- https://github.com/dominictarr/excel-stream /201507/js
  - A stream that converts excel spreadsheets into JSON object arrays.
  - excel isn't really a streamable format. 
  - 依赖csv-stream、JSONStream、j
  - But it's easy to work with streams because everything is a stream. This writes to a tmp file, then pipes it through the unfortunately named j then into csv-stream

- https://github.com/patrik-csak/BB26
  - Convert between numbers and base-26 spreadsheet column letters

- https://github.com/warpech/sheetclip /201505/js
  - Copy/paste from your HTML5 web app to a spreadsheet
  - Tiny library that transforms JavaScript 2-dimensional arrays to clipboard strings compatible with spreadsheets such as Microsoft Excel, Google Docs, LibreOffice and OpenOffice

- https://github.com/unosquare/tubular-common
  - Tubular Common provides TypeScript and Javascript models and data transformer to use any Tubular DataGrid component with an array of Javascript objects.
  - https://github.com/unosquare/tubular-react
    - a Material-UI table (or data grid) with local or remote data-source
  - https://github.com/unosquare/tubular-nodejs
- https://github.com/jammeryhq/gridsome-source-mock-data
  - Simple gridsome source plugin which uses danibram/mocker-data-generator to generate your mock data.
- excelexportjs /88Star/MIT/201909/ts/NoDeps
  - https://github.com/tarunbatta/excelexportjs
  - Various server-side binaries and support libraries are present to help us export grids/tables data to excel sheets, but the same export handling at client side is a tough nut to crack. 
  - This plugin helps you achieve that, thereby providing advance features as well.

- https://github.com/paulfitz/daff /HaxeLang
  - http://paulfitz.github.io/daff/
  - a library for comparing tables, producing a summary of their differences, and using such a summary as a patch file. 
  - It is optimized for comparing tables that share a common origin, in other words multiple versions of the "same" table.
  - The daff library is written in Haxe Lang, which can be translated reasonably well into js/python/java
  - example shows the changes made in the modified table with respect to the original table. The format used is the highlighter tabular diff.
# could-excel
- https://github.com/odwyersoftware/sheet2api-js /js
  - JavaScript Library for Google Sheets/Microsoft Excel Online through [sheet2api](https://sheet2api.com/).
