---
title: lib-list-ag-grid-examples
tags: [ag-grid, examples, grid, list]
created: '2021-07-20T13:44:45.705Z'
modified: '2021-07-20T13:45:26.460Z'
---

# lib-list-ag-grid-examples

# popular

- Talend Datagrid /108Star/Apache2/202202/js
  - https://github.com/Talend/ui/tree/master/packages/datagrid
  - http://talend.surge.sh/datagrid
  - 依赖 ag-grid-community/react.v25.3.0
  - It's an enhanced Ag-Grid.
  - Custom Avro Renderer
    - IntCellRenderer: Renderer for the avro type int
    - StringCellRenderer: Renderer for avro the type string
  - a list of issues encountered with ag-grid that DataGrid resolved.
    - ag-grid doesn't manage a style when the column is active.
    - Ag-grid set the current cell selected by a click. If we navigate with the keyboard, ag-grid sent a new event onCellFocused but the cell isn't selected. 
    - Although that Ag-Grid recommands to avoid to use custom cell renderer to renderer the cell, we used because a cell can't have only text but many elements on this: quality indicator, comments, invisible chars, ...

- GoodData. UI Pivot Table /53Star/Free4NonCommercial/ts/202109/inactive
  - https://github.com/gooddata/gooddata-react-components/tree/develop/src/components/core/pivotTable
  - https://gooddata-examples.herokuapp.com/pivot-table
  - A React-based JavaScript library for building data-driven applications
  - PivotTable基于ag-grid，Table是普通div

- https://github.com/ag-grid/ag-grid-react-example
  - Example of ag-Grid running with React
  - standard - shows a typical grid demonstrating many AG Grid features
  - large - shows a very large grid (767 columns and 1, 000 rows) using React cell renderers

- https://github.com/urbandataanalytics/bento-components/tree/master/src/components/Table
  - https://urbandataanalytics.github.io/bento-components/
  - Bento Components Library
  - 表格的样式被大改
# extensions
- https://github.com/avallete/ag-grid-autocomplete-editor
  - Quick implementation of autocompletion into ag-Grid cell using autocompleter package.
- https://github.com/bchariot/ReactCRUD
  - AG Grid allowing CRUD operations written in React.js

- https://github.com/edit-ag-grid/edit-ag-grid
  - 高性能、满足复杂交互的编辑表格
  - 基于 antd.v4, ag-grid

- https://github.com/target/table-model
  - TableModel is an in-memory data model that automatically calculates your data based on provided equations. 
  - It keeps track of dependencies between data and equations and automatically updates cells quickly and efficiently.
  - TableModel works especially well with UI components like AgGrid because it simplifies your data flow and can add additional features such as predicting which cells in your table are going to be impacted by a change 

- https://github.com/VoyagerScientific/react-jsonschema-form-ui
  - Alternative widgets for the react-jsonschema-form package.
- https://gitlab.com/dgothrek/ipyaggrid
  - The power of ag-Grid in Jupyter notebooks
- https://github.com/lowdefy/blocks-aggrid
  - Lowdefy blocks for AgGrid.
  - Lowdefy is an open-source (Apache-2.0) low-code framework. lowdefy依赖graphql

- https://github.com/ag-grid/ag-grid-customise-theme
  - showcases how the ag-Grid built-in themes can be customized by overriding Sass variables.
- https://github.com/RocketCommunicationsInc/ag-grid-theme
  - AG Grid theme using Astro UXDS styling
# examples
- https://github.com/vigneshwaran-chandrasekaran/react-ag-grid
  - https://vigneshwaran-chandrasekaran.github.io/react-ag-grid/
  - demos: DataTable Server Side Pagination 
- https://github.com/eddy-hu/react-ag-grid
  - A simple demo using React, Redux, Ag-Grid and Ant Design3
- https://github.com/AhmedAGadir/ag-grid-todo-list-react-typescript
  - 依赖material-ui

- https://github.com/whitebrick/whitebrick
  - Open Source Airtable Alternative (No Code DB)
  - Whitebrick is a lightweight No Code Database with 3 points of difference:
    - The front end uses a Gatsby static Jamstack client for dead easy customization and deployment.
    - The back end is a set of Serverless functions for making DDL calls to PostgreSQL and configuring Hasura GraphQL server.
    - The PostgreSQL database schemas can be accessed directly with psql for data import/export and integrations with other tools.

- https://github.com/balafreelancer87/react-ag-grid
  - client + server + mysql
- https://github.com/seanlandsman/ag-grid-crud/tree/part-4
  - crud: java + ag-grid
- https://github.com/annamatveev/luly
  - Tasks board written in React using ag-grid
  - 依赖 express、material-ui、mongodb、redux、styled-components

- https://github.com/raptoria/riskgrid
  - https://codesandbox.io/s/github/raptoria/editablegrid
  - React, Redux, AG-Grid, Typescript, Redux-Observable, CRA, React Router

- https://github.com/gantFDT/gant-design
  - 面向B端管理型软件、专注于数据密集型业务场景、基于Antd聚合型React组件库
  - 基于数据驱动模式快速开发组件、如数据驱动表单
  - grid-g这个子包依赖ag-grid

- https://github.com/xh/hoist-react
  - https://toolbox.xh.io/app/grids
  - Hoist is a web application development toolkit developed by Extremely Heavy.
  - Hoist is designed as a "full stack" UI development framework, meaning that it has both server and client components that work together 
  - hoist-react is the current reference client-side implementation of Hoist. 
  - Hoist React is built on a collection of remarkable third-party libraries
  - 依赖 mobx、ag-grid、blueprint、hightcharts、router5
# more-repos
- https://github.com/terrestris/react-geo
  - https://terrestris.github.io/react-geo/
  - A set of geo related components to use in combination with react, antd and ol.
  - 在地图上方显示要素属性表

- https://github.com/gantFDT/gant-design
  - GantD是面向B端管理型软件、专注于数据密集型业务场景、基于Antd聚合型React组件库 在Antd的基础上做了不同程度的针对性的强化，亦可以视作为Antd的补充，可以和Antd同时使用

- https://github.com/ForceManager/hoi-poi-ui
  - A flexible and customizable react component library.

- https://github.com/AdaptableTools/adaptable-demo
  - https://github.com/AdaptableTools/example-adaptable-react-aggrid
  - AdapTable does not provide a DataGrid control of its own; 
  - AdapTable is most commonly used together with ag-Grid as the 2 products complement each other very well.
  - [AdapTable Overview](https://docs.adaptabletools.com/docs/)
    - AdapTable is a sophisticated HTML5 DataGrid add-on.
    - AdapTable does not provide a DataGrid control of its own; AdapTable is most commonly used together with ag-Grid 
