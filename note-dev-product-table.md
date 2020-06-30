---
tags: [components, dev, table]
title: note-dev-product-table
created: '2019-08-29T01:24:09.168Z'
modified: '2020-06-28T01:51:24.457Z'
---

# note-dev-product-table

- A handy/efficient data table to pivot your data

## faq

- 如何区分click和double click
- infinite scroll vs pagination
  - An infinite scroller is a modern alternative to pagination.
  - Rather than wait for the user to click 'next page', new content is automatically loaded everytime the user reaches the bottom of the page. 
  - 手动实现无限滚动的方法
    - 在componentDidMount方法中this.refs.myscroll.addEventListener("scroll",f)
    - 在滚动事件处理函数中判断，若到达底部，则触发请求新数据，再setState
  - pagination ux vs infinite scroll + search/filter
- infinite scroll vs regular scroll
  - 无限滚动因为在开始时渲染的DOM元素较少而性能较高，在滚动时会不停地添加列表项到列表元素，一旦滚动数量过多，仍会由于DOM节点过多造成样式计算或DOM操作开销大，性能就变差了
  - 无限滚动最好还是结合virtualized使用，在每次scroll事件触发时请求数据
- 列表类组件开发常见问题
  - 是否使用virtualized/window来显示可滚动的表格
    - 虚拟化要求定高，可参考react-window的VariableSizeList提供的解决方案
  - 一个单元格或一行数据的更新会触发整个表格的重新渲染
    - 虽然调用了render方法，真实更新的DOM不一定是所有元素节点
    - 可考虑mini store进行数据分片
    - react-table generates a key for row-group div (trGroup). As a result only the rows that are "actually" updated are re-rendered
    - 使用window来显示数据，就算每次重新渲染整个表格，代价也不会特别高
      - With virtual views, data is rendered only in active viewport 
      - element are added/removed upon scroll reducing the rendering/reconciliation payload
      - The *cells and rows are properly keyed* to allow React to only re-render what has changed. If it is causing performance issues then you may need to consider a different package.
  - 使用**table/tr/td**标签还是使用div来显示列表
      - even minor changes will cause reflows of all other nodes in the table
      - div based table is faster in rendering, animation and reflow
      - 使用tr-td会使后面实现drag,resize,sort ,group更复杂
      - ref
        - https://developer.mozilla.org/en-US/docs/Archive/Table_Reflow_Internals
        - http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/
- 列表组件开发难点
  - try to avoid scroll events, especially if they’re not debounced
    - react-intersection-observer falls back to scroll events *only* if necessary
  - 虚拟滚动时如何实现拖拽排序动画
- virtualized or window
  - List virtualization, or "windowing", is the concept of only rendering what is visible to the user. 
  - The number of elements that are rendered at first is a very small subset of the entire list and the "window" of visible content moves when the user continues to scroll. 
  - This improves both rendering and scrolling performance of the list.
  - "Virtualizing" a list of items involves maintaining a window and moving that window around your list. 
  - virtualization focuses on rendering just items visible to the user.
  - 参考
    - https://addyosmani.com/blog/react-window/

## react-table

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
    - about author
      - react-table
      - react-charts(d3js)/Chartjs
      - react-move

## react-data-grid

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

## toc-list-table

- react-window
- react-virtualized
- ag-grid
  - lack of client-side pagination
  - inconvenient to change cell renderer
- tabler-react
  - https://github.com/tabler/tabler-react
  - almost css 
