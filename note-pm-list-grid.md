---
title: note-pm-list-grid
tags: [grid, list, pm, product, table]
created: '2019-08-29T01:24:09.168Z'
modified: '2020-07-14T13:06:26.826Z'
---

# note-pm-list-grid

- A handy/efficient data table to pivot your data

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

- ag-grid
  - lack of client-side pagination
  - inconvenient to change cell renderer
