---
title: ing-solution-datable
tags: [pm, solution, table]
created: '2019-05-15T03:30:55.244Z'
modified: '2020-07-14T10:25:13.843Z'
---

# ing-solution-datable

- A handy/efficient data table to pivot your data
  - 用更加灵活的表格来透视数据

## todo

- create ag-list from ag-grid
  - ag-grid/react-table
- charting
  - d3
- bi/olap/search
  - superset/kibana

## features

- theme
- usecase-component
  - file-explorer
  - search-view

## ideas

- ui设计
  - 表格左边放置过滤器
  - 类似小程序的布局 layout-for-app
  - list/grid view toggle 

- animation
  - 显示类似gif效果，可预设数据滚动动画，非常interactive
    - 可考虑定时更新
- 其他特性或细节
  - 竖向选择某列上连续的部分单元格

- pivoting
  - 在ag-grid表格ui中预设bi分析工具
    - 可参考searchkit、dejavu、kibana、superset、tableau
- charting
  - 在ag-grid表格之上的新图层支持可拖拽的图表编辑器builder
    - 支持将新图层渲染到表格容器知之外网，如渲染到document.body
- location
  - map layer
- time-series
  - autoplay
- graph
  - uncover the uncommonly common relationships in your data.
- exploring
  - explore the data properties that significantly influence them with unsupervised machine learning features.

- data-mini-app小程序
  - crud
  - dejavu: imdb、hacker news、airbeds
  - reactiveapps: booksearch、dashboard
  - 结构：主页概览、数据浏览、要点分析

## grape-trellis

- kbd键盘字母特殊显示

## Excelbox

- A tool for fast pivoting data list in memory. 快速进行数据分组聚合的工具库

## reference

### jackson-core & jackson-databind

- 通过JsonFactory创建parser和generator
  - `createParser(InputStream in)`
  - The input stream will not be owned by the parser
  - 解析器不直接拥有stream，通过拥有IOContext来操作流
