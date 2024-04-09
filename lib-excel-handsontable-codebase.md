---
title: lib-excel-handsontable-codebase
tags: [codebase, handsontable]
created: 2024-04-08T03:57:07.806Z
modified: 2024-04-08T03:57:18.943Z
---

# lib-excel-handsontable-codebase

# guide
- dev-xp
  - 如何自定义ui、自定义api

- 待确认
  - editor中handsontableEditor类型是否是table作为单元格
# codebase
- 整体class风格

- 独特的事件系统
  - core和plugins支持的操作事件统一抽象在全局globalSingleHook
  - 用户操作的事件统一通过hooks注册，hook的触发逻辑在ui视图层已添加
  - 整体都是事件委托，没有将事件注册到具体的单元格上

- 状态优先的架构，视图层只在renderer中占比高，core/editor/plugins中状态占比高

- 不依赖contenteditable, 部分事件注册在document
  - 🤔 将事件注册到rootElem是否会更好
  - handsontable该如何与使用contenteditable的文本编辑器结合，需要改造事件
# 🏘️ architecture

## init

- 初始化前会注册 cellTypes/editors/renderers/plugins/validators
- `new Handsontable()`初始化时，执行`instance.init()`; 
- new EventManager(instance)
- keyStateStartObserving(): keydown/keyup/visibilitychange/blur
- dataSource = new DataSource(instance); 
- new Selection
- this.selection.addLocalHook beforeSetRangeStart/beforeModifyTransformEnd
- 剩下的逻辑全是将方法赋值给instance实例

- `instance.init()`; 
  - dataSource.setData
  - this.view = new TableView(this); 
    - TableView的初始化
    - this.eventManager = new EventManager(instance); // 自己的emitter
    - const table = document.createElement('TABLE');
    - instance.table = table;
    - 在rootElement注册事件 mousedown/mousemove
    - 在document注册事件 click/keyup/mouseup/contextmenu/touchend/mousedown
    - 在table注册事件 selectstart
    - this.wt = new Walkontable
    - 在wt.wtTable.spreader注册事件 mousedown/contextmenu
  - editorManager = EditorManager.getInstance
  - this.view.render(); 
    - this.wt.draw
    - this.wtTable.draw
    - wtViewport.createRenderCalculators(runFastDraw);
    - syncScroll = wtOverlays.prepareOverlays();
    - wtViewport.createVisibleCalculators();
    - new RowFilter, new ColumnFilter
    - this._doDraw();
      - const wtRenderer = new TableRenderer
      - wtRenderer.render();
      - this.renderColumnHeaders() > renderColumnHeader
      - this.renderRows > this.renderRowHeaders
      - this.renderCells
      - this.wot.wtSettings.settings.cellRenderer
    - refreshSelections
    - resetFixedPosition
    - this.wot.drawn = true;
  - instance.runHooks('afterInit'); 
# model

## update 💡

- 编辑器更改model是单向的，
  - 若model变化，需要手动执行render

- setDataAtCell
  - prop = datamap.colToProp(input[i][1]); 
  - 收集changes.push
  - 🚧 applyChanges(changes)
    - datamap.createRow
    - datamap.createCol
    - datamap.set
    - activeEditor.refreshValue(); 

- 
- 
- 

- Handsontable binds to your data source (list of arrays or list of objects) by reference. 
  - Therefore, all the data entered in the grid will alter the original data source. 
  - A change being made will not be presented on the screen unless you refresh the grid on the screen using the `render` method.

## editing

- Handsontable separates the process of displaying the cell value from the process of changing the value. 

- EditorManager has 4 main tasks:
  - selecting proper editor for an active cell
  - preparing editor to be displayed
  - displaying editor 
  - closing editor 

- openEditor()会执行activeEditor.beginEditing()
- finishEditing
  - this.saveValue(val, ctrlDown)  or  discardEditor
  - this.instance.populateFromArray
  - grid.populateFromArray
  - instance.setDataAtCell

- 编辑器创建的元素统一放在dom的末尾，`position: absolute;` 绝对定位
  - 容器样式名 .handsontableInputHolder

- TextEditor创建的文本编辑元素添加在末尾
  - `this.instance.rootElement.appendChild(this.TEXTAREA_PARENT)`; 

- SelectEditor
  - `this.instance.rootElement.appendChild(this.select)`; 

- 
- 
- 

# view

# selection

- Core初始化时，在this.selection.addLocalHook注册了很多callback

- 
- 
- 

# 🔌 plugins
- 插件的主要作用是注册hook
  - 在插件的`enablePlugin`方法中，会通过this.addHook注册很多callback

- plugin在初始加载时会自动注册class
  - 初始加载时会自动执行 registerPlugin(PLUGIN_KEY, ColumnSortingClass)
- 在Core构造函数的末尾，执行 `construct` 会触发 new PluginClass
- plugin的init方法会检测是否启用，启用则执行`this.enablePlugin()`; 
  - 判断启用类似 `this.hot.getSettings()[this.pluginKey]`; 

- sort
  - The column sorting plugin works as a proxy between the datasource and the Handsontable rendering module. 
  - It can map indices of displayed rows (called “visual indices”) to the indices of corresponding rows in the datasource (called “physical indices”) and vice versa. 
  - This way you can alter the order of rows which are being presented to a user, without changing the datasource’s internal structure. 
  - The sort operation is performed using a stable sort algorithm regardless of the browser you use and the size of the data set which you sort.
# collab

- 
- 
- 

## undo/redo

- not all actions are currently undo-able

- UndoRedo插件初始化时会注册事件 instance.addHook('afterChange')
  - 在事件中会会记录 `plugin.done(new UndoRedo.ChangeAction(changes))`; 
  - this.doneActions.push(action); 

- onBeforeKeyDown 监听ctrl+z/y
  - instance.undoRedo.undo(); 
  - const action = this.doneActions.pop(); 
  - action.undo()
  - instance.setDataAtRowProp(data, null, null, 'UndoRedo.undo'); 
    - 触发 applyChanges
  - instance.alter remove_row/remove_col

- 
- 
- 

# notes
- DataSource
  - this.dataType = 'array'; // array of array, or array of objects
  - 提供了数据操作的方法，大多读取
  - setData(data) { this.data = data; }  // 全量替换

- DataMap 用来更改dataSource
  - Utility class that gets and saves data from/to the data source using mapping of columns numbers to object property names
  - createRow: this.dataSource.push(row); 

- 
- 
- 

# more
