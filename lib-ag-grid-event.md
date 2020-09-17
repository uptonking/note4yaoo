---
title: lib-ag-grid-event
tags: [ag-grid, event]
created: '2020-09-17T17:18:09.303Z'
modified: '2020-09-17T17:19:22.921Z'
---

# lib-ag-grid-event

## EventService

- 全局单例的事件中心

## 重要事件

- `Events.EVENT_GRID_COLUMNS_CHANGED`
  - gridColumnsChanged事件会触发创建或重渲染所有表头行
  - dispatch from `columnController.updateGridColumns()`
  - add listeners from
    - headerContainer.onGridColumnsChanged
      - PostConstruct依赖注入时注册
    - headerRowComp.onGridColumnsChanged
      - PostConstruct依赖注入时注册
    - rowRenderer.registerCellEventListeners
      - gridPanel PostConstruct依赖注入时注册

- `Events.EVENT_COLUMN_EVERYTHING_CHANGED`
  - columnEverythingChanged事件会触发重渲染数据行
