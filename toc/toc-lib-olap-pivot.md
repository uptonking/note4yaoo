---
title: toc-lib-olap-pivot
tags: [lib, olap, pivot, toc]
created: 2020-07-13T02:39:21.789Z
modified: 2020-10-22T06:50:36.740Z
---

# toc-lib-olap-pivot

# pivot

- pivottable /3.5kStar/MIT/201902/CoffeeScript
  - https://github.com/nicolaskruchten/pivottable
  - https://pivottable.js.org/examples/
  - a JS Pivot Table library with drag'n'drop functionality built on top of jQuery/jQueryUI
- react-pivottable /852Star/MIT/202011/js
  - https://github.com/plotly/react-pivottable
  - https://react-pivottable.js.org/
  - a React-based pivot table library with drag'n'drop functionality. 
  - It is a React port of the jQuery-based PivotTable.js by the same author.
  - 基于table标签实现
  - 创建透视表后，可快速展示图表
  - 依赖react-draggable, sortablejs
  - 基于table标签实现
  - 依赖jquery
  - https://github.com/plotly/dash-pivottable
- pivot.js /753Star/BSD/201706/js
  - https://github.com/rwjblue/pivot.js
  - Build Pivot Tables from CSV/JSON Data
- react-pivot /MIT/955Star/202006 
  - https://github.com/davidguttman/react-pivot
  - http://davidguttman.github.io/react-pivot/
  - a data-grid component with pivot-table-like functionality for data display, filtering
  - 依赖dataframe，wildemitter，基于react15，较旧
  - 基于table标签实现
  - 典型的透视表视图
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
# pivot-computation
- ref
  - clickhouse in js

- olap-cube-js /51Star/MIT/201912/js
  - https://github.com/feonit/olap-cube-js
  - The simplest data analysis tools written in javascript. This solution is a means for extracting and replenishing data, which together with your data storage means and a means of providing aggregate data, is intended for decision making.
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

- OLAP-cube /26Star/MIT/201709/js/单文件
  - https://github.com/fibo/OLAP-cube
  - An OLAP cube is a multidimensional array of data you can explore and analyze.

- https://github.com/ajoabraham/tiny-olap /201804/js
  - OLAP functionality for use with data visualizations. Aggregating and grouping data along key dimensions.

- https://github.com/agershun/olap /201507/js
  - extensible and ambeddable JavaScript Online Analytical Processing server and library for browser and Node.js
  - 提供了多种接口
  - olap.execute(mdx); 
  - olap.xmla(xmla); 
  - olap.mdx(mdx); 

- https://github.com/agrohe21/olap4js /201301/js
  - library to talk to multiple OLAP backends from multiple frontends
  - olap4js is intended to be a common set of JS objects that can run on multiple clients and with multiple OLAP backends

- https://github.com/steelbreeze/pivot
  - A minimalist pivot table library for TypeScript/JavaScript.
  - It provides a minimalist pivot table capability, slicing data into cells defined by two dimensions. 
  - This is a spin-off(副产品，派生物) from the steelbreeze/landscape project, where instead of aggregating numerical data from the pivot cube, non-numerical data is needed.
  - It also focuses just on dimension and cube creation, without any layout considerations keeping it small and unopinionated.

- https://github.com/vinnik-dmitry07/db-comp
  - A comparison of DuckDB columnar database and relational PostgreSQL.

- https://github.com/codenautas/sql-tools /js
  - Transfor a SQL sentence in a SQL with totals.
# more-olap
- https://github.com/altair-viz/altair
  - Declarative statistical visualization library for Python
  - built on top of the powerful Vega-Lite JSON specification.
- https://github.com/turnerniles/react-virtualized-pivot
  - /94Star/MIT/201804
  - a React.js pivot UI built on top of react-virtualized and quick-pivot
- https://github.com/pat310/quick-pivot
  - /48Star/MIT/201903
  - Quickly format data to create a pivot table

- https://github.com/cube-js/cube.js
  - /MIT/9kStar/202010
  - https://cube.dev/docs/
  - modular framework to build analytical web applications
  - Cube.js was designed to work with Serverless Query Engines like AWS Athena and Google BigQuery. 
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
- https://github.com/fibo/OLAP-cube
  - /17Star/MIT/202001
  - An OLAP cube is a multidimensional array of data you can explore and analyze

- https://github.com/ankoh/dashql /ts+cpp
  - Scalable Analytics Dashboards powered by WebAssembly
