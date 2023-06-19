---
title: lib-excel-ospreadsheet-codebase
tags: [codebase, ospreadsheet]
created: 2023-06-07T22:37:10.671Z
modified: 2023-06-07T22:37:26.731Z
---

# lib-excel-ospreadsheet-codebase

# guide

# dev-to
- action-queues async
# architecture
- init
  - 在initiateConnection时，new Model(demoData)
  - owlAppComponent.render-SpreadsheetComp

- update
  - SpreadsheetComp初始化时会注册 this.model.on("update", this, () => this.render(true)); 
    - 每次model更新都会重渲染整个SpreadsheetComp
  - keydown事件，如delete会`this.env.model.dispatch("DELETE_CONTENT", payload)`
    - model.dispatch事件会触发 `this.trigger("update");`

- 实现了自己的`css`工具方法
# plugin
- Since the spreadsheet internal state is quite complex, it is split into multiple parts, each managing a specific concern.

- BasePlugin is the common class that defines how each of these model sub parts should interact with each other. 
- There are two kind of plugins: 
  - **core plugins handling persistent data**
  - **UI plugins handling transient(短暂的；临时的) data**

- 实现时，一个feature可拆分为多个plugin，组合多个corePlugin和uiPlugin
  - 比如SheetPlugin+SheetUIPlugin，HeaderVisibilityPlugin+HeaderVisibilityUIPlugin

- `BasePlugin implements CommandHandler`
  - this.history = Object.create(stateObserver); 
    - 每个plugin都有自己的history，但update方法使用全局
  - this.dispatch = dispatch; 
    - 全局dispatch
  - allowDispatch: if the command is allowed
  - beforeHandle: This should only be used if it is not possible to do the work in the handle method
  - handle: handle any command
  - finalize: only want to reevaluate the cell values once at the end

- Core plugins handle spreadsheet data.
  - They are responsible to import, export and maintain the spreadsheet persisted state.
  - They should not be concerned about UI parts or transient state.

- `CorePlugin extends BasePlugin`
  - this.range = range; 
  - this.uuidGenerator = uuidGenerator; 
  - this.getters = getters; 
  - adaptRanges: loop over the plugin's data structure and adapt the plugin's ranges.

- UI plugins handle any transient data required to display a spreadsheet.
  - They can draw on the grid canvas.

- `UIPlugin extends BasePlugin`
  - this.selection = selection; 
  - this.ui = uiActions; 
  - this.getters = getters; 
  - drawGrid(ctx: GridRenderingContext, layer: LAYERS) {}

- Changes to the plugin state that must be restored by Undo must be done through the function `this.history.update()`.
  - `this.history.update("records", 1, "data", 1, "text", "Bye");` can be used with multiple level of depth
  - update操作，属性path中的多个key作为参数
    - add用新key
    - remove用undefined作为值

- corePluginRegistry: persistent data
  - SheetPlugin
  - CellPlugin
  - HeaderVisibilityPlugin
  - FiltersPlugin
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
- 💡 spreadsheet的核心数据结构
  - sheet: `{ sheetId:string, rows:Array<{ cells: {columnIndex:cellId} }> }` rows并不存放具体数据
  - cells: `{ sheetId: { cellId: cellContent } }` cellId直接用的数字
  - 🤔 优化时可进一步扁平化，~~{ rowId: cellIndex[] }~~, { cellId: {sheetId, rowId, cellIndex} }

```typescript
export interface Sheet {
  id: UID;
  name: string;
  numberOfCols: number;
  rows: Row[];
  areGridLinesVisible: boolean;
  isVisible: boolean;
  panes: PaneDivision;
}

export interface Row {
  // number is a column index, uid is cellId
  cells: Record<number, UID | undefined>; 
}

class CellPlugin{
  cells: { [sheetId: string]: { [id: string]: Cell } } = {};
}

export type Cell = LiteralCell | FormulaCell;

interface Cell {
  readonly id: UID;
  /**
   * 👇🏻 Raw cell content
   */
  readonly content: string;
  readonly style?: Style;
  readonly format?: Format;
}
```

- Model初始化
  - load data to get `WorkbookData` internal data
  - setupConfig
  - for (let Plugin of corePluginRegistry.getAll()) 
    - new CorePlugin
    - plugin.import(data); 从数据中获取插件自身需要的数据
    - 会收集commands和handler
  - 依次实例化插件 statefulUIPluginRegistry, coreViewsPluginRegistry, featurePluginRegistry
    - new UIPlugin
    - 将layer排序后存放this.renderers
  - this.dispatch("START"); 触发plugins中注册过的事件
  - this.selection.observe使selection更新时也触发模型更新
  - this.joinSession 协作相关

- `sheetPlugin.sheets: Record<UID, Sheet>` 作为核心数据源

- UIPlugin的图层设计

```typescript
export const enum LAYERS {
  Background,
  Highlights,
  Clipboard,
  Search,
  Chart,
  Autofill,
  Selection,
  Headers, // Probably keep this at the end
}
```

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
  - this.session.save(command, commands, changes); 历史和协作相关
  - `this.trigger("update")`; 通知视图层
  - commands are dispatched most of the time recursively until no plugin want to react anymore.
  - CoreCommands dispatched from this function are saved in the history.
- `dispatch` is defined as an arrow function.  There are two reasons for this:
  - this means that the dispatch method can be "detached" from the model, which is done when it is put in the environment (see the Spreadsheet component)
  - This allows us to define its type by using the interface CommandDispatcher

- actions的设计，类似redux
  - const UNDO_ACTION = (env: SpreadsheetChildEnv) => env.model.dispatch("REQUEST_UNDO"); 

- `drawGrid` rendering
  - When the Grid component is ready (= mounted), it has a reference to its canvas and need to draw the grid on it.  
  - This is then done by calling this method, which will dispatch the call to all registered plugins.
  - Note that nothing prevent multiple grid components from calling this method each, or one grid component calling it multiple times with a different context. 
  - This is probably the way we should do if we want to be able to freeze a part of the grid (so, we would need to render different zones)
  - 插件示例
    - GridSelectionPlugin
    - hightlight
    - find-replace
    - autofill

## StateObserver

- commands: CoreCommand[] 记录操作历史
- changes: root, path, beforeVal, afterVal 记录新旧值

- 每次dispatch时都会recordChanges

- 让SelectiveHistory的applyOperation持有了recordChanges方法
# collaboration

## undo/history/revision

```typescript
export interface HistoryChange {
  root: any;
  path: (string | number)[];
  before: any;
  after: any;
}

// - A `Revision` represents a whole client action (Create a sheet, merge a Zone, Undo, ...).
// - A revision contains the following information:
//   - `id`: ID of the revision
//   - `clientId`: Client who initiated the action
//   - `commands`: CoreCommands that are linked to the action, and should be dispatched in other clients
//   - `changes`: List of changes applied on the state.
class Revision implements RevisionData {
  
  public readonly id: UID;
  public readonly clientId: ClientId;
  private _commands: readonly CoreCommand[] = [];
  private _changes: readonly HistoryChange[] = [];

}

// The local history is responsible for tracking the locally state updates.
// It maintains the local undo and redo stack to allow to undo/redo only local changes
// - 👉🏻 History changes (undo & redo) are *not* applied optimistically on the local state.
//   - We wait a global confirmation from the server. 
//   - The goal is to avoid handling concurrent history changes on multiple clients which are very hard to manage correctly.
class HistoryPlugin extends UIPlugin {
  /**
   * Ids of the revisions which can be undone
   */
  private undoStack: UID[] = [];

  /**
   * Ids of the revisions which can be redone
   */
  private redoStack: UID[] = [];
}

// T is mostly Revision
class Operation<T> {
  constructor(readonly id: UID, readonly data: T) {}

  transformed(transformation: Transformation<T>): Operation<T> {
    return new LazyOperation<T>(
      this.id,
      lazy(() => transformation(this.data))
    );
  }
}
```

- plugin-state的更新基于统一的history机制
  - this.history.update("sheets", sheet.id, "rows", rows); 
  - 每次更新值都会保存change到全局 stateObserver
  - this.changes.push({ root, path, before: value[key], after: val }); 

```JS
if (type === "UNDO") {
  this.session.undo(id);
  this.redoStack.push(id);
} else {
  this.session.redo(id);
  this.undoStack.push(id);
}
```

- session: Manages the collaboration between multiple users on the same spreadsheet.
- 每次`model.dispatch(action)`都会触发
  - `this.session.save(command, commands, changes);` 每次都会创建并保存新的revision
  - new Revision
  - session.revisions.append 触发创建operation
  - `new Operation(operationId, revision)`; 
  - session.revisions.tree.insertOperationLast(branch, operation); 

- `session.revisions`存放了当前协作文档的所有changes，保存类型是SelectiveHistory
  - 支持revertOperation

- `session.undo` 会发送消息到server
  - 客户端接受到ack后，执行`revisions.undo`; 

- `session.onMessageReceived` Handles messages received from other clients when collab
  - this.revisions.undo
  - this.revisions.redo
  - this.revisions.insert

- `session.revisions.undo`
  - `selectiveHistory.revertOperation(operation.data)` // operation.data is revision
  - selectiveHistory.tree.undo(branch, operation); // branch.fork
  - fastForward: Replay the operations between the current HEAD_BRANCH and the end of the tree
  - 协同时undo的可能是中间某个op，所以该位置后的op都要转换

- `session`初始化时注册了undo/redo的model层方法

```JS
{
  applyOperation: (revision: Revision) => {
    const commands = revision.commands.slice();
    const { changes } = args.recordChanges(() => {
      for (const command of commands) {
        args.dispatch(command); // model.dispatchToHandlers
      }
    });
    revision.setChanges(changes);
  },
  revertOperation: (revision: Revision) => revertChanges([revision]),
}

function revertChanges(revisions: readonly Revision[]) {
  for (const revision of revisions.slice().reverse()) {
    for (let i = revision.changes.length - 1; i >= 0; i--) {
      const change = revision.changes[i];
      applyChange(change, "before"); // 基于before值
    }
  }
}

function applyChange(change: HistoryChange, target: "before" | "after") {
  let val = change.root as any;
  let key = change.path[change.path.length - 1];

  if (change[target] === undefined) {
    delete val[key]; // 删除用undefined
  } else {
    val[key] = change[target]; // 修改值
  }
}
```

- The selective history is a data structure used to register changes/updates of a state.
  - Each change/update is called an "operation".
  - An operation can be represented by any data structure. It can be a "command", a "diff", etc.
  - The data structure allows to easily cancel (and redo) any operation individually.
  - Since this data structure doesn't know anything about the state nor the structure of operations, the actual work must be performed by external functions given as parameters. 
  - 操作基于Operation

- The tree is a data structure used to maintain the different branches of the `SelectiveHistory`.
  - Branches can be "stacked" on each other and an execution path can be derived from any stack of branches. The rules to derive this path is explained below.
  - An operation can be cancelled/undone by inserting a new branch below this operation.

- version-history示例
  - session.getRevisions().fastForward(); 
  - session.getRevisions().revertTo(revision.operation.id); 
  - revertOperation
  - 显示version-history时，sheet不可编辑

## ot

- 若初始化时不传入socketService，就会使用默认 LocalTransportService, 执行简单的内存操作

- An Operation can be executed to change a data structure from state A to state B.
  - It should hold the necessary data used to perform this transition.
  - It should be possible to revert the changes made by this operation.
- **In the context of o-spreadsheet, the data from an operation would be a revision**.
  - the commands are used to execute it, the `changes` are used to revert it

- `session.onMessageReceived`收到REMOTE_REVISION时
  - revisionNew = new Revision(message)
  - this.revisions.insert(revisionNew)
  - this.trigger("remote-revision-received", { commands: transformAll(commands, pendingCommands), }); 
    - transformAll > genericTransform/specificTransform

- ot转换transform，分为 genericTransform 和 specificTransform
  - src/collaborative/ot/ot.ts
    - Apply all generic transformation based on the characteristic of the given commands.
  - src/collaborative/ot/ot_specific.ts

- For all Core commands, a transformation function should be written for all core commands. 
- In practice, the transformations are very similar:
  - Checking the sheet on which the command is triggered
  - **Adapting coord, zone, target** with structure manipulation commands (remove, add cols and rows, ...)
- If a command should be skipped (insert a text in a deleted sheet), the transformation function should return undefined.

## commands

- There are two kinds of commands: CoreCommands and LocalCommands
- CoreCommands are commands that
  1. manipulate the imported/exported spreadsheet state
  2. are shared in collaborative environment
- LocalCommands: every other command
  1. manipulate the local state
  2. can be converted into CoreCommands
  3. are not shared in collaborative environment
- For example, "RESIZE_COLUMNS_ROWS" is a CoreCommand. "AUTORESIZE_COLUMNS" can be (locally) converted into a "RESIZE_COLUMNS_ROWS", and therefore, is not a CoreCommand
- CoreCommands should be "device agnostic". 
  - This means that they should contain all the information necessary to perform their job. 
  - Local commands can use inferred information from the local internal state, such as the active sheet.
# view-layer
- 基于odoo自研owl框架，类似vue的reactivity + vdom

- Model初始化时markRaw(this)，未使用owl的reactivity
# formula
- 基于ast
# more
- `key in {}` is ~12 times slower than `{}[key]`.
  - So, we check the absence of key only when the direct access returns a falsy value. It's done to ensure that the registry can contains falsy values
