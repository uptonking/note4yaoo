---
title: toc-lib-excel-virtualized
tags: [excel, grid, lib, list, toc, virtualized]
created: 2023-01-15T15:55:43.004Z
modified: 2023-01-15T15:56:43.100Z
---

# toc-lib-excel-virtualized

# guide

# virtualized-react
- virtua /9Star/MIT/202304/ts
  - https://github.com/inokawa/virtua
  - https://inokawa.github.io/virtua/
  - A zero-config, fast and small (3kB) virtual list component for React.
  - 示例比较了react-virtual/react-window
  - 依赖只有use-sync-external-store
  - Aiming to support many usecases - fixed size, dynamic size, horizontal scrolling, reverse scrolling, rtl direction, sticky, infinite scrolling, placeholder, scrollTo, dnd, table, and more
  - Framework agnostic (WIP): Currently only for React but we could support Vue, Svelte, Solid and more in the future.
  - Fast: Scrolling without frame drop needs optimization in many aspects (reduce CPU usage, reduce GC, reduce layout recalculation, optimize for frameworks, etc). We are trying to combine the best of them.

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
# virtualized-tree
- react-virtualized-sticky-tree
  - https://github.com/marchaos/react-virtualized-sticky-tree
  - https://marchaos.github.io/react-virtualized-sticky-tree/
  - 依赖react-measure
  - 使用场景类似滚动城市列表时能固定省名
  - A React component for efficiently rendering tree like structures with support for `position: sticky`.
  - uses a similar API to react-virtualized.
# virtualized-examples

# more-virtualized

- https://github.com/PolymerLabs/uni-virtualizer
  - provides viewport-based virtualization (including virtual scrolling) for Lit.
