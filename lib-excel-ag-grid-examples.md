---
title: lib-excel-ag-grid-examples
tags: [ag-grid, examples, grid, list, toc]
created: 2021-07-20T13:44:45.705Z
modified: 2022-08-21T10:39:10.445Z
---

# lib-excel-ag-grid-examples

# guide
- ag-grid-pkg dependents
  - https://github.com/search?q=ag-grid-react+filename%3Apackage.json&type=Code
  - `ag-grid-enterprise` contains the Enterprise features only, it does not contain the core grid, hence you still need `ag-grid-community` and `ag-grid-react`. Versions of all three must match.
# popular
- Talend Datagrid /141Star/Apache2/202208/ts
  - https://github.com/Talend/ui/tree/master/packages/datagrid
  - http://talend.surge.sh/datagrid
  - 依赖 ag-grid-community/react、@talend/design-system、i18next、focus-trap-react
  - 提供了数据加载、编辑的示例
  - It's an enhanced Ag-Grid.
  - Custom Avro Renderer
    - IntCellRenderer: Renderer for the avro type int
    - StringCellRenderer: Renderer for avro the type string
    - Extracts records from any given Avro format files for other components to process the records.
  - issues encountered with ag-grid that DataGrid resolved.
    - ag-grid doesn't manage a style when the column is active.
    - Ag-grid set the current cell selected by a click. 
      - If we navigate with the keyboard, ag-grid sent a new event onCellFocused but the cell isn't selected. 
    - Although that Ag-Grid recommands to avoid to use custom cell renderer to renderer the cell, we used because a cell can't have only text but many elements on this: quality indicator, comments, invisible chars, ...
  - [Drop datagrid package · Talend/ui_20221201](https://github.com/Talend/ui/pull/4477)
    - Datagrid has been moved to a private repository.
    - previous commit id: 904dd6c27973e161c2f41a07a4ca1cfa8067598b
    - https://github.com/Talend/ui/tree/904dd6c27973e161c2f41a07a4ca1cfa8067598b

- https://github.com/linz/step-ag-grid
  - https://linz.github.io/step-ag-grid/
  - Reusable ag-grid component for LINZ
  - ag-grid-community based grid with custom popover components implemented using a modified react-menu.

- https://github.com/Alek-S/SwiftSheet /js/graphql/mongoose
  - https://swiftsheet.app/
  - Upload a CSV to share an online spreadsheet or mock API endpoint that auto-deletes after expiration. No user account needed.

- gant-design /48Star/MIT/202208/ts/多种数据与表单组件
  - https://github.com/gantFDT/gant-design
  - http://docs.gant.design/
  - 依赖antd.v3
  - 面向B端管理型软件、专注于数据密集型业务场景、基于Antd聚合型React组件库
  - 基于数据驱动模式快速开发组件、如数据驱动表单
  - grid-g这个子包依赖ag-grid
  - smartGrid相比于grid增加了视图的概念，用户可以自定义列的各种状态并保存到本地存储或者远端，解决的是不同的用户或角色对业务关注点不同的痛点。
  - https://github.com/gantFDT/gant-design-2
    - 新版 gantd， 依赖了antd4, 使用了dumi , 还未全部改造完成

- pro-components /2Star/MIT/202208/ts
  - https://github.com/svl-fe/pro-components
  - https://svl-fe.github.io/pro-components/components/conditions
  - 杭州薮猫科技中后台业务组件库业务组件库，包含了大量的第三方组件库
  - 依赖 antd.v4、ag-grid、rc-virtual-list

- GoodDataUI Pivot Table /53Star/Free4NonCommercial/ts/202104/inactive
  - https://github.com/gooddata/gooddata-react-components/tree/develop/src/components/core/pivotTable
  - https://gooddata-examples.herokuapp.com/pivot-table
  - A React-based JavaScript library for building data-driven applications
  - PivotTable基于ag-grid，Table是普通div
  - https://www.gooddata.com/
    - Modern BI for the modern data stack

- https://github.com/ganeshmani/react-ag-data-grid
  - https://react-ag-data-grid.vercel.app/
  - Using ag-grid-react in React: Guide and Alternatives

- https://github.com/ag-grid/ag-grid-react-package-example
  - shows a very large grid (767 columns and 1, 000 rows) using React cell renderers

- https://github.com/mui/mui-x/blob/master/benchmark/browser
  - mui-x将 mui-data-grid-pro与ag-grid/react-virtualized做了比较

- https://github.com/urbandataanalytics/bento-components/tree/master/src/components/Table
  - https://urbandataanalytics.github.io/bento-components/
  - Bento Components Library
  - 表格的样式被大改

- https://github.com/findable-no/findable-components
  - React components created for Findable AS applications based on @Mantine

- https://github.com/lee-chun-91/dashboard /js
  - https://lee-chun-91.github.io/
  - 可拖拽的仪表板示例，卡片不能重叠，表格和图表不能联动
  - 依赖ag-grid、chartjs3、react-grid-layout
- https://github.com/SumitKumar-2000/AgGrid-Dashboard
  - https://filterdashboard.netlify.app/
  - 支持table view、chart view
  - 依赖zustand

- https://github.com/mongodb-js/compass
  - This repository contains the source code and build tooling used in MongoDB Compass.

- https://github.com/onur-yildiz/epias-reports
  - http://epias-reports.vercel.app/
  - 依赖mui5、ag-grid、chartjs3、redux-toolkit、react-window
- https://github.com/cybowind/data-grid
  - This exercise addresses the challenge of how to view, sort and filter big amount of the data in grid efficiently.

- https://github.com/JTG91389/ag-grid-transaction-demo
  - simple demo site to add ag-grid transaction to our previous ag-grid websocket demo

- https://github.com/spbhat672/ReactProjects
  - react示例

- https://github.com/na-ji/leaderboard
  - https://pogo-leaderboard.vercel.app/
  - A fully automated leaderboard for Pokémon Go trainers
  - 设计得很好

- https://github.com/lowdefy/lowdefy /js
  - low-code framework that lets you build web apps with YAML or JSON configuration files.
# ag-grid-react
- ag-grid-react-example /150Star/MIT/202208/js/官方
  - https://github.com/ag-grid/ag-grid-react-example
  - Example of ag-Grid running with React
  - standard - shows a typical grid demonstrating many AG Grid features
  - large - shows a very large grid (767 columns and 1, 000 rows) using React cell renderers

- https://github.com/ag-grid/react-data-grid
  - React Data Grid Examples used on the AG Grid blog.

- https://github.com/samjulien/ag-grid-react-thinkster
  - Sample code and resources for my tutorials on ag-Grid and React on Thinkster.io.

- https://github.com/339598u5uut/sales-report
  - react
# design-system-using-ag-grid
- https://github.com/Client-Relationship-Consultancy/open-source-design-system
  - react-modal, react-select

- https://github.com/baloise/design-system/tree/master/packages/components-table
  - vanillajs 实现

- https://github.com/anthony-y-zhu14/MikoshiUI
  - https://62fc0f7c0d92b3b43bd42f5d-aftsqdiujd.chromatic.com/?path=/story/application-data-grid--data-grid-demo
  - A React UI Component library features Google's Material Design system and glassmorphis.
  - 依赖mui5

- https://github.com/blackbaud/skyux-ag-grid
  - angular示例

- https://github.com/odpi/egeria-ui-components
  - Encapsulated reactjs components with business logic inside.
# examples
- https://github.com/carlyrichmond/data-grid-alternatives
  - 依赖ag-grid-react.v27、react-redux、recharts、highcharts
  - This repository contains the accompanying examples for the talk Oh No! Not Another Data Grid.

- https://github.com/railmapgen/rmg-palette
  - https://railmapgen.github.io/rmg-palette
  - Line colour resources of multiple railway systems

- https://github.com/tolopsy/react-trader
  - A stock trading react application
  - 依赖mui5、redux-toolkit、ag-grid、highcharts
  - I created a mock server for the stock trading app. 
    - To start the mock server: Run node `./src/server`

- https://github.com/devdreamsolution/react-query-mui-context
  - Highcharts, Ag Grid, MUI, React Query, Typescript, Context demo
- https://github.com/anna-maria-j/visualization-samples
  - Sample visualizations with AG Grid and Highcharts

- https://github.com/Akashamba/Coronavirus-Tracker
  - https://coronavirus-tracker-live.netlify.app/
  - A Coronavirus Tracker built using the React Library.

- https://github.com/vigneshwaran-chandrasekaran/react-ag-grid
  - https://vigneshwaran-chandrasekaran.github.io/react-ag-grid/
  - demos: DataTable Server Side Pagination 
- https://github.com/eddy-hu/react-ag-grid
  - A simple demo using React, Redux, Ag-Grid and Ant Design3
- https://github.com/AhmedAGadir/ag-grid-todo-list-react-typescript
  - 依赖material-ui.v4

- https://github.com/shuheb/ag-grid-pomodoro
  - https://shuheb.github.io/ag-grid-pomodoro/
  - [React Data Grid: Use React Hooks to build a Pomodoro App](https://blog.ag-grid.com/react-data-grid-use-hooks-to-build-a-pomodoro-app/)
  - A productivity app built with React and AG Grid. 

- https://github.com/lab49/quickbits-react-ag-grid-speed-demo
  - a quickbits showcase of a React & Redux + AG Grid application

- https://github.com/huangyuanzhen/react-node-test
  - A system about human resource management; A practice of react & node; 
  - 包含前后端

- https://github.com/whitebrick/whitebrick
  - Open Source Airtable Alternative (No Code DB)
  - Whitebrick is a lightweight No Code Database with 3 points of difference:
    - The front end uses a Gatsby static Jamstack client for dead easy customization and deployment.
    - The back end is a set of Serverless functions for making DDL calls to PostgreSQL and configuring Hasura GraphQL server.
    - The PostgreSQL database schemas can be accessed directly with psql for data import/export and integrations with other tools.

- https://github.com/kychoiyohoho/ag-gridCRUD
  - 模拟后台基于 json-server
  - 简单示例

- https://github.com/balafreelancer87/react-ag-grid
  - client + server + mysql
- https://github.com/seanlandsman/ag-grid-crud/tree/part-4
  - crud: java + ag-grid
- https://github.com/berdyshevol/ag-grid-with-crud
  - react
- https://github.com/bchariot/ReactCRUD
  - AG Grid allowing CRUD operations written in React.js
- https://github.com/RSC01/Crud-Demo
  - purpose to check skills useFormik, Ag-Grid and react-bootstrap

- https://github.com/annamatveev/luly
  - Tasks board written in React using ag-grid
  - 依赖 express、material-ui、mongodb、redux、styled-components

- https://github.com/raptoria/riskgrid
  - https://codesandbox.io/s/github/raptoria/editablegrid
  - React, Redux, AG-Grid, Typescript, Redux-Observable, CRA, React Router

- https://github.com/xh/hoist-react
  - https://toolbox.xh.io/app/grids
  - Hoist is a web application development toolkit developed by Extremely Heavy.
  - Hoist is designed as a "full stack" UI development framework, meaning that it has both server and client components that work together 
  - hoist-react is the current reference client-side implementation of Hoist. 
  - Hoist React is built on a collection of remarkable third-party libraries
  - 依赖 mobx、ag-grid、blueprint、hightcharts、router5

- https://github.com/ramepras/node-app-consuming-fake-rest-service
  - Node-Express app consumes JSON fake rest api and displays data on ag-grid.

- https://github.com/tchassijordan/js_dashboard
  - A dashboard built with Ag-grid, chart.js, HTML, CSS, and native JS

- https://github.com/MapColonies/discrete-layer-client
  - React app written in typescript to define manage and browse discrete layers image catalog.

- https://github.com/abbasKareem/dashboard-using-electron-react
  - Admin Dashboard

- https://github.com/sourav9599/Spreadsheet-data-visualizer
  - Spreadsheet-data-visualizer
  - 依赖flask、dtale-pandas

- https://github.com/ackerleytng/logaze
  - Better interface for filtering laptops on Lenovo outlet
  - Scraper, written in clojure!
- https://github.com/demiurge16/tpm-ui /kotlin-api
  - Translation project management system

- https://github.com/meetbryce/pipelinr
  - Personal data pipeline GUI
- https://github.com/sanaz-git/ag-grid-table
  - A Table working with React and AG Grid Community.
# server-side
- https://github.com/ag-grid/ag-grid-server-side-nodejs-example
  - A reference implementation showing how to perform server-side operations using ag-Grid with node.js and MySQL.
  - https://github.com/eogra7/ag-grid-server-side-nodejs-example
# more
- https://github.com/terrestris/react-geo
  - https://terrestris.github.io/react-geo/
  - A set of geo related components to use in combination with react, antd and ol.
  - 在地图上方显示要素属性表

- https://github.com/ForceManager/hoi-poi-ui
  - A flexible and customizable react component library.

- https://github.com/AdaptableTools/adaptable-demo
  - https://github.com/AdaptableTools/example-adaptable-react-aggrid
  - https://github.com/AdaptableTools/example-adaptable-aggrid
  - AdapTable does not provide a DataGrid control of its own; 
  - AdapTable is most commonly used together with ag-Grid as the 2 products complement each other very well.
  - [AdapTable Overview](https://docs.adaptabletools.com/docs/)
    - AdapTable is a sophisticated HTML5 DataGrid add-on.
    - AdapTable does not provide a DataGrid control of its own; AdapTable is most commonly used together with ag-Grid 

- https://github.com/xjdesigns/excelui
  - Web UI built to look and work like excel

- https://github.com/bloom-housing/bloom
  - Bloom consists of a client/server architecture using Next.js (a React-based site framework) for the frontend applications and NestJS for the backend API.

- https://github.com/Meersource/react-spreadsheet
  - 简单玩具
- https://github.com/dongjay00/react-trading-app
  - React Trading App with Redux toolkit | Typescript | Material ui | AG Grid and HighCharts

- https://github.com/ghostfuel/amplified-tools-ui
  - React UI for amplified.tools, to provide more powerful, automated ways of interacting with your Spotify playlists.

- https://github.com/mongodb-js/compass
  - The GUI for MongoDB.

- https://github.com/InsistZch/ag-grid
  - 菜品比对功能迭代
