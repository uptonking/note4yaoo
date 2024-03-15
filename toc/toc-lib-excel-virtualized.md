---
title: toc-lib-excel-virtualized
tags: [excel, grid, lib, list, toc, virtualized]
created: 2023-01-15T15:55:43.004Z
modified: 2023-01-15T15:56:43.100Z
---

# toc-lib-excel-virtualized

# guide
- list
  - 常见场景: virtual, infinite, lazy
  - 滚动时，infinite列表的按需加载可看做是lazy
# virtualized
- virtua /871Star/MIT/202403/ts
  - https://github.com/inokawa/virtua
  - https://inokawa.github.io/virtua/
  - A zero-config, fast and small (~3kB) virtual list (and grid) component for React, Vue and Solid.
  - core无依赖，react依赖只有use-sync-external-store
  - 示例比较了react-virtual/react-window
  - 示例非常丰富，包括chat/date-picker/feed(无限滚动)/lazy
  - 提供了同类virtual库的比较表格
  - Aiming to support many usecases - fixed size, dynamic size, horizontal scrolling, reverse scrolling, rtl direction, sticky, infinite scrolling, placeholder, scrollTo, dnd, table, and more
  - Framework agnostic
  - [Bug: `shift` causes render artifacts when items are added/removed mid-list _202312](https://github.com/inokawa/virtua/issues/284)
    - `shift` works great when prepending items, but causes lots of rendering artifacts when adding/removing items from anywhere else in the list
  - [An issue I haven't seen handled in any virtualized library _202312](https://github.com/inokawa/virtua/discussions/293)
    - I have an array of elements that elements might be added or removed for any position in the array. The issue i have seen in every virtualized list is that the scroll position is not maintained
    - It seems that the scroll position maintainer doesn't support adding item to(or removing item from) upper middle of the list.
    - this problem might be solvable with comparing React keys. I'll take a time to research
  - [Virtualized list of items where each item is a virtualized list _202312](https://github.com/inokawa/virtua/discussions/299)
    - Virtualization in virtualized list hasn't been officially tested yet so it may work or may not work. Overriding some styles of VList may help it.
  - [Padding is buggy _202312](https://github.com/inokawa/virtua/issues/272)
    - Padding is always unintentionally buggy. header/footer div approach like other libraries might be better.
    - Incomplete padding support was dropped from `VList` in 0.20.0. Use new `Virtualizer` which has header/footer support. It only supports static header/footer. Dynamic ones will be supported in #315 .

- tanstack-virtual /4.1kStar/MIT/202303/ts
  - https://github.com/TanStack/virtual
  - https://tanstack.com/virtual
  - Headless UI for Virtualizing Large Element Lists in JS/TS, React, Solid, Vue and Svelte
  - Row, Column, and Grid virtualization
  - Fixed, variable and dynamic measurement modes
  - Custom scrolling function support (eg. smooth scroll)
  - [Add reverse support](https://github.com/TanStack/virtual/pull/400)
    - [an inverted chat like list with tanstack's virtual](https://codesandbox.io/p/sandbox/immutable-silence-76pwko)

- react-tiny-virtual-list /MIT/1.8kStar/201910/ts
  - https://github.com/clauderic/react-tiny-virtual-list
  - https://clauderic.github.io/react-tiny-virtual-list/
  - A tiny but mighty 3kb list virtualization library, with zero dependencies
  - Supports variable heights/widths, sticky items, scrolling to index, and more
  - This library draws inspiration from react-virtualized, and is meant as a bare-minimum replacement for the `List` component.
  - [Height of item](https://github.com/clauderic/react-tiny-virtual-list/issues/9)
    - You can pass in a function to itemSize which returns the height of an item given its index. 
  - [I have to force render the list again, if the list item heights are dynamic](https://github.com/clauderic/react-tiny-virtual-list/issues/52)
    - react-tiny-virtual-list uses `PureComponent`, and as such, it has no way to know when the sizes of your items changes when you use a function to get the item sizes.
  - https://github.com/clauderic/virtualized-list
    - A tiny vanilla virtualization library, with DOM diffing
  - 🍴 forks
  - https://github.com/matyas-igor/react-small-virtual-list
    - storybook
  - https://github.com/manvydasu/react-tiny-virtual-list-oss
    - support react v18

- react-window /14kStar/MIT/202304/js
  - https://github.com/bvaughn/react-window
  - https://react-window.now.sh/
  - 基于div实现，每行对应的dom元素不存在
  - React components for efficiently rendering large lists and tabular data
  - React window works by only rendering part of a large data set(just enough to fill viewport).
  - 🐛 [暂不支持 Support just-in-time measured content](https://github.com/bvaughn/react-window/issues/6)
    - https://codesandbox.io/s/dynamic-size-list-zcntp
    - It took me quite some time to figure out that dynamic content is not actually supported by the library and it's only useful for items with fixed/known size
    - if you are looking for a table/grid/tree, this would be a good start autodesk/react-base-table, built on VariableSizeGrid
    - 支持的替代: tanstack-virtual, react-virtuoso
    - [Question: What happened to DynamicSizeList](https://github.com/bvaughn/react-window/issues/516)
  - 🍴 forks
    - https://github.com/webcore-it/react-window
  - https://github.com/vikadata/vikatable /ts
    - 基于 react-window Grid 构建的表格组件
    - @apitable/react-flow 基于其中的 Grid 构建，通过扩展 Grid 的 props 参数，非侵入式支持更多的表格特性, 使其更方便构建表格。
 - table using react-window
    - https://github.com/pupudu/window-table
    - https://github.com/mckervinc/react-fluid-table
    - https://github.com/Autodesk/react-base-table
    - https://github.com/nick-keller/react-datasheet-grid
    - https://github.com/bvaughn/react-window-table /unfinished
- https://github.com/Lodin/react-vtree /202109/ts
  - https://lodin.github.io/react-vtree/
  - React component for efficiently rendering large tree structures
  - provides a lightweight and flexible solution for rendering large tree structures. 
  - It is built on top of the `react-window` library.
  - This library is entirely rewritten to work with the react-window.
- https://github.com/ranneyd/sticky-table /js
  - This is a remake of the incredible `react-window` lib. 
  - It has optionally "locked" headers on all sides implemented with `position: sticky`.
- https://github.com/numero33/react-visual-window
  - React components for fast and efficiently rendering large lists
  - Heavily inspired by react-window
- https://github.com/Console2016/react-window-pro
  - 基础react-window的功能封装，冻结列, 冻结行, 分组等功能
- https://github.com/victor-magarlamov/react-virtualized-tree /201908/js
  - A virtualized tree view react component based on react-window

- react-virtuoso /3.7kStar/MIT/202305/ts/list/table
  - https://github.com/petyosi/react-virtuoso
  - https://virtuoso.dev/
  - powerful React virtual list/table component
  - V1 brings improvements to reverse infinite scrolling behavior - suitable for chat and feed user interfaces.
  - [Dynamic item height](https://github.com/petyosi/react-virtuoso/issues/169)
    - The way react-window handles that is by caching the offsets.
  - [Is it possible to use react-virtuoso with tree components?](https://github.com/petyosi/react-virtuoso/issues/202)
    - That could easily be achieved if the treeview has a "flat" rendering rather than a nested one. I don't know if such mode is possible, though.

- react-virtual-grid /30Star/NALic/202005/js
  - https://github.com/fulcrumapp/react-virtual-grid
  - https://fulcrumapp.github.io/react-virtual-grid/
  - 基于div实现，特别的是，每行的源码顺序从上到下显示出来的单元格dom元素是从右到左排列
  - 依赖element-resize-detector、iscroll、react-proptypes
  - a low level component for building fast tables
- rc-virtual-list /172Star/MIT/202010/ts
  - https://github.com/react-component/virtual-list
  - https://rc-virtual-list.react-component.now.sh/
  - 依赖rc-util、rc-resize-observer
  - React Virtual List Component which worked with animation

- https://github.com/chiefGui/virtualform /202211/ts
  - https://virtualform.vercel.app/
  - fast, responsive and headless virtualization engine for React.
  - We chose `O(1)` algorithms and good caching management over Intersection Observers to guarantee lightning fast, consistent performance
  - designed to satisfy our needs at Starchive. For example, it still does not virtualize plain, vertical lists or masonry-like grids. Also, it is fully responsive without the option to opt-out.
  - I'd only suggest you to use Virtualform if you are specifically looking for a way to virtualize symmetrical, responsive grids. Otherwise, I'd suggest you to use react-window.

- https://github.com/nomic-ai/deepscatter /ts
  - Zoomable, animated scatterplots in the browser that scales over a billion points
  - This is an evolving library for displaying more points than are ordinarily possible over the web.
    - All data is sent in the Apache Arrow feather format, in a custom quadtree format that makes it possible to **only load data as needed on zoom**.
    - Most rendering is done in custom layers using WebGL, with a buffer management strategy handled by REGL.
    - Almost all grammar-of-graphics transforms such are handled on the GPU
    - It also runs in completely static settings, so you can host a million-point scatterplot over something like Github Pages.
  - https://twitter.com/benmschmidt/status/1646549908546113537

- https://github.com/NeXTs/Clusterize.js /202301/js
  - https://clusterize.js.org/
  - Tiny vanilla JS plugin to display large data sets easily
  - [Added option for DOM-node-based virtualization](https://github.com/NeXTs/Clusterize.js/pull/150)
  - [Issue in Implementation](https://github.com/NeXTs/Clusterize.js/issues/74)
    - clusterize just doesn't play well with rowspan
    - Take it as a disadvantage of using virtual scrolling

- https://github.com/WICG/display-locking
  - https://github.com/WICG/virtual-scroller
  - The idea of a virtual scroller is to provide a scrolling "viewport" onto some content, allow extremely large numbers of elements to exist, but maintain high performance by only paying the cost for those that are currently visible. 
  - things like accessible landmark navigation, find in page, or intra-page anchor navigation are based solely on DOM structure, and virtualized content is by definition not in the DOM. 
  - today's virtualized content does not work with search engine
  - https://caniuse.com/css-content-visibility
# virtualized-tree
- react-virtualized-sticky-tree
  - https://github.com/marchaos/react-virtualized-sticky-tree
  - https://marchaos.github.io/react-virtualized-sticky-tree/
  - A React component for efficiently rendering tree like structures with support for `position: sticky`.
  - 依赖react-measure
  - 使用场景类似滚动城市列表时能固定省名
  - uses a similar API to react-virtualized.
# infinite/lazy
- https://github.com/bvaughn/react-window-infinite-loader /MIT/202102/js/inactive
  - https://codesandbox.io/s/5wqo7z2np4
  - InfiniteLoader component inspired by react-virtualized but for use with react-window
  - This demo app mimics loading remote data. Once data has been "loaded", the row number will be displayed.

- https://github.com/omer73364/lazy-load-list /MIT/202202/js
  - https://lazy-load-react-example.netlify.app/
  - Lazy Load List is a lightweight web package that loads items in lazy way
  - Supports most loved JS frameworks

- https://github.com/wellyshen/react-cool-virtual /MIT/202201/ts/inactive/示例丰富
  - A tiny React hook for rendering large datasets like a breeze.
  - 仅依赖react
  - Renders millions of items with highly performant way, using DOM recycling.
  - react-virtual is flexible and headless but using and styling it can be verbose (because it's a low-level hook).
  - a tiny React hook that gives you a better DX and modern way for virtualizing a large amount of data
  - Supports fixed, variable, dynamic, and real-time heights/widths.
  - Built-ins load more callback for you to deal with infinite scroll + skeleton screens.
  - Supports server-side rendering (SSR) for a fast FP + FCP and better SEO.
  - https://github.com/wellyshen/react-cool-virtual/tree/master/examples/infinite-scroll

- https://github.com/onderonur/react-infinite-scroll-hook /MIT/202303/ts/inactive
  - https://onderonur.github.io/react-infinite-scroll-hook/
  - React hook for creating infinite scroll components

- https://github.com/ankeetmaini/react-infinite-scroll-component /MIT/202104/ts
  - https://react-infinite-scroll-component.netlify.com/
  - An infinite-scroll that actually works and super-simple to integrate

- https://github.com/select2/select2 /25.8kStar/MIT/202303/js/inactive
  - https://select2.org/
  - a jQuery based replacement for select boxes. 
  - It supports searching, remote data sets, and infinite scrolling of results.

- react-list /2kStar/MIT/202010/inactive
  - https://github.com/caseywebdev/react-list
  - https://ca.sey.me/react-list/
  - 基于div实现，样式太陈旧
  - 只依赖react
  - A versatile infinite scroll React component.
  - [Support loading data on demand](https://github.com/caseywebdev/react-list/issues/60)
    - it's up to you to decide when you should fetch new data and how. You can use itemRenderer as a gauge for what's being displayed, and you can use getVisibleRange() to get similar information on demand. ReactList won't tell you when to fetch more data because each use case is different
  - [Question: Implementing 'FetchList'](https://github.com/caseywebdev/react-list/issues/24)
  - [Question: How is data fetched, could you hook it up to Relay?](https://github.com/caseywebdev/react-list/issues/104)
    - There isn't a specific callback to fetch data because this is a low-level component that makes no assumptions of your data. You can leverage the renderItem method to know what section of the list is attempting to be rendered and act accordingly
- https://github.com/u-wave/react-list-lazy-load /MIT/202102/js/archived
  - https://u-wave.github.io/react-list-lazy-load/
  - Lazy loading wrapper for react-list
  - This component works for finite collections only. If you have a large list of a known size that you do not want to load all at once, this component allows loading pages once the user scrolls near them. 
  - It does not implement infinite scrolling.

- list.js /11.1kStar/MIT/202011/js/inactive
  - https://github.com/javve/list.js
  - https://listjs.com/
  - https://codepen.io/javve/pen/cLdfw
  - adding search, sort, filters and flexibility to tables, lists and various HTML elements.
  - Built to be invisible and work on existing HTML.

- https://github.com/alibaba/alist /MIT/202206/ts/inactive
  - https://alist.wiki/
  - 在 Fusion/Ant-Design 的 Table 已经成为业界事实标准的情况下，且 Formily 表单方案作为搜索区域的不二之选时，通过对这些方案的整合，可以快速实现标准化的列表场景。
  - 列表状态核心管理包(不依赖任何第三方UI框架)
  - 管理 搜索框 Filter 状态、列表 Table 状态、分页 Pagination 状态、Filter/Table/Pagination 之间的依赖关系、列表生命周期 ListLifeCycle
  - AList是集各方成熟方案于一体的框架
    - 搜索区域使用UForm，Pagination，Table区域则使用Fusion-Next或Ant-Design或其他第三方组件库。 
    - 底层通过核心层抽象列表各个维度数据，UI层则负责适配不同端的特性，顶层通过Schema协议描述快速渲染。

- https://github.com/webcreate/infinite-ajax-scroll /AGPLv3/202209/js/inactive
  - https://docs.infiniteajaxscroll.com/
  - https://infiniteajaxscroll.com/
  - https://infiniteajaxscroll.com/examples
  - a javascript infinite scrolling plugin. 
  - It works by reading the next (and previous) links of your existing server-side pagination and load these pages via AJAX when the visitor scrolls to the end of the page.
  - Progressive enhancement: Infinite Ajax Scroll progressively enhances your server-side pagination with AJAX. When a client doesn't support JavaScript it will fall back on your server-side pagination
# examples

# more
- https://github.com/PolymerLabs/uni-virtualizer
  - provides viewport-based virtualization (including virtual scrolling) for Lit.
