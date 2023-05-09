---
title: lib-excel-tanstack-table-codebase
tags: [codebase, lib, tanstack-table]
created: 2020-08-21T09:01:31.263Z
modified: 2022-08-21T10:19:58.756Z
---

# lib-excel-tanstack-table-codebase

# guide

- tanstack-query
- tanstack-virtual

- tips
  - 注意row id的类型在应用层决定，可能为number
    - dnd-kit的id默认string，注意类型转换
# not-yet
- row.getAllCells的args为什么只有leafColumns

- e.persist()
  - getToggleSortingHandler
# codebase
- table和virtual都用到了react forceRender模式

- createTable 的初始化流程
  - 计算插件options，合并feature options
  - 添加插件initialState到全局initialState
  - add core props and methods to table instance
  - 逐个执行插件的createTable方法，将table实例作为参数传入来增强

- 一个feature的设计
  - 添加到table options
  - 在table、column、header暴露api
# architecture/dataflow
- data => model
  - 计算rowModel的入口 `const rowModel = table.getRowModel(); `，手动触发
- 计算rowModel的顺序
  - table.getPaginationRowModel(); 
  - table.getPrePaginationRowModel(); 
  - table.getExpandedRowModel(), 
  - table.getPreExpandedRowModel(); 
  - table.getSortedRowModel(), 
  - table.getPreSortedRowModel(); 
  - table.getGroupedRowModel(), 
  - table.getPreGroupedRowModel(); 
  - table.getFilteredRowModel(), 
  - table.getPreFilteredRowModel(); 
  - table.getCoreRowModel(), 

- serverModel
# virtual
- 固定高度的原理
  - 在目标区域上下方显示invisible元素高度和

- 动态计算内容元素高度的原理
  - 利用callback ref在首次渲染时计算元素高度
  - 首次渲染时注册scroll事件，让滚动时执行
