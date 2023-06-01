---
title: lib-excel-luckysheet-docs
tags: [docs, luckysheet]
created: 2020-10-19T17:18:33.770Z
modified: 2022-08-21T09:57:51.074Z
---

# lib-excel-luckysheet-docs

# [Luckysheet](https://github.com/mengshukeji/Luckysheet)

- Luckysheet是用纯JavaScript编写的前端表格库
- 基于canvas实现的表格
- [在线示例](https://mengshukeji.github.io/LuckysheetDemo/)
  - https://mengshukeji.gitee.io/luckysheetdemo/


# 整体配置

- 初始化表格时，可以设置一个对象配置串 `options` 来自定义配置Luckysheet表格。
- 这里的 `options` 配置项会作用于整个表格，特别的，单个sheet的配置则需要在 `options.data` 数组中，分别设置对应更详细的参数

# 工作表配置

- 表格初始化完成之后，通过方法 `luckysheet.getAllSheets()` 可以获取所有工作表的配置信息。

# 单元格

- 单元格是Luckysheet中最基本的单位，每个单元格都会保存为一个对象
- 一个工作表的数据则会保存为一个由单元格对象组成的二维数组，并存入当前工作表的 `luckysheetfile[i].data` 中。

# 表格操作

- 每一次操作都会保存历史记录，用于撤销和重做
- 如果在表格初始化的时候设置了 `allowUpdate` 为true和 `updateUrl` 数据更新地址，则会通过websocket将操作实时更新到后台，并且支持共享编辑。
