---
title: toc-lib-comp-drag-resize-move
tags: [components, drag, gesture, resize, toc]
created: 2022-02-05T18:44:27.679Z
modified: 2022-02-05T18:45:34.558Z
---

# toc-lib-comp-drag-resize-move

# popular

- dnd-kit /7kStar/MIT/202302/ts/NoDeps
  - https://github.com/clauderic/dnd-kit
  - http://dndkit.com/
  - http://examples.dndkit.com
  - Zero dependencies and modular: built around built-in React state management and context
  - extensible drag & drop toolkit for React.
    - Built for React: exposes hooks such as useDraggable and useDroppable
  - Supports a wide range of use cases: lists, grids, multiple containers, nested contexts, variable sized items, virtualized lists, 2D Games, and more.
  - 作者旧轮子 [react-sortable-hoc](https://github.com/clauderic/react-sortable-hoc)
  - 树形组件示例
    - https://github.com/clauderic/dnd-kit/tree/master/stories/3%20-%20Examples/Tree
    - https://5fc05e08a4a65d0021ae0bf2-vrdufzklrj.chromatic.com/?path=/story/examples-tree-sortable--basic-setup
  - https://twitter.com/clauderic_d/status/1375623307060510731
    - I recently built a sortable tree example with @dndkit.
    - Collapsible subtrees, removable items, unlimited nesting, dynamic placeholder, keyboard support and zero external dependencies.
  - forks
    - https://github.com/wix-playground/dnd-kit
    - https://github.com/replayio/dnd-kit

- use-gesture /7.5kStar/MIT/202302/ts/vanillajs
  - https://github.com/pmndrs/use-gesture
  - https://use-gesture.netlify.app/docs/examples/
  - a library that lets you bind richer mouse and touch events to any component or view
  - move it, zoom it, drag it, scroll it, pinch it
  - originally built for React, v10 is now platform agnostic, and can work in vanilla javascript.

- react-draggable /6kStar/MIT/202201/js
  - https://github.com/react-grid-layout/react-draggable
  - http://react-grid-layout.github.io/react-draggable/example/
  - React draggable component
- react-resizable /1.2kStar/MIT/202009/js
  - https://github.com/react-grid-layout/react-resizable
  - https://react-grid-layout.github.io/react-resizable/index.html
  - A simple React component that is resizable with a handle.
  - 依赖react-draggable

- react-dnd /14.5kStar/MIT/202009/ts/redux
  - https://github.com/react-dnd/react-dnd
  - https://react-dnd.github.io/react-dnd/examples/sortable/simple
  - core依赖于redux
  - Drag and Drop for React
  - 拖拽列表项的示例，没有显示底层被拖拽项的阴影

- react-beautiful-dnd /26.2kStar/Apache2/202103/js/redux/inactive
  - https://github.com/atlassian/react-beautiful-dnd
  - https://react-beautiful-dnd.netlify.app/
  - Beautiful and accessible drag and drop for lists with React
  - 可参考并重写示例
  - rbd is a higher level abstraction specifically built for lists (vertical, horizontal, movement between lists, nested lists and so on). 
  - [DnD with line drop indicators](https://github.com/atlassian/react-beautiful-dnd/issues/2461)
    - https://codesandbox.io/s/react-beautiful-dnd-react-virtualized-forked-c7sm5b
  - [Maintenance will continue with @hello-pangea/dnd 🎉 (react 18 support)](https://github.com/atlassian/react-beautiful-dnd/issues/2437)
- https://github.com/hello-pangea/dnd /ts
  - https://dnd.hellopangea.com/
  - 依赖react-redux.v8、memoize-one、raf-schd

- dflex /1.5kSStar/MIT/202302/ts
  - https://github.com/dflex-js/dflex
  - https://www.dflex.dev/demo/lists/nested/
  - built with vanilla Javascript and implemented an enhanced transformation mechanism to manipulate DOM elements. 
  - It is by far the only Drag and Drop library on the internet that manipulates the DOM instead of reconstructing it and has its own scheduler and reconciler.
  - Support strict transformation between containers.

- neodrag /509Star/MIT/202210/ts
  - https://github.com/PuruVJ/neodrag
  - https://stackblitz.com/edit/typescript-wvnloa
  - A vanilla JS draggable library
  - Lightweight multi-framework libraries for draggability on the web.
  - 支持vanillajs/react/vue/svelte/solid
  - Is the library also good for dragging items between lists?
    - Not directly, I'm afraid. This is for arbitrary dragging, not the sortable kind. You can use svelte-dnd-action or SortableJS for that for easy usage

- re-resizable /1.1kStar/MIT/202110/ts/代码少
  - https://github.com/bokuweb/re-resizable
  - https://bokuweb.github.io/re-resizable/
  - A resizable component for React
  - 只依赖fast-memoize
- react-rnd /1.8kStar/MIT/202106/ts/代码少
  - https://github.com/bokuweb/react-rnd
  - https://bokuweb.github.io/react-rnd/stories
  - A resizable and draggable component for React.
  - 依赖react-draggable、re-resizable

- moveable /4.8kStar/MIT/202009/ts
  - https://github.com/daybrush/moveable
  - https://daybrush.com/moveable/
  - https://daybrush.com/moveable/
  - Moveable! Draggable! Resizable! Scalable! Rotatable! Warpable! Pinchable! Groupable! Snappable!

- react-grid-layout /16.9kStar/MIT/202202/js
  - https://github.com/react-grid-layout/react-grid-layout
  - https://strml.github.io/react-grid-layout/examples/0-showcase.html
  - A draggable and resizable grid layout with responsive breakpoints, for React.
  - 卡片能随意拖动和缩放
  - 静止状态时，卡片不可重叠遮挡
  - forks
  - https://github.com/DEXAGA/react-grid-layout-hooks /202105/ts
    - Migration to Hooks
    - Migration to Typescript

- https://github.com/wouterraateland/use-pan-and-zoom
  - https://codesandbox.io/s/n3rpmj60w0
  - React hook for panning and zooming a container

- https://github.com/tanishqkancharla/draggable-list
  - https://github.com/ccorcos/draggable-list
  - A well-contained abstraction with simple performant animations.

- https://github.com/taye/interact.js /ts
  - http://interactjs.io/
  - JavaScript drag and drop, resizing and multi-touch gestures with inertia and snapping for modern browsers
  - not modifying the DOM except to change the cursor (but you can disable that)
  - Support for HTML and SVG
# zoomable ui
- https://github.com/aarondail/react-zoomable-ui
  - https://aarondail.github.io/react-zoomable-ui/example/
  - Make your HTML elements and React components zoomable, and build interesting zoomable UIs. 
  - Make your whole page zoomable and pan-able, or just part of it.
- https://github.com/zumly/zumly
  - https://zumly.org/
  - a JS library for building zooming user interfaces
  - Instead of hyperlinks and windows, Zumly uses zooming as a metaphor for browsing through information.
- https://github.com/zircleUI/zircleUI
  - https://zircleui.github.io/docs/
  - Enjoy a different UI/UX with the built-in zoomable navigation.
  - Circles everywhere: Breaking away from the conventional UI with a circular UI Kit.

- https://github.com/allain/zuite /202205/js
  - A toolkit for building modern zoomable user interfaces
# more
- sortablejs /21.1kStar/MIT/202203/js/NoDeps/代码少/inactive
  - https://github.com/SortableJS/sortablejs
  - https://sortablejs.github.io/sortablejs/
  - a JS library for reorderable drag-and-drop lists.
  - You can use any element for the list and its elements, not just ul/li

- https://github.com/bevacqua/dragula /js
  - Drag and drop so simple it hurts

- https://github.com/Shopify/draggable /js
  - Draggable is no longer maintained by its original authors
