---
title: toc-lib-excel-list-grid-popular
tags: [grid, lib, list, toc]
created: 2020-10-22T06:47:15.435Z
modified: 2022-08-21T10:02:27.788Z
---

# toc-lib-excel-list-grid-popular

# focus

- features
  - **editable operations support** : logux/ospreadsheet/slate/typewriter
  - group/aggregate/ **pivot** : tanstack-table(大量缓存)
  - multi views
  - _collaborative optional_: 作为插件，似乎将ospreadsheet的ot去掉就是llw了
  - _undo/redo+batch-undo_: 存反向op和存值2种方案，存值本身也是反向op
  - _transaction_
  - end-user database: 用户自定义数据支持 graph/relational queries
  - formula: excel, google-sheet, powerbi
  - headless utils: state/actions/props/api: autocomplete/tanstack，state和a11y不同粒度，可实现为core+plugin
  - view-layer: vdom+reactive(mobx/signal): autocomplete/typewriter/Simple-DataTables/slate-dom/sleek
  - closer to excel
  - virtualized
  - keyboard/a11y
  - mobile friendly
  - optimized for text-table/markdown-table
  - support list
  - image
    - 单元格图片懒加载
  - 接入现有组件库
  - modular, extensible, customizable
  - the-elm-architecture
  - drag between windows
  - stream
  - 常见场景: virtual, infinite, lazy
  - excel specification: xlsx, md-table, notion-db

- collaborative-editing
  - 数据模型考虑 持久化(一般db-text/json/blob)、展示(json)、协作(llw/map/sequence)、衍生计算(如聚合)
    - 以哪种数据作为single source of truth
    - 一般以crdt形式的数据结构作为唯一数据源，是否在内存？
  - 实时协作、冲突处理
  - 离线合并，last-write-win对 ~~同一用户~~ 不同设备的合并不友好
  - 对于现有系统，是不是只用替换模型层数据结构且保留api接口不变就可以了
  - 自己实现sync，参考hlc；使用现有同步层，参考logux、automerge
  - undo/redo的实现
    - slate： inverseOps = batch.map(Operation.inverse).reverse(); 再逐个apply
    - [撤销重做的程序设计](https://plantain-00.github.io/blogs/?src=./contents/undo-redo.md)

- plugins-ready
  - plugin支持视图层的优点包括更灵活的渲染(decorations)、场景更广的commands，参考prosemirror
    - 明确区分state-only-plugin和with-view-plugin，纯state相关的plugin可跨框架使用
  - prosemirror Plugin class
  - slate hoc
  - tanstack-table hoc
  - luckysheet
  - ospreadsheet
  - sleekgrid: plugin.init(thisGrid)
  - SlickGrid
  - autocomplete: state层的hooks
  - gridjs: a function component to render
  - 未实现plugin: tui.grid

- view-layer 进一步优化需要深入前端框架如react
  - 视图层的优化方案主要2个方向
    - 优化rerender，参考memo、forget
    - 优化reconciliation，参考million.js
  - 自定义组件的渲染返回值都是vnode，允许用户替换默认renderFunction
    - 自定义组件都是纯函数，状态放在编辑器数据层统一触发更新
    - 是否可以使用多个vdom-tree，允许只订阅部分state的更新
    - recursive render to iteration，在迭代时方便考虑并行
  - 避免每次全量render和diff的方案
    - 使用double buffer，参考react-fiber/lexical
    - immer使用copy-on-write和structural-sharing
    - prosemirror的node使用structural-sharing
  - 提高性能方案，异步渲染
    - react reconciler废弃递归，使用fiber链表
    - 腾讯文档智能表格使用异步分片计算
  - block/cell-based render
    - 参考 notion-render/editor-render
  - 👉🏻 reactive实现的方案
    - 发布订阅，参考redux、ag-grid、ospreadsheet、tui.grid、gridjs、mxgraph
    - 手动先更新数据再更新view，参考prosemirror、slate、typewriter、tanstack-table、sleekgrid、simple-dt

- collab-如何在表中间位置插入行或列
  - 最简单和常见的数据结构是crdt map，可尝试基于`无序map+有序array`实现有序arrayMap
  - 前端问题都可从db的角度来考虑，在db表上可添加一个单独的order列
  - tanstack-table使用了 `type ColumnOrderState = string[]`
  - [Is it possible to insert data into the mid section of a table using the INSERT command?](https://stackoverflow.com/questions/4127169)
  - [What could be the direction for making Peritext support block elements](https://github.com/inkandswitch/peritext/issues/27)
    - I helped design a convergent data model for tables at Notion recently that would work well using 3 convergent data types: Map (to group and address fields), Ordered Set (for defining the order of rows and the order of columns), and Rich Text (for defining the contents of cells).
    - `type Table = { rowOrder: OrderedSet<RowId>, columnOrder: OrderedSet<ColumnId>, rows: Map<RowId, Row> }` 行顺序和列顺序都单独存储
    - `type Row = { cells: Map<ColumnId, RichText> }`

- features
  - excel/docs的前端组件通常需要一个import工具进行数据转换，方便直接在前端组件编辑，可参考流行的开源工具

- 开源表格
  - 国内: luckysheet
  - 国外: ag-grid, tanstack-table, handsontable, o-spreadsheet, tui.grid, sleekgrid, simple-datatables
  - ethercalc
  - tinybase

- src-list-grid
  - **ag-grid** 
  - **tanstack-table** 
  - **react-virtual** 
  - react-tiny-virtual-list
  - react-virtualized/window

- src-list-grid-canvas
  - **luckysheet** : 未使用class类，函数式风格
  - glide-data-grid: react组件
  - x-spreadsheet/wolf: class类和函数式都有
  - cheetah-grid(ts): 基于class类继承

- resources
  - [TablesGenerator.com: 支持latex/markdown/html/text/mediawiki](https://www.tablesgenerator.com/)
# list-grid-div
- tanstack-table /MIT/11.6kStar/202202/ts
  - https://github.com/tannerlinsley/react-table
  - https://react-table.tanstack.com/
  - Hooks for building fast and extendable tables and datagrids for React
  - React Table is a headless utility, which means it doesn't supply any actual UI elements.
  - https://github.com/tannerlinsley/react-virtual

- ag-grid /MIT/6.4kStar/202202/ts/NoDeps
  - https://github.com/ag-grid/ag-grid
  - https://www.ag-grid.com/example/
  - 基于div实现，每行对应的dom元素存在
  - a fully-featured and highly customizable JavaScript data grid
    - has no 3rd party dependencies
    - integrates smoothly with all major JavaScript frameworks
  - ag-grid-enterprise is Commercial licensed but opensourced
  - [Client-Side Data - Transaction Updates](https://www.ag-grid.com/javascript-data-grid/data-update/)
    - A `transaction` object contains the details of what rows should be added, removed and updated
    - There are some differences with updating Row Data (with Row IDs) and Transaction Updates
      - When setting Row Data, the grid will have the overhead of identifying what rows are added, removed and updated.
      - When setting Row Data, the grid stores the data in the same order as the data was provided
  - [Why is the minified bundle so large?](https://github.com/ag-grid/ag-grid/issues/1459)
    - Main reason IMO: the grids has no dependencies

- handsontable v6.2.2 /13.8kStar/MIT~Paid/201903/js
  - https://github.com/handsontable/handsontable
  - https://handsontable.com/
  - 基于table标签实现
  - 依赖numbro, moment, pikaday
  - a JS HTML5 data grid with spreadsheet look & feel
  - free for all non-commercial purposes since 7.0
  - 不支持协作
  - 支持undo，[Q: Possible to combine multiple actions into single undo/redo step?](https://github.com/handsontable/handsontable/issues/7324)
  - [Handsontable drops open source for a non-commercial license_201903](https://github.com/handsontable/handsontable/issues/5831)
    - https://github.com/handsontable/handsontable/releases/tag/7.0.0
    - [Handsontable v7 and later versions are fully commercial so it really depends on your case](https://twitter.com/handsontable/status/1164198101726433282)

- luckysheet /4.5kStar/MIT/202202/js/vanillajs
  - https://github.com/dream-num/Luckysheet
  - https://github.com/mengshukeji/Luckysheet
  - https://github.com/dream-num/univer
  - https://mengshukeji.github.io/LuckysheetDemo/
  - an online spreadsheet like excel
  - 基于canvas实现
  - 依赖jquery、pako、jspdf
  - https://github.com/dream-num/chartMix /js
    - chart plugins for Luckysheet
    - 依赖echarts4、jquery、element-ui、vue2、vuex3
  - 🍴 forks
  - https://github.com/carl-jin/RichSpreadsheet
  - https://github.com/fromatlantis/Luckysheet
  - https://github.com/titanDevelopers/Luckysheet
- https://gitee.com/zhouweng/mini_sheet /js
  - 我花了两周时间，通读了LuckySheet的源码，并且裁剪出了可执行的最小项目MiniSheet
  - [MiniSheet目录_舟翁的博客](https://blog.csdn.net/u010593516/article/details/113743472)
  - https://github.com/dream-num/LuckysheetServer /java
    - Luckysheet official Java version backend.
    - [LuckysheetServer – Google Sheets-like realtime collaborative spreadsheet | Hacker News_202012](https://news.ycombinator.com/item?id=25261004)

- fortune-sheet /1.4kStar/MIT/202208/ts
  - https://github.com/ruilisi/fortune-sheet
  - https://ruilisi.github.io/fortune-sheet-docs/zh/guide/
  - https://ruilisi.github.io/fortune-sheet-demo
  - https://ruilisi.github.io/fortune-sheet-demo/
  - FortuneSheet是一款开箱即用的类似Excel和Google Sheets的javascript表格组件。
  - 本项目源于 Luckysheet，并继承了它的很多代码。我们为将其转换为typescript做了很多努力，并且解决了一些原项目设计层面的问题。
  - 完全使用typescript编写。
  - 去掉了 jQuery 的依赖, 用React/Vue + immer来管理DOM和状态。
    - 架构分为 core+react
  - 同页面支持多个实例。目前只支持单个实例，因为有全局状态
  - 避免在window对象上存储数据。
  - 用一个forked handsontable/formula-parser 来处理公式计算。
  - A working example with Express (backend server) and MongoDB (data persistence) is available in backend-demo folder.
  - 👀 从luckysheet未迁移的功能
    - undo/redo、协作
    - 透视表、图表、拖拽
    - 下拉填充、查找替换
  - [Is there any plan to make a Vue version? soon](https://github.com/ruilisi/fortune-sheet/issues/14)
  - [I created a new Excel-like spreadsheet component for React with collabration support : r/reactjs _202204](https://www.reddit.com/r/reactjs/comments/u9flzs/i_created_a_new_excellike_spreadsheet_component/)
    - Collabration is implemented by patch generated by Immer.js, the patch is also used for undo/redo.

- x-sheet /50Star/MPL/202209/js/vanillajs/canvas/luckysheet开发者
  - https://github.com/eiji-th/x-sheet
  - https://gitee.com/eigi/x-sheet
  - 高性能 web javaScript 电子表格
  - 依赖exceljs

- o-spreadsheet /130Star/LGPLv3/202305/ts
  - https://github.com/odoo/o-spreadsheet
  - https://odoo.github.io/o-spreadsheet/
  - A standalone spreadsheet for the web, easily integrable and extendable.
  - 支持公式formula
  - 支持history、undo、branch
  - 依赖bootstrap5、@odoo/owl
  - 图表基于chart.js.v2
  - 自定义实现了`css()`形式的css-in-js的方法
  - 透视表和图表功能弱于luckysheet
  - Real time collaboration
    - The solution we implement is based on Operation Transform (OT).
    - concurrent undo/redo are allowed
    - This solution has a lot of pros, but also some cons:
    - We need to write a transformation function for each command we create
    - Undo/Redo is synchronous, i.e. it should be accepted by the server before being executed locally.
  - Model is the owner of the state of the Spreadsheet
    - it defers the actual state manipulation work to **plugins** .
    - State changes are then performed through commands. Commands are dispatched to the model
    - Model can be used in a standalone way to manipulate programmatically a spreadsheet
  - [[WIP] Version history](https://github.com/odoo/o-spreadsheet/pull/2259)
    - I'd keep the concepts of tree and branches hidden. They really are internal implementation details of the data structure.
- https://github.com/odoo/owl /LGPLv3/ts/NoDeps
  - A web framework for structured, dynamic and maintainable applications
  - 初始化前，需要先从服务器fetch界面ui相关的xml模版文件
  - 视图层使用xml模版，组件与视图耦合(view+state+effect)，react也这样
  - Owl's virtual dom is a fork of `snabbdom`.
  - Class based components with hooks, reactive state and concurrent mode
  - a fine grained reactivity system similar to Vue
  - Owl components are defined with ES6 classes and xml templates, uses an underlying **virtual DOM** , integrates beautifully with hooks, and the rendering is asynchronous.
  - Most frameworks will compile templates ahead of time. 
    - However, this is not what Odoo needs: Odoo will fetch templates from the database and need to compile them only at the last possible moment, so we can apply all necessary xpaths
    - Odoo needs to be able to generate (and compile) templates at runtime.
  - [owl/comparison with react/vue](https://github.com/odoo/owl/blob/master/doc/miscellaneous/comparison.md)
    - Owl supports slots, which is the primary mechanism to make generic reusable/composable components
    - Owl is not dependant on any external build tool. Owl uses the standard xml parser that comes with every browser.
    - components in OWL are totally asynchronous. useful for lazy/dynamic loading
    - owl reactivity is done with a `Proxy`. once state prop changes, rendering is scheduled in the next microtask(promise)
      - We like the way Vue did it, but it has a flaw: it is not really optional.
      - 但spreadsheet并没有使用owl的reactivity
      - there certainly are situations where we need a state, which is not read-only, and not observed. For example, a spreadsheet
      - It may have a very large internal state, and it knows exactly when it needs to be rendered (basically, whenever the user performs some action). Then, observing its state is a net performance loss, both for the CPU and the memory.
  - [perfectly synchronising actual DOM update of components](https://github.com/odoo/owl/issues/845)
    - What we want is the button to change color at the exact same time as the composer dropdown appearing.
    - Owl is designed asynchronously, and you cannot force two child components to be updated at the same time. This is just not possible.
    - this is really weird to me, if there is no async work going on, they will however be updated in the same animation frame
    - problem: there is a css transition rule on the button
  - [[IMP] reactivity: synchronous batch context](https://github.com/odoo/owl/pull/1157)
    - Can be useful for implementing computed values.
    - rename to transaction

- react-window /14kStar/MIT/202304/js
  - https://github.com/bvaughn/react-window
  - https://react-window.now.sh/
  - 基于div实现，每行对应的dom元素不存在
  - React components for efficiently rendering large lists and tabular data
  - React window works by only rendering part of a large data set(just enough to fill viewport).
  - [Support just-in-time measured content](https://github.com/bvaughn/react-window/issues/6)
  - 🍴 forks
    - https://github.com/webcore-it/react-window
  - https://github.com/vikadata/vikatable /ts
    - 基于 react-window Grid 构建的表格组件
    - @apitable/react-flow 基于其中的 Grid 构建，通过扩展 Grid 的 props 参数，非侵入式支持更多的表格特性, 使其更方便构建表格。
  - https://github.com/bvaughn/react-window-infinite-loader /MIT/202102/js/inactive
    - https://codesandbox.io/s/5wqo7z2np4
    - InfiniteLoader component inspired by react-virtualized but for use with react-window
    - This demo app mimics loading remote data.Once data has been "loaded" the row number will be displayed.
  - https://github.com/pupudu/window-table /202207/ts/inactive
    - https://window-table.netlify.com/
    - Windowing Table for React based on React Window
    - [Roadmap for bvaughn/react-window-table](https://github.com/bvaughn/react-window-table/issues/1)
  - https://github.com/mckervinc/react-fluid-table /202009/ts/inactive
    - https://mckervinc.github.io/react-fluid-table/
    - A windowed React table built on top of react-window

- react-virtuoso /3.7kStar/MIT/202305/ts/list/table
  - https://github.com/petyosi/react-virtuoso
  - https://virtuoso.dev/
  - powerful React virtual list/table component
  - V1 brings improvements to reverse infinite scrolling behavior - suitable for chat and feed user interfaces.

- onlyoffice-sdkjs /190Star/AGPLv3/202302/js
  - https://github.com/ONLYOFFICE/sdkjs
  - https://api.onlyoffice.com/docbuilder/spreadsheetapi
  - Contains API for all the included components client-side interaction.
  - 通过TypedArray，将表格数据以二进制格式存储，通过字段压缩+共享字符串表来优化内存空间
  - [精读onlyoffice在线表格存储设计](https://juejin.cn/post/7202252704978386999)

- https://github.com/jmptrader/SpreadJS /201608/js
  - gcspread.sheets.all.9.40.20161.0.min.js

- react-tiny-virtual-list /MIT/1.8kStar/201910/ts
  - https://github.com/clauderic/react-tiny-virtual-list
  - https://clauderic.github.io/react-tiny-virtual-list/
  - A tiny but mighty 3kb list virtualization library, with zero dependencies
  - Supports variable heights/widths, sticky items, scrolling to index, and more
  - https://github.com/clauderic/react-infinite-calendar /201705/js
    - 依赖tiny-virtual-list,date-fns
- react-virtualized /MIT/19.5kStar/202105/js
  - https://github.com/bvaughn/react-virtualized
  - http://www.reactvirtualized.com/
  - https://github.com/bvaughn/react-virtualized/blob/master/docs/Grid.md
  - 基于div实现，每行对应的dom元素不存在
  - 表格主体ReactVirtualized__Grid__innerScrollContainer内全是单元格
  - React components for efficiently rendering large lists and tabular data
- https://github.com/developit/preact-virtual-list
  - https://jsfiddle.net/developit/qqan9pdo/
  - Virtual List that only renders visible items. Supports millions of rows.
  - 单文件，代码简单

- react-data-grid /MIT/4kStar/202201/ts
  - https://github.com/adazzle/react-data-grid
  - https://adazzle.github.io/react-data-grid/
  - 基于div实现，每行对应的dom元素存在，未实现row/column-span(merge cells)
  - 项目模块化，分为core和addons
  - Excel-like grid component built with React, with editors, keyboard navigation, copy...

- sleekgrid /25Star/MIT/202304/ts/NoDeps/vanillajs
  - https://github.com/serenity-is/sleekgrid
  - https://serenity-is.github.io/sleekgrid/examples/classic/example06-editing-with-undo
  - a complete rewrite of the original SlickGrid in TypeScript with ES6 modules
  - 未实现分页
  - 支持插件
  - 提供了编辑、format示例
  - 实现了undo，未实现redo
    - 原理是将command记录保存在stack，每次undo会恢复prevValue，注意值的粒度在单元格，ag-grid也这样
    - 很多更新操作都基于EditorLock
    - A locking helper to track the active edit controller and ensure that only a single controller can be active at a time. This prevents a whole class of state and validation synchronization issues.
  - EditCommand设计
    - 数据 value,prevValue,cell,row
    - execute: update cell+row，更新单元格时会更新行
    - undo: update cell+row
  - used extensively in Serenity, our open source ASP. NET Core / TypeScript based business application framework. 
  - 为了兼容jquery，添加了很多判断`if(this._jQuery)`的逻辑
  - 大多数事件都是直接操作dom
  - init初始化流程
    - new BasicLayout() + init container
    - calcViewportSize
    - measureCellPaddingAndBorder
    - createColumnHeaders
    - this.resizeCanvas();  > 触发render
  - update更新流程
    - 注册各种事件，触发更新都会触发render
      - cleanupRowsFromCache
      - renderRows，使用了_rowsCache，里面缓存了dom对象
      - 创建rowNode使用document.createElement
    - 有的cb会先this.invalidate，再rerender

- SlickGrid /1.7kStar/MIT/202312/ts/功能丰富
  - https://github.com/6pac/SlickGrid
  - https://github.com/6pac/SlickGrid/wiki/Examples
  - https://slickgrid.net/
  - http://6pac.github.io/SlickGrid/examples/example4-model.html
  - 基于div实现，每行对应的dom元素存在
  - A lightning fast JavaScript grid/spreadsheet
  - 依赖sortablejs
  - added Plugins: RowDetail, CellMenu, ContextMenu, GridMenu, CustomTooltip, GridState
  - removed jQuery requirement in v4
  - in v5(202312) migrating to TypeScript (we kept IIFE and added ES6/ESM build targets) 
  - https://github.com/mleibman/SlickGrid
    - /archived/6.7kStar
- https://github.com/ghiscoding/slickgrid-universal /MIT/202312/ts
  - https://ghiscoding.github.io/slickgrid-universal/
  - a monorepo which includes all Editors, Filters, Extensions, Services and is Framework Agnostic to take full advantage of SlickGrid core lib
  - 依赖sortablejs、moment-mini、un-flatten-tree、flatpickr
  - https://github.com/ghiscoding/slickgrid-react /ts
  - https://github.com/ghiscoding/slickgrid-universal-webpack-demo /ts

- Simple-DataTables /1.1kStar/LGPLv3/202304/ts
  - https://github.com/fiduswriter/Simple-DataTables
  - https://fiduswriter.github.io/simple-datatables/
  - A extendable, dependency-free javascript HTML table plugin.
  - 支持编辑，不支持undo
  - DataTable自身是个event-emitter
  - 使用了diff-dom中的vnode定义
  - init初始化流程
    - 优先从dom中读取table元素，构建初始vdom
    - 读取数据
    - 使用update触发首次渲染
  - update更新流程
    - 各种事件都绑定了update回调； 也有先手动更新数据再手动调用update
    - _paginate()
    - _renderPage()
    - _renderTable()
    - dataToVirtualDOM
    - diff = this._dd.diff(this._virtualDOM, newVirtualDOM)
    - this._dd.apply(this.dom, diff)
  - Similar to jQuery DataTables, but without the jQuery dependency.
  - Based on Vanilla-DataTables, but written in ES2018.
  - Using diffDOM for updating the DOM
  - 依赖dayjs、diff-dom
  - https://github.com/Mobius1/Vanilla-DataTables /201809/js/MIT/inactive
    - no longer maintained
  - https://github.com/fiduswriter/diffDOM /LGPLv3/ts
    - Gets all modifications, insertions and removals between two DOM fragments.
    - relocations of DOM nodes are preferred over remove-insert operations.

- tui.grid /2.2kStar/MIT/202305/ts/vanillajs
  - https://github.com/nhn/tui.grid
  - http://ui.toast.com/tui-grid/
  - https://nhn.github.io/tui.grid/latest/tutorial-example26-infinite-scroll
  - 基于table标签实现，合并表头列实际样式为.tui-grid-lside/rside-area
  - 不支持plugin
  - 支持sort, filter, 不支持group
  - 支持Merging-cell、支持级联列(column-relations)
  - 依赖xlsx、tui-date-picker、tui-pagination
  - 支持多实例，初始化时返回实例id，用于store/dataSource/eventemitter
  - 视图层依赖preact(多使用extends Component)
    - 但使用时不要求react环境，通过new Grid(options)
    - 很少使用setState, didMount/Update有使用
    - .tsx组件大概40个
  - 状态使用自定义createStore，包含rawData(Row[])、viewData(ViewRow[])、column
    - 内部是个observable对象，基于Object.defineProperty拦截set/get实现
    - 更新store通过dispatch，统一列出了所有更新store的方法，执行`updateFn(store, ...args)`，更新时直接store.prop1 = newValue
  - init初始化流程
    - createStore时会注册一些函数
    - 初始render时会传入dispatch到视图层并放在context，所有后代组件都能拿到
  - update更新流程
    - 交互操作都通过 `grid.dispatch('upFn Name', 参数)` 来触发store更新
    - 自定义connect高阶hoc选取store中部分值传到view层顶级组件，在store值变化时通过hoc更新
  - Powerful Component to Display and Edit Data.
  - TOAST UI Grid is available when using the Plain JS, React, Vue Component.
  - [Is there no undo function?_202207](https://github.com/nhn/tui.grid/issues/1735)
    - Unfortunately, it is not supported.
  - [dataSource](https://github.com/nhn/tui.grid/blob/master/packages/toast-ui.grid/docs/en/data-source.md)
    - Generally, the TOAST UI Grid operates with the local data in the Front End environment. 
    - However, with `dataSource`, TOAST UI Grid can be configured to host remote data as well.
    - Usually when sending a request to a remote server, Pagination is required. 

- gridjs /MIT/3.3kStar/202202/ts/preact
  - https://github.com/grid-js/gridjs
  - https://gridjs.io/
  - 基于display-table实现，使用class类风格
  - data参数支持 `TCell[][]` 或 `{ [key: string]: TCell }[]` or Function
  - 依赖preact，但只作为视图层，useState/useEffect有使用
    - .tsx大概16个，包含主要ui组件
  - store对象自身是个eventemitter，和redux几乎相同，暴露了getState/dispatch/subscribe
    - 使用ContextProvider直接将store传下去
    - 后代组件都可以通过useContext拿到并触发 dispatch(actionFn)，这里和redux不同，会触发所有subscribe过的子状态更新
    - 取值时使用的是useSelector而不是getState，每次都会自动subscribe
  - HTML table plugin written in TypeScript using vanilla js
  - Grid.js can be used with any JavaScript frameworks (React, Angular or VanillaJS)
  - Grid.js has an internal pipeline which takes care of processing, filter and refining the raw data.
  - [Server-side setup | Grid.js](https://gridjs.io/docs/server-side)
    - components like search, sort and pagination can be connected to a server-side backend.
    - All Grid.js plugins support server-side storage.
  - [Plugin basics | Grid.js](https://gridjs.io/docs/plugins/basics)
    - A Grid.js plugin is a Preact Functional Component that render a Virtual Node. 
    - Grid.js will take care of rendering your plugin.

- tabulator /MIT/3.4kStar/202202/js/NoDeps
  - https://github.com/olifolkerd/tabulator
  - http://tabulator.info/
  - https://github.com/ngduc/react-tabulator
    - a JS table library with many advanced features based on tabulator
  - 基于div实现，每行对应的dom元素存在，未实现column span
  - Interactive Tables and Data Grids for JavaScript supporting react, angular, vue
- frappe-datatable /877Star/MIT/202303/js
  - https://github.com/frappe/datatable
  - https://frappe.io/datatable
  - 基于div实现，每行对应的dom元素存在
  - 依赖hyperlist、sortablejs、lodash
  - A simple, modern and interactive datatable for the web
  - https://github.com/tbranyen/hyperlist
    - /MIT/291Star/202006/js/NoDeps
    - A performant virtual scrolling list utility capable of rendering millions of rows
    - a fork of the existing (unmaintained) project: sergi/virtual-list
- FancyGrid /BuyLic/153Star/20212/js/NoDeps
  - https://github.com/FancyGrid/FancyGrid
  - https://fancygrid.com/
  - JS grid library with charts integration and server communication.
  - 基于div实现，实现很特别，表格ui是一列一列相邻放置构成的，每列对应的dom元素存在

- react-datasheet-grid /259Star/MIT/202305/ts
  - https://github.com/nick-keller/react-datasheet-grid
  - https://github.com/Equify/react-datasheet-grid
  - https://react-datasheet-grid.netlify.app/docs/features
  - 依赖react、tanstack-virtual、react-resize-detector
  - more like Airtable or Notion and less like Excel in the sense that instead of dealing with individual cells it deals with entire rows, and each column is responsible for a single property of each row
  - 默认可编辑单元格
  - 操作支持获取operation对象
  - Supports copy / pasting to and from Excel, Google-sheet...
  - Virtualized rows and columns, supports hundreds of thousands of rows
  - undo支持撤销编辑单元格，不支持撤销添加行
    - [Is there anyway I can implement Undo, Update button just after addRow button ?](https://github.com/nick-keller/react-datasheet-grid/discussions/221)
  - [V2 status update_202106](https://github.com/Equify/react-datasheet-grid/issues/37)
  - [Feature Roadmap_202106](https://github.com/Equify/react-datasheet-grid/issues/38)
  - [Show HN: DataSheetGrid, an Airtable-like React component | Hacker News_202311](https://news.ycombinator.com/item?id=38228788)

- react-base-table /1.4kStar/MIT/202303/js
  - https://github.com/Autodesk/react-base-table
  - https://autodesk.github.io/react-base-table/
  - 基于div实现，每行对应的dom元素存在
  - 依赖react-window、memoize-one
  - A react table component to display large datasets with high performance and flexibility
  - 未实现row select(作者为组件unopinionated的目标而未合并pr)，但提供示例
 
- fast-grid /23Star/NALic/202305/ts
  - https://github.com/gabrielpetersson/fast-grid
  - https://fast-grid.vercel.app/
  - performant DOM-based web table.
  - Resuses parts of DOM-tree to reduce expensive DOM mutations
  - Own event loop to prioritize tasks. Never drops a frame
  - Custom virtualization and scrolling. Not limited by browsers 15 million pixel div height limit
  - Non-passive scrolling. Rows will never be seen rows loading into the UI while scrolling

- rsuite-table /327Star/MIT/202010/ts
  - https://github.com/rsuite/rsuite-table
  - http://rsuite.github.io/rsuite-table/
  - 基于div实现
  - 依赖react、rsuite/dom-lib、element-resize-event、lodash
  - 支持colspan, rowspan
  - Support virtualized.

- active-table /9Star/MIT/202305/ts
  - https://github.com/OvidijusParsiunas/active-table
  - https://activetable.io/
  - Framework agnostic table component for editable data experience.
  - 依赖lit
  - 不支持 Undo/Redo、drag-row/column
  - 只有入口处用了lit-@customElement，其他地方vanillajs
  - Column types: Text/Number/Currency/Select/Label/Date/Checkbox
  - API for building custom column types
  - Stream data and update cells programmatically 
  - Import/Export/Paste/Drag&Drop csv, xls, xlsx, ods, txt files

- react-spreadsheet /MIT/953Star/202305/ts/偏向编辑
  - https://github.com/iddan/react-spreadsheet
  - https://iddan.github.io/react-spreadsheet
  - https://iddan.github.io/react-spreadsheet/storybook
  - 依赖scheduler、use-context-selector、fast-formula-parser
  - customizable yet performant spreadsheet for React
  - Performant (yet not virtualized)
  - 支持async cell data
  - 输入数据的类型是二维数组 matrix

- websheets /274Star/MIT/202102/js/inactive
  - https://github.com/WebSheets/websheets
  - https://websheets.github.io/websheets/demo/
  - A ready-to-use component for spreadsheets in the browser
  - https://github.com/WebSheets/websheets-core /js
    - spreadsheet engine in JS for the browser and Node.

- https://github.com/soquel/spreadsheet-in-js /201507/js
  - http://soquel.github.io/spreadsheet-in-js/
  - One idea to implement a spreadsheet in html and javascript.
  - doesn't support more than 26 columns, no AA/AB/...
  - written in pure js, no dependencies
# excel-like-apps
- https://github.com/infinite-table/infinite-react
  - https://infinite-table.com/
  - https://infinite-table.com/docs/learn/examples/dynamic-pivoting-example
  - Infinite Table is a React DataGrid component for displaying virtualized tabular data. 
  - row grouping - both server-side and client-side
  - pivoting - both server-side and client-side
  - column grouping
  - lazy loading
  - keyboard navigation for cells and rows

- https://github.com/1771-Technologies/lytenyte /423Star/apache2+pro/202603/ts/NoDeps
  - https://www.1771technologies.com/
  - https://www.1771technologies.com/demo
  - LyteNyte Grid is a ~40 KB, zero-dependency React data grid engineered for high performance and enterprise-scale datasets. 
  - It can handle 10, 000 updates/sec and render millions of rows. No wrappers. No heavy abstractions.
  - Choose between headless components or a pre-styled grid out of the box, and ship faster with a declarative API that is purpose-built for React.
  - Single & Multi Column Sort
  - Simple Data & Custom Filters
  - Group By Column
  - Group Row Selection
  - Built-In & Custom Aggregation Functions
  - Custom Edit Providers & Update Function
  - Detail Rows (Master Detail)
  - CSV & Excel Export
  - Pinning & Spanning
  - Paginated Rows
  - Row Virtualization
  - 💰 paid
    - Quick Search Filters
    - Set & Tree Set Filters
    - Single & Range Cell Selection
    - Pivot Mode
    - Tree Views
    - Copy, Cut, Paste
    - Server Data Loading
  - [We spent 2 years building the most powerful data table on the market. 4 painful lessons we learned along the way. : r/opensource _202603](https://www.reddit.com/r/opensource/comments/1rtdm93/we_spent_2_years_building_the_most_powerful_data/)
    - Make your code public if your product is a developer library or tool
    - Be patient for promotion
    - Confidence externally, honesty internally
    - Trust the process

- https://github.com/jupyterlab/lumino /ts/PhosphorJS/jupyter
  - https://lumino.readthedocs.io/en/latest/examples.html
  - a set of JavaScript packages, written in TypeScript, that provide a rich toolkit of widgets, layouts, events, and data structures. 
  - 提供了3个经典示例: accordion、data-grid with merged-cell、dock-panel
  - These enable developers to construct extensible high-performance desktop-like web applications, such as JupyterLab. 
  - Lumino was formerly known as PhosphorJS.
  - https://github.com/jupyterlab/lumino/tree/main/packages/datagrid
    - 表格自研，用在 https://github.com/bloomberg/ipydatagrid

- S2 /1.1kStar/MIT/202302/ts
  - https://github.com/antvis/S2
  - https://s2.antv.antgroup.com/examples
  - S2是多维交叉分析领域的表格解决方案，数据驱动视图，提供底层核心库、基础组件库、业务场景库
  - 依赖 @antv/g-canvas、g-gesture、d3-interpolate

- https://github.com/VisActor/VTable /MIT/202401/ts
  - https://visactor.io/vtable
  - VTable is not just a high-performance multidimensional data analysis table, but also a grid artist that creates art between rows and columns
  - based on visual rendering engine VRender.
  - Provides flexible and powerful graphic capabilities, seamlessly integrating with charts of VChart.
  - [VTable: 免费，开源，基于 Canvas 的百万数据秒级渲染前端表格组件库 - 知乎_202310](https://zhuanlan.zhihu.com/p/660261038)
  - https://github.com/VisActor/VRender
    - Rich in features: customizable animations, element composition, narrative arrangement, suitable for various visualization scenarios
    - provides a plugin system for unrestricted expansion.
    - seamless transition between 2D/3D effects with the same configuration.
  - https://github.com/VisActor/VChart
    - cross-platform charting library, but also an expressive data storyteller.
    - It wraps the charting logic based on visual grammar library VGrammar and the component encapsulation based on visual rendering engine VRender

- https://github.com/UgnisSoftware/react-spreadsheet-import /ts
  - https://ugnissoftware.github.io/react-spreadsheet-import
  - Import flow for Excel (.xlsx) and CSV file with automated column matching and validation.
  - A component used for importing XLS / XLSX / CSV documents built with Chakra UI.
  - 导入流程不支持后退

- ali-react-table /530Star/MIT/202112/ts
  - https://github.com/alibaba/ali-react-table
  - https://ali-react-table.js.org/examples/big-data
  - 依赖rxjs、popperjs、styled-components
  - 提供了很多业务场景示例的live demo，以及测试数据
  - 内置虚拟滚动，数据量较大时自动开启，实现了pivot

- https://github.com/flexicious/react-data-grid /未开源/示例多/测试数据
  - https://flexicious.github.io/react-data-grid/
  - a team with 20+ years of experience building data grids
  - This is a monorepo of all the samples and examples

- reactdatagrid /25Star/MIT/202201/ts/class组件/示例友好
  - https://github.com/inovua/reactdatagrid
  - https://reactdatagrid.io/demo
  - 基于div实现，每行对应的dom元素存在
  - 依赖shallowequal、lodash.debounce
  - We've poured our soul into ReactDataGrid and built it from scratch with React
  - Community Edition
    - sort,filter,pagination,edit inline,row selection
    - **colspan** ,context menu,remote data source,column resize/reorder
  - Enterprise Edition也开源了
    - group,pivot,master/detail,tree-grid
    - locked column,row resize/reorder,footer

- https://github.com/fbaligand/kibana-enhanced-table
  - This project is a Kibana plugin that provides two visualizations:
  - Enhanced Table: same than Data Table, but with enhanced features like computed columns, filter bar and pivot table.
  - Document Table (NEW): same thing than 'Enhanced Table' visualization, but for single documents (not aggregations).

- reactgrid /760Star/MIT/202206/ts/inactive
  - https://github.com/silevis/reactgrid
  - https://reactgrid.com/
  - https://reactgrid.com/examples
  - 基于div实现
  - 支持编辑、
  - Add spreadsheet-like behavior to your React app
  - ReactGrid is NOT
    - Record-based data table(like ag-grid, handsontable)
    - Spreadsheet with formulas(like Telerik Kendo UI DataTable, dhtmlxSpreadsheet)
  - [The Great Merge of PRO version into MIT_202201](https://github.com/silevis/reactgrid/pull/65)
  - [Is there any pricing for this library](https://github.com/silevis/reactgrid/issues/101)
    - MIT License
  - https://github.com/silevis/reactgrid-samples
    - /ts/202011
  - fork
    - https://github.com/alonshmiel/reactgrid

- ka-table /58Star/MIT/202305/ts/react/示例丰富
  - https://github.com/komarovalexander/ka-table
  - http://ka-table.com/
  - https://komarovalexander.github.io/ka-table
  - 基于table标签实现
  - Controllable React Table component with Sorting, Filtering, Grouping, Virtualization, Editing and many more

- https://github.com/Apollo-Spreadsheet/apollo-spreadsheet /ts
  - https://apollo.famousgadget.pt/
  - 基于div实现
  - Apollo spreadsheet that supports table and grids out of the box
  - uses Material-UI, React hooks, styled-components and it's fully written in Typescript
  - support cell merging with virtualisation
  - Virtualizable (uses react-virtualized under the hood)
  - Immutable (the data is 100% controlled outside and simply displays that data without modifying it)

- https://github.com/softindex/uikernel /ts/react
  - React.js UI library for building forms, editable grids and reports with drilldowns and filters, 
  - based on simple **unified record model** with client-side and server-side validations and data bindings.

- https://github.com/vitmalina/w2ui
  - /1.8kStar/MIT/202009/js
  - UI widgets for modern apps. Data table, forms, toolbars, sidebar, tabs, tooltips, popups. All under 120kb (gzipped).
  -  It aims to let you define your UI in a declarative way via JSON data structures.
  - [Goals for w2ui 2.0](https://github.com/vitmalina/w2ui/discussions/1955)
    - There is a branch for 1.5 version, it plays a role of a legacy branch

- https://github.com/activewidgets/js /js
  - ActiveWidgets is a multi-framework UI component library. 
  - This package provides datagrid component for javascript / no-framework environments.

- https://github.com/The-Data-Grid/The-Data-Grid
  - https://www.thedatagrid.org/
  - database creation, data collection, and data management platform for environmental auditing.

- https://github.com/KevinVandy/mantine-react-table
  - https://www.mantine-react-table.com/
  - forked from Material React Table
- https://github.com/icflorescu/mantine-datatable /示例丰富
  - https://icflorescu.github.io/mantine-datatable
  - A table component for your Mantine data-rich applications, supporting asynchronous data loading, column sorting, custom cell data rendering, row context menus, dark theme, and more
- https://github.com/Kuechlin/mantine-data-grid
  - https://kuechlin.github.io/mantine-data-grid/
  - Data Grid component with Mantine UI and react-table v8

- https://github.com/karlb/litespread /202108/js/inactive
  - https://github.com/karlb/litespread/wiki
  - https://www.litespread.com/
  - Webapp that uses SQLite as a spreadsheet engine
  - Litespread is viewer and editor for SQLite and CSV files with basic spreadsheet functionality.
  - Litespread runs in your browser without the need for any server-side code
  - 依赖sql.js、blueprintjs、file-saver、moment、papaparse、react
  - formula公式几乎未实现
  - Use SQL syntax in formulas
  - Sync data via Remote Storage

- ethercalc /2.9kStar/Artistic/202012/js/inactive
  - https://github.com/audreyt/ethercalc
  - https://ethercalc.net/
  - EtherCalc is a web spreadsheet
  - Node.js port of Multi-user SocialCalc
  - 依赖xlsx、jquery-ui、jszip
  - Your data is saved on the web, and people can edit the same document at the same time. 
  - [EtherCalc: Open-source web spreadsheet | Hacker News_201408](https://news.ycombinator.com/item?id=8129281)
  - 🍴 forks
  - https://github.com/Tuanshu/ethercalc /202312/
    - post to ethercalc ok
  - https://github.com/davidbwaikato/cbh-ethercalc /202111/js
    - Cell Block HTML fork of Ethercal to support rich HTML representation along with text analysis in a spreadsheet

- https://github.com/githubocto/flat-ui /MIT/202206/ts/inactive
  - https://githubnext.com/projects/flat-data
  - a React component that will render your flat dataset (an array of objects) in a table view
  - 依赖radix-ui、d3、downshift、react-window、zustand
  - auto-detect types
  - show a distribution of each quantitative column
  - calculate a diff between the main dataset and a `diffData` dataset
  - flatgithub.com will automatically re-build and deploy when changes are pushed to the main branch.
  - https://github.com/githubocto/flat-viewer /MIT/202202/ts/inactive
    - https://flatgithub.com/
    - a tool to view un-nested data (CSV & JSON files) in an interactive table
  - https://github.com/githubocto/flat-demo-covid-dashboard /MIT/202406/ts
    - https://octo.github.com/projects/flat-data
    - A Flat Data GitHub Action demo repo
# async/concurrency/worker
- https://github.com/Magnithor/CanvasTable /202201/ts/inactive
  - https://magni.strumpur.net/CanvasTable/
  - Typescript library who draws a table on canvas
  - If you like to use offscreenCanvas and/or keep the data in webworker, then you use mthb-offscreen-canvas-table on main javascript and mthb-offscreen-canvas-table-worker in webworker they will work together

- https://github.com/finos/regular-table /202303/js/NoDeps
  - regular-table exports a custom element named `<regular-table>`, which renders a regular HTML `<table>` to a sticky position within a scrollable viewport. 
  - Only visible cells are rendered and queried from a natively `async` virtual data model, making regular-table ideal for enormous or remote data sets
  - Use it to build Data Grids, Spreadsheets, Pivot Tables, File Trees
  - async Data Models
    - async data model handles slow, remote, enormous, and/or distributed backends.
    - `<regular-table>` won't render until the Promise is resolved
    - The following async example uses a Web Worker, but the same principle applies to Web Sockets
  - Virtual Data Model
    - a simple data model, a two dimensional Array
    - even for very small data sets, regular-table won't read your entire dataset at once. 
    - Instead, we'll need to write a simple virtual data model to access DATA and COLUMN_NAMES indirectly
    - With an async data model, it's easy to serve getDataSlice() remotely from node.js or re-implement the JSON response protocol in any language. 
  - regular-table is natively compatible with `perspective`, a WebAssembly streaming visualization engine. 
    - https://github.com/finos/perspective

- https://github.com/Neovici/cosmoz-omnitable /202211/js
  - Filtering, grouping, sorting table with support for remote data

- https://github.com/eclipse/streamsheets /js
  - An open-source tool for processing stream data using a spreadsheet-like interface.

- https://github.com/blackfisk-tech/vstx-data-table /201904/vue/inactive
  - A data table component for the Vue Stacks Ecosystem
  - VSTX Data Table is a powerful data grid component plugin (Vue.js 2.4+) for displaying, sorting, searching, filtering, and interacting with large and deeply nested data set
  - (Optional) Web Worker support for Filtering, Sorting, and Slicing data
# collab-excel
- https://github.com/microsoft/FluidFramework/tree/main/examples/data-objects/table-view
  - a basic table/grid view built on top of the `@fluid-example/table-document` data object.
  - it only uses it's DDS to store a reference to the created Table Document

- https://github.com/itoumlilt/CRDT-Spreasheet /MIT/202010/ts/inactive
  - CRDT based collaborative Spreadsheet
  - 依赖concordant-crdtlib、delta-crdts、react-spreadsheet
  - This demo app shows a collaborative application developed using a draft implementation of the Concordant API.
  - The application uses the C-Service API which currently supports two eventual consistency backends: revision-based and CRDT-based
# list-grid-div-react
- fixed-data-table-2 /BSD/1kStar/202111/js
  - https://github.com/schrodinger/fixed-data-table-2
  - http://schrodinger.github.io/fixed-data-table-2/
  - React table component designed to allow presenting millions of rows of data.
  - https://github.com/facebook/fixed-data-table
    - /4.3kStar/archived

- react-spreadsheet-grid /MIT/949Star/202101/js/inactive
  - https://github.com/denisraslov/react-spreadsheet-grid
  - https://denisraslov.github.io/grid
  - An Excel-like grid component for React with custom cell editors, performant scroll & resizable columns
  - 功能较少

- https://github.com/walkframe/gridsheet /ts
  - https://docs.walkframe.com/products/gridsheet/examples/
  - Spreadsheet component for React
  - Support formula, custom function
  - Undo & Redo

- react-fluid-table /26Star/MIT/202009/ts/inactive
  - https://github.com/mckervinc/react-fluid-table
  - https://mckervinc.github.io/react-fluid-table/#/
  - 基于div实现，每行对应的dom元素存在
  - 依赖react-window
  - A windowed React table built on top of react-window
- react-data-browser /4Star/MIT/202001/ts/NoDeps/inactive
  - https://github.com/davidalekna/react-components/tree/master/packages/react-data-browser
  - https://codesandbox.io/s/github/davidalekna/data-browser-examples
  - 基于div和flexbox实现
  - The original use case of this component is to build flexbox tables, 
  - however the API is powerful and flexible enough to build things like grids as well.
  - DataBrowser component will not provide any styles, only the functionality.
  - use-table-tools /MIT/18Star/202009/ts/NoDeps/inactive
    - https://github.com/davidalekna/use-table-tools
    - Hooks for building kickass react table components
    - flexbox table with adjustable column configuration
- react-final-table /9Star/MIT/202104/ts/inactive
  - https://github.com/Buuntu/react-final-table
  - https://githubbox.com/Buuntu/react-final-table/tree/master/examples/basic
  - A headless UI component libray for managing complex table state in React.
  - Inspired by react-table but with Typescript support built in and a simpler API.

- https://github.com/petera2c/simple-table /202510/ts
  - https://www.simple-table.com/docs/quick-start
  - a lightweight, high-performance React data grid component
  - 仅依赖react，无其他依赖
  - Free for individuals & startups, affordable PRO tier for growing businesses 

- react-table-library /563Star/MIT/202305/ts
  - https://github.com/table-library/react-table-library
  - yet another table library for React
  - 依赖styled-components
  - 提供了多个主题 material-ui、semantic、bootstrap、antd
  - server-side operations (e.g. search, pagination) as first-class citizens
  - composition over configuration

- react-data-table-component /1.2kStar/Apache2/202112/ts
  - https://github.com/jbetancur/react-data-table-component
  - https://jbetancur.github.io/react-data-table-component
  - 基于div和flexbox实现
  - 依赖styled-components
  - table library with built in sorting, pagination, selection, expandable rows and customizable styling.
  - If you want to achieve balance with the force and want a simple but flexible table library give React Data Table Component a chance.
  - If you require an Excel clone or heavy "enterprise" capabilities, then this is not the React table library you are looking for
  - https://github.com/barisates/react-data-table-component-extensions /js/react
  - Export table data as a CSV or Excel file, filter and print the data.
- react-advanced-table
  - https://github.com/ThaddeusJiang/react-advanced-table
  - http://react-advanced-table.vercel.app/
  - React Advanced Table

- react-bolivianite-grid /MIT/85Star/201905/inactive
  - https://github.com/papasnippy/react-bolivianite-grid
  - https://papasnippy.github.io/react-bolivianite-grid/
  - 基于div实现，每行对应的dom元素不存在
  - React grid component for virtualized rendering large tabular data.
- react-datagrid2 /MIT/20Star/201903/js
  - https://github.com/stevelacy/react-datagrid2
  - https://stevelacy.github.io/react-datagrid2/
  - 基于div实现，样式太简单
  - DataGrid for React. a fork of zippyui
- react-tablize /7Star/MIT/202007/ts
  - https://github.com/alonrbar/react-tablize
  - 基于div和flexbox实现
  - 依赖@emotion/styled、react-custom-scrollbars、react-virtualized-auto-sizer
  - High performance virtual table and grid components for React.
- https://github.com/benox3/react-data-scroller
  - /13Star/MIT/202003/ts
  - 基于div和flexbox实现，大部分功能未完成
  - react-data-scroller was originally designed as a drop in replacement for react-virtualized but focused on preventing the constant mounting, unmounting and repainting of entire rows that occurs.
  - The focus is rendering your data in the most efficient way which involves only rerendering (no unmounts/mounts and only minimal repainting) of the rows and shifting the data around.
- react-absolute-grid /MIT/906Star/202002/layout
  - https://github.com/jrowny/react-absolute-grid
  - http://jrowny.github.io/react-absolute-grid/demo
  - 多用于布局，不用于数据操作，按字段过滤未实现
  - An absolutely positioned, animated, filterable, sortable, drag and droppable, ES6 grid for React.
  - The idea behind AbsoluteGrid is high performance.
    - This is achieved by using `translate3d` to position each item in the layout.
    - Items are never removed from the DOM, instead they are hidden.

- expandable-grid /1Star/MIT/202009/ts/layout
  - https://github.com/MiDovaah/expandable-grid
  - https://codesandbox.io/s/expandable-grid-cw8zx
  - 自身依赖react hooks，示例依赖@reduxjs/toolkit、react-router、material-ui，示例效果好
  - 多用于布局
  - This component is for building grid where elements can be expanded and collapsed.

- smart-grid /3Star/NALic/202006/ts/NoDeps
  - https://github.com/mukuljainx/smart-grid
  - https://mukuljainx.github.io/smart-grid/
  - highly customizable with css.
  - 基于div实现，无依赖，功能较少

- https://github.com/andrglo/react-window-grid /js
  - A react grid with synced column and row headers based on react-window

- window-table /MIT/143Star/202009/ts
  - https://github.com/pupudu/window-table
  - https://window-table.netlify.com/
  - This is a implementation of a virtualized table, based off react-window.
  - Render thousands of rows in a HTML table in React

## div-more

- revogrid /3.4kStar/MIT/202604/ts/web-comp/stencil
  - https://github.com/revolist/revogrid
  - https://revolist.github.io/revogrid
  - https://github.com/revolist/revogrid-react
  - 基于div实现
  - Powerful data grid component built on top of StencilJS.
  - Millions of cells virtual viewport scroll with a powerful core is in-build by default.
  - [Show HN: RevoGrid – Spreadsheet data table for all frameworks | Hacker News_202101](https://news.ycombinator.com/item?id=25894174)
    - Seems more like an alternative to Handsontable than for LibreOffice Calc. That is, its not an end-user spreadsheet, but rather a spreadsheet/datatable component for use in your web applications.
  - [Open source data grid 4 years of experience, what I've learned working on RevoGrid : r/vuejs _202409](https://www.reddit.com/r/vuejs/comments/1fe9w8q/open_source_data_grid_4_years_of_experience_what/)
    - It’s DOM with VNODES. So we put a peace of mind into smart recombinations to make it work faster. Also there is almost no node creation, mostly recombinations and content replacement. 
    - New Technical Goals and version 4+: Customization and integrity are crucial. We build our favorite components straight inside the cells and customize everything without diving into the grid core or forking from the main branch.
    - How fun/gr8/cool would it be to have a data grid/spreadsheet that could transform into a Kanban board or a Gantt chart within the same component? I mean, who doesn’t love multitasking? Our customers usually take these 3 components from different companies and on separate licenses.

- https://github.com/xem/sheet /public/201710/html/js
  - https://xem.github.io/sheet/
  - A 188b/253b spreadsheet app in HTML/JS
  - supports any value: texts, numbers, floats, and formulae. Ex: "=A1+8"
  - cells update in cascade, circular reference protection
  - localStorage persistence
  - [Tinysheet | Hacker News_202110](https://news.ycombinator.com/item?id=28967514)

- https://github.com/seveibar/react-watertable /201911/js/inactive
  - https://www.seveibar.com/react-watertable/
  - A table with advanced editable controls

- recline /2kStar/MIT/202008/js
  - https://github.com/datopian/recline
  - https://github.com/datopian/portaljs
  - https://datopian.github.io/recline/demos/
  - 2020: A framework for building data driven applications in React.
  - 2014: A simple, powerful library for building data applications in pure Javascript and HTML
- zinggrid /38Star/Free4NonCommercial/202008/js/web-comp
  - https://github.com/ZingGrid/zinggrid
  - https://www.zinggrid.com/
  - Our main focus is on fast, responsive, and customizable grids utilizing ES6 and native web components.
  - Our goal is to solve the problem of creating a CRUD grid in under five minutes.
# list-grid-canvas
- x-spreadsheet/wolf-table /10.1kStar/MIT/202112/ts
  - https://github.com/wolf-table/table /ts
  - https://github.com/wolf-table/table-renderer
  - A web-based JavaScript（canvas） spreadsheet
  - Undo & Redo
  - https://github.com/myliang/x-spreadsheet /js
    - https://myliang.github.io/x-spreadsheet
    - [类似石墨文档多人编辑同一个文档是否可以锁定某个区域单元格](https://github.com/myliang/x-spreadsheet/issues/121)
      - 表格对于协同编辑没有什么意义，暂时不会考虑类似功能
    - [Load Json Data Or Excel Data](https://github.com/myliang/x-spreadsheet/issues/55)
  - [Show HN: X-spreadsheet – A JavaScript canvas spreadsheet for web | Hacker News_201901](https://news.ycombinator.com/item?id=19017270)
    - It is hard to makes formulas fast enough with JS.
    - The main speed problems with ethercalc are loading the data from the server and calculating the formulas. I did strip down the code to remove these problems to make web apps work.

- glide-data-grid /836Star/MIT/202202/ts/react-heavy
  - https://github.com/glideapps/glide-data-grid
  - https://grid.glideapps.com/
  - https://glideapps.github.io/glide-data-grid
  - high-performance React grid component, with rich rendering
  - core依赖react、marked、canvas-hypertxt
  - features
    - 支持undo/redo
    - 未实现group
    - scales to millions of rows. Cells are rendered lazily on demand for memory efficiency.
    - Supports multiple types of cells. Numbers, text, markdown, bubble, image, drilldown, uri
    - Editing is built in.
    - Resizable and movable columns.
  - [I wrote an HTML canvas data grid (for Glide) so you don’t have to_202209](https://itnext.io/i-wrote-an-html-canvas-data-grid-so-you-dont-have-to-d945aa4780b4)
  - Canvas based data editor supporting millions of rows, rapid updating, and fully native scrolling.
  - the open-source data grid powering @glideapps, as the basis for the Glide Data Editor.

- treb /4Star/LGPLv3/202305/ts/NoDeps
  - https://github.com/trebco/treb
  - https://treb.app/
  - TREB is a library for adding fully interactive spreadsheets to any web page, web app or blog with just a few lines of code.
  - 支持公式
  - 支持undo，暂未实现redo

- simple-sheet /89Star/MIT/202208/ts/react
  - https://github.com/lvming6816077/simple-sheet
  - https://www.nihaoshijie.com.cn/mypro/simple-sheet/index.html
  - 高性能（使用canvas进行渲染）
  - 依赖react-knova、mobx-react-lite、react-viewer
  - 支持行、列宽度高度、自动筛选视图、单元格样式和格式设置等
  - [【simple-sheet】前端在线Sheet文档技术解析](https://zhuanlan.zhihu.com/p/547293952)

- json5-sheet-editor /10Star/MIT/202208/js
  - https://github.com/smalllong/json5-sheet-editor
  - https://smalllong.github.io/json5-sheet-editor/
  - A simple and high efficient JSON5 based spreadsheet editor
  - 依赖自研lightue、json5

- cheetah-grid /1.3kStar/MIT/202304/ts/NoDeps/vanillajs/偏展示
  - https://github.com/future-architect/cheetah-grid
  - https://future-architect.github.io/cheetah-grid/documents/introduction/
  - Cheetah Grid is a high performance JavaScript data table component that works on canvas
  - 只能选择表格最外层容器div元素，canvas元素无法直接通过拾取工具选中

- rowsncolumns-grid /558Star/MIT/202105/ts/react/inactive
  - https://github.com/rowsncolumns/grid
  - https://rowsncolumns.app/
  - https://www.rowsncolumns.app/demo
  - https://rowsncolumns.github.io/grid
  - Declarative Canvas Grid.
  - 示例非常丰富
  - 依赖react-konva、scroller
  - SpreadSheet - Commercially available Excel-like Grid
  - Exporter - Excel Export plugin
  - Formulas with Cross-sheet references
  - Konva Grid is a pure renderer, that will work with many third-party table plugins
  - [Show HN: React SpreadSheet – Google Sheets-like performance | Hacker News_202007](https://news.ycombinator.com/item?id=23930268)

- canvas-datagrid /BSD/636Star/202202/js/支持vanillajs和web-comp
  - https://github.com/TonyGermaneri/canvas-datagrid
  - https://tonygermaneri.github.io/canvas-datagrid/tutorials/demo.html
  - Canvas based data grid web component.
  - Capable of displaying millions of contiguous hierarchical rows and columns without paging or loading, on a single canvas element.

- https://github.com/ericdrowell/PowerGrid /inactive
  - blazing fast performance and massive scale (100M cells+) via virtualized viewport

- https://github.com/linhuiw/canvas-excel
  - https://linhuiw.github.io/canvas-excel/
  - online excel built with canvas
  - 半成品玩具

- https://github.com/nusr/excel /MIT/ts/NoDeps
  - https://nusr.github.io/excel/
  - Online Excel

- https://github.com/ykg3211/KGSheet /ts/wip
  - http://ykgykg.fun/
  - 一个开源的 Canvas 绘制的高性能 Sheet 组件

- OpenWebSheet /MIT/14Star/202003/ts/vue/inactive
  - https://github.com/SiamandMaroufi/OpenWebSheet
  - https://siamandmaroufi.github.io/OpenWebSheet/
  - OpenSource Web based spreadsheet
  - 基于canvas实现，依赖vue

- https://github.com/farseerdev/sheet-happens /ts/react
  - https://farseerdev.github.io/sheet-happens/
  - Canvas-based spreadsheet component for React.

- react-ws-canvas /MIT/1Star/202005/ts
  - https://github.com/devel0/react-ws-canvas
  - https://codesandbox.io/s/github/devel0/react-ws-canvas/tree/master/example
  - Spreadsheet like react canvas datagrid optimized for performance
- canvas-table /12Star/MIT/202009/ts
  - https://github.com/el/canvas-table
  - https://codesandbox.io/s/canvas-table-6q65o
  - fast table implementation in Canvas with string truncating support.
  - Supports both browser HTML5 canvas and node-canvas
- https://github.com/bojue/canvas-excel
  - 基于Canvas开发Excel的技术预研项目
- https://github.com/Harlock123/LCTDataGrid
  - keep the Canvas object as small as possible by only rendering the visible parts of the resulting Grid

- https://github.com/jakever/canvas-spreadsheet /js/vue/inactive
  - https://harlen.cn/canvas-spreadsheet/
  - 基于Canvas的一款高性能在线编辑组件，拥有仿Excel的复制粘贴、拖拽柄、实时编辑、6种不同数据类型、基本数据校验等功能
  - 支持undo/redo
  - 目前仅提供了Vue版组件，后续会提供React版组件和支持纯JS环境中使用
# list-grid-svg
- svgtable /10Star/NALic/202105/js/d3
  - https://github.com/analyzer2004/svgtable
  - https://observablehq.com/@analyzer2004/svgtable
  - An SVG Table with sticky rows, columns and many other features.
# list-grid-table-tr-td
- jspreadsheet-ce /6.4kStar/MIT/202403/js/单文件
  - https://github.com/jspreadsheet/ce
  - https://github.com/paulhodel/jexcel
  - https://bossanova.uk/jspreadsheet/v4
  - https://bossanova.uk/jspreadsheet/v4/examples/spreadsheet-formulas
  - Vanilla JavaScript data grid plugin to create amazing web-based interactive HTML tables, and spreadsheets compatible data grid with other spreadsheet software
  - 基于table标签实现
  - jQuery is not required anymore.
  - paid-pro: csv, comment, charts, form, formula, search, validator
  - paid-ultimate: toolar-menu, server, shapes
  - https://github.com/sorryljt/react-jexcel
    - 基于jspreadsheet v4版本，封装的React 版本的轻量级Excel插件

- GridManager /551Star/MIT/202308/ts
  - https://github.com/baukh789/GridManager
  - https://gridmanager.lovejavascript.com/
  - https://gridmanager.lovejavascript.com/demo/index.html
  - 快速、灵活的对Table标签进行实例化，让Table标签充满活力
  - 支持常见功能，还提供了如: 导出、打印、列配置、右键菜单、行列移动、用户偏好记忆等功能。
  - 支持在原生JS、jQuery、Angular 1.x、Vue、React环境下使用
  - 内置基础类库jTool, 对原生DOM提供了缓存机制。

- https://github.com/renanlecaro/importabular /js
  - https://renanlecaro.github.io/importabular/
  - Minimal spreadsheet javascript component
  - spreadsheet editor for the web, to easily let your users import their data from excel
  - No sorting, pivot, formula, virtualization etc

- https://github.com/NeXTs/Clusterize.js /6.8kStar/MIT/201901/js/inactive
  - https://clusterize.js.org/
  - Tiny vanilla JS plugin to display large data sets easily
  - 支持table标签、li标签

- FathGrid /12Star/MIT/202011/js/NoDeps
  - https://github.com/admirhodzic/FathGrid
  - 源码是传统的单文件
  - frontend data table/grid with paging, sorting, filtering, grouping, sub-grids, exporting and editing.
  - Can be used with any framework.

- https://github.com/lebonnet/bomtable /js
  - https://lebonnet.github.io/
  - web table like simple excel

## table-tr-td-react

- react-datasheet /MIT/4.2kStar/202108/js/NoDeps
  - https://github.com/nadbm/react-datasheet
  - https://nadbm.github.io/react-datasheet/
  - Excel-like data grid (table) component for React
  - 基于table标签实现，样式太简单

- rc-table /MIT/693star/202010/ts
  - https://github.com/react-component/table
  - http://react-component.github.io/table/
  - 基于table标签实现
  - 依赖react，rc-util，rc-resize-observer，shallowequal

- React-Spreadsheet-Component /MIT/650Star/201811
  - https://github.com/felixrieseberg/React-Spreadsheet-Component
  - http://felixrieseberg.github.io/React-Spreadsheet-Component/
  - 基于table标签实现，功能较少，支持编辑
  - 依赖jquery、mousetrap
  - Spreadsheet Component for ReactJS
  - It's made with ❤️️ by Microsoft DX
- react-data-components /MIT/382Star/201707/js/inactive
  - https://github.com/carlosrocha/react-data-components
  - https://rocha.dev/react-data-components/
  - React components for sorting, filtering and pagination of data.
- react-smart-data-table /MIT/46Star/202006
  - https://github.com/joaocarmo/react-smart-data-table
  - https://joaocarmo.com/react-smart-data-table/examples/bootstrap/
  - 功能较少，样式太简单
  - A smart data table component for React.js meant to be configuration free
  - https://github.com/joaocarmo/react-very-simple-data-table
- material-table /3.4kStar/MIT/202203/js
  - https://github.com/mbrn/material-table
  - https://material-table.com/
  - powerful Datatable for React based on Material-UI Table with some additional features.
  - 依赖 mui5、react-beautiful-dnd、jspdf、date-fns

- Griddle /MIT/2400star/201907/js/inactive
  - http://github.com/griddlegriddle/Griddle
  - http://griddlegriddle.github.io/Griddle/
  - 依赖react，lodash，redux，reselect，recompose
  - Griddle now has a customizable architecture that allows for one-off customizations or reusable plugins.
  - These customization options allow for overriding everything from components, to internal datagrid state management, and more
  - [Architecture](http://griddlegriddle.github.io/Griddle/docs/architecture/)
  - [Plugins](http://griddlegriddle.github.io/Griddle/docs/plugins/)
  - [Customization](http://griddlegriddle.github.io/Griddle/docs/customization/)

- sou-react-table /MIT/184Star/201812/js
  - https://github.com/miadwang/sou-react-table
  - https://miadwang.github.io/sou-react-table/
  - A spreadsheet component for React

- reactabular /MIT/895star/202001/js/NoDeps/inactive
  - https://github.com/reactabular/reactabular
  - https://reactabular.js.org/#/examples/all-features
  - 基于table标签实现，提供了扩展包sticky、virtualized、dnd、resizable

- https://github.com/axisj/axframe-datagrid
  - https://axframe-datagrid.vercel.app/
  - DataSheet for React

- axui-datagrid /MIT/122Star/201912
  - https://github.com/jsdevkr/axui-datagrid
  - https://axui-datagrid.jsdev.kr/introduction
  - 基于table标签实现
  - DataGrid, DataSheet for React
- https://github.com/erfangc/GigaGrid
  - /30Star/MIT/201703/ts
  - http://erfangc.github.io/GigaGrid/
  - React.js table widget with Subtotals (Written in TypeScript)
- reactable /MIT/1.5kStar/201611
  - https://github.com/glittershark/reactable
  - http://glittershark.github.io/reactable/
  - 依赖react, table, data-tables
- https://github.com/bencripps/react-redux-grid
  - /453Star/MIT/202007
  - http://react-redux-grid.herokuapp.com/
  - 依赖react-redux
  - A Grid and Tree Component written in React using the Redux Pattern
  - Local and/or Remote Data Source
  - Local and/or Remote Pagination
- https://github.com/nowaalex/af-virtual-scroll
  - React components for rendering large scrollable data
- https://github.com/qimus/semantic-ui-grid
  - Extended grid for data
- https://github.com/GigaTables/reactables /201906/js
  - a ReactJS plug-in to help web-developers process table-data

## table-tr-td-more

- DataTables /MIT/6.6kStar/202005/jquery
  - https://github.com/DataTables/DataTablesSrc
  - https://github.com/DataTables/DataTables
  - http://www.datatables.net/
  - 基于table标签实现
  - 依赖jquery
  - datable enhancing plug-in for jQuery

- bootstrap-table /10.5kStar/MIT/202010
  - https://github.com/wenzhixin/bootstrap-table
  - https://examples.bootstrap-table.com/
  - 基于table标签实现
  - An extended Bootstrap table with radio, checkbox, sort, pagination, extensions and other added features.
  - Created for Twitter Bootstrap (All versions supported)
  - integration with some of the most widely used CSS frameworks. (Supports Semantic UI, Bulma, Material Design, Foundation, Vue.js)
- ej2-grids /BuyLic/39Star/201810
  - https://github.com/syncfusion/ej2-grids
  - https://www.syncfusion.com/javascript-ui-controls
  - 基于table标签实现
  - Feature-rich grid control with built-in support for data binding, filtering
  - free for gross revenue of less than one million
- sensei-grid /807Star/MIT/201711/js
  - https://github.com/datazenit/sensei-grid
  - https://datazenit.com/static/sensei-grid/examples/index.html
  - 基于table标签实现
  - 依赖jQuery、underscore.js/lodash
  - Simple data grid library written in JavaScript
- WickedGrid /MIT/570Star/201611
  - https://github.com/Spreadsheets/WickedGrid
  - http://spreadsheets.github.io/WickedGrid/
  - 基于table标签实现
  - 依赖jquery
- vaadin-grid /374Star/Apache2/202010/web-comp
  - https://github.com/vaadin/vaadin-grid
  - https://github.com/vaadin/web-components
  - https://vaadin.com/docs/latest/components/grid
  - 基于table标签实现，源码全在html文件中
  - 依赖polymer2、vaadin-text-field、vaadin-themable-mixin
  - a free, high quality data grid / data table Web Component
- https://github.com/vaadin/spreadsheet
  - /44Star/CVALv3/202003/java
  - https://demo.vaadin.com/spreadsheet/
  - 基于div实现
  - a UI component add-on for Vaadin 7 which provides means to view and edit Excel spreadsheets in Vaadin applications.

- https://github.com/stacksjs/table
  - Vue component library
  - fast facet-filtering, sorting, and searching.
  - Meilisearch & Laravel Scout API compatible

- backgrid /2kStar/MIT/201702/js/backbone
  - https://github.com/cloudflarearchive/backgrid
  - an easily stylable semantic HTML data grid
  - 依赖Backbone.js
- dgrid /627Star/BSD/202009/js/dojo
  - https://github.com/SitePen/dgrid
  - https://dgrid.io
  - 每行都有一个table标签，样式太陈旧
  - mobile-ready, data-driven, modular grid widget designed for use with dstore
  - Dojo core is the only hard dependency for dgrid
  - dstore >= 1.0.3 or 1.1.1, for store-backed grids

- ornamentum /140Star/MIT/202001/ts/angular
  - https://github.com/yohangz/ornamentum
  - https://ornamentum.app/
  - 基于table标签实现
  - a highly configurable, UI framework agnostic, fully responsive Angular data table with no external dependencies.
- https://github.com/filamentgroup/tablesaw
  - A group of plugins for responsive tables.
- https://github.com/juijs/jui-grid
  - http://uiplay.jui.io/?p=xtable_1
  - 基于table标签实现
  - JUI grid can handle millions of data, and can display data in a hierarchical structure

- https://github.com/webismymind/editablegrid
  - http://www.editablegrid.net/
  - /765Star/MIT/201811/js
  - aimed at turning HTML tables into advanced editable components
- https://github.com/tim-band/js-dataentrygrid
  - Featherweight Excel-like grid for data entry
# excel
- hyperformula /1.6kStar/GPLv3/202309/ts
  - https://github.com/handsontable/hyperformula
  - https://handsontable.com/docs/hyperformula
  - HyperFormula is a headless spreadsheet built on top of TypeScript. 
  - It is a parser and evaluator of Excel formulas for web applications. 
  - 依赖chevrotain
  - You can use it in a browser or as a service, with Node.js as your back-end technology.
  - HyperFormula comes with a huge library of 391 built-in functions grouped into categories
    - Function syntax compatible with Microsoft Excel and Google Sheets
  - It also supports the use of cross-sheet references, named expressions, different data types, and custom functions.
  - HyperFormula doesn't assume any existing user interface, which makes it a great general-purpose library that can be used in various business applications.
  - Think of it as of the calculation engine behind Excel, but without Excel.
  - [Key concepts | HyperFormula](https://hyperformula.handsontable.com/guide/key-concepts.html)
    - Data processing consists of three phases.
    - Phase 1. Parsing and construction of ASTs
    - Phase 2. Construction of the dependency graph. find the right order of processing cells, also known as topological order
    - Phase 3. Evaluation
  - [Hyperformula support for ag grid](https://github.com/handsontable/hyperformula/discussions/817)
    - The only supported integration of HyperFormula with a spreadsheet solution with an advanced scope of features is with the Handsontable.

- https://github.com/formulajs/formulajs /500Star/MIT/202403/js
  - https://formulajs.info/
  - JavaScript implementation of most Microsoft Excel formula functions
  - originally forked from @handsontable/formulajs version 2.0.2 (released in January 2020). There is no regression, only fixes and new functions since the fork.
  - 依赖jstat、bessel(fn)
  - 🍴 forks
  - https://github.com/handsontable/formula.js /MIT/202001/js/archived
  - https://github.com/davidpolberger/formulajs /201801/js
    - improved error handling, cutting down on dependencies
  - https://github.com/jspreadsheet/formulajs
  - https://github.com/sutoiku/formula.js
- https://github.com/vogtb/spreadsheet /MIT/201807/ts
  - TypeScript/javascript spreadsheet parser, with formulas.
  - This is largely a re-write of Handsontable's https://github.com/handsontable/ruleJS, and https://github.com/sutoiku/formula.js/.
  - The parser was derived from Handsontable's, and many of the formulas were created with FormulaJS's formulas as a reference point.

- https://github.com/ironcalc/IronCalc /3.2kStar/MIT/202512/rust/ts/canvas
  - https://www.ironcalc.com/
  - https://playground.ironcalc.com/
  - IronCalc is a spreadsheet engine and ecosystem
  - This repository contains the main engine and the xlsx reader and writer.
  - Excel compatible
  - https://github.com/ironcalc/web-skin
    - React frontend for IronCalc
  - [IronCalc: a new selfhosted spreadsheet engine and ecosystem : r/selfhosted _202510](https://www.reddit.com/r/selfhosted/comments/1oavgbi/ironcalc_a_new_selfhosted_spreadsheet_engine_and/)
    - where does it store the spreadsheets? Are those local files on the server or in-browser storage?
      - The local files are in browser localstorage. Unless you share they are not public
    - It would be great to have some kind of server-side support for storing files per user. Is this something in the project roadmap?
      - There is a really simple server. But you can expand it anyway you want
    - How many rows of data can it handle? Modern xslz can handle about 1mil.
      - Same as Excel for now. 1 million
    - Is there a roadmap to something larger, perhaps utilizing something like chunked / lazy loading (e.g. Dask on Python)
      - For the time being we are not thinking in going beyond Excel although there might be good reasons to do so.
    - Can the sheets be stored on the server and accessed from anywhere? Do you support accounts? Collaboration? I want to share sheets with my wife.
      - Not yet, we are working on that. If you share a workbook it would be visible to anyone with the link. We are working on the collaboration layer, but we are months away from that. Also we will want to support users. Very early stages
    - Works great, even on mobile. Well done!

- https://github.com/hoplon/javelin /clojure
  - Spreadsheet-like dataflow programming in ClojureScript.

- https://github.com/wx-chevalier/excel.ts /ts
  - excel.ts 是基于 TypeScript 编写的前端 Excel 综合解决方案，包含了 POJO Schema 定义、多框架支持的 Web 端渲染以及 Node 导出服务

- https://github.com/paulfitz/coopy /clang/inactive
  - Diffing, patching, merging, and revision-control for spreadsheets and databases. 
  - Focused on keeping data in sync across different technologies (e.g. a MySQL table and an Excel spreedsheet).
- https://github.com/paulfitz/daff /HaxeLang
  - http://paulfitz.github.io/daff/
  - a library for comparing tables, producing a summary of their differences, and using such a summary as a patch file. 
  - It is optimized for comparing tables that share a common origin, in other words multiple versions of the "same" table.
  - The daff library is written in Haxe Lang, which can be translated reasonably well into js/python/java
  - example shows the changes made in the modified table with respect to the original table. The format used is the highlighter tabular diff.

- https://github.com/SeunMatt/excel_uploader /js
  - a simple JavaScript library that simplify the process of uploading data from large excel files to the server
  - processing the file on the local machine and uploading the extracted data (which is what you actually want) to the server in batch.

- https://github.com/jobsta/reportbro-designer /js
  - https://www.reportbro.com/demo/invoice
  - A javascript plugin to create PDF and XLSX report templates.
  - Everyone can design & edit document templates, and preview them directly in the browser
  - The reports can be generated with ReportBro Lib (a Python package) on the server.
  - 依赖quill.v1、jsbarcode、qrcode
  - https://github.com/jobsta/reportbro-lib

- jsreport /1.1kStar/LGPLv3/202401/js
  - https://github.com/jsreport/jsreport
  - https://jsreport.net/
  - a reporting server letting developers define reports using javascript templating engines like handlebars. 
  - It supports various report output formats like html, pdf, excel, docx, and others. 
  - It also includes advanced reporting features like user management, REST API, scheduling, designer, or sending emails.
  - https://github.com/jsreport/jsreport/tree/master/packages/jsreport-electron-pdf
    - jsreport recipe which renders pdf from html using electron

- https://github.com/tjbearse/sheet-block-editor /js
  - https://tjbearse.github.io/sheet-block-editor/
  - A block based visual editor for Google Sheets

- https://github.com/tabulapdf/tabula /js
  - http://tabula.technology/
  - Tabula is a tool for liberating data tables trapped inside PDF files
  - Tabula only works on text-based PDFs, not scanned documents

- https://github.com/pgte/js-sparse-array /201812/js
  - Sparse array implementation in JS with no dependencies

- https://github.com/handsontable/spreadsheet-viewer /NonOpen
  - A 30-day trial license is available

- https://github.com/vkaswin/google-sheets /202312/ts
  - https://vkaswin.github.io/google-sheets/
  - Built a Google Sheet Clone Using React.js, Node.js, Express.js, MongoDB, and Tailwind

- https://github.com/tanwarAalok/google-sheet-clone /202309/js
  - https://google-sheet-clone.netlify.app/
  - A google sheets clone developed using Vanilla Javascript
  - more
  - https://github.com/Prakhar-FF13/GoogleSheetClone /202307
  - https://github.com/nidhiG30/Sheets-Clone /202307
  - https://github.com/Yashkanekar/excel-vanilla-js
  - https://github.com/Raj-Stark/Google-Sheet-2.0
  - https://github.com/noobCode-69/ExcelClone
  - https://github.com/PrinceAttri/sheets-clone
# server
- https://github.com/forensic-architecture/datasheet-server /MIT/202105/js/inactive
  - Turn spreadsheet data into a structured, dynamic API.
  - Extensible architecture. Currently supports Google Sheet as a source and a REST-like query language, but structured modularly with an intention to support other sources and query languages.
  - [Topic/xlsx_202004](https://github.com/forensic-architecture/datasheet-server/pull/50)
    - adds support for using a local XLSX file as a source

- https://github.com/ExcQL/ExcQL /js
  - A web application transforming excel spreadsheets into SQL scripts

- https://github.com/jupemara/spreadsheet-sql /ts
  - Getting Google spreadsheet data by using like SQL.

- https://github.com/mP1/walkingkooka-spreadsheet /apache2/202401/java
  - A web based spreadsheet application.
  - https://github.com/mP1/walkingkooka-spreadsheet-react /202310/js
    - web client with little if any spreadsheet logic.
    - 依赖mui.v5
  - https://github.com/mP1/walkingkooka-spreadsheet-server
    - A technology agnostic server abstraction for walkingkooka-spreadsheet.
    - It includes a router and some handlers for spreadsheet services.
    - Currently communication between the browser and the server follows a browser client and Http server paradigm
    - The switch to offline mode means the React application simply replaces the Jetty servlet container, rather than using the browser's fetch object to communicate via http to a Jetty server, the request is serialized and posted to a webworker. The webworker hosts the same java server code translated to javascript.

- https://github.com/Roffelchen/spreadsheet-crdt
  - npx y-websocket-server

- https://github.com/gucorpling/gitdox /apache2/202401/python/js
  - https://gucorpling.org/gitdox/
  - GitDox is an online editor for version controlled collaborative XML and spreadsheet editing used for linguistic corpus annotation.
  - The editor interface is based on CodeMirror. 
  - GitHub is used as a remote backend, and SQLite is used for local storage.
  - GitDox is used by Coptic SCRIPTORIUM as an xml editor/transcription tool for Coptic texts
  - Save data locally and directly to GitHub
  - One collaborative version per file: no forks, branches or conflicts possible
  - XML syntax highlighting and auto complete using CodeMirror
  - Realtime collaborative spreadsheet editing with EtherCalc
  - In XML mode, the GitDox editor lets you use a browser based XML editor to enter annotated text in any annotation scheme
  - You can use the spreadsheet mode to annotate tokens of running text, in a one token per line format
# css-table/grid
- https://codepen.io/scottjehl/pen/abJrPOP
  - A CSS-only responsive table with fixed column & row headers, inside a layout, with scroll snapping!

- https://github.com/coston/react-super-responsive-table
  - https://react-super-responsive-table.netlify.app/
  - converts your table data to a user-friendly list in mobile view.
# text-table
- https://github.com/PlainTextTools/plain-text-table /MIT/201504/js/inactive
  - https://plaintexttools.github.io/plain-text-table/
  - Interactively create and edit tables and export them to plain text
  - Interactive input table (using handsontable)
  - Merged cell support (colspan and rowspan)
  - Multiline text in the cells
  - Text alignement support (horizontal and vertical)
# more
- https://github.com/cidgoh/DataHarmonizer /js
  - A standardized browser-based spreadsheet editor and validator that can be run offline and locally
  - Handsontable was used to build the grid
  - SheetJS was used to open and save local files

- https://github.com/rankingdigitalrights/datalab /js
  - Spreadsheet Engineering

- https://github.com/jamerst/o-data-grid
  - A React Data Grid and Query Builder for OData APIs. Based on the Material-UI DataGrid/DataGridPro.
  - an extension to the MUI DataGrid React component which implements features such as sorting, pagination, column selection, and filtering using the OData Standard. 
  - It also utilises Recoil for state management in the filter builder

- https://github.com/amurgola/OpenGridJs /js/wip
  - lightweight JavaScript grid framework that allows you to create fast and easy-to-use data grids in your web application
