---
title: lib-excel-tanstack-table-examples-v7
tags: [examples, tanstack-table, toc]
created: 2021-07-20T12:42:45.044Z
modified: 2022-08-21T10:37:01.349Z
---

# lib-excel-tanstack-table-examples-v7

# guide

- top-dependents-of-react-table.v7
  - 各类组件库中的table或list组件
    - @component-controls/components
    - @edx/paragon
    - ref
      - https://www.npmjs.com/browse/depended/react-table
      - https://github.com/search?o=desc&q=react-table+filename%3Apackage.json&s=indexed&type=Code
- top-dependents-of-react-table.v6
  - nteract/data-explorer: 依赖d3、numeral
# popular-v7
- ui-table /25Star/MIT/202112/ts
  - https://github.com/habx/ui-table
  - https://habx.github.io/ui-table/
  - UI components for react-table based on [ui-core](https://github.com/habx/ui-core)
  - 依赖@habx/ui-core、react-table.v7、react-window、styled-components、lodash、exceljs、papaparse(csv)、react-dropzone
  - display布局: table-grid, tr-grid, td-flex
  - 例子非常多，包括 virtualized、infiniteScroll、filter、header、footer、CompareTable
  - 单元格类似包括 array、boolean、icon、image；没有dropdown
  - filter支持搜索框、滑动条、下拉菜单
  - 支持导入导出csv, xlsx
  - 缺点是不支持编辑、不支持改变列宽度

- editable-react-table /410Star/MIT/202108/js
  - https://github.com/archit-p/editable-react-table
  - https://codesandbox.io/s/editable-react-table-gchwp
  - React table built to resemble a database.
  - 依赖react-table.v7, react-window, popperjs.v2, react-contenteditable, clsx
  - display布局： table.div-block, tr.div-flex, td.div-flex
  - 支持3种单元格类型 number, text, select，弹出框很好用
  - 没有全局工具条，但表头每列的下拉菜单很完整；不支持分组
  - https://github.com/hermanbanken/editable-react-table
    - /ts
  - https://github.com/koyal-tech/editable-react-table

- react-table-ui /7Star/MIT/202107/ts
  - https://github.com/GuptaSiddhant/react-table-ui
  - https://react-table-ui.js.org/
  - https://codesandbox.io/s/react-table-ui-basic-8ukxd
  - Out-of-the-box UI for React-Table 7
  - 依赖只有react-table
  - 样式完全自己实现，样式添加基于完全自己实现的styled，useStylesheet会添加css到dom中，`document.head.insertAdjacentElement`手动插到dom头部
  - 示例类似kitchen sink，支持排序、过滤，不支持分组，每行hover时会出现悬浮操作菜单，点击有弹框
  - 有全局工具条，但没有每列工具条

- lumen-table
  - https://github.com/EQWorks/lumen-table
  - https://eqworks.github.io/lumen-table/
  - React data table component.
  - 依赖 @material-ui/core.v4、@eqworks/lumen-ui
  - display布局: table, table-row, table-cell
  - 示例比较多
  - 单元格支持可展开元素，当该元素展开时，整行会变高，示例在 render json
  - 工具条支持下拉菜单选择要显示的字段列
  - filter支持 range滑动条、按现有值、日期范围
  - ref
    - https://github.com/EQWorks/react-labs
    - https://github.com/EQWorks/lumen-ui

- @heathmont/moon-table
  - https://github.com/coingaming/moon-design
  - https://moon.io/components/table/table
  - display布局: table.div-block, tr.div-flex, td.div-block
  - 拖动表格滚动条时，可以显示minimap
  - 提供了日期字段作为一列的Calendar示例

- table-x
  - https://github.com/gmfe/gm-pc/tree/master/packages/table-x
  - https://gmfe.github.io/gm-pc-docs/?path=/story/tablex-tablex--com-table-x
  - 依赖 react-window、sortablejs、@gm-pc/react
  - 注意不要随意升级版本，目前使用 react-table.v7.0.0-rc.11
  - 7.0.0-rc.11 天然不支持 column.show, 所以自行实现了 column.show 的支持
  - 斑马线，不能用 css 的 :even 和 :odd 实现。因为在使用虚拟列表的时候有坑。

- @superset-ui/plugin-chart-table
  - https://github.com/apache/superset/tree/master/superset-frontend/plugins/plugin-chart-table
    - https://apache-superset.github.io/superset-ui/?path=/story/chart-plugins-plugin-chart-table--big-table
    - This plugin provides Table chart for Superset.
  - https://github.com/apache-superset/superset-ui
    - https://apache-superset.github.io/superset-ui/
    - packages that power the Apache Superset UI, and can be used to craft custom data applications
  - https://github.com/Arthanadftz/plugin-chart-table
    - 依赖@emotion/core、@superset-ui/core、d3、react-table
  - https://github.com/w11k/superset-chart-plugins
    - Table Chart; Scatter Chart

- lineup-lite /7Star/MPLv2/202104/ts
  - https://github.com/sgratzl/lineup-lite
  - https://lineup-lite.js.org/docs/
  - 依赖 react-table.v7、react-virtual.v2、lineup-lite
  - LineUp-lite is an extension of the excellent react-table library for rendering beautiful interactive table visualizations based on the LineUp ranking visualization technique.
  - @lineup-lite/hooks provide extensions to react-table such as additional React hooks and custom renderers. 
  - @lineup-lite/table provides a wrapper around react-table providing a single LineUp-like React table component.

- https://github.com/patternfly/patternfly-react/tree/main/packages/react-table
  - https://patternfly-react.surge.sh/components/table
  - 给了很多示例，Compound expandable，Tree table
- @equinor/fusion-react-table
  - https://github.com/equinor/fusion-react-components/tree/main/packages/table
  - https://equinor.github.io/fusion-react-components/?path=/docs/table-examples-toolbar-table--toolbar-table
  - 功能简单，但sort、filter实现的结构清晰
# design-system-ui-v7
- https://github.com/onaio/js-tools/tree/master/packages/DrillDownTable
  - a bootstrap-based higher order component that works with React Table.

- https://github.com/entando/frontend-libraries/tree/master/packages/entando-datatable
  - customizable data table powered by react-table used in Entando projects specifically in Appbuilder & CMS.
  - columns resizable and reorderable (except actions column)

- more ui/design system using react-table
  - https://github.com/scality/zenko-ui
  - @zenbu-ui/table
    - https://github.com/KodepandaID/zenbu-ui
  - https://github.com/SAP/ui5-webcomponents-react/tree/main/packages/main/src/components/AnalyticalTable
    - https://sap.github.io/ui5-webcomponents-react/?path=/docs/data-display-analyticaltable--default-story

- 过于简单
  - https://github.com/edx/paragon/tree/master/src/Table
    - https://edx.github.io/paragon/
  - https://github.com/ccontrols/component-controls/tree/master/ui/components/src/Table
    - https://component-controls.com/api/components-table--overview
  - https://github.com/coingaming/moon-design/tree/develop/packages/table
    - Lightweight, fast and extendable table. Based on react-table

- https://github.com/grafana/grafana/tree/main/packages/grafana-ui/src/components/Table
- https://github.com/iTwin/iTwinUI-react/tree/main/src/core/Table

- https://www.npmjs.com/package/@preamp/tables
- https://www.npmjs.com/package/@gmfe/table-x
# examples-v7
- https://github.com/ggascoigne/react-table-example
  - https://codesandbox.io/s/github/ggascoigne/react-table-example
  - Demo of React Table V7 using TypeScript as well as Material UI v4
  - 全局filter，各种类型的filter
- https://github.com/legendarydev007/react-material-dashboard
  - built with material-ui framework coded by Lahm
- https://github.com/toni783/MUI-react-virtual-table
  - https://codesandbox.io/s/github/toni783/MUI-react-virtual-table
  - react-table.v7, react-virtual, material-ui.v4

- https://github.com/paalamugan/exce  l-sheet-react-table
  - https://paalamugan.github.io/excel-sheet-react-table/
  - You can import you excel sheet and edit your excel sheet in the UI and download that updated excel sheet.
  - 依赖 react-table、react-window、react-toastify、xlsx-parse-json

- https://github.com/bezkoder/react-table-crud-example
  - React Table example: CRUD App with react-table v7, axios, Bootstrap
  - [React Table example: CRUD App | react-table 7](https://www.bezkoder.com/react-table-example-hooks-crud/)
- https://github.com/jcape-gt/RemoteDataTable
  - A CRUD data table library for React 
  - 依赖react-table.v7、material-ui.v4、date-fns、react-hook-form
  - Rows automatically support read/edit mode
- https://github.com/MelisaMert/crud-react-contextapi
  - Basic Crud Operation with contextapi

- https://github.com/jimmybutton/react-tailwind-table
  - 只依赖 react-table7、@tailwindcss/forms
  - [React Table Tutorial Part 2: Style the table with Tailwind CSS](https://www.samuelliedtke.com/blog/react-table-tutorial-part-2/)
  - [React Table Tutorial Part 1: Build a fully featured table component](https://www.samuelliedtke.com/blog/react-table-tutorial-part-1/)
    - https://github.com/jimmybutton/react-tailwind-table/tree/part1

- https://github.com/TheWidlarzGroup/RT7-example 
  - https://rt7-example.netlify.app/
  - /202008
  - hooks-table-demo-with-pagination
  - 依赖bootstrap4、react-table7、reactstrap8
  - [React Table 7 - Hooks based library](https://thewidlarzgroup.com/react-table-7/)

- https://github.com/Eversoft-Group/react-table
  - React table component build with Bootstrap and react-table
  - https://eversoft-group.github.io/react-table/

- https://github.com/datopian/datapub
  - https://tech.datopian.com/publish/
  - 依赖ckan-client、frictionless.js、react-table、stream-to-array、axios
  - DataPub is a React-based framework for rapidly building modern data publishing flows (esp for CKAN). 
  - It provides a variety of core components as well as example apps and flows.
  - https://github.com/datopian/datapub-nhs
    - NHS data publishing app in React using DataPub.js framework.
- https://github.com/CDCgov/cdc-open-viz
  - [Example Numeric Maps](https://www.cdc.gov/wcms/4.0/cdc-wp/data-presentation/examples/example-numeric-maps.html)
  - [Example Filterable Data Map](https://www.cdc.gov/wcms/4.0/cdc-wp/data-presentation/examples/example-numeric-maps-filterable.html)
  - 依赖d3、react-table、react-dropzone、html-react-parser、bootstrap4
  - 示例简单实用，表格很简单

- https://github.com/vishal-nath-chauhan/React-table-v7-blog-series
  - https://github.com/vishal-nath-chauhan/React-table-v7-blog-series-Part-2

- https://github.com/nteract/data-explorer
  - https://data-explorer.nteract.io/
  - Data Explorer is nteract's automatic visualization tool.
  - 依赖react-table6
  - 样式比比较简陋
- data-catalog-components /5Star/GPLv3/202104/js
  - https://github.com/getdkan/data-catalog-components
  - https://getdkan.github.io/data-catalog-components
  - 依赖bootstrap.v4、reactstrap、react-dnd, react-table.v7
  - 样式普通
  - A set of React components to facilitate the creation of Open Data Catalogs with React.
  - built for dkan(基于php，而ckan基于python)

- react-table chart column 图表作为一列
  - https://codesandbox.io/s/react-table-highcharts-jm125

- https://github.com/codefromrvk/sql-editor
  - https://sql-editor-demo.netlify.app/

- https://github.com/earthshakira/csv-modifier /python
  - https://csv-update-pipeline.herokuapp.com/
  - CSV Uploads, Validation, Editing and Storage
