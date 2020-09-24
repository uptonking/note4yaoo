---
title: lib-ag-grid-latest-todo
tags: [ag-grid, lib]
created: '2020-09-16T12:35:28.597Z'
modified: '2020-09-17T17:17:58.423Z'
---

# lib-ag-grid-latest-todo

## discuss

- 考虑移除部分事件监听器，或延迟添加事件监听器，监听器加早了数据未装载会执行无效事件，但似乎对性能影响不大

- 事件的跳转全靠搜索类似 `Events.EVENT_GRID_COLUMNS_CHANGED` 字符串常量

- validate这类方法太长，如gridOptions、checkDeprecated、module是否注册

- Lazy Height Calculation
  - The vertical scroll range (how much you can scroll over) will change dynamically to fit the rows. 
  - If scrolling by dragging the scroll thumb with the mouse, the scroll thumb will not follow the mouse. 

## optimization

## extend

- Undo/Redo feature is designed to be a recovery mechanism for user editing mistakes. 
  - Performing grid operations that change the row/column order, e.g. sorting, filtering and grouping, will clear the undo/redo stacks.

## debug

- import ag-grid的ts源码用babel转义进行开发调试时出现的error
  - `"main": "./src/ts/main.ts"` ，直接使用@ag-grid-community/core的源码编译会抛出异常
  - `"main": "./dist/es6/main.js"` 使用编译后的js文件则能正常编译，以此可作为临时过渡方案

``` 
Uncaught ReferenceError: Cannot access 'Component' before initialization
  at Module.Component (component.ts:3)
  at eval (agAbstractLabel.ts?deaf:14)
  at Module.../../community-modules/core/src/ts/widgets/agAbstractLabel.ts (main.js:4222)
```

- babel编译ag-grid源码中的types出现warning
  - 这些warning相关的导出内容都是type类型定义，可忽略

``` 
WARNING in ../../community-modules/core/src/ts/main.ts 13:0-84
export 'ColumnState' (reexported as 'ColumnState') was not found in './columnController/columnController' (possible exports: ColumnController)
```
