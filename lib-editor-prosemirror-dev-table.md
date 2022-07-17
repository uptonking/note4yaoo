---
title: lib-editor-prosemirror-dev-table
tags: [editor, prosemirror, table]
created: 2021-06-16T07:09:12.311Z
modified: 2021-06-16T07:09:26.009Z
---

# lib-editor-prosemirror-dev-table

# guide

- pm-tables-xp
  - resize浏览器窗口，不会触发updateState()
  - resize column会触发updateState()

- pm-tables
  - 提供了符合html table元素schema
  - 提供了CellSelection，支持跨单元格的选择、设置样式
  - 提供了commands工具
  - 提供了copy-paste工具
  - 提供了fixTables工具，能修复错误col-spans, row-spans导致的overlap问题

- pm-tables-pros
  - document中插入的table直接可编辑单元格，开箱即用
  - 支持column-resizing

- pm-tables-cons
  - 表格插件间的耦合度很高，自定义样式难度大

- tips
# pieces
