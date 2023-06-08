---
title: lib-excel-ospreadsheet-codebase
tags: [codebase, ospreadsheet]
created: 2023-06-07T22:37:10.671Z
modified: 2023-06-07T22:37:26.731Z
---

# lib-excel-ospreadsheet-codebase

# guide

# architecture
- init
  - 在initiateConnection时，new Model(demoData)
  - owlAppComponent.render-SpreadsheetComp

- update
  - SpreadsheetComp初始化时会注册 this.model.on("update", this, () => this.render(true)); 
  - 每次model更新都会重渲染整个sheet组件
  - keydown事件，如delete this.env.model.dispatch("DELETE_CONTENT", payload)
# plugin
- Since the spreadsheet internal state is quite complex, it is split into multiple parts, each managing a specific concern.

- BasePlugin is the common class that defines how each of these model sub parts should interact with each other. 
- There are two kind of plugins: 
  - **core plugins handling persistent data**
  - **UI plugins handling transient(短暂的；临时的) data**

- BasePlugin
  - this.history = Object.create(stateObserver); 每个plugin都有自己的history
  - this.dispatch = dispatch; 

- Core plugins handle spreadsheet data.
  - They are responsible to import, export and maintain the spreadsheet persisted state.
  - They should not be concerned about UI parts or transient state.

- CorePlugin extends BasePlugin
  - this.range = range

- UI plugins handle any transient data required to display a spreadsheet.
  - They can draw on the grid canvas.

- UIPlugin extends BasePlugin
  - this.selection = selection; 
  - this.ui = uiActions; 
  - drawGrid

- corePluginRegistry: persistent data
  - SheetPlugin
  - HeaderVisibilityPlugin
  - FiltersPlugin
  - CellPlugin
  - MergePlugin
  - HeaderSizePlugin
  - BordersPlugin
  - ConditionalFormatPlugin
  - FigurePlugin
  - ChartPlugin
  - ImagePlugin

- featurePluginRegistry: handle a specific feature, without handling any core commands
  - SheetUIPlugin
  - HeaderVisibilityUIPlugin
  - SelectionInputsManagerPlugin
  - HighlightPlugin
  - RendererPlugin
  - AutofillPlugin
  - SortPlugin
  - FindAndReplacePlugin
  - FormatPlugin
  - CellPopoverPlugin
  - HistoryPlugin
  - CollaborativePlugin

- statefulUIPluginRegistry: have a state, but which should not be shared in collaborative
  - ClipboardPlugin
  - EditionPlugin
  - GridSelectionPlugin

- coreViewsPluginRegistry: have a derived state from core data
  - FilterEvaluationPlugin
  - EvaluationChartPlugin
  - SheetViewPlugin
  - CustomColorsPlugin
# model-layer
- Model初始化
  - load data to get `WorkbookData` internal data
  - setupConfig
  - for (let Plugin of corePluginRegistry.getAll()) 获取并实例化core plugins
    - 会收集commands和handler
  - 依次实例化插件 statefulUIPluginRegistry, coreViewsPluginRegistry, featurePluginRegistry
  - this.dispatch("START"); 触发plugins中注册过的事件
  - this.selection.observe使selection更新时也触发模型更新
  - this.joinSession 协作相关

- The `Model` class is the owner of the state of the Spreadsheet. 
  - However, it has more a coordination role: it **defers the actual state manipulation work to plugins**.
- At creation, the Model instantiates all necessary plugins. 
  - They each have a private state (for example, the Selection plugin has the current selection).
- State changes are then performed through **commands**.
  - Commands are dispatched to the model, which will then relay them to each plugins (and the history handler). 
  - Then, the model will trigger an `update` event to notify whoever is concerned that the command was applied (if it was not cancelled).
- Model actually renders the visible viewport on a canvas. 
  - This is because each plugins actually manage a specific concern about the content of the spreadsheet, and it is more natural
  if they are able to read data from their internal state to represent it on the
  screen.
- Model can be used in a standalone way to manipulate programmatically a spreadsheet

- Getters are the main way the rest of the UI read data from the model.
  - it is shared between all plugins, so they can also communicate with each other.
  - coreGetters a subset of `getters`, without the UI getters

- The `dispatch` method is the only entry point to manipulate data in the model.
  - const command = createCommand(type, payload); 类似action-object
  - this.state.addCommand(command); 
  - this.dispatchToHandlers(this.handlers, command); 
  - this.state.recordChanges
  - this.session.save(command, commands, changes); 协作相关
  - this.trigger("update"); 
  - commands are dispatched most of the time recursively until no plugin want to react anymore.
  - CoreCommands dispatched from this function are saved in the history.
- `dispatch` is defined as an arrow function.  There are two reasons for this:
  - this means that the dispatch method can be "detached" from the model, which is done when it is put in the environment (see the Spreadsheet component)
  - This allows us to define its type by using the interface CommandDispatcher

- `drawGrid` rendering
  - When the Grid component is ready (= mounted), it has a reference to its canvas and need to draw the grid on it.  
  - This is then done by calling this method, which will dispatch the call to all registered plugins.
  - Note that nothing prevent multiple grid components from calling this method each, or one grid component calling it multiple times with a different context. 
  - This is probably the way we should do if we want to be able to freeze a part of the grid (so, we would need to render different zones)
# view-layer
- 基于odoo自研owl框架，类似vue的reactivity + vdom

- Model初始化时markRaw(this)，未使用owl的reactivity
# more
