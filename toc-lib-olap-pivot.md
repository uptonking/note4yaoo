---
title: toc-lib-olap-pivot
tags: [lib, olap, pivot, toc]
created: '2020-07-13T02:39:21.789Z'
modified: '2020-10-22T06:50:36.740Z'
---

# toc-lib-olap-pivot

## pivot

- react-pivot /MIT/955Star/202006 
  - https://github.com/davidguttman/react-pivot
  - http://davidguttman.github.io/react-pivot/
  - a data-grid component with pivot-table-like functionality for data display, filtering
  - 基于table标签实现
  - 典型的透视表视图
  - 依赖dataframe，wildemitter，基于react15，较旧
- react-pivottable /MIT/629Star/202006
  - https://github.com/plotly/react-pivottable
  - https://react-pivottable.js.org/
  - React-based drag'n'drop pivot table with Plotly.js charts
  - 基于table标签实现
  - 创建透视表后，可快速展示图表
  - 依赖react-draggable, sortablejs
- pivottable /MIT/3.5kStar/201902/CoffeeScript
  - https://github.com/nicolaskruchten/pivottable
  - https://pivottable.js.org/examples/
  - a JS Pivot Table library with drag'n'drop functionality built on top of jQuery/jQueryUI
  - 基于table标签实现
  - 依赖jquery
- PivotHelper /Apache2.0/19Star/202007/angular
  - https://github.com/BjoernKW/PivotHelper
  - https://bjoernkw.github.io/PivotHelper/
  - a utility web app that generates Pivot tables and charts from CSV files and Microsoft Excel spreadsheets.
  - 基于angular10实现

## more-olap

- https://github.com/altair-viz/altair
  - Declarative statistical visualization library for Python
  - built on top of the powerful Vega-Lite JSON specification.
- https://github.com/turnerniles/react-virtualized-pivot
  - /94Star/MIT/201804
  - a React.js pivot UI built on top of react-virtualized and quick-pivot
- https://github.com/pat310/quick-pivot
  - /48Star/MIT/201903
  - Quickly format data to create a pivot table
- https://github.com/ObservedObserver/pivot-chart
  - /20Star/MIT/202005
  - pivot chart is build based on cube-core: an MOLAP cube solution in js.
- https://github.com/ObservedObserver/cube-core
  - /25Star/GPLv3/201912
  - 无依赖
  - cube-core是一个高效的Cube求解工具，你可以借助它来实现快速的Cube运算或搭建pivot table组件
  - cube-core的优势在于其在保证性能的同时，又可以支持所有复杂类指标的聚合函数：Distributive, Algebraic与Holistic(如众数、中位数、k大数)。
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
