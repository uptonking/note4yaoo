---
title: lib-luckysheet-dev
tags: [excel, lib, luckysheet, spreadsheet]
created: '2020-10-19T16:48:46.206Z'
modified: '2020-10-19T16:49:51.766Z'
---

# lib-luckysheet-dev

## guide

- luckysheet-repos
  - https://github.com/mengshukeji/Luckysheet
    - an online spreadsheet like excel
    - 基于div实现
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
