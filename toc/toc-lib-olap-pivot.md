---
title: toc-lib-olap-pivot
tags: [lib, olap, pivot-table, toc]
created: 2020-07-13T02:39:21.789Z
modified: 2023-01-23T11:24:41.943Z
---

# toc-lib-olap-pivot

# guide

# olap-dataset
- [Get samples for Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/sample-datasets)
  - An Excel workbook version of the AdventureWorks dimensional model

- [Curated Datasets Overview / ObservableHQ](https://observablehq.com/@observablehq/curated-datasets)
  - [Sample Datasets / Observable](https://observablehq.com/@observablehq/sample-datasets)
# pivot
- pivottable /3.5kStar/MIT/201811/CoffeeScript
  - https://github.com/nicolaskruchten/pivottable
  - https://pivottable.js.org/examples/
  - a JS Pivot Table library with drag'n'drop functionality built on top of jQuery/jQueryUI
  - 基于table标签实现
  - https://github.com/jjagielka/pivottable-grouping
    - fork of PivotTable.js adds the data grouping capability, similar to Subtotal.js but made directly in the PivotTable
  - https://github.com/nagarajanchinnasamy/subtotal /201810/CoffeeScript
    - https://nagarajanchinnasamy.github.io/subtotal
    - A JavaScript plugin for PivotTable.js. 
    - It renders subtotals of rows and columns with the ability to expand and collapse rows and columns
- react-pivottable /852Star/MIT/202011/js/inactive
  - https://github.com/plotly/react-pivottable
  - https://react-pivottable.js.org/
  - a React-based pivot table library with drag'n'drop functionality. 
  - It is a React port of the jQuery-based PivotTable.js by the same author.
  - 基于table标签实现
  - 创建透视表后，可快速展示图表
  - 依赖react-draggable, sortablejs
  - https://github.com/jjagielka/react-pivottable-grouping
    - https://jjagielka.github.io/react-pivottable-demo/
    - a fork of react-pivottable with added capacity of grouping and displaying subtotals.
    - 作者实现了很多pivot table
  - https://github.com/JerryYuanJ/react-sort-pivottable
    - An enhanced react-pivottable component with sort and fixed header functions
    - Now it has the ability to sort columns and rows. 
  - https://github.com/devisionteam/react-pivottable
    - a fork of react-pivottable with grouping and sorting. 合并了前两个仓库
  - https://github.com/apache-superset/react-pivottable
    - Refactored the table renderer code to make it easier to understand
    - Added the ability to compute and show subtotals.
    - Implement barchart table
    - Implement sorting key_z_to_a
  - https://github.com/webdacjs/react-pivottable
    - Adding multivalue support.
    - Removing plotly renderers.
    - Replacing gauge charts with d3 ones.
  - https://github.com/YuyaoZhong/react-pivottable-custom
    - some customized functions based on react-pivottable, mainly for testing and demo.
    - Customized the default orders of unused attributes
  - https://github.com/davinciWangYang/react-pivottable-custom
    - Update package.json
  - https://github.com/TheDanielPBerry/react-pivottable
    - 手写类型定义
  - https://github.com/plotly/dash-pivottable
- react-pivot /MIT/955Star/202006 
  - https://github.com/davidguttman/react-pivot
  - http://davidguttman.github.io/react-pivot/
  - a data-grid component with pivot-table-like functionality for data display, filtering
  - 依赖dataframe，wildemitter，基于react15，较旧
  - 基于table标签实现
  - 典型的透视表视图
- pivot.js /753Star/BSD/201706/js
  - https://github.com/rwjblue/pivot.js
  - Build Pivot Tables from CSV/JSON Data

- S2 /1.1kStar/MIT/202302/ts
  - https://github.com/antvis/S2
  - https://s2.antv.antgroup.com/examples
  - S2是多维交叉分析领域的表格解决方案，数据驱动视图，提供底层核心库、基础组件库、业务场景库
  - 依赖 @antv/g-canvas、g-gesture、d3-interpolate

- quick-pivot /49Star/MIT/201812/js
  - https://github.com/pat310/quick-pivot
  - Quickly format data to create a pivot table
  - https://github.com/turnerniles/react-virtualized-pivot
- PivotHelper /Apache2/19Star/202007/angular
  - https://github.com/BjoernKW/PivotHelper
  - https://bjoernkw.github.io/PivotHelper/
  - a utility web app that generates Pivot tables and charts from CSV files and Microsoft Excel spreadsheets.
  - 基于angular10实现

- more-pivot
  - [How to Use Excel Pivot Tables to Organize Data](https://www.timeatlas.com/excel-pivot-tables/)
  - Excel_notes 教學檔案
    - https://github.com/jeanetsai/Excel_notes
# pivot/olap
- duckdb /7.5kStar/MIT/202212/cpp
  - https://github.com/duckdb/duckdb
  - http://www.duckdb.org/
  - DuckDB is an in-process SQL OLAP Database Management System
  - DuckDB supports arbitrary and nested correlated subqueries, window functions, collations, complex types (arrays, structs), and more. 
# pivot-computation
- ref
  - clickhouse in js

- olap-cube-js /51Star/MIT/201912/js
  - https://github.com/feonit/olap-cube-js
  - The simplest data analysis tools written in javascript. 
  - This solution is a means for extracting and replenishing data, which together with your data storage means and a means of providing aggregate data, is intended for decision making.
  - Tree structure for representing hierarchical data

- olap-in-memory /6Star/202004/js
  - https://github.com/romain-gilliotte/olap-in-memory
  - a library to manipulate OLAP cubes without relying on a database
  - All OLAP operations (slice, dice, drill-up, drill-down, ...)
  - 👉🏻 The library avoids useless allocations, slow array methods and does all the computations on TypedArrays, so it is reasonably fast.
  - However, it was built with small cubes in mind (under 100k cells): there are no pre-computed indexes, all data is kept in flat buffers, and most query operations have a O(numCells) complexity.
  - Olap in memory was written as a companion library for Monitool
  - https://github.com/medecins-du-monde/monitool
    - Monitool is an indicator monitoring application for humanitarian organisations
  - https://github.com/medecins-du-monde/monitool-frontend
    - /angular

- pivot-chart /51Star/MIT/202005/ts
  - https://github.com/ObservedObserver/pivot-chart
  - https://chspace.oss-cn-hongkong.aliyuncs.com/pivot-chart/index.html
  - 数据透视表数据展示的形式不再限于单纯的数字，使得用户可以同时拥有数据透视(旋转、切片、下钻、上卷)与可视化图表的能力。
  - pivot-chart是基于cube-core提供的前端cube计算能力搭建的。
  - 依赖cube-core、immer、react-beautiful-dnd、vega-lite
  - pivot chart is build based on cube-core: an MOLAP cube solution in js.
  - Sync Pivot Chart 的计算都发生在前端。这里叫sync其实有点不合适，因为后续优化这些计算也可以发生在webworker中。
  - Async Pivot Chart的cube计算是服务端或用户自己提供的。组件本身会帮助用户缓存一些已经计算过的结果
- cube-core /30Star/GPLv3/201912/ts/NoDeps
  - https://github.com/ObservedObserver/cube-core
  - cube-core是一个高效的Cube求解工具，你可以借助它来实现快速的Cube运算或搭建pivot table组件
  - cube-core的优势在于其在保证性能的同时，又可以支持所有复杂类指标的聚合函数：Distributive, Algebraic与Holistic(如众数、中位数、k大数)。

- Rath /347Star/AGPLv3/202211/ts/go/python
  - https://github.com/Kanaries/Rath
  - https://rath.kanaries.net/
  - Rath is an auto EDA tool (or Augmented Analytic BI), which automates exploring your dataset and discovering interesting patterns and relations
  - 主要方向是自动化数据分析/增强分析型BI，借助autoVis、因果推断、机器学习等技术帮助用户自动化掉其数据分析中的大部分过程，对外提供开源的版本Rath
- https://github.com/Kanaries/graphic-walker
  - https://graphic-walker.kanaries.net/
  - An open source alternative to Tableau.
  - The original purpose of graphic-walker is not to be a heavy BI platform, but a easy to embed, lite, plugin.
  - A grammar of graphics based visual analytic user interface where users can build visualizations from low-level visual channel encodings. (based on `vega-lite`)
- https://github.com/Kanaries/pygwalker /python
  - Turn your pandas dataframe into a Tableau-style User Interface for visual analysis
  - It integrates Jupyter Notebook (or other jupyter-based notebooks) with Graphic Walker
- https://github.com/Kanaries/web-data-loader /ts
  - allows you to load large data files in browser. 
  - It supports stream data and runs in webworker which will not block the main thread while loading the data. 
  - web-data-loader also support stream data sampling, it now support Reservoir Sampling methods.

- OLAP-cube /26Star/MIT/201709/js/单文件
  - https://github.com/fibo/OLAP-cube
  - An OLAP cube is a multidimensional array of data you can explore and analyze.

- https://github.com/ajoabraham/tiny-olap /201804/js
  - OLAP functionality for use with data visualizations. Aggregating and grouping data along key dimensions.

- https://github.com/agershun/olap /201507/js
  - extensible and embeddable JavaScript Online Analytical Processing server and library for browser and Node.js
  - 提供了多种接口
  - olap.execute(mdx); 
  - olap.xmla(xmla); 
  - olap.mdx(mdx); 

- https://github.com/agrohe21/olap4js /201301/js
  - library to talk to multiple OLAP backends from multiple frontends
  - olap4js is intended to be a common set of JS objects that can run on multiple clients and with multiple OLAP backends

- https://github.com/steelbreeze/pivot /ts/非典型
  - A minimalist pivot table library for TypeScript/JavaScript.
  - It provides a minimalist pivot table capability, slicing data into cells defined by two dimensions. 
  - This is a spin-off(副产品，派生物) from the steelbreeze/landscape project, where instead of aggregating numerical data from the pivot cube, non-numerical data is needed.
  - It also focuses just on dimension and cube creation, without any layout considerations keeping it small and unopinionated.

- https://github.com/vinnik-dmitry07/db-comp
  - A comparison of DuckDB columnar database and relational PostgreSQL.

- https://github.com/gratico/satya /inactive
  - WIP: Satya is a distributed database using Apache Arrow as a Storage format and aims to support both OTLP(transaction processing) and OLAP(analytical processing) workloads. 
  - 依赖 duckdb-wasm、apache-arrow

- https://github.com/codenautas/sql-tools /js
  - Transfor a SQL sentence in a SQL with totals.

- deepscatter /186Star/MIT/202301/ts
  - https://github.com/nomic-ai/deepscatter
  - This is an evolving library for displaying more points than are ordinarily possible over the web.
  - 依赖apache-arrow, d3-zoom, regl, rbush-3d
  - All data is sent in the Apache Arrow `feather` format, in a custom quadtree(四叉树) format that makes it possible to only load data as needed on zoom
    - This is a 2d library. No fake 3d.
    - The central zoom state is handled by d3-zoom.
  - Most rendering is done in custom layers using WebGL, with a buffer management strategy handled by `regl`. 
  - Almost all grammar-of-graphics transforms such are handled on the GPU, which allows for interpolated transitions with calculations done in parallel.
# more-olap
- https://github.com/rilldata/rill-developer /202212/ts/svelte/go
  - https://docs.rilldata.com/
  - transform your datasets with SQL and create powerful, opinionated dashboards.
  - powered by Sveltekit & DuckDB
  - works with your local and remote datasets – imports and exports Parquet and CSV

- https://github.com/altair-viz/altair
  - Declarative statistical visualization library for Python
  - built on top of the powerful Vega-Lite JSON specification.
- https://github.com/turnerniles/react-virtualized-pivot
  - /94Star/MIT/201804
  - a React.js pivot UI built on top of react-virtualized and quick-pivot
- https://github.com/pat310/quick-pivot
  - /48Star/MIT/201903
  - Quickly format data to create a pivot table

- https://github.com/antonycourtney/tad /202211/ts
  - Tad desktop application enables you to quickly view and explore tabular data in several of the most popular tabular data file formats: CSV, Parquet, and SQLite and DuckDb database files. 
  - Internally, the application is powered by an in-memory instance of DuckDb, a fast, embeddable database engine optimized for analytic queries.
  - The core of Tad is a React UI component that implements a hierarchical pivot table that allows you to specify a combination of pivot, filter, aggregate, sort, column selection
  - Tad uses SlickGrid for rendering the data grid. 

- cube.js /14.4kStar/MIT+apache2/202301/ts+rust
  - https://github.com/cube-js/cube.js
  - https://cube.dev/docs/
  - Headless Business Intelligence for Building Data Applications
  - modular framework to build analytical web applications
  - Cube.js was designed to work with Serverless Query Engines like AWS Athena and Google BigQuery.
  - [Cube.js is now Cube_202208](https://cube.dev/blog/cube-js-is-now-cube)
    - We started Cube as an open-source analytics framework in 2019. written in js
    - Since then, we have written more lines of code in Rust than in JavaScript and moved from npm to Docker for distribution. 
    - we’re going to migrate the rest of Cube’s codebase to it over time.
  - Most modern RDBMS work with Cube.js as well and can be tuned for adequate performance.
  - Cube.js Backend
    - Schema. It acts as an ORM for analytics and allows to model everything from simple counts to
    - Query Orchestration and Cache. It optimizes query execution by breaking queries into small
    - API Gateway. It provides idempotent long polling API which guarantees analytic query results delivery without request time frame limitations
  - Cube.js Frontend
    - Javascript Client. Сore set of methods to access Cube.js API Gateway 
    - React, Angular and Vue. Framework specific wrappers for Cube.js API.
- https://github.com/square/cube
  - /3.9kStar/Apache2/201407
  - Cube is a system for collecting timestamped events and deriving metrics. 
  - By collecting events rather than metrics, Cube lets you compute aggregate statistics post hoc. 
  - Cube is built on MongoDB

- https://github.com/ankoh/dashql /202203/ts+cpp/inactive
  - Scalable Analytics Dashboards powered by WebAssembly

- https://github.com/flexmonster/flexmonster-mongodb-connector
  - Flexmonster Pivot is a powerful JavaScript tool for interactive web reporting. 
  - It allows you to visualize and analyze data from JSON, CSV, SQL, NoSQL, Elasticsearch, and OLAP data sources quickly and conveniently.
