---
title: lib-list-ag-grid-events
tags: [ag-grid, events]
created: '2020-09-17T17:18:09.303Z'
modified: '2021-05-13T02:43:23.818Z'
---

# lib-list-ag-grid-events

# EventService

- 全局单例的事件中心

- `Events.EVENT_MODEL_UPDATED`
  - modelUpdated 事件会更新
  - dispatched from
  - add listeners

# 重要事件

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

- `Events.EVENT_DISPLAYED_COLUMNS_CHANGED`
  - displayedColumnsChanged 事件会更新表头的样式，会重新渲染数据行的单元格
  - dispatched from
    - `columnController.updateGroupsAndDisplayedColumns()`
  - add listeners
    - headerContainer.onDisplayedColumnsChanged
      - headerContainer PostConstruct时注册
      - 可见表头列变化时，更新grid表格的总宽度
    - headerRowComp.onDisplayedColumnsChanged
      - 由headerContainer触发，headerRowComp的PostConstruct时注册
      - 更新viewport中的表头列和表头行宽度值
    - gridPanel.onDisplayedColumnsChanged
      - gridPanel PostConstruct时注册
      - 更新pinned容器尺寸、表头高度、水平视口、滚动条可见性
    - rowRenderer.onDisplayedColumnsChanged
      - gridPanel PostConstruct时注册
      - 更新this.pinningLeft/Right的属性值
    - rowComp.onDisplayedColumnsChanged
      - init方法中注册
      - 重新渲染一行的所有单元格，分左中右3个容器
    - cellComp.onDisplayColumnsChanged
      - cellComp的构造函数中调用
      - 更新合并列单元格的width和left样式值
    - selectAllFeature.showOrHideSelectAll
      - selectAllFeature PostConstruct时注册
      - 更新全选框显示或隐藏的状态值
    - checkboxSelectionComponent.showOrHideSelect
      - init方法中注册
      - 设置一个checkbox的显示或隐藏状态值

- `Events.EVENT_COLUMN_EVERYTHING_CHANGED`
  - columnEverythingChanged 事件会触发开始执行重渲染数据行
  - dispatched from
    - `columnController.setColumnDefs()`
    - `columnController.setColumnState()`
  - add listeners 
    - clientSideRowModel.refreshModel (Constants.STEP_EVERYTHING)
      - PostConstruct时注册
      - 重新计算数据rowModel，然后触发 modelUpdated 事件
    - FocusController.onColumnEverythingChanged
      - PostConstruct时注册
      - 根据新数据，判断是继续保持焦点单元格，还是丢弃旧的焦点单元格
    - UndoRedoService.clearStacks
    - InfiniteRowModel.onColumnEverything

- `Events.EVENT_MODEL_UPDATED`
  - modelUpdated 事件会更新数据分页，导致更新数据行
  - dispatched from
    - `clientSideRowModel.refreshModel()`
  - add listeners
    - selectAllFeature.onModelChanged
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
  - paginationChanged 事件会更新 所有行组件
  - dispatched from
    - `PaginationProxy.onModelUpdated`
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

- `Events.EVENT_ROW_DATA_CHANGED`
  - rowDataChanged 事件会更新
  - dispatched from
    - `clientSideRowModel.setRowData`
  - add listeners
