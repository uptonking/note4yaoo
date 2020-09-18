---
title: lib-ag-grid-event
tags: [ag-grid, event]
created: '2020-09-17T17:18:09.303Z'
modified: '2020-09-17T17:19:22.921Z'
---

# lib-ag-grid-event

## EventService

- 全局单例的事件中心

- `Events.EVENT_MODEL_UPDATED`
  - modelUpdated 事件会更新
  - dispatched from
  - add listeners

## 重要事件

- `Events.EVENT_GRID_COLUMNS_CHANGED`
  - gridColumnsChanged 事件会触发创建或重渲染所有表头行，并给单元格列添加事件监听器函数
  - dispatched from
    - `columnController.updateGridColumns()`
  - add listeners
    - headerContainer.onGridColumnsChanged
      - headerContainer PostConstruct时注册
      - 先执行removeHeaderRowComps()，再执行createHeaderRowComps()，创建所有表头行
    - headerRowComp.onGridColumnsChanged
      - 由headerContainer触发，headerRowComp的PostConstruct时注册
      - 通过element.removeChild移除dom元素，再执行HeaderRowComp的destroyBean钩子函数
    - rowRenderer.registerCellEventListeners
      - gridPanel PostConstruct时注册
      - 用来重新给单元格列添加事件监听器

- `Events.EVENT_COLUMN_EVERYTHING_CHANGED`
  - columnEverythingChanged 事件会触发重渲染数据行
  - dispatched from
    - `columnController.setColumnDefs()`
    - `columnController.setColumnState()`
  - add listeners 
    - ClientSideRowModel.refreshModel (Constants.STEP_EVERYTHING)
      - PostConstruct时注册
      - 重新计算数据rowModel，然后触发 modelUpdated 事件
    - FocusController.onColumnEverythingChanged
      - PostConstruct时注册
      - 根据新数据，判断是继续保持焦点单元格，还是丢弃旧的焦点单元格
    - UndoRedoService.clearStacks
    - InfiniteRowModel.onColumnEverything

- `Events.EVENT_MODEL_UPDATED`
  - modelUpdated 事件会更新数据分页，进而更新数据行
  - dispatched from
    - `ClientSideRowModel.refreshModel()`
  - add listeners
    - SelectAllFeature.onModelChanged
      - postConstruct时注册
      - 会更新复选框的状态
    - PaginationProxy.onModelUpdated
      - postConstruct时注册
      - 计算分页数据，再触发 paginationChanged 事件
    - RowComp.onModelUpdated
      - init方法中注册
      - 添加或删除首尾行样式名
    - UndoRedoService
    - InfiniteRowModel

- `Events.EVENT_PAGINATION_CHANGED`
  - paginationChanged 事件会更新
  - dispatched from
    - PaginationProxy.onModelUpdated
  - add listeners
    - PaginationComp.onPaginationChanged
      - PostConstruct时注册
      - 更新当前页的页码和当前页的首位行索引号 
    - RowComp.onPaginationChanged
      - init方法中注册
      - 当前页页面更新时，更新顶部行对象
    - rowRenderer.onPageLoaded
      - rowRenderer.registerGridComp执行时注册，发生在GridPanel的PostConstruct过程中
      - 当前页加载完成后，手动调用 modelUpdated 函数，重新渲染所有行组件
