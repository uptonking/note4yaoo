---
title: note-pm-list-grid-dev
tags: [dev, grid, list, product, table]
created: '2020-07-13T13:34:22.833Z'
modified: '2020-07-14T13:05:46.032Z'
---

# note-pm-list-grid-dev

## usage

## api

## summary

- 如何区分click和double click
  - setTimeout
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
