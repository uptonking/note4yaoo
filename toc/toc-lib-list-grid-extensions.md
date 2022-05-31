---
title: toc-lib-list-grid-extensions
tags: [extensions, grid, list, toc]
created: '2021-05-23T16:31:14.208Z'
modified: '2021-05-23T16:31:36.100Z'
---

# toc-lib-list-grid-extensions

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
# handsontable-extensions
- https://github.com/laomu1988/handsontable
  - 在线表格编辑，可编辑公式、添加Object对象
- https://github.com/handsontable/performance-lab
  - JavaScript performance tests for Handsontable
- https://github.com/hand-dot/table2md
  - Convert from Excel-like table to markdown table.
- https://github.com/orestisrodriguez/handsontable-multi-select
  - Editor for handsontable that allows multiple select cells. Based on jshjohnson/Choices
- https://github.com/WranglHQ/handsontable_vs_reactdatagrid
  - a website to compare the performance of two excel-type React spreadsheet components: react-data-grid and handsontable
- https://github.com/burnash/dataimport
  - Simple JavaScript CSV Importer
# grid-utils
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
