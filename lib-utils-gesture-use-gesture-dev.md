---
title: lib-utils-gesture-use-gesture-dev
tags: [dnd, use-gesture]
created: 2023-07-03T08:54:34.802Z
modified: 2023-07-03T08:55:09.372Z
---

# lib-utils-gesture-use-gesture-dev

# guide
- who is using #use-gesture
  - antd-mobile, react-vant, zarm, nutui-react
  - @react-three/drei
  - gutenberg-components
# codebase
- drag-example示例
  - 被拖拽元素的样式 
    - `position: absolute;` 浮层元素基于绝对定位
    - 位置信息保存在 `style="transform: translate3d(-80px, -5px, 0px) scale(1);"`

- 很多非ui类功能(如dnd、zoom)的实现都是给dom对象添加事件监听器
  - 很多hooks的返回值就是这些listeners
# examples
- https://github.com/tackboon/react-grid-rearrange /ts
  - Rearrange grid items via drag and drop
  - 依赖use-gesture、react-spring/web

- https://github.com/woofers/react-sheet-slide /ts
  - https://jaxs.onl/react-sheet-slide/
  - A responsive React draggable sheet and dialog component
  - 依赖use-gesture、react-spring/web

- https://github.com/Mattixes/bottomsheet /ts
  - https://bottomsheet.mattixes.com/
  - built on top of @react-spring/web and @use-gesture/react

- https://github.com/marcoromag/react-tiles-dnd /ts
  - https://codesandbox.io/s/react-tiles-dnd-responsive-bd0ly
  - Manage tiles that can be reordered with drag and drop
  - tiles in multiple sizes: each tile can span an arbitrary number of columns and rows of the grid

- https://github.com/xcfox/react-tile-pane /ts
  - https://xcfox.github.io/react-tile-pane/demo/
  - A React tiling pane manager
  - use @use-gesture/react, react-use-measure as peerDependencies

- https://github.com/beamworks/react-csv-importer /ts/依赖少
  - This library combines an uploader + CSV parser + raw file preview + UI for custom user column mapping, all in one.
  - drag-drop UI to remap input columns as needed
  - 1GB+ CSV file size (true streaming support without crashing browser)
  - automatically strip leading BOM character in data
  - Papa Parse for CSV parsing
  - react-dropzone for file upload
  - @use-gesture/react for drag-and-drop

- https://github.com/jotform/dnd-builder /43Star/MIT/202305/js
  - https://www.jotform.com/open-source/dnd-builder/
  - accessible drag and drop page builder with React
  - 依赖use-gesture、fuse.js、react-dnd-cjs、react-quill、recharts
  - 示例很好

- https://github.com/qiuxiang/canvas-tilemap /ts
  - Super smooth 2d tilemap build with canvas2d.

- https://github.com/wobsoriano/svelte-gesture
  - utility for component-tied mouse/touch gestures in Svelte.
# more
