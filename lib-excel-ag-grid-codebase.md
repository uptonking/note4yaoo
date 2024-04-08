---
title: lib-excel-ag-grid-codebase
tags: [ag-grid, codebase, lib]
created: 2020-08-21T09:00:56.176Z
modified: 2022-08-21T09:54:02.990Z
---

# lib-excel-ag-grid-codebase

# overview

# 🏘️ architecture
- init
  - Grid入口类初始化时
    - 会初始化很多基础类，注册很多事件
    - 会执行rowModel.start()，计算rowModel
  - EVENT_MODEL_UPDATED会触发paginationProxy.onModelUpdated计算分页数据，
    - 然后执行rowRenderer注册的onPageLoaded
    - rowRenderer.onPageLoaded.onModelUpdated 会执行 redrawAfterModelUpdate, 触发首次渲染当前页所有行
  - rowModel初始化时会注册很多事件到eventService
    - 比如EVENT_SORT/Filter_CHANGED，这些事件被触发时会执行refreshModel更新rowModel

- update
  - refreshModel在rowModel每次计算后都会触发`EVENT_MODEL_UPDATED`事件，从而更新ui
    - 主要触发paginationProxy.onModelUpdated
  - `api.setRowData` 更新全量数据
    - this.clientSideRowModel.setRowData(rowData)
    - this.nodeManager.setRowData(rowData);
    - 先清空原rowModel，再重新计算全量rowModel
    - refreshModel触发view更新
  - `applyTransaction(tr)` 更新多行才触发modelUpdated事件
    - this.clientSideRowModel.updateRowData(tr)
    - this.nodeManager.updateRowData(tr)
    - 依次执行add/remove/update tr，根据参数id逐个查找
    - refreshModel触发view更新
    - ~~this.rowRenderer.refreshFullWidthRows();~~
    - this.rowRenderer.refreshCells();  // do change detection for all present cells
  - `applyTransactionAsync`异步批量更新
    - this.clientSideRowModel.batchUpdateRowData(tr)
    - 在setTimeout(cb)的cb中执行this.nodeManager.updateRowData + refreshModel
  - 对于modelUpdated事件
    - rowComp.onModelUpdated会更新每行样式
# model-layer
- ClientSideRowModel是event-emitter
- primaryColumnTree
  - 计算成多叉树平衡树结构的表头对象
- secondaryBalancedTree
  - If pivoting, these are the generated columns as a result of the pivot
# view-layer
- GridCore会从内置模板template初始化dom
- GridPanel初始化时，会注册到rowRenderer
- RowRender初始化时，会注册各种redraw事件
- rowRenderer.onModelUpdated会执行 redrawAfterModelUpdate
  - 计算需要重新渲染的行的索引index，然后遍历这些行索引创建或更新RowComp
- rowRenderer.redrawAfterModelUpdate 直接操作dom
  - 先计算rowsToRecycle，会复用已有行
  - this.redraw(rowsToRecycle, animate); 
    - this.calculateIndexesToDraw(rowsToRecycle);
    - this.removeRowCompsNotToDraw > renderedRow.destroy()
    - this.createOrUpdateRowComp
    - 先获取数据rowNode, this.paginationProxy.getRow(rowIndex);
    - 再渲染视图, this.createRowComp(rowNode) 
      - new RowComp 
      - this.setupRowContainers()
      - createRowContainer
      - createCells
      - rowContainerComp.appendRowTemplate(cellTemplatesAndComps)
  - this.restoreFocusedCell
- rowRenderer.refreshCells
  - cellComp.refreshCell
  - el.removeChild(el.firstChild); 
  - this.eParentOfValue.innerHTML = _.escape(valueToUse); 
# undo/redo
- 对于rowEditing/cellEditing/paste/fill操作，都会触发事件执行
  - const action = new UndoRedoAction(this.cellValueChanges); 
    - 会保留 **oldValue和newValue**
  - pushActionsToUndoStack(action); 

- undo
  - action = this.undoStack.pop(); 
  - currentRow.setDataValue(columnId, oldValue); 
  - this.redoStack.push(undoAction); 

- redo
  - action = this.redoStack.pop(); 
  - currentRow.setDataValue(columnId, newValue); 
  - this.undoStack.push(redoAction); 

- 对于特殊类型的action要特殊处理
# packages/modules
- ag-grid-packages
  - ag-grid-community: All Community Features
    - community-modules: 主要4部分
      - core
      - client-side-row-model 
      - infinite-row-model
      - csv-export 
      - 框架相关: react,vue,angular,polymer
  - ag-grid-enterprise: All Enterprise Features
    - enterprise-modules
      - core
      - row-grouping
      - rich-select
      - column-tool-panel
      - range-selection
      - date-time-cell-editor
      - filter-tool-panel
      - clipboard
      - excel-export
      - master-detail
      - menu
      - server-side-row-model 
      - set-filter
      - side-bar
      - status-bar
      - viewport-row-model
  - ag-grid-react: React Support
  - ag-grid-vue: Vue Support
  - ag-grid-angular: Angular Support
  - charts-packages 也提供了框架集成

- There are two main ways to install ag-Grid - either by using `packages` , or by using `modules` .
  - packages are the easiest way to use ag-Grid, but by default include all code specific to each package, 
  - whereas modules allow you to cherry pick what functionality you want, which will allow for a reduced overall bundle size.
  - If you're unsure whether to use packages or modules, then we'd recommend starting with packages and migrate to modules if you wish to reduce overall bundle size.
- When using `packages` , you get all of the code within that package and cannot pick and choose which features you require. 
  - You also don't need to register these packages in the same way you do with `modules` .
  - This means that it is easier to use packages, but the trade-off will be you'll end up with a larger bundle size if you don't require all features within a given package.

- ag-Grid `modules` allow you to pick and choose which features you require, resulting in a smaller application size overall, with the trade-off being that you need to register the modules you require.
  - @ag-grid-community/all-modules: All Community Modules
  - @ag-grid-community/core: Core Grid Components, GridOptions, ColDef etc
  - @ag-grid-community/client-side-row-model: ClientSideRowModelModule
  - @ag-grid-community/infinite-row-model: InfiniteRowModelModule
  - @ag-grid-community/csv-export: CsvExportModule

- `@ag-grid-community/all-module` s can be considered to be equivalent to `ag-grid-community` , but with the additional need to register modules within.
- `@ag-grid-enterprise/all-modules` will contain all Community modules.
- Note that neither `@ag-grid-community/all-module` s nor `@ag-grid-enterprise/all-modules` contain framework support 
  - if you require framework support you need to explicitly specify it, like `@ag-grid-community/react`
  - You do not need to register framework modules (ie. `@ag-grid-community/angular` etc).
- If you choose to select individual modules, then at a minimum the a Row Model need to be specified. 
  - After that all other modules are optional depending on your requirements.
- Providing Modules Globally
  - You can import and provide all modules to the Grid globally if you so desire, but you need to ensure that this is done before any Grids are instantiated.
- Providing Modules To Individual Grids
  - use `modules` prop
- If you specify any Community or Enterprise dependency, then the corresponding `core` module will also be pulled in and be made available to you.
- `@ag-grid-community/core`
  - This module contains the core code required by the Grid and all modules (Enterprise or Community) depend on it. 
  - As such `@ag-grid-community/core` will always be available no matter what module you specify in your `package.json` .
