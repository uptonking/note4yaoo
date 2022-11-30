---
title: lib-excel-tanstack-table-examples
tags: [examples, tanstack-table, toc]
created: 2021-07-20T12:42:45.044Z
modified: 2022-08-21T10:37:01.349Z
---

# lib-excel-tanstack-table-examples

# guide

- tips
  - react-table的问题在于没有成熟的使用案例，没有大公司案例支持，缺少样式主题、性能优化，特别是缺少在表格的单元格中显示图表的示例如ag-grid-charts
    - github最新的issues多维表格界面基于react-table实现
    - outline wiki使用了react-table和react-window
  - ✨ list和grid切换功能 需要自己实现

- top-dependents-of-react-table.v7
  - 各类组件库中的table或list组件
    - guidu
    - @component-controls/components
    - @edx/paragon
    - ref
      - https://www.npmjs.com/browse/depended/react-table
      - https://github.com/search?o=desc&q=react-table+filename%3Apackage.json&s=indexed&type=Code
- top-dependents-of-react-table.v6
  - nteract/data-explorer: 依赖d3、numeral
# popular-v8
- material-react-table /106Star/MIT/202208/ts
  - https://github.com/KevinVandy/material-react-table
  - https://www.material-react-table.com/
  - 依赖 material-ui.v5、emotion/styled、react-table.v8、match-sorter
  - A fully featured Material UI V5 implementation of Tanstack React Table V8
  - Inspired by material-table and the MUI X DataGrid
  - All internal Material UI components are easily customizable

- material-grid /2Star/MIT/202208/ts
  - https://github.com/zmrl010/material-grid
  - Feature-rich datagrid component
  - 依赖 mui5、emotion

- mantine-data-grid /58Star/MIT/202208/ts
  - https://github.com/Kuechlin/mantine-data-grid
  - https://kuechlin.github.io/mantine-data-grid/
  - https://mantine.dev/
  - 支持sort/filter/pagination，不支持group
  - 提供了一个类似storybook的表格属性开关工具
  - 依赖mantine、dayjs
  - Data Grid component with Mantine UI and react-table v8.
  - 样式非常友好
  - https://github.com/mantinedev/mantine
    - React components library with native dark theme support

- mantine-datagrid /1Star/ISC/202208/ts
  - https://github.com/FabienDeborde/mantine-datagrid
  - https://mantine-datagrid.netlify.app/
  - A wrapper around React Table (TanStack Table v8) using Mantine.
  - I do not plan to really maintain or update this library

- react-crud /2Star/MIT/202208/ts
  - https://github.com/sefirosweb/react-crud
  - https://sefirosweb.github.io/react-crud
  - It´s a React compononet to be used at multiple projets
  - Normally you are interested to have a CRUD system for a lot of things, usually you want to make a fast and simple CRUD system
  - It is made by bootstrap (react-bootstrap) you can modify colors and styles for these components
  - ref
    - https://github.com/toofaniCoder/react-table-8.5-crud

- @uidu/table /13Star/MIT/202105/ts/react
  - https://github.com/uidu-org/guidu
  - https://uidu.design/
  - https://uidu.design/packages/data/dashlets
  - https://github.com/uidu-org/guidu/tree/main/packages/data/table
    - 依赖react-table.v7、react-virtual、styled-components5、react-intl5、@uidu/popup
  - Guidu is uidu's design system library
    - 完全复制了atlassian-editor，并将组件替换成了自己的design system
    - dashlet会不会也是复制的？
    - 提供了专门的数据类别组件：list, table, data manager, data views, timeline, dashlet, dashboard
    - These components are Atlassian Design Guidelines(ADG) compliant
  - https://github.com/uidu-org/guidu/tree/main/packages/data/dashlets
    - 依赖@uidu/table、styled-components、@amcharts/amcharts4、d3、@cubejs-client/react、react-table、twin.macro

- https://github.com/zendricom/tableus
  - A react library for rendering highly configurable tables.
  - intended to be integrated fully with your backend to deliver tables with sorting, filtering and pagination.
  - Tableus does not state any requirements on your preferred UI (bootstrap, material UI, etc.) or backend API (REST, GraphQL, etc.), by externalizing those into seperate modules called fetchers and UIs.
  - ref
    - https://github.com/zendricom/tableus-ui-bootstrap5
    - https://github.com/zendricom/tableus-fetcher-laravel-rest
# design-system-ui-v8
- https://github.com/blockchain/constellation/blob/development/packages/constellation
  - 依赖tanstack-table、radix-ui、headlessui、tailwindcss

- https://github.com/netdata/netdata-ui/tree/master/src/components/table  /js
  - https://netdata.github.io/netdata-ui/
  - 提供了一套设计系统的ui，table实现过于简单
  - Table component Implementation based on react-table lib.
  - Virtualized settings are mostly replicating react-window
  - Requires numeric width and height of the container.

- https://github.com/Achaak/pikas-ui
  - https://pikas-ui.vercel.app/
  - Pikas-UI is a React UI library for building web applications with StitchesJS.

- https://github.com/provectus/kafka-ui
  - Open-Source Web UI for Apache Kafka Management
# examples-v8
- https://github.com/freewind-demos/typescript-react-data-grid-table-demo
  - Define a wrapper component for @tanstack/react-table
- https://github.com/polyms/vite-boilerplate
  - A starter for React with Typescript with the fast Vite and all static code testing with Eslint and formatting with Prettier.

- https://github.com/dogukanakkaya/next-boilerplate
  - Next Auth Prisma tRPC Tailwind React Table React Select

- teamManagement /6Star/NALic/202208/js/MERN
  - https://github.com/sayinmehmet47/teamManagement
  - https://team-management12.herokuapp.com/
  - Team management app with authentication(MERN project)
  - 依赖 redux、reactstrap、socket.io

- https://github.com/lawrencecchen/planetsheet
  - https://planetsheet.vercel.app/
  - 依赖 glide-data-grid、radix-ui、trpc、knex、react-query.v3
  - A SQL editor designed for developers and content editors.
  - Today, Planetsheet is an (early) alternative to npx prisma studio, Postico, and TablePlus. 
  - In the future, Planetsheet will give you (and your content editors) an interface as intuitive as Airtable and Google Sheets, while letting you (as a developer) use powerful databases underneath.

- https://github.com/pankaspe/Azansca-project
  - http://azansca-project.vercel.app/
  - Azansca.it project bootstrapped with Next js & Chakra UI.
  - 简洁且有设计感，绿色主题

- https://github.com/lqd1434/MatexPro
  - 基于electron的万能工具软件

- https://github.com/joangavelan/corteza
  - https://corteza-book-tracker.vercel.app/
  - An app that works with your local storage to keep track of the book(s) you read, save notes, ideas and more.

- https://github.com/Danzo7/doctorIO
  - medical management software to improve the connectivity between doctors and patients
  - 依赖 redux-toolkit、electron、localforage、react-beautiful-dnd、redux-persist

- https://github.com/Saszr/vite-react-chill
  - a react app with Vite / TypeScript / Chakra-UI / Redux Toolkit (include RTK Query) setup.

- https://github.com/myriadsocial/myriad-dashboard
  - 依赖 mui5、headlessui、tanstack-table/query、formik、@fontsource/noto-sans-sc

- https://github.com/Dev-CasperTheGhost/earnings-tracker
  - https://earnings.caspertheghost.me/
  - track your income and expenses with a simple chart and a simple interface.

- https://github.com/RafaelGB/obsidian-db-folder
  - Obsidian Plugin to Allow Notion like database based on folders

- https://github.com/tourist/coinscan-front
  - https://coinscan-front-git-dev-tourist.vercel.app/
  - 暗黑主题，设计感很强

- https://github.com/kuroski/github-issue-viewer
  - https://github-issue-viewer.up.railway.app/
  - A Github issue viewer apps

- https://github.com/m1guelsb/deals-cms
  - SaaS CMS App for manage costumers, deals and tasks, using as backend a json-server with jwt auth and relationships.

- https://github.com/Reza1878/dts-task-fe
  - https://dts-task-fe.vercel.app/
  - 标准的crud界面

- https://github.com/aoigj100a/react-table-demo
  - react-table v8、chakra-ui

- https://github.com/Mallet1/tanstack-editable-data
  - https://codesandbox.io/s/github/Mallet1/tanstack-editable-data

- https://github.com/sajclarke/react-table-8-rowactions
  - an example of using Tanstack table v8 with row action column displaying Edit and Delete buttons

- https://github.com/evriyanaindrasaputra/react-dashboard
  - https://react-dashboard-pi-ten.vercel.app/
  - Tailwind Css Headless UI Tanstack Query Tanstack Table React Hook Form

- https://github.com/iambinodstha/react-salesforce-admin-ui
  - This application cover admin UI with highchart, tailwindcss, salesforce ui
  - Integration with Lightning Design System

- https://github.com/grkmtsn/smart-table
  - A minimal React Vite starter template.

- https://github.com/wooboo/the-playform
  - https://the-playform.vercel.app/admin/dashboard
  - 提供了典型的仪表板示例
  - 依赖 headlessui、trpc、recharts、prisma、next-auth

- https://github.com/manuel-mauky/tanstack-table-core-example
  - Trying out TanStack Table without frameworks but only standard HTML and web components
- https://github.com/freewind-demos/typescript-tanstack-react-table-global-filter-demo
  - ts+react

- more-table-repos
  - https://github.com/Elduwani/cashbar-admin-demo
  - https://github.com/AbdQaadir/movie-app
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

- https://github.com/saas-js/saas-ui/tree/main/packages/saas-ui-data-table
  - https://www.saas-ui.dev/docs/data-display/data-table
  - A DataTable component for Chakra UI, build with react-table.
  - 功能过于简单
  - 文档样式非常好

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
