---
title: note-pm-list-grid-table
tags: [grid, list, pm, product, table]
created: '2019-08-29T01:24:09.168Z'
modified: '2020-07-26T04:15:18.011Z'
---

# note-pm-list-grid-table

## summary

- data-grid实现的难点
  - row span  
    - 采用z-index，合并后的对齐需要计算
    - 实现 `flex-direction:column` 不合适，难以同时实现row span和col span
    - ui结构采用分组，每次合并单元格需要动态修改的元素过多
  - 滚动

## grid-implementation-vs

- ### react-table
  - required-props: data, columns
  - data: 必需，类型是 array of objects
  - style: 自定义
  - ui实现：自定义，headless
  - note
    - 基于react实现，react only 
    - 用于方便实现ui的工具: useBlock/Absolute/FlexLayout
      - 不同布局需要的条件不一样，如BlockLayout需要指定宽度
- ### ag-grid
  - required-props:rowData, columnDefs, 父元素width, height
  - data: 必需，类型是 array of objects
  - style: ag-grid.css, ag-theme-alpine.css
  - ui实现：行列部分基于position-absolute，整体结构基于div-flex
  - note
    - 基于js实现，可用于react/vue/angular
- ### handsontable
  - required-props: 都是非必需，宽高也是非必需
  - data: 非必需，类型可以是array of arrays, array of objects, 还可以将columns值设为函数再计算处理后返回列信息
    - 不传入data时，会显示占满父元素的空格表格
    - 可以通过columns设置处理方式，从nested object的属性中取值
  - style: handsontable.full.css
  - ui实现: 基于table, tr, td和display-table-cell
  - note
    - 从自身向父元素查找带有width,height和 `overflow:hidden` 的元素并占满
- ### react-virtualized
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
- ### react-window
  - required-props:children, width, height, rowCount, rowHeight, colCount, colWidth
  - data: 必需，通过react component的children传入，类型自定义
    - 要能在children中通过rowIndex,colIndex获取
  - style: 无内置，需要自定义
  - ui实现: div-flexbox
  - note
    - VariableSizeGrid的colWidth和rowHeight值类型都是函数
- ### react-data-grid

## pieces

- MUI tables use HTML table elements, not divs and styles. 
- To use an absolute layout, you would need to either 
  - use divs instead of table elements 
  - or, switch all of your table element styles to be `display: block` ( `display: inline-block` for cells) 
  - and last but not least, when using an absolute layout, your rows must have a predefined height, eg. 50px.

## product-react-table

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
    - about viz
      - 海量svg元素的动画和操作体验很不友好
      - Chart.js has support for mixing chart types, animations

## product-react-data-grid

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

## solution-catalog-list-table

- antd table
  - https://ant.design/components/table-cn/

- ag-grid
  - lack of client-side pagination
  - inconvenient to change cell renderer

## office-online-product-catalog

- office软件提供商
  - 国内一线：石墨，腾讯文档，语雀，钉钉文档，金山文档
  - 国内二线：飞书
  - 国外主流：Gsuite, MS Office
  - 周边产品：Canva

- 文字编辑器
  - 石墨 Quill
  - 腾讯 Etherpad
  - 语雀 slate转自研

- 表格
  - 石墨 spreadjs
  - 腾讯 handsontable转自研 

- 多人协作冲突解决  
  - OT算法，石墨和腾讯文档都是
  - [揭开在线协作的神秘面纱 – OT算法](http://www.alloyteam.com/2019/07/13659/)
  - [实现一个多人协作在线文档有哪些技术难点?](https://www.zhihu.com/question/274573543)

- 选型参考
  - 既满足协作编辑需求，也满足Office功能的兼容性需求，支持 office open xml
  - 在线文档作为其他产品的基础功能，如网盘支持在线打开文档
