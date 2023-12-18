---
title: lib-excel-ospreadsheet-dev
tags: [canvas, excel, ospreadsheet]
created: 2023-06-07T22:36:21.411Z
modified: 2023-06-07T22:37:07.042Z
---

# lib-excel-ospreadsheet-dev

# guide

- pros
  - 架构清晰可扩展
  - 支持协作，基于ot
  - 支持selective undo，支持branch
  - 支持添加自定义函数，addFunction("MY. FUNC", MY_FUNC); 

- cons
  - 视图层基于odoo自研的owl
  - 不支持外部数据源
  - undo和collab的插件不够解耦
  - 透视表和图表功能弱于luckysheet

- features
  - license LGPLv3
  - 支持公式formula
  - 支持图表，基于chart.js.v2
  - 支持批量删除rows，但未暴露transaction

- tips
# dev

# examples
- https://github.com/hokolomopo/o-spreadsheet-chrome-tools
  - Clear & Reload o-spreadsheet with a keyboard shortcut

- https://github.com/hokolomopo/o-spreadsheet-demo-data-generator
  - copy the results in results/demoData.json

- https://github.com/rrahir/spreadsheet-tools
  - O-spreadsheet deployment tooling
# more
