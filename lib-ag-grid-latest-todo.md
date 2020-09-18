---
title: lib-ag-grid-latest-todo
tags: [ag-grid, lib]
created: '2020-09-16T12:35:28.597Z'
modified: '2020-09-17T17:17:58.423Z'
---

# lib-ag-grid-latest-todo

## discuss

- 移除部分事件监听器，或延迟添加事件监听器，监听器加早了会执行空事件，似乎对性能影响不大

- `"main": "./src/ts/main.ts"` ，直接使用@ag-grid-community/core的源码编译会抛出异常
  - `"main": "./dist/es6/main.js"` 使用编译后的js文件则能正常编译，以此可作为临时过渡方案

``` 
Uncaught ReferenceError: Cannot access 'Component' before initialization
  at Module.Component (component.ts:3)
  at eval (agAbstractLabel.ts?deaf:14)
  at Module.../../community-modules/core/src/ts/widgets/agAbstractLabel.ts (main.js:4222)
```

- 事件的跳转全靠搜索类似 `Events.EVENT_GRID_COLUMNS_CHANGED`

## optimization

## extend
