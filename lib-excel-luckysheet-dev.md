---
title: lib-excel-luckysheet-dev
tags: [excel, grid, lib, luckysheet]
created: 2020-10-19T16:48:46.206Z
modified: 2022-08-21T09:57:46.814Z
---

# lib-excel-luckysheet-dev

# guide

# codebase

- luckysheet-repos
  - https://github.com/mengshukeji/Luckysheet
    - an online spreadsheet like excel
    - 基于canvas实现
    - 依赖jspdf
  - https://github.com/mengshukeji/Luckyexcel
    - an excel import and export library adapted to Luckysheet.
    - only supports .xlsx format files (not .xls).
  - https://github.com/mengshukeji/luckysheet-react
    - a simple project that shows the use of luckysheet in a React project

## ui结构层次

- `<div id="luckysheet" style="margin:0px;padding:0px;position:absolute;width:100%;height:100%;left: 0px;top: 0px;"></div>`
- `<div id="luckysheet-sheettable_0" class="luckysheet-cell-sheettable" style="height: 936px; width: 2072px; cursor: default;"></div>`

``` CSS
.luckysheet-cell-sheettable {
  position: relative;
  text-align: left;
  font-size: 11pt;
  color: #000;
  text-decoration: none;
}

.luckysheet * {
  box-sizing: initial;
  outline: 0;
}
```

# pieces

- ## [hacker news: Luckysheet, an open-source spreadsheet ](https://news.ycombinator.com/item?id=23994619)
- One reason I prefer Apple Numbers to Excel is that in Numbers you arrange tables on a canvas. 
  - The tables can refer to each other. 
  - I think it makes it easier to work with, for example, an input table and an output table because they are separate entities and not just different ranges on the same grid. 
  - It’s similar to how some websites enable you to configure a dashboard view of multiple tables and charts.
  - I’m wondering if the Numbers approach might work better. 
  - In particular it might be more natural for dynamic arrays because they would not “overlay” a range of cells.
  - They would be their own dynamically resizing table on the canvas.
- The main reason I tend to avoid Google Sheets is that they're slow. Slow to open, slow to update more complex sheets
