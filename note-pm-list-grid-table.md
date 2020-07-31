---
title: note-pm-list-grid-table
tags: [grid, list, pm, product, table]
created: '2019-08-29T01:24:09.168Z'
modified: '2020-07-26T04:15:18.011Z'
---

# note-pm-list-grid-table

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

## product-catalog

- 软件提供商
  - 国内一线：石墨，腾讯文档，语雀，钉钉文档，金山文档
  - 国内二线：飞书
  - Gsuite, MS Office
  - Canva

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
