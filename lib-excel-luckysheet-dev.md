---
title: lib-excel-luckysheet-dev
tags: [excel, grid, lib, luckysheet]
created: 2020-10-19T16:48:46.206Z
modified: 2022-08-21T09:57:46.814Z
---

# lib-excel-luckysheet-dev

# guide


- https://github.com/ruilisi/fortune-sheet
  - 本项目源于 Luckysheet，并继承了它的很多代码。我们为将其转换为typescript做了很多努力，并且解决了一些原项目设计层面的问题。
  - 完全使用typescript编写。
  - 同页面支持多个实例。
  - 避免在window对象上存储数据。
  - 去掉了 jQuery 的依赖, 用原生 React / Vue + immer 来管理Dom和状态。
  - 用一个forked handsontable/formula-parser 来处理公式计算。
  - 用SVG代替iconfont的图标，因为iconfont的图标对其他开发者而言很不方便改动。
  - 容器外面不创建可见的页面元素。

- luckysheet-repos
  - https://github.com/mengshukeji/Luckysheet
    - https://dream-num.github.io/LuckysheetDocs/zh/guide/
    - an online spreadsheet like excel
    - 基于canvas实现
    - 依赖jspdf
    - 最好通过 iframe 使用 - 嵌入到页面会污染当前环境
  - https://github.com/mengshukeji/Luckyexcel
    - an excel import and export library adapted to Luckysheet.
    - only supports .xlsx format files (not .xls).
  - https://github.com/mengshukeji/luckysheet-react
    - a simple project that shows the use of luckysheet in a React project

## ui结构层次

- `<div id="luckysheet" style="margin:0px;padding:0px;position:absolute;width:100%;height:100%;left: 0px;top: 0px;"></div>`
- `<div id="luckysheet-sheettable_0" class="luckysheet-cell-sheettable" style="height: 936px; width: 2072px; cursor: default;"></div>`

```CSS
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

# blogging

## [LuckySheet源码分析目录_舟翁_202011](https://blog.csdn.net/u010593516/article/details/109604358)

1. 源代码项目结构
2. core.js源码分析
3. 函数实现原理
4. 页面加载过程
5. 主界面绘制draw.js
6. 界面刷新策略fresh.js

## [MiniSheet开发记录目录_舟翁_202102](https://blog.csdn.net/u010593516/article/details/113743472)

- https://gitee.com/zhouweng/mini_sheet

Day 1 为什么会有mini_sheet
Day 2 Win10系统配置开发环境
Day 3 如何看源码学习
Day 4 编译工具说明
Day 5 第一个最小化系统
Day 6 让表格动起来
Day 7 选择一个单元格
Day 8 双击单元格编辑
Day 9 编辑单元格回写内存
Day10 点亮单元格行列标题
Day11 拖动选择单元格区域
Day12 从excel文件复制粘贴
Day13 鼠标右键菜单复制粘贴
Day14 在页面顶部显示工具条
Day15 一次规模比较大的重构
Day16 单元格样式(背景色/下划线/删除线等)
Day17 工具条设置单元格样式
Day18 工具条设置字体大小
Day19 如何做合并单元格
Day20 左右对齐、上下对齐
Day21 工具条设置单元格颜色
【完结篇】Day22 行高和列宽的设置
