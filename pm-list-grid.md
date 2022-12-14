---
title: pm-list-grid
tags: [grid, list, pm, pmgr, table]
favorited: true
created: 2019-08-29T01:24:09.168Z
modified: 2021-05-23T16:34:27.206Z
---

# pm-list-grid

# roadmap

- features
  - local-first
  - database views
  - collaborative editing

- table-view
  - sort/filter/group + test
  - resizable-table/list
- kanban-view
  - sort/filter/group + test
  - views switch test
- pivot-table component
  - examples/stories
- prosemirror-pivot-table
  - alternative to prosemirror-table
- pivot-table collab
  - crdt
  - yjs
  - prosemirror yjs
  - test
- ckeditor-pivot-table
  - alternative to ckeditor-table
- refactor pivot table  to vanillajs
  - react-table v7 to v8
- refactor to plugins support
# guide
- ag-grid源码要点
  - ioc
  - rowModel
  - eventService
  - virtualize
  - rowRender
  - cellRender
- data-grid实现的难点
  - col span  
    - 实现起来较容易，参考cellRangeRenderer
  - row span  
    - 难以实现
    - 采用z-index，合并单元格后的内容对齐方式需要计算
    - 实现 `flex-direction:column` 不合适，难以同时实现row span和col span
    - ui结构采用分组，每次合并单元格需要动态修改的元素过多
  - multi-row-col-span
    - 同时合并多行多列，如相邻的两行两列合并成一个单元格
  - 滚动
- grid实现细节
  - 常将大部分样式如display布局放在className中，但元素具体位置相关的样式如position, left, top, width, height通过style object直接传递
  - 注意header-column和row-cell的相同点，可以共用很多逻辑，如virtualize
# why-datable
- very few options for a data table with all the following 
  - div-based css table, not html table element
  - framework agnostic
  - fully featured

- ag-grid缺点
  - group功能在企业版，需付费
# features
- core
  - sort/filter/group
    - group-header
  - select/edit
  - virtualize
  - component-wrapper
    - ag-list
    - read-only-grid

- 特色功能点
  - 现有表格的快速集成(导入、theming)
    - 开发单独库实现table-tr-td的操作
  - table-clone: 或复制粘贴表格到同一文档，需要设计布局，auto-layout自动对齐
  - table from table: 大表中copy部分小表进行分析
  - data(~~viz~~)-replay: 两种方案，puppeteer、rrweb

- 表格版本区分
  - readonly，适合分析
  - edit，适合编辑
# draft
- fields
  - column type: rich text editor

- 功能相关
  - 搜索结果
    - 快速跳转到第1个、最后一个、第N个
    - 随着浏览位置的变化，显示当前显示的是第几个，如11/28

- 样式相关
  - 默认显示成没有分行样式的整篇文档，鼠标悬浮时该行浮起提升

- 可拖拽的主界面
  - 考虑设计成类似trello这类数据卡片，可以任意拖动、缩放、auto-layout自动对齐

- 类似wikipedia，设计模版时，当连续几行单元格内容相同时，自动合并单元格
# extensions
- grid-config(defaults+utils)

- Multiple Sorting
  - The DataGrid can sort values by a single or multiple columns.
    - Single sorting mode. 
      - A user can click the column header to sort by this column and click it again to change the sort order (ascending or descending). 
      - An arrow icon in the column's header indicates the sort order.
    - Multiple sorting mode. 
      - A user can hold the Shift key and click column headers in the order the user wants to apply sorting. 
      - To cancel a column's sorting settings, a user should hold the Ctrl key and click the column header.

- keyboard-shortcuts
  - 列表使用jk键导航

## experimental

- canvas renderer for data-grid/table
- web worker
- apache-arrow columnar format vs pandas-dataframe
- wasm vs webgpu
# integrations/connections
- excalidraw
- remotion
  - 快速制作数据动态变化图/视频
# grid-implementation
- ## react-table
  - required-props: data, columns
  - data: 必需，类型是 array of objects
  - style: 自定义
  - ui实现：自定义，headless
  - note
    - 基于react实现，react only 
    - 用于方便实现ui的工具: useBlock/Absolute/FlexLayout
      - 不同布局需要的条件不一样，如BlockLayout需要指定宽度
- ## ag-grid
  - required-props:rowData, columnDefs, 父元素width, height
  - data: 必需，类型是 array of objects
  - style: ag-grid.css, ag-theme-alpine.css
  - ui实现：行列部分基于position-absolute，整体结构基于div-flex
  - note
    - 基于js实现，可用于react/vue/angular
- ## handsontable
  - required-props: 都是非必需，宽高也是非必需
  - data: 非必需，类型可以是array of arrays, array of objects, 还可以将columns值设为函数再计算处理后返回列信息
    - 不传入data时，会显示占满父元素的空格表格
    - 可以通过columns设置处理方式，从nested object的属性中取值
  - style: handsontable.full.css
  - ui实现: 基于table, tr, td和display-table-cell
  - note
    - 从自身向父元素查找带有width,height和 `overflow:hidden` 的元素并占满
- ## react-virtualized
  - required-props: cellRenderer, width, height，rowCount, rowHeight, colCount, colWidth
    - cellRenderer is responsible for rendering a single cell, given its row and column index.
  - data: 必需，间接通过cellRenderer传入
  - style: styles.css, ReactVirtualized__Grid
  - ui实现: div-position-absolute
  - note
    - Grid row heights and column widths must be calculated ahead of time and specified as a fixed size or returned by a getter function.
    - `List` uses a `Grid` internally to render the rows and all props are relayed to that inner `Grid`
    - `Table` Component is created with flexbox. 
      - This allows it to have a fixed header and scrollable body content. 
      - It also makes use of `Grid` for windowing table content so that large lists are rendered efficiently
- ## react-window
  - required-props:children, width, height, rowCount, rowHeight, colCount, colWidth
  - data: 必需，通过react component的children传入，类型自定义
    - 要能在children中通过rowIndex,colIndex获取
  - style: 无内置，需要自定义
  - ui实现: div-flexbox
  - note
    - VariableSizeGrid的colWidth和rowHeight值类型都是函数
# popular-data-grid-docs
- https://www.ag-grid.com/javascript-grid-reference-overview/
- https://handsontable.com/docs/8.0.0/tutorial-features.html
- https://fancygrid.com/samples/
  - https://fancygrid.com/docs/grid-concepts/understanding-fancygrid
- https://ej2.syncfusion.com/demos/?#/material/grid/filter.html
- https://js.devexpress.com/Demos/WidgetsGallery/Demo/DataGrid/
- https://www.grapecity.com/spreadjs/docs/v13/online/UsingtheSpreadSheetsElement.html
# pieces
- To use an absolute layout, you would need to either 
  - use div instead of table element
  - or, switch all of your table element styles to be `display: block` ( `display: inline-block` for cells) 
  - and last but not least, when using an absolute layout, your rows must have a predefined height, eg. 50px.
# product-react-table
- a lightweight, fast and extendable datagrid built for React
- features
  - Lightweight at 11kb (and just 2kb more for styles)
  - Fully customizable (JSX, templates, state, styles, callbacks)
  - Column-definition-driven. No composition needed.
  - Client-side & Server-side pagination
  - Multi-sort
  - Filters
  - Pivoting & Aggregation
  - Minimal design & easily themeable
  - Controllable via optional props and callbacks everywhere possible(Fully Controlled Component)
- drawbacks
  - cell edit not support 
- usage
  - basic table view
  - sort
  - filter
  - Row grouping & aggregation
  - Multi-Pivoting
  - pagination & page jumping
  - row selection
  - expand/collapse
  - subcomponent/table in table
  - editable data
  - column reordering
  - fixed columns
  - column rendering
- reference
  - [Why I wrote React-Table](https://medium.com/@tannerlinsley/why-i-wrote-react-table-and-the-problems-it-has-solved-for-nozzle-others-445c4e93d4a8#.axza4ixba)
    - expectation for tables
      - Good Visual and Architectural Structure
      - Client-Side Sorting and Pagination
      - Support functional customization(styles) by callbacks
      - Powerful Templating to override the display of cells
      - Group and aggregate
      - More
    - pitfalls
      - infinite or virtualized scrolling was the cause of problems
      - difficult for sorting, grouping, column dragging
      - react-table styles are minimal and designed to be overridden
    - ag-grid-xp
      - lack of client-side pagination
      - inconvenient to change cell renderer
    - about viz
      - 海量svg元素的动画和操作体验很不友好
      - Chart.js has support for mixing chart types, animations
# product-react-data-grid
- Excel-like grid component built with React
- features
  - Lightning Fast Rendering by smart windowing 
  - Rich Editing and Formatting for cells
  - Configurable & Customizable
  - Packed common Excel Features
- drawbacks
  - pivot not supported
- usage
  - custom cell editor
  - custom cell formatter
  - column frozen/reorder/resizing/events
  - custom row renderer
  - row/cell range selection
  - sort
  - filter
  - group
  - tree view
  - context menu
  - keyboard navigation
- changelog
  - 201606-1.0.0-only exports one package react-data-grid, rdg/addons
  - 201701-2.0.0-exports two main packages react-data-grid and rdg-addons
  - 201709-3.0.0-replace create-react-class with es6 class
  - 201804-4.0.0-use latest version of react-context-menu(2.9 breaking)
  - 201810-5.0.0-rewrite core to improve nav and scroll performance 
  - 201811-6.0.0-use react portals for cell editors & upgrade build tools
  - 201904-7.0.0-alpha.2-migrate to typescript
- react-data-grid使用的className
  - 不确定的类
    - row-selected， has-tooltip，has-error
  - 使用了的样式
    - pull-right
    - glyphicon-remove form-control-feedback
  - ChildRowDeleteButton组件使用了glyphicon glyphicon-remove-sign 
  - FilterableHeaderCell组件使用了form-group/control
# product-react-base-table
- A react table component to display large datasets with high performance and flexibility
- BaseTable is designed to be the base component to build your own complex table component
- dependencies: react-window, react-virtualized-auto-sizer
- There are a lot of highly flexible props like `xxxRenderer` and `xxxProps` for you to build your own table component
- There is a PR to add selection feature, but I don't want to merge it with good reasons
- Inline Editing is a very common feature in a table, 
  - but it's highly coupled with specific ui libraries, so it won't be a part of BaseTable itself.
  - Inline Editing would be a bit tricky in BaseTable because of it's using the virtualization technology to render the rows, there is `overflow: hidden` for the table and rows and cells, 
  - so if your editing content is larger than the cell area, the content would be cut, 
  - you genius would find that you could override the `overflow: hidden` via style to prevent the content to be clipped, but PLEASE DON'T DO THAT, as there would be always problems with this solution, e.g. what would happens if it's in the last row?
  - The **recommended solution** is using something like `Portal` to render the editing content out of the cell, then it won't be constrained in the cell. 
    - As `Portal` needs a container to attach the target to, most of the custom renderers provide a param `container` to be used in this case, the `container` is the table itself.
  - Internally we are using the `Overlay` component from `react-overlays` to do that, react-overlays is based on `Popper.js` which provides excellent positioning mechanism.
  - If you are using fixed mode(fixed=true) with frozen columns, there will be a problem with the Popper.js.
    - there would be three tables internal tables to implement the frozen feature, 
    - and those tables are all scrollable, then the positioning could be not expected, 
    - you could change the `boundariesElement` to `viewport` or the `container` to fix that.
