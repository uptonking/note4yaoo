---
title: lib-excel-luckysheet-examples
tags: [examples, luckysheet, toc]
created: 2022-08-13T18:32:43.761Z
modified: 2022-08-21T10:37:45.959Z
---

# lib-excel-luckysheet-examples

# popular

- fortune-sheet /1.4kStar/MIT/202208/ts
  - https://github.com/ruilisi/fortune-sheet
  - https://ruilisi.github.io/fortune-sheet-docs/zh/guide/
  - https://ruilisi.github.io/fortune-sheet-demo
  - FortuneSheet是一款开箱即用的类似Excel和Google Sheets的javascript表格组件。
  - 本项目源于 Luckysheet，并继承了它的很多代码。我们为将其转换为typescript做了很多努力，并且解决了一些原项目设计层面的问题。
  - 完全使用typescript编写。
  - 去掉了 jQuery 的依赖, 用React/Vue + immer来管理DOM和状态。
  - 同页面支持多个实例。目前只支持单个实例，因为有全局状态
  - 避免在window对象上存储数据。
  - 用一个forked handsontable/formula-parser 来处理公式计算。
  - 用SVG代替iconfont的图标，因为iconfont的图标对其他开发者而言很不方便改动。
  - 容器外面不创建可见的页面元素。
  - 数据结构总体兼容Luckysheet
  - 👀 未迁移luckysheet的功能：透视表、图表、协作、截图、拖拽
  - [Is there any plan to make a Vue version? soon](https://github.com/ruilisi/fortune-sheet/issues/14)
# more-luckysheet
