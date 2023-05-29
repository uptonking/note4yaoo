---
title: toc-lib-excel-list-grid-popular
tags: [grid, lib, list, toc]
created: 2020-10-22T06:47:15.435Z
modified: 2022-08-21T10:02:27.788Z
---

# toc-lib-excel-list-grid-popular

# focus

- requirements
  - group/aggregate/pivot
  - virtualized
  - undo/redo
  - operations
  - keyboard/a11y

- 开源表格
  - 国内: luckysheet
  - 国外: ag-grid, tanstack-table, glide, handsontable, o-spreadsheet, tui-grid
  - tinybase

- src-list-grid
  - **ag-grid**
  - **tanstack-table**
  - **react-window**
  - **react-virtuoso**
  - react-tiny-virtual-list
  - react-virtualized

- src-list-grid-canvas
  - **luckysheet**: 未使用class类，函数式风格
  - glide-data-grid: react组件
  - x-spreadsheet/wolf: class类和函数式都有
  - cheetah-grid(ts): 基于class类继承
# list-grid-with-div
- ag-grid /MIT/6.4kStar/202202/ts/NoDeps
  - https://github.com/ag-grid/ag-grid
  - https://www.ag-grid.com/example.php
  - 基于div实现，每行对应的dom元素存在
  - a fully-featured and highly customizable JavaScript data grid
    - has no 3rd party dependencies
    - integrates smoothly with all major JavaScript frameworks
  - ag-grid-enterprise is Commercial licensed but opensourced
  - [Why is the minified bundle so large?](https://github.com/ag-grid/ag-grid/issues/1459)
    - Main reason IMO: the grids has no dependencies

- tanstack-table /MIT/11.6kStar/202202/ts
  - https://github.com/tannerlinsley/react-table
  - https://react-table.tanstack.com/
  - Hooks for building fast and extendable tables and datagrids for React
  - React Table is a headless utility, which means it doesn't supply any actual UI elements.
  - react-virtual /MIT/1.1kStar/202007
    - https://github.com/tannerlinsley/react-virtual
    - Hooks for virtualizing scrollable elements in React

- react-window /14kStar/MIT/202304/js
  - https://github.com/bvaughn/react-window
  - https://react-window.now.sh/
  - 基于div实现，每行对应的dom元素不存在
  - React components for efficiently rendering large lists and tabular data
  - React window works by only rendering part of a large data set(just enough to fill viewport).
  - [Support just-in-time measured content](https://github.com/bvaughn/react-window/issues/6)
  - forks
    - https://github.com/webcore-it/react-window
  - https://github.com/vikadata/vikatable /ts
    - 基于 react-window Grid 构建的表格组件
    - @apitable/react-flow 基于其中的 Grid 构建，通过扩展 Grid 的 props 参数，非侵入式支持更多的表格特性, 使其更方便构建表格。
  - https://github.com/bvaughn/react-window-infinite-loader
    - https://codesandbox.io/s/5wqo7z2np4
    - InfiniteLoader component inspired by react-virtualized but for use with react-window
    - This demo app mimics loading remote data.Once data has been "loaded" the row number will be displayed.
  - https://github.com/pupudu/window-table /202207/ts/inactive
    - https://window-table.netlify.com/
    - Windowing Table for React based on React Window
    - [Roadmap for bvaughn/react-window-table](https://github.com/bvaughn/react-window-table/issues/1)
  - https://github.com/mckervinc/react-fluid-table /202009/ts/inactive
    - https://mckervinc.github.io/react-fluid-table/
    - A windowed React table built on top of react-window

- react-virtuoso /3.7kStar/MIT/202305/ts/list/table
  - https://github.com/petyosi/react-virtuoso
  - https://virtuoso.dev/
  - powerful React virtual list/table component
  - V1 brings improvements to reverse infinite scrolling behavior - suitable for chat and feed user interfaces.

- onlyoffice-sdkjs /190Star/AGPLv3/202302/js
  - https://github.com/ONLYOFFICE/sdkjs
  - https://api.onlyoffice.com/docbuilder/spreadsheetapi
  - Contains API for all the included components client-side interaction.
  - 通过TypedArray，将表格数据以二进制格式存储，通过字段压缩+共享字符串表来优化内存空间
  - [精读onlyoffice在线表格存储设计](https://juejin.cn/post/7202252704978386999)

- https://github.com/jmptrader/SpreadJS /201608/js
  - gcspread.sheets.all.9.40.20161.0.min.js

- react-tiny-virtual-list /MIT/1.8kStar/201910/ts
  - https://github.com/clauderic/react-tiny-virtual-list
  - https://clauderic.github.io/react-tiny-virtual-list/
  - A tiny but mighty 3kb list virtualization library, with zero dependencies
  - Supports variable heights/widths, sticky items, scrolling to index, and more
  - https://github.com/clauderic/react-infinite-calendar /inactive
    - 依赖tiny-virtual-list,date-fns

- react-virtualized /MIT/19.5kStar/202105/js
  - https://github.com/bvaughn/react-virtualized
  - http://www.reactvirtualized.com/
  - https://github.com/bvaughn/react-virtualized/blob/master/docs/Grid.md
  - 基于div实现，每行对应的dom元素不存在
  - 表格主体ReactVirtualized__Grid__innerScrollContainer内全是单元格
  - React components for efficiently rendering large lists and tabular data
- react-data-grid /MIT/4kStar/202201/ts
  - https://github.com/adazzle/react-data-grid
  - https://adazzle.github.io/react-data-grid/canary/
  - 基于div实现，每行对应的dom元素存在，未实现row/column span(merging cells)
  - 项目模块化，分为core和addons
  - Excel-like grid component built with React, with editors, keyboard navigation, copy...

- sleekgrid /25Star/MIT/202304/ts/NoDeps/vanillajs
  - https://github.com/serenity-is/sleekgrid
  - https://serenity-is.github.io/sleekgrid/
  - a complete rewrite of the original SlickGrid in TypeScript with ES6 modules
  - 支持插件
  - used extensively in Serenity, our open source ASP. NET Core / TypeScript based business application framework. 

- tui.grid /2.2kStar/MIT/202305/ts/vanillajs
  - https://github.com/nhn/tui.grid
  - http://ui.toast.com/tui-grid/
  - 基于table标签实现，合并表头列实际样式为.tui-grid-lside/rside-area
  - 支持sort, filter, 不支持group
  - 依赖xlsx、tui-date-picker、tui-pagination
  - 视图层依赖preact，但使用时不要求react环境，通过new Grid(options)
  - 部分使用class组件，
  - 状态使用自定义createStore
  - Powerful Component to Display and Edit Data.
  - TOAST UI Grid is available when using the Plain JS, React, Vue Component.
  - [Is there no undo function?_202207](https://github.com/nhn/tui.grid/issues/1735)
    - Unfortunately, it is not supported.

- hyperformula /1.5kStar/GPLv3/202304/ts
  - https://github.com/handsontable/hyperformula
  - https://handsontable.com/docs/hyperformula
  - HyperFormula is a headless spreadsheet built on top of TypeScript. 
  - It is a parser and evaluator of Excel formulas for web applications. 
  - You can use it in a browser or as a service, with Node.js as your back-end technology.
  - Function syntax compatible with Microsoft Excel and Google Sheets
  - HyperFormula comes with a huge library of 391 built-in functions grouped into categories
  - It also supports the use of cross-sheet references, named expressions, different data types, and custom functions.
  - HyperFormula doesn't assume any existing user interface, which makes it a great general-purpose library that can be used in various business applications.
  - [Key concepts | HyperFormula ](https://hyperformula.handsontable.com/guide/key-concepts.html)
    - Data processing consists of three phases.
    - Phase 1. Parsing and construction of ASTs
    - Phase 2. Construction of the dependency graph. find the right order of processing cells, also known as topological order
    - Phase 3. Evaluation

- tabulator /MIT/3.4kStar/202202/js/NoDeps
  - https://github.com/olifolkerd/tabulator
  - http://tabulator.info/
  - https://github.com/ngduc/react-tabulator
    - a JS table library with many advanced features based on tabulator
  - 基于div实现，每行对应的dom元素存在，未实现column span
  - Interactive Tables and Data Grids for JavaScript supporting react, angular, vue
- frappe-datatable /877Star/MIT/202303/js
  - https://github.com/frappe/datatable
  - https://frappe.io/datatable
  - 基于div实现，每行对应的dom元素存在
  - 依赖hyperlist、sortablejs、lodash
  - A simple, modern and interactive datatable for the web
  - https://github.com/tbranyen/hyperlist
    - /MIT/291Star/202006/js/NoDeps
    - A performant virtual scrolling list utility capable of rendering millions of rows
    - a fork of the existing (unmaintained) project: sergi/virtual-list
- FancyGrid /BuyLic/153Star/20212/js/NoDeps
  - https://github.com/FancyGrid/FancyGrid
  - https://fancygrid.com/
  - JS grid library with charts integration and server communication.
  - 基于div实现，实现很特别，表格ui是一列一列相邻放置构成的，每列对应的dom元素存在

- react-base-table /1.4kStar/MIT/202303/js
  - https://github.com/Autodesk/react-base-table
  - https://autodesk.github.io/react-base-table/
  - 基于div实现，每行对应的dom元素存在
  - 依赖react-window、memoize-one
  - A react table component to display large datasets with high performance and flexibility
  - 未实现row select(作者为组件unopinionated的目标而未合并pr)，但提供示例
- react-datasheet-grid /242Star/MIT/202302/ts
  - https://github.com/nick-keller/react-datasheet-grid
  - https://react-datasheet-grid.netlify.app/docs/features
  - 依赖react、tanstack-virtual~~react-window~~、react-resize-detector
  - more like Airtable or Notion and less like Excel in the sense that instead of dealing with individual cells it deals with entire rows, and each column is responsible for a single property of each row

- fast-grid /23Star/NALic/202305/ts
  - https://github.com/gabrielpetersson/fast-grid
  - https://fast-grid.vercel.app/
  - performant DOM-based web table.
  - Resuses parts of DOM-tree to reduce expensive DOM mutations
  - Own event loop to prioritize tasks. Never drops a frame
  - Custom virtualization and scrolling. Not limited by browsers 15 million pixel div height limit
  - Non-passive scrolling. Rows will never be seen rows loading into the UI while scrolling

- rsuite-table /327Star/MIT/202010/ts
  - https://github.com/rsuite/rsuite-table
  - http://rsuite.github.io/rsuite-table/
  - 基于div实现
  - 依赖react、rsuite/dom-lib、element-resize-event、lodash
- react-fluid-table /26Star/MIT/202009/ts/inactive
  - https://github.com/mckervinc/react-fluid-table
  - https://mckervinc.github.io/react-fluid-table/#/
  - 基于div实现，每行对应的dom元素存在
  - 依赖react-window
  - A windowed React table built on top of react-window
- react-data-browser /4Star/MIT/202001/ts/NoDeps/inactive
  - https://github.com/davidalekna/react-components/tree/master/packages/react-data-browser
  - https://codesandbox.io/s/github/davidalekna/data-browser-examples
  - 基于div和flexbox实现
  - The original use case of this component is to build flexbox tables, 
  - however the API is powerful and flexible enough to build things like grids as well.
  - DataBrowser component will not provide any styles, only the functionality.
  - use-table-tools /MIT/18Star/202009/ts/NoDeps/inactive
    - https://github.com/davidalekna/use-table-tools
    - Hooks for building kickass react table components
    - flexbox table with adjustable column configuration
- react-final-table /9Star/MIT/202104/ts/inactive
  - https://github.com/Buuntu/react-final-table
  - https://githubbox.com/Buuntu/react-final-table/tree/master/examples/basic
  - A headless UI component libray for managing complex table state in React.
  - Inspired by react-table but with Typescript support built in and a simpler API.

- react-spreadsheet /MIT/245Star/202003/matrix
  - https://github.com/iddan/react-spreadsheet
  - https://iddan.github.io/react-spreadsheet
  - 依赖 developit/unistore(state container with component actions for Preact & React，支持redux devtools)
  - Simple, customizable yet performant spreadsheet for React, (yet not virtualized)
# excel-like-apps
- https://github.com/infinite-table/infinite-react
  - https://infinite-table.com/
  - https://infinite-table.com/docs/learn/examples/dynamic-pivoting-example
  - Infinite Table is a React DataGrid component for displaying virtualized tabular data. 
  - row grouping - both server-side and client-side
  - pivoting - both server-side and client-side
  - column grouping
  - lazy loading
  - keyboard navigation for cells and rows

- S2 /1.1kStar/MIT/202302/ts
  - https://github.com/antvis/S2
  - https://s2.antv.antgroup.com/examples
  - S2是多维交叉分析领域的表格解决方案，数据驱动视图，提供底层核心库、基础组件库、业务场景库
  - 依赖 @antv/g-canvas、g-gesture、d3-interpolate

- ali-react-table /530Star/MIT/202112/ts
  - https://github.com/alibaba/ali-react-table
  - https://ali-react-table.js.org/examples/big-data
  - 依赖rxjs、popperjs、styled-components
  - 提供了很多业务场景示例的live demo，以及测试数据
  - 内置虚拟滚动，数据量较大时自动开启，实现了pivot

- https://github.com/flexicious/react-data-grid /未开源/示例多/测试数据
  - https://flexicious.github.io/react-data-grid/
  - a team with 20+ years of experience building data grids

- reactdatagrid /25Star/MIT/202201/js/class组件
  - https://github.com/inovua/reactdatagrid
  - https://reactdatagrid.io/demo
  - 基于div实现，每行对应的dom元素存在
  - 依赖shallowequal、lodash.debounce
  - We've poured our soul into ReactDataGrid and built it from scratch with React
  - Community Edition
    - sort,filter,pagination,edit inline,row selection
    - colspan,context menu,remote data source,column resize/reorder
  - Enterprise Edition
    - group,pivot,master/detail,tree-grid
    - locked column,row resize/reorder,footer

- https://github.com/softindex/uikernel /ts
  - React.js UI library for building forms, editable grids and reports with drilldowns and filters, based on simple unified record model with client-side and server-side validations and data bindings.

- https://github.com/The-Data-Grid/The-Data-Grid
  - https://www.thedatagrid.org/
  - database creation, data collection, and data management platform for environmental auditing.
# editable
- https://github.com/OvidijusParsiunas/active-table /ts
  - https://activetable.io/
  - Framework agnostic table component for editable data experience.
  - 依赖lit
  - customizable web component built with a focus on delivering the best editable table experience
  - Import/Export/Paste/Drag&Drop csv, xls, xlsx, ods, txt files
# async/concurrency/worker
- https://github.com/Magnithor/CanvasTable /202201/ts/inactive
  - https://magni.strumpur.net/CanvasTable/
  - Typescript library who draws a table on canvas
  - If you like to use offscreenCanvas and/or keep the data in webworker then you use mthb-offscreen-canvas-table on main javascript and mthb-offscreen-canvas-table-worker in weworker they will work to geather

- https://github.com/finos/regular-table /202303/js/NoDeps
  - regular-table exports a custom element named `<regular-table>`, which renders a regular HTML `<table>` to a sticky position within a scrollable viewport. 
  - Only visible cells are rendered and queried from a natively async virtual data model, making regular-table ideal for enormous or remote data sets
  - Use it to build Data Grids, Spreadsheets, Pivot Tables, File Trees
  - Virtual Data Model
    - a simple data model, a two dimensional Array
    - even for very small data sets, regular-table won't read your entire dataset at once. 
    - Instead, we'll need to write a simple virtual data model to access DATA and COLUMN_NAMES indirectly
    - With an async data model, it's easy to serve getDataSlice() remotely from node.js or re-implement the JSON response protocol in any language. 
  - Because of the structure of the HTML `<table>` element,  `<td>` elements must be aligned with their respective row/column, which causes default `<regular-table>` to only be able to scroll in increments of a cell, which can be irregular when column data is of different lengths. 
  - regular-table is natively compatible with `perspective`, a WebAssembly streaming visualization engine. 
    - https://github.com/finos/perspective

- https://github.com/blackfisk-tech/vstx-data-table /201904/vue/inactive
  - A data table component for the Vue Stacks Ecosystem
  - VSTX Data Table is a powerful data grid component plugin (Vue.js 2.4+) for displaying, sorting, searching, filtering, and interacting with large and deeply nested data set
  - (Optional) Web Worker support for Filtering, Sorting, and Slicing data
# div-react
- react-data-table-component /1.2kStar/Apache2/202112/ts
  - https://github.com/jbetancur/react-data-table-component
  - https://jbetancur.github.io/react-data-table-component
  - 基于div和flexbox实现
  - 依赖styled-components
  - table library with built in sorting, pagination, selection, expandable rows and customizable styling.
  - If you want to achieve balance with the force and want a simple but flexible table library give React Data Table Component a chance.
  - If you require an Excel clone or heavy "enterprise" capabilities, then this is not the React table library you are looking for
- react-advanced-table
  - https://github.com/ThaddeusJiang/react-advanced-table
  - http://react-advanced-table.vercel.app/
  - React Advanced Table
- fixed-data-table-2 /BSD/1kStar/202111/js
  - https://github.com/schrodinger/fixed-data-table-2
  - http://schrodinger.github.io/fixed-data-table-2/
  - React table component designed to allow presenting millions of rows of data.
  - https://github.com/facebook/fixed-data-table
    - /4.3kStar/archived
- react-spreadsheet-grid /MIT/949Star/202101/js/inactive
  - https://github.com/denisraslov/react-spreadsheet-grid
  - https://denisraslov.github.io/grid
  - An Excel-like grid component for React with custom cell editors, performant scroll & resizable columns
  - 功能较少
- react-table-library /51Star/MIT/202202/js
  - https://github.com/table-library/react-table-library
  - yet another table library for React
  - 依赖styled-components
  - 提供了多个主题 material-ui、semantic、bootstrap、antd
- react-bolivianite-grid /MIT/85Star/201905/inactive
  - https://github.com/papasnippy/react-bolivianite-grid
  - https://papasnippy.github.io/react-bolivianite-grid/
  - 基于div实现，每行对应的dom元素不存在
  - React grid component for virtualized rendering large tabular data.
- reactgrid /MIT/229Star/202202/ts
  - https://github.com/silevis/reactgrid
  - https://reactgrid.com/
  - 基于div实现
  - Add spreadsheet-like behavior to your React app
  - ReactGrid is available in two versions, MIT (this package) which serve the full interface but is limited in functionality and PRO which is fully functional version.
  - ReactGrid is NOT
    - Record-based data table(like ag-grid, handsontable)
    - Spreadsheet with formulas(like Telerik Kendo UI DataTable, dhtmlxSpreadsheet)
- react-datagrid2 /MIT/20Star/201903/js
  - https://github.com/stevelacy/react-datagrid2
  - https://stevelacy.github.io/react-datagrid2/
  - 基于div实现，样式太简单
  - DataGrid for React. a fork of zippyui
- react-tablize /7Star/MIT/202007/ts
  - https://github.com/alonrbar/react-tablize
  - 基于div和flexbox实现
  - 依赖@emotion/styled、react-custom-scrollbars、react-virtualized-auto-sizer
  - High performance virtual table and grid components for React.
- https://github.com/benox3/react-data-scroller
  - /13Star/MIT/202003/ts
  - 基于div和flexbox实现，大部分功能未完成
  - react-data-scroller was originally designed as a drop in replacement for react-virtualized but focused on preventing the constant mounting, unmounting and repainting of entire rows that occurs.
  - The focus is rendering your data in the most efficient way which involves only rerendering (no unmounts/mounts and only minimal repainting) of the rows and shifting the data around.
- react-absolute-grid /MIT/906Star/202002/layout
  - https://github.com/jrowny/react-absolute-grid
  - http://jrowny.github.io/react-absolute-grid/demo
  - 多用于布局，不用于数据操作，按字段过滤未实现
  - An absolutely positioned, animated, filterable, sortable, drag and droppable, ES6 grid for React.
  - The idea behind AbsoluteGrid is high performance.
    - This is achieved by using `translate3d` to position each item in the layout.
    - Items are never removed from the DOM, instead they are hidden.
- react-list /MIT/1.8kStar/202009/layout
  - https://github.com/caseywebdev/react-list
  - https://ca.sey.me/react-list/
  - 基于div实现，样式太陈旧
  - 多用于布局
  - A versatile infinite scroll React component.
- expandable-grid /1Star/MIT/202009/ts/layout
  - https://github.com/MiDovaah/expandable-grid
  - https://codesandbox.io/s/expandable-grid-cw8zx
  - 自身依赖react hooks，示例依赖@reduxjs/toolkit、react-router、material-ui，示例效果好
  - 多用于布局
  - This component is for building grid where elements can be expanded and collapsed.
  - It's just like accordion. And if you set up this grid one column you get same accordion effect.

- functional-data-grid /MIT/120Star/201907/ts/react-comp
  - https://github.com/energydrink9/functional-data-grid
  - https://energydrink9.github.io/functional-data-grid-examples
  - 依赖react-virtualized、emotion、immutable.v3
  - 基于div实现，每行对应的dom元素存在，样式太陈旧
  - Data grids in functional style with ReactJS
  - made with React-Virtualized for creating data grids with filtering, sorting, grouping and aggregates computation.
  - written in functional programming style with ES2016 and Flow.
- https://github.com/flexicious/react-datagrid
  - /8kStar/MIT/201810/js
  - Powerful DataGrid/DataTable/Tree Table component for React
- smart-grid /3Star/NALic/202006/ts/NoDeps
  - https://github.com/mukuljainx/smart-grid
  - https://mukuljainx.github.io/smart-grid/
  - highly customizable with css.
  - 基于div实现，无依赖，功能较少
- https://github.com/underfisk/apollo-spreadsheet
  - https://xenodochial-brahmagupta-15bc2b.netlify.app/
  - 基于div实现
  - Apollo spreadsheet that supports table and grids out of the box
  - uses Material-UI, React hooks, styled-components and it's fully written in Typescript
- https://github.com/developit/preact-virtual-list
  - https://jsfiddle.net/developit/qqan9pdo/
  - Virtual List that only renders visible items. Supports millions of rows.
  - 单文件，代码过于简单

- https://github.com/walkframe/gridsheet
  - https://docs.walkframe.com/products/gridsheet/examples/
  - Spreadsheet component for React

- https://github.com/andrglo/react-window-grid /js
  - A react grid with synced column and row headers based on react-window

## div-more

- SlickGrid /MIT/1.3kStar/202007/js/jquery
  - https://github.com/6pac/SlickGrid
  - http://6pac.github.io/SlickGrid/examples/example4-model.html
  - 基于div实现，每行对应的dom元素存在
  - a JS client-side grid control, based on jQuery and jQueryUI and compatible with Bootstrap.
  - SlickGrid 4.x drops jQuery requirement
  - https://github.com/mleibman/SlickGrid
    - /archived/6.7kStar
- revogrid /MIT/58Star/202010/ts/web-comp/stencil
  - https://github.com/revolist/revogrid
  - https://revolist.github.io/revogrid
  - https://github.com/revolist/revogrid-react
  - 基于div实现
  - Powerful data grid component built on top of StencilJS.
  - Millions of cells virtual viewport scroll with a powerful core is in-build by default.
- recline /2kStar/MIT/202008/js
  - https://github.com/datopian/recline
  - https://github.com/datopian/portaljs
  - https://datopian.github.io/recline/demos/
  - 2020: A framework for building data driven applications in React.
  - 2014: A simple, powerful library for building data applications in pure Javascript and HTML
- zinggrid /38Star/Free4NonCommercial/202008/js/web-comp
  - https://github.com/ZingGrid/zinggrid
  - Our main focus is on fast, responsive, and customizable grids utilizing ES6 and native web components.
  - Our goal is to solve the problem of creating a CRUD grid in under five minutes.
# list-grid-with-canvas
- Luckysheet /4.5kStar/MIT/202202/js/vanillajs
  - https://github.com/mengshukeji/Luckysheet
  - https://github.com/dream-num/univer
  - https://mengshukeji.github.io/LuckysheetDemo/
  - an online spreadsheet like excel
  - 基于canvas实现
  - 依赖jspdf
  - forks
    - https://github.com/carl-jin/RichSpreadsheet
    - https://github.com/fromatlantis/Luckysheet
    - https://github.com/titanDevelopers/Luckysheet
- https://gitee.com/zhouweng/mini_sheet /js
  - 我花了两周时间，通读了LuckySheet的源码，并且裁剪出了可执行的最小项目MiniSheet
  - [MiniSheet目录_舟翁的博客](https://blog.csdn.net/u010593516/article/details/113743472)

- fortune-sheet /1.4kStar/MIT/202208/ts
  - https://github.com/ruilisi/fortune-sheet
  - https://ruilisi.github.io/fortune-sheet-docs/zh/guide/
  - https://ruilisi.github.io/fortune-sheet-demo
  - FortuneSheet是一款开箱即用的类似Excel和Google Sheets的javascript表格组件。
  - 本项目源于 Luckysheet，并继承了它的很多代码。我们为将其转换为typescript做了很多努力，并且解决了一些原项目设计层面的问题。
  - 完全使用typescript编写。
  - 去掉了 jQuery 的依赖, 用React/Vue + immer来管理DOM和状态。
    - 架构分为 core+react
  - 同页面支持多个实例。目前只支持单个实例，因为有全局状态
  - 避免在window对象上存储数据。
  - 用一个forked handsontable/formula-parser 来处理公式计算。
  - A working example with Express (backend server) and MongoDB (data persistence) is available in backend-demo folder.

- x-sheet /50Star/MPL/202209/js/vanillajs/luckysheet开发者
  - https://github.com/eiji-th/x-sheet
  - https://gitee.com/eigi/x-sheet
  - 高性能 web javaScript 电子表格
  - 依赖exceljs

- x-spreadsheet/wolf-table /10.1kStar/MIT/202112/ts
  - https://github.com/wolf-table/table /ts
  - https://github.com/wolf-table/table-renderer
  - A web-based JavaScript（canvas） spreadsheet
  - Undo & Redo
  - https://github.com/myliang/x-spreadsheet /js
    - https://myliang.github.io/x-spreadsheet
    - [类似石墨文档多人编辑同一个文档是否可以锁定某个区域单元格](https://github.com/myliang/x-spreadsheet/issues/121)
      - 表格对于协同编辑没有什么意义，暂时不会考虑类似功能
    - [Load Json Data Or Excel Data](https://github.com/myliang/x-spreadsheet/issues/55)

- o-spreadsheet /130Star/LGPLv3/202305/ts
  - https://github.com/odoo/o-spreadsheet
  - https://odoo.github.io/o-spreadsheet/
  - A standalone spreadsheet for the web, easily integrable and extendable.
  - 支持公式
  - 依赖bootstrap5、@odoo/owl
  - 图标基于chart.js.v2
  - Real time collaboration
    - The solution we implement is based on Operation Transform (OT).
    - concurrent undo/redo are allowed
    - This solution has a lot of pros, but also some cons:
    - We need to write a transformation function for each command we create
    - Undo/Redo is synchronous, i.e. it should be accepted by the server before being executed locally.
  - [[WIP] Version history](https://github.com/odoo/o-spreadsheet/pull/2259)
    - I'd keep the concepts of tree and branches hidden. They really are internal implementation details of the data structure.
  - https://github.com/odoo/owl /ts/NoDeps
    - A web framework for structured, dynamic and maintainable applications
    - 初始化前，需要先从服务器fetch界面ui相关的xml模版文件
    - 视图层使用xml模版，组件与视图耦合，react也这样
    - Model is the owner of the state of the Spreadsheet
      - it defers the actual state manipulation work to plugins.
      - State changes are then performed through commands.  Commands are dispatched to the model
      - Model can be used in a standalone way to manipulate programmatically a spreadsheet
    - Class based components with hooks, reactive state and concurrent mode
    - a fine grained reactivity system similar to Vue
    - Owl components are defined with ES6 classes and xml templates, uses an underlying virtual DOM, integrates beautifully with hooks, and the rendering is asynchronous.

- glide-data-grid /836Star/MIT/202202/ts
  - https://github.com/glideapps/glide-data-grid
  - https://grid.glideapps.com/
  - https://glideapps.github.io/glide-data-grid
  - high-performance React grid component, with rich rendering
  - core依赖react、marked、canvas-hypertxt
  - features
    - 支持undo/redo
    - 未实现group
    - scales to millions of rows. Cells are rendered lazily on demand for memory efficiency.
    - Supports multiple types of cells. Numbers, text, markdown, bubble, image, drilldown, uri
    - Editing is built in.
    - Resizable and movable columns.
  - [I wrote an HTML canvas data grid (for Glide) so you don’t have to_202209](https://itnext.io/i-wrote-an-html-canvas-data-grid-so-you-dont-have-to-d945aa4780b4)
  - Canvas based data editor supporting millions of rows, rapid updating, and fully native scrolling.
  - the open-source data grid powering @glideapps, as the basis for the Glide Data Editor.

- treb /4Star/LGPLv3/202305/ts/NoDeps
  - https://github.com/trebco/treb
  - https://treb.app/
  - TREB is a library for adding fully interactive spreadsheets to any web page, web app or blog with just a few lines of code.
  - 支持公式
  - 支持undo，暂未实现redo

- simple-sheet /89Star/MIT/202208/ts
  - https://github.com/lvming6816077/simple-sheet
  - https://www.nihaoshijie.com.cn/mypro/simple-sheet/index.html
  - 高性能（使用canvas进行渲染）
  - 依赖react-knova、mobx-react-lite、react-viewer
  - 支持行、列宽度高度、自动筛选视图、单元格样式和格式设置等
  - [【simple-sheet】前u n do端在线Sheet文档技术解析](https://zhuanlan.zhihu.com/p/547293952)

- json5-sheet-editor /10Star/MIT/202208/js
  - https://github.com/smalllong/json5-sheet-editor
  - https://smalllong.github.io/json5-sheet-editor/
  - A simple and high efficient JSON5 based spreadsheet editor
  - 依赖自研lightue、json5

- cheetah-grid /1.3kStar/MIT/202304/ts/NoDeps/vanillajs
  - https://github.com/future-architect/cheetah-grid
  - https://future-architect.github.io/cheetah-grid/documents/introduction/
  - Cheetah Grid is a high performance JavaScript data table component that works on canvas
  - 只能选择表格最外层容器div元素，canvas元素无法直接通过拾取工具选中

- canvas-datagrid /BSD/636Star/202202/js/支持vanillajs和web-comp
  - https://github.com/TonyGermaneri/canvas-datagrid
  - https://tonygermaneri.github.io/canvas-datagrid/tutorials/demo.html
  - Canvas based data grid web component.
  - Capable of displaying millions of contiguous hierarchical rows and columns without paging or loading, on a single canvas element.

- rowsncolumns-grid /MIT/29Star/202105/ts/inactive
  - https://github.com/rowsncolumns/grid
  - https://rowsncolumns.app/
  - Declarative Canvas Grid.
  - 依赖react-konva、scroller
  - SpreadSheet - Commercially available Excel-like Grid
  - Exporter - Excel Export plugin

- https://github.com/ericdrowell/PowerGrid /inactive
  - blazing fast performance and massive scale (100M cells+) via virtualized viewport

- https://github.com/linhuiw/canvas-excel
  - https://linhuiw.github.io/canvas-excel/
  - online excel built with canvas
  - 半成品玩具

- https://github.com/nusr/excel /MIT/ts/NoDeps
  - https://nusr.github.io/excel/
  - Online Excel

- https://github.com/ykg3211/KGSheet /ts/wip
  - http://ykgykg.fun/
  - 一个开源的 Canvas 绘制的高性能 Sheet 组件

- OpenWebSheet /MIT/14Star/202003/ts/vue/inactive
  - https://github.com/SiamandMaroufi/OpenWebSheet
  - https://siamandmaroufi.github.io/OpenWebSheet/
  - OpenSource Web based spreadsheet
  - 基于canvas实现，依赖vue

- https://github.com/farseerdev/sheet-happens /ts/react
  - https://farseerdev.github.io/sheet-happens/
  - Canvas-based spreadsheet component for React.

- react-ws-canvas /MIT/1Star/202005/ts
  - https://github.com/devel0/react-ws-canvas
  - https://codesandbox.io/s/github/devel0/react-ws-canvas/tree/master/example
  - Spreadsheet like react canvas datagrid optimized for performance
- canvas-table /12Star/MIT/202009/ts
  - https://github.com/el/canvas-table
  - https://codesandbox.io/s/canvas-table-6q65o?fontsize=14&hidenavigation=1
  - fast table implementation in Canvas with string truncating support.
  - Supports both browser HTML5 canvas and node-canvas
- https://github.com/bojue/canvas-excel
  - 基于Canvas开发Excel的技术预研项目
- https://github.com/Harlock123/LCTDataGrid
  - keep the Canvas object as small as possible by only rendering the visible parts of the resulting Grid
# list-grid-with-svg
- svgtable /10Star/NALic/202105/js/d3
  - https://github.com/analyzer2004/svgtable
  - https://observablehq.com/@analyzer2004/svgtable
  - An SVG Table with sticky rows, columns and many other features.
# list-grid-with-table-tr-td
- handsontable 6.2.2 /MIT/13.8kStar/202007/js
  - https://github.com/handsontable/handsontable
  - https://handsontable.com/
  - 基于table标签实现
  - 依赖numbro, moment, pikaday
  - a JS HTML5 data grid with spreadsheet look & feel.
  - free for all non-commercial purposes since 7.0
  - 不支持协作
  - [Q: Possible to combine multiple actions into single undo/redo step?](https://github.com/handsontable/handsontable/issues/7324)
  - https://github.com/handsontable/handsontable/releases/tag/7.0.0
  - [Handsontable drops open source for a non-commercial license_201903](https://github.com/handsontable/handsontable/issues/5831)
  - forks
    - https://github.com/swsvindland/opentable /inactive
    - https://github.com/pingyuanChen/handsontable /inactive

- gridjs /MIT/3.3kStar/202202/ts
  - https://github.com/grid-js/gridjs
  - https://gridjs.io/
  - 基于display-table实现，使用class类风格
  - 依赖preact，但只作为视图层
  - HTML table plugin written in TypeScript using vanilla js
  - Grid.js can be used with any JavaScript frameworks (React, Angular, Preact or VanillaJS)

- jexcel /MIT/4.8kStar/202007/js
  - https://github.com/paulhodel/jexcel
  - https://bossanova.uk/jexcel
  - 基于table标签实现
  - a lightweight vanilla js plugin to create web-based interactive tables
- https://github.com/sorryljt/react-jexcel
  - 基于jspreadsheet v4版本，封装的React 版本的轻量级Excel插件
- https://github.com/jspreadsheet/ce /MIT/js
  - https://bossanova.uk/jspreadsheet/v4
  - Vanilla JavaScript data grid plugin to create amazing web-based interactive HTML tables, and spreadsheets compatible data grid with other spreadsheet software

- regular-table /233Star/Apache2/202203/js/NoDeps
  - https://github.com/jpmorganchase/regular-table
  - A Javascript library for the browser, regular-table exports a custom element named `<regular-table>`, which renders a regular HTML `<table>` to a sticky position within a scrollable viewport.
  - Only visible cells are rendered and queried from a natively async virtual data model, making regular-table ideal for enormous or remote data sets.
  - Small bundle size, no dependencies.

- Simple-DataTables /1.1kStar/LGPLv3/202304/ts
  - https://github.com/fiduswriter/Simple-DataTables
  - https://fiduswriter.github.io/Simple-DataTables/
  - A extendable, dependency-free javascript HTML table plugin.
  - Similar to jQuery DataTables, but without the jQuery dependency.
  - Based on Vanilla-DataTables, but written in ES2018.
  - https://github.com/Mobius1/Vanilla-DataTables
    - /MIT/inactive

- FathGrid /12Star/MIT/202011/js/NoDeps
  - https://github.com/admirhodzic/FathGrid
  - 源码是传统的单文件
  - frontend data table/grid with paging, sorting, filtering, grouping, sub-grids, exporting and editing.
  - Can be used with any framework.

- list.js /9.8kStar/MIT/201912/js/inactive
  - https://github.com/javve/list.js
  - https://codepen.io/javve/pen/cLdfw
  - adding search, sort, filters and flexibility to tables, lists and various HTML elements.
  - Built to be invisible and work on existing HTML.

- CSS responsive table
  - https://codepen.io/scottjehl/pen/abJrPOP
  - A CSS-only responsive table with fixed column & row headers, inside a layout, with scroll snapping!

- https://github.com/lebonnet/bomtable /js
  - https://lebonnet.github.io/
  - web table like simple excel

## table-tr-td-react

- react-datasheet /MIT/4.2kStar/202108/NoDeps
  - https://github.com/nadbm/react-datasheet
  - https://nadbm.github.io/react-datasheet/
  - Excel-like data grid (table) component for React
  - 基于table标签实现，样式太简单
- https://github.com/komarovalexander/ka-table
  - /58Star/MIT/202010/ts/inactive
  - http://ka-table.com/
  - 基于table标签实现
  - Controllable React Table component with Sorting, Filtering, Grouping, Virtualization, Editing and many more

- rc-table /MIT/693star/202010/ts
  - https://github.com/react-component/table
  - http://react-component.github.io/table/
  - 基于table标签实现
  - 依赖react，rc-util，rc-resize-observer，shallowequal
- window-table /MIT/143Star/202009/ts
  - https://github.com/pupudu/window-table
  - https://window-table.netlify.com/
  - This is a implementation of a virtualized table, based off react-window.
  - Render thousands of rows in a HTML table in React
- React-Spreadsheet-Component /MIT/650Star/201811
  - https://github.com/felixrieseberg/React-Spreadsheet-Component
  - http://felixrieseberg.github.io/React-Spreadsheet-Component/
  - 基于table标签实现，功能较少，支持编辑
  - 依赖jquery、mousetrap
  - Spreadsheet Component for ReactJS
  - It's made with ❤️️ by Microsoft DX
- react-data-components /MIT/382Star/201707/js/inactive
  - https://github.com/carlosrocha/react-data-components
  - https://rocha.dev/react-data-components/
  - React components for sorting, filtering and pagination of data.
- react-smart-data-table /MIT/46Star/202006
  - https://github.com/joaocarmo/react-smart-data-table
  - https://joaocarmo.com/react-smart-data-table/examples/bootstrap/
  - 功能较少，样式太简单
  - A smart data table component for React.js meant to be configuration free
  - https://github.com/joaocarmo/react-very-simple-data-table
- material-table /3.4kStar/MIT/202203/js
  - https://github.com/mbrn/material-table
  - https://material-table.com/
  - powerful Datatable for React based on Material-UI Table with some additional features.
  - 依赖 mui5、react-beautiful-dnd、jspdf、date-fns

- Griddle /MIT/2400star/201907/js/inactive
  - http://github.com/griddlegriddle/Griddle
  - http://griddlegriddle.github.io/Griddle/
  - 依赖react，lodash，redux，reselect，recompose
  - Griddle now has a customizable architecture that allows for one-off customizations or reusable plugins.
  - These customization options allow for overriding everything from components, to internal datagrid state management, and more
  - [Architecture](http://griddlegriddle.github.io/Griddle/docs/architecture/)
  - [Plugins](http://griddlegriddle.github.io/Griddle/docs/plugins/)
  - [Customization](http://griddlegriddle.github.io/Griddle/docs/customization/)

- sou-react-table /MIT/184Star/201812/js
  - https://github.com/miadwang/sou-react-table
  - https://miadwang.github.io/sou-react-table/
  - A spreadsheet component for React

- reactabular /MIT/895star/202001/js/NoDeps
  - https://github.com/reactabular/reactabular
  - https://reactabular.js.org/#/examples/all-features
  - 基于table标签实现，提供了扩展包sticky、virtualized、dnd、resizable

- https://github.com/axisj/axframe-datagrid
  - https://axframe-datagrid.vercel.app/
  - DataSheet for React

- axui-datagrid /MIT/122Star/201912
  - https://github.com/jsdevkr/axui-datagrid
  - https://axui-datagrid.jsdev.kr/introduction
  - 基于table标签实现
  - DataGrid, DataSheet for React
- https://github.com/erfangc/GigaGrid
  - /30Star/MIT/201703/ts
  - http://erfangc.github.io/GigaGrid/
  - React.js table widget with Subtotals (Written in TypeScript)
- reactable /MIT/1.5kStar/201611
  - https://github.com/glittershark/reactable
  - http://glittershark.github.io/reactable/
  - 依赖react, table, data-tables
- https://github.com/bencripps/react-redux-grid
  - /453Star/MIT/202007
  - http://react-redux-grid.herokuapp.com/
  - 依赖react-redux
  - A Grid and Tree Component written in React using the Redux Pattern
- https://github.com/nowaalex/af-virtual-scroll
  - React components for rendering large scrollable data
- https://github.com/qimus/semantic-ui-grid
  - Extended grid for data
- https://github.com/GigaTables/reactables
  - a ReactJS plug-in to help web-developers process table-data

## table-tr-td-more

- DataTables /MIT/6.6kStar/202005
  - https://github.com/DataTables/DataTablesSrc
  - https://github.com/DataTables/DataTables
  - http://www.datatables.net/
  - 基于table标签实现
  - 依赖jquery
  - datable enhancing plug-in for jQuery

- bootstrap-table /10.5kStar/MIT/202010
  - https://github.com/wenzhixin/bootstrap-table
  - https://examples.bootstrap-table.com/
  - 基于table标签实现
  - An extended Bootstrap table with radio, checkbox, sort, pagination, extensions and other added features.
  - Created for Twitter Bootstrap (All versions supported)
  - integration with some of the most widely used CSS frameworks. (Supports Semantic UI, Bulma, Material Design, Foundation, Vue.js)
- ej2-grids /BuyLic/39Star/201810
  - https://github.com/syncfusion/ej2-grids
  - https://www.syncfusion.com/javascript-ui-controls
  - 基于table标签实现
  - Feature-rich grid control with built-in support for data binding, filtering
  - free for gross revenue of less than one million
- sensei-grid /807Star/MIT/201711/js
  - https://github.com/datazenit/sensei-grid
  - https://datazenit.com/static/sensei-grid/examples/index.html
  - 基于table标签实现
  - 依赖jQuery、underscore.js/lodash
  - Simple data grid library written in JavaScript
- WickedGrid /MIT/570Star/201611
  - https://github.com/Spreadsheets/WickedGrid
  - http://spreadsheets.github.io/WickedGrid/
  - 基于table标签实现
  - 依赖jquery
- vaadin-grid /374Star/Apache2/202010/web-comp
  - https://github.com/vaadin/vaadin-grid
  - https://vaadin.com/components/vaadin-grid/java-examples
  - 基于table标签实现，源码全在html文件中
  - 依赖polymer2、vaadin-text-field、vaadin-themable-mixin
  - a free data grid/data table Web Component
- https://github.com/vaadin/spreadsheet
  - /44Star/CVALv3/202003/java
  - https://demo.vaadin.com/spreadsheet/
  - 基于div实现
  - a UI component add-on for Vaadin 7 which provides means to view and edit Excel spreadsheets in Vaadin applications.
- https://github.com/renanlecaro/importabular
  - https://renanlecaro.github.io/importabular/
  - 功能较少
  - Minimal spreadsheet javascript component
- backgrid /2kStar/MIT/201702/js/backbone
  - https://github.com/cloudflarearchive/backgrid
  - an easily stylable semantic HTML data grid
  - 依赖Backbone.js
- dgrid /627Star/BSD/202009/js/dojo
  - https://github.com/SitePen/dgrid
  - https://dgrid.io
  - 每行都有一个table标签，样式太陈旧
  - mobile-ready, data-driven, modular grid widget designed for use with dstore
  - Dojo core is the only hard dependency for dgrid
  - dstore >= 1.0.3 or 1.1.1, for store-backed grids
- GridManager /551Star/MIT/202010/js
  - https://github.com/baukh789/GridManager
  - https://gridmanager.lovejavascript.com/
  - 快速、灵活的对Table标签进行实例化，让Table标签充满活力
  - 支持常见功能，还提供了如: 导出、打印、列配置、右键菜单、行列移动、用户偏好记忆等功能。
  - 支持在原生JS、jQuery、Angular 1.x、Vue、React环境下使用
- ornamentum /140Star/MIT/202001/ts/angular
  - https://github.com/yohangz/ornamentum
  - https://ornamentum.app/
  - 基于table标签实现
  - a highly configurable, UI framework agnostic, fully responsive Angular data table with no external dependencies.
- https://github.com/filamentgroup/tablesaw
  - A group of plugins for responsive tables.
- https://github.com/juijs/jui-grid
  - http://uiplay.jui.io/?p=xtable_1
  - 基于table标签实现
  - JUI grid can handle millions of data, and can display data in a hierarchical structure
- https://github.com/NeXTs/Clusterize.js
  - /6.8kStar/GPLv3/201901/js
  - Tiny vanilla JS plugin to display large data sets easily
  - 支持table标签、li标签
- https://github.com/vitmalina/w2ui
  - /1.8kStar/MIT/202009/js
  - UI widgets for modern apps. Data table, forms, toolbars, sidebar, tabs, tooltips, popups. All under 120kb (gzipped).
  -  It aims to let you define your UI in a declarative way via JSON data structures.
  - 依赖jquery
- https://github.com/webismymind/editablegrid
  - /765Star/MIT/201811/js
  - aimed at turning HTML tables into advanced editable components
- https://github.com/tim-band/js-dataentrygrid
  - Featherweight Excel-like grid for data entry
# excel
- https://github.com/handsontable/formula.js /MIT/js
  - JavaScript implementation of most Microsoft Excel formula functions
  - forks
  - https://github.com/jspreadsheet/formulajs
  - https://github.com/formulajs/formulajs

- https://github.com/wx-chevalier/excel.ts /ts
  - excel.ts 是基于 TypeScript 编写的前端 Excel 综合解决方案，包含了 POJO Schema 定义、多框架支持的 Web 端渲染以及 Node 导出服务

- https://github.com/barisates/react-data-table-component-extensions /js
  - Export table data as a CSV or Excel file, filter and print the data.

- jsreport /1.1kStar/LGPLv3/202305/js
  - https://github.com/jsreport/jsreport
  - https://jsreport.net/
  - jsreport is a reporting server letting developers define reports using javascript templating engines like handlebars. 
  - It supports various report output formats like html, pdf, excel, docx, and others. 
  - It also includes advanced reporting features like user management, REST API, scheduling, designer, or sending emails.

- https://github.com/forensic-architecture/datasheet-server /js
  - Turn spreadsheet data into a structured, dynamic API.
  - Extensible architecture. Currently supports Google Sheet as a source and a REST-like query language, but structured modularly with an intention to support other sources and query languages.

- https://github.com/ExcQL/ExcQL /js
  - A web application transforming excel spreadsheets into SQL scripts

- https://github.com/jupemara/spreadsheet-sql /ts
  - Getting Google spreadsheet data by using like SQL.

- https://github.com/Roffelchen/spreadsheet-crdt
  - npx y-websocket-server

- https://github.com/handsontable/spreadsheet-viewer /NonOpen
  - A 30-day trial license is available
# css-table/grid
- https://github.com/coston/react-super-responsive-table
  - https://react-super-responsive-table.netlify.app/
  - converts your table data to a user-friendly list in mobile view.
# more
- https://github.com/flexmonster/flexmonster-mongodb-connector
  - Flexmonster Pivot is a powerful JavaScript tool for interactive web reporting. 
  - It allows you to visualize and analyze data from JSON, CSV, SQL, NoSQL, Elasticsearch, and OLAP data sources quickly and conveniently.

- https://github.com/cidgoh/DataHarmonizer
  - A standardized browser-based spreadsheet editor and validator that can be run offline and locally

- https://github.com/eclipse/streamsheets /js
  - An open-source tool for processing stream data using a spreadsheet-like interface.

- https://github.com/rankingdigitalrights/datalab
  - Spreadsheet Engineering

- https://github.com/activewidgets/js /js
  - ActiveWidgets is a multi-framework UI component library. 
  - This package provides datagrid component for javascript / no-framework environments.

- https://github.com/jamerst/o-data-grid
  - A React Data Grid and Query Builder for OData APIs. Based on the Material-UI DataGrid/DataGridPro.
  - an extension to the MUI DataGrid React component which implements features such as sorting, pagination, column selection, and filtering using the OData Standard. 
  - It also utilises Recoil for state management in the filter builder

- https://github.com/antvis/data-set
  - state driven all in one data process for data visualization

- https://github.com/amurgola/OpenGridJs /js/wip
  - lightweight JavaScript grid framework that allows you to create fast and easy-to-use data grids in your web application

- https://github.com/icflorescu/mantine-datatable
  - https://icflorescu.github.io/mantine-datatable
  - A table component for your Mantine data-rich applications, supporting asynchronous data loading, column sorting, custom cell data rendering, row context menus, dark theme, and more
