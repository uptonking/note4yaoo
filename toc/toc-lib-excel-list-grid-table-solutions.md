---
title: toc-lib-excel-list-grid-table-solutions
tags: [excel, grid, list, solutions, spreadsheet, table, toc]
created: 2020-07-12T13:01:37.487Z
modified: 2023-11-12T06:25:03.307Z
---

# toc-lib-excel-list-grid-table-solutions

# guide

- 很多design system都实现了自己的list和grid组件

- keyword: data list/grid/table/excel/spreadsheet

- sheet-test
  - [SheetJS Test Files](https://github.com/SheetJS/test_files)
    - XLS/XLSX/XLSB and other spreadsheet formats
  - [vaadin spreadsheet test sheets](https://github.com/vaadin/spreadsheet/tree/master/vaadin-spreadsheet/src/test/resources/test_sheets)
# awesome-list-grid
- https://jsgrids.statico.io/
  - https://github.com/statico/jsgrids /MIT/202402/ts
  - 卡片上列出了该项目所支持的表格特性及不支持的特性
  - 无详情页
  - 支持多条件filter+sort

- https://amitmy.github.io/grids/
  - https://github.com/AmitMY/grids /202112/js/jekyll/inactive
  - A grid comparison. 只比较特性，统计不完整。

- https://jspreadsheets.com/
  - https://github.com/Handsoncode/JSpreadsheets.com /201806/js/inactive
  - 点击卡片可切换查看每个项目的详情及预览图
  - 支持详情页
  - 依赖react-static、marked

- https://github.com/FancyGrid/awesome-grid /markdown
  - A curated list of grid(table) libraries and resources that developers may find useful.
# excel
- https://github.com/dataspread/dataspread-web /202105/后端java/js/inactive
  - http://dataspread.github.io/
  - DataSpread is a spreadsheet-database hybrid system, with a spreadsheet frontend, and a database backend. 
  - Thus, DataSpread inherits the flexibility and ease-of-use of spreadsheets, as well as the scalability and power of databases.
  - A flexible hybrid data model to represent spreadsheet data within a database
  - 前端依赖 handsontable.v6

- https://github.com/dataspread/spreadsheet-benchmark
  - We developed an exhaustive benchmark, sheetperf, to evaluate the performance of spreadsheet systems.
    - measures the scalability of spreadsheet systems for a range of canonical spreadsheet operations, and
    - investigates how a spreadsheet system stores data and whether it adopts optimizations to speed up computation.
  - Our benchmark has been implemented for three popular spreadsheet systems, Microsoft Excel, LibreOffice Calc, and Google Sheets.

- https://github.com/programcsharp/griddly /c#
  - Griddly is an extremely configurable MVC/AJAX grid that separates render and data logic. 
  - Data is returned from an action method, settings are done in the view.
  - install NuGet, Install-Package Griddly
# commercial-list-grid
- FancyGrid /OneOffLic
  - https://www.fancygrid.com/
  - JS grid library with charts integration and server communication.

- GrapeCity SpreadJS /AnnualLic|PerpetualLic
  - https://www.grapecity.com/spreadjs
  - SpreadJS offers a complete Excel-like experience, including tables, charts, shapes, sparklines, 
    - high-speed calculation engine, conditional formatting, sorting and filtering along with extensive support for importing 
    - and exporting native Excel spreadsheets with no Excel dependencies. 
  - Some exclusive features like barcodes, rich text, cell buttons, cell dropdowns 
    - and range templates are also provided to assist developers in creating flawless JavaScript applications.

- DevExtreme DataGrid /Free4NonCommercial
  - https://js.devexpress.com/
  - DevExtreme HTML5 Data Grid is a feature-rich data shaping and editing client-side widget 
  - DevExtreme React Grid /Free4NonCommercial
    - https://devexpress.github.io/devextreme-reactive/react/grid/ 
    - It is a component that displays table data from a local or remote source.
    - It supports paging, sorting, filtering, grouping and other data shaping options, row selection, and data editing. 
    - Support for controlled and uncontrolled state modes allows you to use the Grid in a regular or Redux-based application. 
    - DevExtreme Grid component has a composable and extendable plugin-based architecture and is provided with Twitter Bootstrap and Material-UI rendering and theming out of the box.

- Telerik Kendo Grid /BuyLic
  - https://www.telerik.com/kendo-ui
  - https://demos.telerik.com/kendo-ui/spreadsheet/index
  - Grid is a powerful control for displaying data in a tabular format.
    - paging, sorting, filtering, grouping, and editing
  - Spreadsheet allows you to edit and visualize tabular data by using cell formatting options, styles, and themes.

- DataGridXL /FreeWithLink/canvas
  - https://www.datagridxl.com/
  - https://github.com/DataGridXL/DataGridXL
  - Vanilla Javascript data grid with Excel-like controls
  - 只开源了源码编译后的bundle，不友好
  - https://github.com/DataGridXL/DataGridXL2 /432Star/linkware/202303/js/canvas
    - https://www.datagridxl.com/
    - Excel-like Experience for Web Apps 
    - The performant & reliable Vanilla Javascript data grid with Excel-like controls
    - 开源了压缩后的代码
    - v3 ing
    - [Show HN: Datagridxl2.js – Fast Excel-like data table library | Hacker News_202204](https://news.ycombinator.com/item?id=30919257)

- DHTMLX Spreadsheet /GPLv2/26Star/201909/js
  - https://dhtmlx.com/
  - https://github.com/DHTMLX/dhtmlx-suite-gpl
    - 仅公开打包后未压缩的代码
    - Standard edition
  - https://github.com/DHTMLX/gantt
  - To use dhtmlxSuite in non-GPL projects (and get Pro version), please obtain Commercial/Enterprise License
  - 只开源了源码编译后的bundle，不友好

- Sencha /Free4FiveDev
  - https://www.sencha.com/
  - 基于Ext JS实现
  - 基于div实现表格，单元格中可包含canvas图表

- Webix SpreadSheet 产品线齐全，包括表格、透视表、看板、文件管理器、gantt
  - https://webix.com/spreadsheet/
  - a customizable web widget which offers all functions of Excel-style spreadsheets
# more
- [Alternatives to Handsontable and ag-Grid - DZone](https://dzone.com/articles/alternatives-to-handsontable-and-ag-grid)
  - DHTMLX JavaScript Components
  - Webix Widgets
  - Syncfusion Essential JS 2
  - Ignite UI components
  - Kendo UI for jQuery
  - GrapeCity’s JavaScript UI Components
