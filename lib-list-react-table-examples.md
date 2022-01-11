---
title: lib-list-react-table-examples
tags: [examples, react-table]
created: '2021-07-20T12:42:45.044Z'
modified: '2021-07-20T13:28:26.296Z'
---

# lib-list-react-table-examples

# guide

- tips
  - react-table的问题在于没有成熟的使用案例，没有大公司案例支持，缺少样式主题、性能优化
    - github最新的issues多维表格界面基于react-table实现
    - outline wiki使用了react-table和react-window

- top-dependents-of-react-table.v7
  - 各类组件库中的table或list组件
    - @component-controls/components
    - @edx/paragon
    - guidu
- top-dependents-of-react-table.v6
  - nteract/data-explorer: 依赖d3、numeral
# popular
- ui-table /25Star/MIT/202112/ts
  - https://github.com/habx/ui-table
  - https://habx.github.io/ui-table/
  - UI components for react-table based on [ui-core](https://github.com/habx/ui-core)
  - 依赖@habx/ui-core、react-table.v7、react-window、styled-components、lodash、exceljs、papaparse(csv)、react-dropzone
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
  - 支持3种单元格类型 number, text, select，弹出框很好用
  - 没有全局工具条，但表头每列的下拉菜单很完整；不支持分组

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
  - 拖动表格滚动条时，可以显示minimap
  - 提供了日期字段作为一列的Calendar示例

- @uidu/table /13Star/MIT/202105/ts/react
  - https://github.com/uidu-org/guidu
  - https://uidu.design/
  - table组件依赖于 react-table, react-virtual, styled-components, numeral
  - Guidu is uidu's design system library
  - 完全复制了atlassian-editor，并将组件替换成了自己的design system
  - 提供了专门的数据类别组件：list, table, data manager, data views, timeline, dashlet, dashboard
  - 依赖styled-components、@amcharts/amcharts4、d3、@cubejs-client/react、react-table、twin.macro
  - These components are Atlassian Design Guidelines(ADG) compliant
  - https://github.com/uidu-org/guidu/tree/main/packages/data/table
    - 依赖react-table7、react-virtual、styled-components5、react-intl5、@uidu
  - https://github.com/uidu-org/guidu/tree/main/packages/data/dashlets
    - 依赖@uidu/table、d3、amcharts4、cubejs-client/react、s-c

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
# react-table-extensions
- https://github.com/GuillaumeJasmin/react-table-sticky
  - Sticky hook for React Table v7

- https://github.com/gargroh/react-table-plugins
  - This repository contains miscellaneous react-table v7 plugins
  - useExportData - Exporting data from table
  - useColumnSummary - For displaying and calculating column summaries
  - useCellRangeSelection - Allows Cell selection and Cell range selection
# examples
- https://github.com/ggascoigne/react-table-example
  - https://codesandbox.io/s/github/ggascoigne/react-table-example
  - Demo of React Table V7 using TypeScript as well as Material UI v4
- https://github.com/legendarydev007/react-material-dashboard
  - built with material-ui framework coded by Lahm
- https://github.com/Podoprigora/material-ui-custom-theme
  - https://podoprigora.github.io/material-ui-custom-theme/
  - Custom theme for material-ui by making use of sass.
  - 依赖material-ui.v5

- https://github.com/paalamugan/excel-sheet-react-table
  - https://paalamugan.github.io/excel-sheet-react-table/
  - You can import you excel sheet and edit your excel sheet in the UI and download that updated excel sheet.

- https://github.com/bezkoder/react-table-crud-example
  - React Table example: CRUD App with react-table v7, axios, Bootstrap
  - [React Table example: CRUD App | react-table 7](https://www.bezkoder.com/react-table-example-hooks-crud/)

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

- https://github.com/jcape-gt/RemoteDataTable
  - A CRUD data table library for React 
  - 依赖react-table.v7、material-ui.v4、date-fns、react-hook-form
  - Rows automatically support read/edit mode

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
  - A set of React components to facilitate the creation of Open Data Catalogs with React.
  - built for dkan(基于php，而ckan基于python)

- https://github.com/toni783/MUI-react-virtual-table
  - https://codesandbox.io/s/github/toni783/MUI-react-virtual-table
  - react-table.v7, react-virtual, material-ui.v4

- https://github.com/MelisaMert/crud-react-contextapi
  - Basic Crud Operation with contextapi
# design system/ui built with react-table
- https://github.com/netdata/netdata-ui/tree/master/src/components/table
  - https://netdata.github.io/netdata-ui/
  - 提供了一套设计系统的ui，table实现过于简单
  - Table component Implementation based on react-table lib.
  - Virtualized settings are mostly replicating react-window
  - Requires numeric width and height of the container.
- https://github.com/onaio/js-tools/tree/master/packages/DrillDownTable
  - a bootstrap-based higher order component that works with React Table.

- https://github.com/entando/frontend-libraries/tree/master/packages/entando-datatable
  - customizable data table powered by react-table used in Entando projects specifically in Appbuilder & CMS.
  - columns resizable and reorderable (except actions column)

- more ui/design system using react-table
  - https://github.com/scality/zenko-ui
  - @zenbu-ui/table
    - https://github.com/KodepandaID/zenbu-ui

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
# more-repos
- https://github.com/imcva/reactstrap-table
  - A reactstrap skin for react-table v7

- https://github.com/uqix/reactkit-table
  - Table component using react-table and material-ui
  - 和kitchen-sink示例太类似

- https://github.com/brycemcl/covid-table
  - https://covid-table-675ae.web.app/
  - Just a short project parsing a CSV file into a table

- https://github.com/pramodsvidyarthi/react-table-virtualized
  - Created with CodeSandbox

- https://github.com/ToolJet/ToolJet
  - low-code framework to build and deploy internal tools

- https://github.com/savecost/datav
  - datav.io is a lightweight but better alternative to Grafana
- https://github.com/nasa/earthdata-search
  - Earthdata Search is a web application developed by NASA EOSDIS to enable data discovery, search, comparison

- https://github.com/Buffme/superset-dashboard
  - 抽出dashboard这块功能
# non-react-table
- https://github.com/venkatakireeti/meta-data-editor
  - React table component with useful functions.
  - 未使用react-table，但用了react-window

- https://github.com/quantmind/metablock-js
  - TypeScript tools for the metablock cloud
