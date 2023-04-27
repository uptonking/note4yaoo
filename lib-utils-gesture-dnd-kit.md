---
title: lib-utils-gesture-dnd-kit
tags: [dnd, drag, gesture, lib, list, utils]
created: 2022-02-06T13:40:34.638Z
modified: 2022-06-04T00:44:30.749Z
---

# lib-utils-gesture-dnd-kit

# guide

- features
  - good docs and examples
    - tree
    - kanban
  - 官方提供了virtualized示例
    - 基于同作者的 react-tiny-virtual-list
  - Built for React
    - exposes hooks such as useDraggable and useDroppable, 
    - and won't require you to re-architect your app or create additional wrapper DOM nodes.
  - Feature packed
    - customizable collision detection algorithms, multiple activators, draggable overlay, drag handles, auto-scrolling, constraints, and so much more.
  - Fully customizable & extensible
    - Customize every detail – animations, transitions, behaviours, styles. 
    - Build your own sensors, collision detection algorithms, customize key bindings and so much more.
  - Zero dependencies and modular
    - the core of the library weighs around 10kb minified and has no external dependencies. 
    - It's built around built-in React state management
  - Built-in support for multiple input methods
    - Pointer, mouse, touch and keyboard sensors.
  - Performance
    - It was built with performance in mind in order to support silky smooth animations.
  - Presets
    - Check out @dnd-kit/sortable

- examples
  - 官方示例要点 server
    - droppable - collision detection algorithm 切换内置的冲突检测算法
    - restrict to window edges 限制被拖拽元素在容器内
    - snap to grid 可让被拖拽元素沿着网格格子移动
    - snap center to cursor 让元素中心先移动到鼠标，再拖拽
    - render before sorting
    - transformed container
    - pages layout 提供了指示线示例
  - [virtualized with react-tiny-virtual-list](https://master--5fc05e08a4a65d0021ae0bf2.chromatic.com/?path=/story/presets-sortable-virtualized--basic-setup)
  - [Drag and Drop Form Builder](https://github.com/clauderic/dnd-kit/discussions/639)
    - https://codesandbox.io/s/dnd-kit-form-builder-fii0zh
      - 页面内容块能再次拖拽
    - https://codesandbox.io/s/distracted-mendel-hibbgu
      - 页面内容块不能再次拖拽
  - dnd-kit builder
  - 效果参考
  - [树形控件 Tree - Ant Design，拖拽时显示指示线](https://ant.design/components/tree-cn)
    - 拖拽父级菜单时，所有子级会先隐藏为一条指示线

- alternatives
  - use-gesture(vanillajs)
  - react-dnd

- 拖拽功能的调试方法
  - 👉🏻 使用浏览器devtools，对类似mouseup/keyDown的事件打断点，或在代码中debugger
  - 👉🏻 使用键盘实现拖拽，很容易调试拖拽中的状态
# issues

## not-yet

- not-yet
  - 🤔 树的递归渲染是如何实现的
  - DragOverlay内为什么不要使用useDraggable/useSortable
  - 如何接收外部(非DndContext内)的dnd事件
  - resize
  - performance: rerender
  - collision

- [Is there any way to force a droppable to accept draggables that come from outside its parent DndContext? ](https://github.com/clauderic/dnd-kit/discussions/181)
  - [Difficult to manage drags across sections of the app](https://github.com/clauderic/dnd-kit/issues/58)
  - This should be a lot easier to manage with the introduction of the `useDndMonitor` hook along with the fact that data defined in `useDraggable` and `useDroppable` is now exposed on the `active` and `over` properties.

- 💡 [re-rendering ALL draggable items on drag start and such](https://github.com/clauderic/dnd-kit/issues/1071)
  - [React Context Performance Pitfalls](https://blog.devgenius.io/react-context-pitfalls-9fb67723183b)
  - https://codesandbox.io/p/sandbox/throbbing-moon-uvbor3
  - it seems that all draggable components will re-render when one of them is dragged, it happens because of the use of context in useDraggable and the way that the context exposes the values, for example, active (which definitely changes when you start dragging).
  - there is a way around it. the idea is to expose functions instead of values on the context value so it won't re-render all components that use it when something that is irrelevant to them changes.
  - a workaround for this issue could be creating a Draggable component that will receive the content (the actual component) as children. but then you cannot pass isDraggable and such to it
  - Or you can separate the draggable item into 2 components: DraggableItem and Item + memo the Item.

## collision

- [Add verticalSortableList collision detection strategy](https://github.com/clauderic/dnd-kit/pull/805)
  - We created a vertical list recently, with useSortable, and couldn't get the dragging / collision detection to work with our variable height items, without also using an overlay. The overlay was difficult to achieve for us, for reasons I won't go in to.
  - Anyway, we created a new collision detection strategy that allows it to work as you would expect, 

## done

- perf regression: all Sortables in 5.0 rerender constantly on even smallest mouse movement
  - https://github.com/clauderic/dnd-kit/issues/623
  - The same problem is happening to me, 'useSortable' is causing retenders due to 'useContext'. 
  - The easiest way to fix this is to use `useContextSelector` .

- [feature request: collision detection for sibling `useDraggable`](https://github.com/clauderic/dnd-kit/issues/810)
  - You can detect collisions between sibling draggables by also connecting them to useDroppable, similar to how the useSortable hook works

- [How to drag by copying?](https://github.com/clauderic/dnd-kit/issues/456)
  - when you drop that item you keep that same unique id and generate a new one for the sidebar to replace the item that was just moved from the sidebar to your other droppable region
  - [Consider adding Clone from List example](https://github.com/clauderic/dnd-kit/issues/45)
  - https://codesandbox.io/s/distracted-mendel-hibbgu

- [How do I implement multiple items drag in a container](https://github.com/clauderic/dnd-kit/issues/1048)
  - [Multiple draggable at the same time?](https://github.com/clauderic/dnd-kit/issues/644)
  - [Add multi-select story by clauderic](https://github.com/clauderic/dnd-kit/pull/588)
# codebase
- DragOverlay
  - 默认布局 `position:fixed`

- keyboard
  - The keyboard activator is the `onKeyDown` event handler. 
    - The Keyboard sensor is initialized if the `event.code` property matches one of the `start` keys passed to `keyboardCodes` option of the Keyboard sensor.
    - By default, the keys that activate the Keyboard sensor are `Space` and `Enter`.
# changelog

## [v6.0.0_202205](https://github.com/clauderic/dnd-kit/releases/tag/%40dnd-kit%2Fcore%406.0.0)

- Accessibility-related props have been regrouped under the `accessibility` prop of `<DndContext>`.
- The DOM nodes for the screen reader instructions and announcements are no longer portaled into the document.body element by default.
- The drop animation now ensures that the the draggable node that we are animating to is in the viewport before performing the drop animation and scrolls it into view if needed.

- @dnd-kit/sortable@7.0.0
  - The UniqueIdentifier type has been updated to now accept either string or number identifiers. 
    - As a result, the id property of useDraggable, useDroppable and useSortable and the items prop of `<SortableContext>` now all accept either string or number identifiers.
  - Better handling of overlapping droppable
  - Introducing the concept of activator node refs for useDraggable and useSortable. 
    - This allows @dnd-kit to handle common use-cases such as restoring focus on the activator node after dragging via the keyboard or only allowing the activator node to instantiate the keyboard sensor.
  - Focus management is now automatically handled by @dnd-kit.
# examples
- https://github.com/shaddix/dnd-kit-sortable-tree
  - https://shaddix.github.io/dnd-kit-sortable-tree/
  - a Tree component extracted from dnd-kit examples and abstracted a bit. 
- https://github.com/yaju19/dnd-kit-tree
  - https://dnd-kit-tree.vercel.app/
  - 拖拽父级菜单时，会连带子菜单，类似官方示例
- https://github.com/TNick/dnd-kit-tree-example
  - This repository contains several examples derived from the examples in the dnd-kit source code.
  - This is just the original example with the plain HTML elements replaced by MUI components.

- https://github.com/yangfei4913438/react-window-table
  - 基于react-window和dnd-kit编写的一个超灵活的表格。
  - 支持折叠部分行、虚拟滚动、拖拽行、数据filter/sort
  - 基于 FixedSizeList
- https://github.com/yangfei4913438/react-demos
  - 基于 react-window 库编写的一个超灵活的表格。使用了 dnd-kit 来实现列的顺序拖拽调换，列的宽度拖拽调整。

- https://github.com/el-tumakov/react-virtual-gantt-repo
  - https://react-virtual-gantt.vercel.app/
  - Gantt chart component for React.
  - 依赖dnd-kit、tippyjs、react-window
  - 示例左边是任务列表，右边是日期安排

- https://github.com/Achaak/pikas-ui /MIT/ts
  - https://github.com/Achaak/pikas/tree/main/packages/ui/table
  - https://pikas-ui.vercel.app/components/table
  - Pikas-UI is a React UI library for building web applications with StitchesJS.
  - The library uses Stitches for styling and Radix for the accessibility.
  - table依赖dnd-kit、pikas-ui

- mantine-data-grid /117Star/MIT/202212/ts
  - https://github.com/Kuechlin/mantine-data-grid
  - https://kuechlin.github.io/mantine-data-grid/
  - 支持sort/filter/pagination，不支持group
  - 提供了一个类似storybook的属性开关工具，方便尝试示例各种交互
  - 依赖mantine、dayjs、transtack-virtual
  - Data Grid component with Mantine UI and react-table v8.
  - 样式非常友好

- undb /20Star/AGPLv3/202304/ts
  - https://github.com/undb-xyz/undb
  - https://www.undb.xyz/
  - https://docs.undb.xyz/
  - Private first, unified, self-hosted no code database.
  - 前端依赖 undb, dnd-kit、tanstack-table, react-redux, emotion, @loadable/component, jotai, react-hook-form, trpc
    - 前端正迁移到svelte
  - 后端依赖 nestjs、mikro-orm、trpc、undb

- react-tiny-virtual-list /MIT/1.8kStar/201910/ts
  - https://github.com/clauderic/react-tiny-virtual-list
  - https://clauderic.github.io/react-tiny-virtual-list/
  - A tiny but mighty 3kb list virtualization library, with zero dependencies
  - Supports variable heights/widths, sticky items, scrolling to index, and more
  - forks
    - https://github.com/matyas-igor/react-small-virtual-list

- https://github.com/RohanShrestha01/task-planner /ts
  - https://tasksplanner.vercel.app/
  - 看板和日历切换

- https://github.com/somidad/antd-table-dnd-sortable
  - [Drag sorting Ant Design Table with dnd kit](https://jeon.engineer/2021/07/16/drag-sorting-ant-design-table-with-dnd-kit/)

- https://github.com/wuifdesign/antd-react-extensions
  - https://wuifdesign.github.io/antd-react-extensions/
  - Extentions for Ant Design React

- https://github.com/jado66/reactive-site-creator /js
  - https://jado66.github.io/reactive-site-creator-live/
  - A website creator for React.
  - 依赖dnd-kit、react-quill、react-reveal、bootstrap5

- https://github.com/devsayog/ui-dashboard
  - https://ui-dahboard.vercel.app/
  - Dashboard build with NextJs with kanban and calendar apps.
  - 依赖dnd-kit、headlessui、zustand、chartjs
  - https://github.com/devsayog/kanban-board /react-dnd
  - https://github.com/devsayog/MovieFLix
- https://github.com/devsayog/nextjs-ecommerce
  - https://fashion-lac.vercel.app/
  - Nextjs ecommerce is fullstack ecommerce web app with admin panel.

- https://github.com/learnsomesome/drag-drop
  - https://learnsomesome.github.io/drag-drop/
  - A drag and drop demo by dnd-kit
  - 类似白板拖拽、显示网格

- https://github.com/huaiyukhaw/plain-notes-app
  - https://notes.huaiyukhaw.com/
  - Note taking application that saves data locally in the user’s browser LocalStorage for convenient access.

- https://github.com/Make-md/makemd
  - http://www.make.md/
  - Make.md gives makers the ultimate experience on Obsidian.

- https://github.com/StaticJsCMS/static-cms
  - https://www.staticcms.org/
  - A Git-based CMS for Static Site Generators

## kanban

- https://github.com/mehdi-zibout/kanban-t3
  - A kanban task management app, with drag and drop, multiple boards and subtasks
  - tRPC - Backend library

- https://github.com/rahulnpadalkar/react-dnd-kanban
  - [Build a Kanban board with dnd kit and React - LogRocket Blog](https://blog.logrocket.com/build-kanban-board-dnd-kit-react/)

- https://github.com/ZauJulio/AdaKanban
  - https://ada-kanban.vercel.app/
  - a Kanban board with DragandDrop, Chakra-ui and Next.js, making use of the API available by them in Nodejs.

- https://github.com/azadov-azamat/kanban-board-todo
  - https://kanban-board-todo-eight.vercel.app/
  - Kanban board, xalq-bank task

- https://github.com/LcsGomes94/react-kanban
  - https://react-kanban-mauve.vercel.app/
  - 不能拖拽列

- https://github.com/matews-sousa/trello-clone
  - A Trello Clone application called Thullo. Built with Next.js, Firebase, TailwindCSS and DnD Kit.

## builder

- https://github.com/mongodb-js/compass
  - The GUI for MongoDB.

- https://github.com/pdfme/pdfme
  - https://pdfme.com/
  - A TypeScript based PDF generator library, made with React.

- https://github.com/i-VRESSE/workflow-builder
  - https://wonderful-noether-53a9e8.netlify.app/
  - Graphical interface to build a workflow file
  - The builder allows you to create a complex TOML formatted config file based on a set of JSON schemas.

- https://github.com/fayez-nazzal/Astonish
  - The React library for creating presentations
  - Wrap your presentation with the Astonish component
  - Wrap each Slide with the Slide component

- https://github.com/hlerenow/chameleon
  - https://hlerenow.github.io/chameleon/documents/docs/tutorial/quickStart
  - https://hlerenow.github.io/chameleon/
  - Web visual programming engine. (lowcode)
  - A streamlined low-code engine, all modules support custom extensions, which can be used for web page generation and rendering.

- https://github.com/crossjs/cofe
  - No-Code System
  - 依赖chakra-ui.v1、recoil、nextjs、unist-builder(tree)

- https://github.com/sadanandpai/resume-builder
  - https://e-resume.vercel.app/builder
  - 整体页面不支持拖拽，右侧属性项目支持

- https://github.com/ljtechdotca/resume-builder
  - http://resume-builder-beta.vercel.app/

- https://github.com/zachhannum/calamus
  - React Electron App for Writing and Publishing Novels

## utils

- https://github.com/sindresorhus/array-move
  - Move an array item to a different position

- https://github.com/itsMapleLeaf/dnd-kit-masonry-demo
  - masonry

- https://github.com/rashagu/dnd-kit-vue
  - a Vue adaptation based on @dnd-kit

- https://github.com/kvandake/lexorank-ts
  - A reference implementation of a list ordering system like JIRA's Lexorank algorithm

- https://github.com/onmotion/react-tabtab-next
  - https://onmotion.github.io/react-tabtab-next/
  - A mobile support, draggable, editable and api based Tab for ReactJS

## more-repos

- https://github.com/wyhinton/react_konva-dnd_kit
  - https://codesandbox.io/s/react-konva-dnd-kit-e6rck
  - Example of using dnd-kit to drag an element out a react konva canvas
  - 依赖konva、react-konva

- https://github.com/ThaddeusJiang/react-sortable-list
  - Easy Drag & Drop sort items
# more
