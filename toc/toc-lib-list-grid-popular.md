---
title: toc-lib-list-grid-popular
tags: [grid, lib, list, toc]
created: '2020-10-22T06:47:15.435Z'
modified: '2020-10-22T06:49:10.760Z'
---

# toc-lib-list-grid-popular

# focus

- src-react-list-grid-ts
  - **react-data-grid**
  - react-tiny-virtual-list

- src-list-grid-ts
  - **ag-grid**

- src-react-list-grid-es6
  - **react-table**
  - **react-window**
  - react-virtualized

- src-list-grid-es6
  - **tabulator**
  - frappe-datatable

- src-list-grid-canvas
  - **luckysheet**: 未使用class类，函数式风格
  - **x-spreadsheet**: class类和函数式都有
  - cheetah-grid(ts): 基于class类继承

- top-dependents-of-react-table.v7
  - 各类组件库中的table或list组件
    - @component-controls/components
    - @edx/paragon
    - guidu
- top-dependents-of-react-table.v6
  - nteract/data-explorer: 依赖d3、numeral
# list-grid-with-div
- ag-grid /MIT/6.4kStar/202006/ts/NoDeps
  - https://github.com/ag-grid/ag-grid
  - https://www.ag-grid.com/example.php
  - 基于div实现，每行对应的dom元素存在
  - a fully-featured and highly customizable JavaScript data grid
    - has no 3rd party dependencies 
    - integrates smoothly with all major JavaScript frameworks
  - ag-grid-enterprise is Commercial licensed but opensourced
- react-data-grid /MIT/4kStar/202007/ts
  - https://github.com/adazzle/react-data-grid
  - https://adazzle.github.io/react-data-grid/canary/
  - 基于div实现，每行对应的dom元素存在，未实现row/column span(merging cells)
  - 项目模块化，分为core和addons
  - Excel-like grid component built with React, with editors, keyboard navigation, copy...
- react-tiny-virtual-list /MIT/1.8kStar/201910/ts
  - https://github.com/clauderic/react-tiny-virtual-list/
  - https://clauderic.github.io/react-tiny-virtual-list/
  - A tiny but mighty 3kb list virtualization library, with zero dependencies
  - Supports variable heights/widths, sticky items, scrolling to index, and more
- tabulator /MIT/3.4kStar/202007/js/NoDeps
  - https://github.com/olifolkerd/tabulator
  - http://tabulator.info/
  - https://github.com/ngduc/react-tabulator
    - a JS table library with many advanced features based on tabulator
  - 基于div实现，每行对应的dom元素存在，未实现column span
  - Interactive Tables and Data Grids for JavaScript supporting react, angular, vue
- react-table /MIT/11.6kStar/202007/js
  - https://github.com/tannerlinsley/react-table
  - https://react-table.tanstack.com/
  - Hooks for building fast and extendable tables and datagrids for React
  - React Table is a headless utility, which means it doesn't supply any actual UI elements.
  - react-virtual /MIT/1.1kStar/202007
    - https://github.com/tannerlinsley/react-virtual
    - Hooks for virtualizing scrollable elements in React
- react-virtualized /MIT/19.5kStar/202006/js
  - https://github.com/bvaughn/react-virtualized
  - http://www.reactvirtualized.com/
  - https://github.com/bvaughn/react-virtualized/blob/master/docs/Grid.md
  - 基于div实现，每行对应的dom元素不存在
  - 表格主体ReactVirtualized__Grid__innerScrollContainer内全是单元格
  - React components for efficiently rendering large lists and tabular data
- react-window /MIT/8.5kStar/202001/js
  - https://github.com/bvaughn/react-window
  - https://react-window.now.sh/
  - 基于div实现，每行对应的dom元素不存在
  - React components for efficiently rendering large lists and tabular data
  - React window works by only rendering part of a large data set(just enough to fill viewport).
- frappe-datatable /MIT/502Star/202009/js
  - https://github.com/frappe/datatable
  - https://frappe.io/datatable
  - 基于div实现，每行对应的dom元素存在
  - 依赖hyperlist、sortablejs、lodash
  - A simple, modern and interactive datatable for the web
  - https://github.com/tbranyen/hyperlist
    - /MIT/291Star/202006/js/NoDeps
    - A performant virtual scrolling list utility capable of rendering millions of rows
    - a fork of the existing (unmaintained) project: sergi/virtual-list
- FancyGrid /BuyLic/153Star/202007/js/NoDeps
  - https://github.com/FancyGrid/FancyGrid
  - https://fancygrid.com/
  - JS grid library with charts integration and server communication.
  - 基于div实现，实现很特别，表格ui是一列一列相邻放置构成的，每列对应的dom元素存在
- functional-data-grid /MIT/120Star/201907/ts/react-comp
  - https://github.com/energydrink9/functional-data-grid
  - https://energydrink9.github.io/functional-data-grid-examples
  - 基于div实现，每行对应的dom元素存在，样式太陈旧
  - 依赖react-virtualized、emotion
  - Data grids in functional style with ReactJS
  - made with React-Virtualized for creating data grids with filtering, sorting, grouping and aggregates computation.
  - written in functional programming style with ES2016 and Flow.
- react-base-table /MIT/761Star/202007/js
  - https://github.com/Autodesk/react-base-table
  - https://autodesk.github.io/react-base-table/
  - 基于div实现，每行对应的dom元素存在
  - 依赖react-window
  - A react table component to display large datasets with high performance and flexibility
  - 未实现row select(作者为组件unopinionated的目标而未合并pr)，但提供示例
- react-fluid-table /26Star/MIT/202009/ts
  - https://github.com/mckervinc/react-fluid-table
  - https://mckervinc.github.io/react-fluid-table/#/
  - 基于div实现，每行对应的dom元素存在
  - 依赖react-window
  - A windowed React table built on top of react-window
- rsuite-table /327Star/MIT/202010/ts
  - https://github.com/rsuite/rsuite-table
  - http://rsuite.github.io/rsuite-table/
  - 基于div实现
  - 依赖react、rsuite/dom-lib、element-resize-event、lodash
- react-data-browser /4Star/MIT/202001/ts/NoDeps
  - https://github.com/davidalekna/react-components/tree/master/packages/react-data-browser
  - https://codesandbox.io/s/github/davidalekna/data-browser-examples
  - 基于div和flexbox实现
  - The original use case of this component is to build flexbox tables, 
  - however the API is powerful and flexible enough to build things like grids as well.
  - DataBrowser component will not provide any styles, only the functionality.
  - use-table-tools /MIT/18Star/202009/ts/NoDeps
    - https://github.com/davidalekna/use-table-tools
    - Hooks for building kickass react table components
- https://github.com/Buuntu/react-final-table
  - https://githubbox.com/Buuntu/react-final-table/tree/master/examples/basic
  - /9Star/MIT/202009
  - A headless UI component libray for managing complex table state in React.
  - Inspired by react-table but with Typescript support built in and a simpler API.

## div-react

- reactdatagrid /25Star/MIT/202010/js
  - https://github.com/inovua/reactdatagrid
  - https://reactdatagrid.io/demo
  - 基于div实现，每行对应的dom元素存在
  - 依赖shallowequal、fast-deep-equal、lodash.debounce
  - We've poured our soul into ReactDataGrid and built it from scratch with React
  - Community Edition
    - sort,filter,pagination,edit inline,row selection
    - colspan,context menu,remote data source,column resize/reorder
  - Enterprise Edition
    - group,pivot,master/detail,tree-grid
    - locked column,row resize/reorder,footer
- fixed-data-table-2 /BSD/1kStar/202007/js
  - https://github.com/schrodinger/fixed-data-table-2
  - http://schrodinger.github.io/fixed-data-table-2/
  - React table component designed to allow presenting millions of rows of data.
  - https://github.com/facebook/fixed-data-table 
    - /4.3kStar/archived
- react-data-table-component /MIT/598Star/202007/js
  - https://github.com/jbetancur/react-data-table-component
  - https://jbetancur.github.io/react-data-table-component
  - table library with built in sorting, pagination, selection, expandable rows and customizable styling.
- react-spreadsheet-grid /MIT/949Star/202004/js/inactive
  - https://github.com/denisraslov/react-spreadsheet-grid
  - https://denisraslov.github.io/grid
  - An Excel-like grid component for React with custom cell editors, performant scroll & resizable columns
  - 功能较少
- react-table-library /51Star/MIT/202106/js
  - https://github.com/table-library/react-table-library
  - yet another table library for React
- react-bolivianite-grid /MIT/85Star/201905
  - https://github.com/papasnippy/react-bolivianite-grid
  - https://papasnippy.github.io/react-bolivianite-grid/
  - 基于div实现，每行对应的dom元素不存在
  - React grid component for virtualized rendering large tabular data.
- reactgrid /MIT/229Star/202010/ts
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
- react-virtual-grid /30Star/NALic/202005/js
  - https://github.com/fulcrumapp/react-virtual-grid
  - https://fulcrumapp.github.io/react-virtual-grid/
  - 基于div实现，特别的是，每行的源码顺序从上到下显示出来的单元格dom元素是从右到左排列
  - 依赖element-resize-detector、iscroll、react-proptypes
  - a low level component for building fast tables
- react-datasheet-grid 
  - https://github.com/Equify/react-datasheet-grid
  - more like Airtable or Notion and less like Excel in the sense that instead of dealing with individual cells it deals with entire rows, 
  - and each column is responsible for a single property of each row
- rc-virtual-list /172Star/MIT/202010/ts
  - https://github.com/react-component/virtual-list
  - https://rc-virtual-list.react-component.now.sh/
  - 依赖rc-util、rc-resize-observer
  - React Virtual List Component which worked with animation
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
- react-virtuoso /876Star/MIT/202011/ts/list
  - https://github.com/petyosi/react-virtuoso
  - virtual list component for React
  - V1 brings improvements to reverse infinite scrolling behavior - suitable for chat and feed user interfaces. 

## div-more

- SlickGrid /MIT/1.3kStar/202007/js/jquery
  - https://github.com/6pac/SlickGrid
  - http://6pac.github.io/SlickGrid/examples/example4-model.html
  - 基于div实现，每行对应的dom元素存在
  - a JS client-side grid control, based on jQuery and jQueryUI and compatible with Bootstrap.
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
  - https://datopian.github.io/recline/demos/
  - 2020: A framework for building data driven applications in React.
  - 2014: A simple, powerful library for building data applications in pure Javascript and HTML
- zinggrid /38Star/Free4NonCommercial/202008/js/web-comp
  - https://github.com/ZingGrid/zinggrid
  - Our main focus is on fast, responsive, and customizable grids utilizing ES6 and native web components. 
  - Our goal is to solve the problem of creating a CRUD grid in under five minutes. 
# list-grid-with-canvas
- Luckysheet /MIT/4.5kStar/202010/js
  - https://github.com/mengshukeji/Luckysheet
  - https://mengshukeji.github.io/LuckysheetDemo/
  - an online spreadsheet like excel
  - 基于canvas实现
  - 依赖jspdf
- x-spreadsheet /MIT/10.1kStar/202010/js
  - https://github.com/myliang/x-spreadsheet
  - https://myliang.github.io/x-spreadsheet
  - A web-based JavaScript（canvas） spreadsheet
- cheetah-grid /MIT/337Star/202007/ts 
  - https://github.com/future-architect/cheetah-grid
  - https://future-architect.github.io/cheetah-grid/documents/introduction/
  - Cheetah Grid is a high performance JavaScript data table component that works on canvas
  - 只能选择表格最外层容器div元素，canvas元素无法直接通过拾取工具选中
- canvas-datagrid /BSD/636Star/202006/js/web-comp
  - https://github.com/TonyGermaneri/canvas-datagrid
  - https://tonygermaneri.github.io/canvas-datagrid/tutorials/demo.html
  - Canvas based data grid web component. 
  - Capable of displaying millions of contiguous hierarchical rows and columns without paging or loading, on a single canvas element.
- rowsncolumns-grid /MIT/29Star/202007/ts
  - https://github.com/rowsncolumns/grid
  - https://rowsncolumns.app/
  - Declarative Canvas Grid.
  - SpreadSheet - Commercially available Excel-like Grid
  - Exporter - Excel Export plugin
- https://github.com/glideapps/glide-data-grid
  - https://grid.glideapps.com/
  - /417Star/MIT/202104/ts
  - high-performance React grid component, with rich rendering
  - the open-source data grid powering @glideapps
- https://github.com/ericdrowell/PowerGrid
  - blazing fast performance and massive scale (100M cells+) via virtualized viewport

- OpenWebSheet /MIT/14Star/202003/ts/vue
  - https://github.com/SiamandMaroufi/OpenWebSheet
  - https://siamandmaroufi.github.io/OpenWebSheet/
  - OpenSource Web based spreadsheet
  - 基于canvas实现，依赖vue
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
- https://github.com/analyzer2004/svgtable
  - https://observablehq.com/@analyzer2004/svgtable
  - /10Star/NALic/202011/js/d3
  - An SVG Table with sticky rows, columns and many other features.
# list-grid-with-table-tr-td
- handsontable 6.2.2 /MIT/13.8kStar/202007/js
  - https://github.com/handsontable/handsontable
  - https://handsontable.com/
  - 基于table标签实现
  - 依赖numbro, moment, pikaday
  - a JS HTML5 data grid with spreadsheet look & feel.
  - free for all non-commercial purposes since 7.0 
  - https://github.com/handsontable/handsontable/releases/tag/7.0.0
  - [Handsontable drops open source for a non-commercial license](https://github.com/handsontable/handsontable/issues/5831)
- tui.grid /MIT/1.5kStar/202007/ts
  - https://github.com/nhn/tui.grid
  - http://ui.toast.com/tui-grid/
  - 基于table标签实现，合并表头列实际样式为tui-grid-lside/rside-area
  - 支持sort, filter, 不支持group
  - 依赖tui-date-picker、tui-pagination
  - Powerful Component to Display and Edit Data. 
  - TOAST UI Grid is available when using the Plain JS, React, Vue Component.
- gridjs /MIT/2.4kStar/202009/ts
  - https://github.com/grid-js/gridjs
  - https://gridjs.io/
  - 基于table标签实现
  - HTML table plugin written in TypeScript using vanilla js
- jexcel /MIT/4.8kStar/202007/js
  - https://github.com/paulhodel/jexcel
  - https://bossanova.uk/jexcel
  - 基于table标签实现
  - a lightweight vanilla js plugin to create web-based interactive tables
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
## table-tr-td-react

- ali-react-table /530Star/MIT/202105/ts
  - https://github.com/alibaba/ali-react-table
  - https://ali-react-table.js.org/examples/big-data
  - 依赖rxjs、styled-components
  - 提供了很多业务场景示例的live demo，以及测试数据
  - 内置虚拟滚动，数据量较大时自动开启，实现了pivot
- react-datasheet /MIT/4.2kStar/202005/NoDeps
  - https://github.com/nadbm/react-datasheet
  - https://nadbm.github.io/react-datasheet/
  - Excel-like data grid (table) component for React
  - 基于table标签实现，样式太简单
- rc-table /MIT/693star/202010/ts
  - https://github.com/react-component/table
  - http://react-component.github.io/table/
  - 基于table标签实现
  - 依赖react，rc-util，rc-resize-observer，shallowequal 
- window-table /MIT/143Star/202007
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
- react-data-components /MIT/382Star/201905/js
  - https://github.com/carlosrocha/react-data-components
  - https://rocha.dev/react-data-components/
  - React components for sorting, filtering and pagination of data.
- react-spreadsheet /MIT/245Star/202003
  - https://github.com/iddan/react-spreadsheet
  - https://iddan.github.io/react-spreadsheet
  - Simple, customizable yet performant spreadsheet for React
- react-smart-data-table /MIT/46Star/202006
  - https://github.com/joaocarmo/react-smart-data-table
  - https://joaocarmo.com/react-smart-data-table/examples/bootstrap/
  - 功能较少，样式太简单
  - A smart data table component for React.js meant to be configuration free
  - https://github.com/joaocarmo/react-very-simple-data-table
- Griddle /MIT/2400star/201907
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
- axui-datagrid /MIT/122Star/201912
  - https://github.com/jsdevkr/axui-datagrid
  - https://axui-datagrid.jsdev.kr/introduction
  - 基于table标签实现
  - DataGrid, DataSheet for React
- https://github.com/komarovalexander/ka-table
  - /58Star/MIT/202010/ts
  - http://ka-table.com/
  - 基于table标签实现
  - Controllable React Table component with Sorting, Filtering, Grouping, Virtualization, Editing and many more
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
- Simple-DataTables /LGPLv3/315Star/202010
  - https://github.com/fiduswriter/Simple-DataTables
  - https://fiduswriter.github.io/Simple-DataTables/
  - A extendable, dependency-free javascript HTML table plugin. 
  - Similar to jQuery DataTables, but without the jQuery dependency.
  - Based on Vanilla-DataTables, but written in ES2018.
  - https://github.com/Mobius1/Vanilla-DataTables 
    - /MIT/inactive
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
  - w2ui is a JavaScript UI library for building rich data-driven web applications. 
  - 依赖jquery
- https://github.com/webismymind/editablegrid
  - /765Star/MIT/201811/js
  - aimed at turning HTML tables into advanced editable components
- https://github.com/tim-band/js-dataentrygrid
  - Featherweight Excel-like grid for data entry
