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
# tips
- 支持外部控制的options
  - manualFiltering
  - manualSorting
  - manualGrouping
  - manualPagination
  - manualExpanding

- ~~table和virtual都用到了react forceRender模式~~
# architecture
- init createTable 的初始化流程
  - 计算插件options，合并feature options
  - 添加插件initialState到全局initialState
  - add core props and methods to table instance
  - 逐个执行插件的createTable方法，将table实例作为参数传入来增强

- 💡 feature-state的状态由外部控制
  - 每次useReactTable都会将外部最新状态如sorting，通过 table.setOptions合并到table.options.state.featureState
  - `table.getState() === table.options.state` // true
  - setOptions合并state后table内就可以取到最新state
# plugin/feature
- feature的设计
  - defaultOptions，以及添加到table options
  - initialState，以及更新table.state
  - createTable在init时增强table，在table对象增加api
  - createColumn在init时增强column对象
  - createRow在init时增强row对象

- feature的options和state都会在createTable初始化时合并到table.options/state

- 👉🏻 feature.state的更新
  - feature.state变化时，不会触发table.state的onStateChange方法
    - 注意feature的defaultOptions是会触发onStateChange方法的，但用户自己提供的，需要手动触发onSortingChange
  - options的部分只用来更新ui，table.options.onColumnVisibilityChange()
  - 将操作feature.state的方法直接暴露出去，如getToggleAllColumnsVisibilityHandler，暴露的是方法，而不是action对象
# model-layer
- data => model
  - 计算rowModel的入口 `const rowModel = table.getRowModel(); `，手动触发
  - rowModel对象在table.state之外，通过table.getRowModel()获取

```typescript
export interface RowModel<TData extends RowData> {
  rows: Row<TData>[];
  flatRows: Row<TData>[];
  rowsById: Record<string, Row<TData>>;
}
```

- 计算rowModel的顺序 💡 从下向上
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
  - 提供了`manual*`控制属性
# virtual
- 触发ui更新的原因是options.onChange()，执行时机包括
  - observeElementRect
  - observeElementOffset
  - _measureElement/measure
  - calculateRange
  - 可考虑通过useSyncStore订阅这些值来去掉onChange

- 固定高度的原理
  - 在目标区域上下方显示invisible元素高度和

- 动态计算内容元素高度的原理
  - 利用callback ref在首次渲染时计算元素高度
  - 首次渲染时注册scroll事件，让滚动时执行
