---
title: toc-lib-web-layer
tags: [layer, lib, toc, web]
created: 2021-01-17T06:17:44.570Z
modified: 2021-01-17T06:18:28.855Z
---

# toc-lib-web-layer
- ref
  - search: layer, stack, pop
  - layer管理时要考虑焦点管理 FocusTrap/Lock
  - 相关组件：modal、dialog、tooltip、dropdown、overlay、portal
  - 要参考成熟组件库的实现方案，如antd、mui
# popular
- popper.js/floating-ui /15.4kStar/MIT/202007
  - https://github.com/floating-ui/floating-ui
    - https://floating-ui.com/docs/motivation
    - Floating UI is the evolution of Popper v2, with a more modern API.
    - Cross-platform: React Native, Canvas, WebGL...
    - Inversion of control
      - Floating UI is just a function that returns some unrounded numbers for you, which you can use as you please.
    - Modular: everything is modular by default, and thus tree-shakeable. 
    - Improved extensibility
      - The order of the array is yours to control and configure. 
      - The new architecture also supports finer control over the middleware lifecycle.
    - Strongly typed by default
  - https://github.com/popperjs/popper-core
    - https://popper.js.org/
    - https://github.com/popperjs/react-popper
    - https://popper.js.org/react-popper/
    - It will position any UI element that "pops out" from the flow of your document and floats near a target element
  - https://github.com/atomiks/tippyjs
    - https://atomiks.github.io/tippyjs/v6/headless-tippy/
    - The complete tooltip, popover, dropdown, and menu solution for the web
    - 依赖 @popperjs/core.v2
    - [Stretching the popover to the full width and height of the screen](https://github.com/atomiks/tippyjs/issues/897)

- reactjs-popup /1.5kStar/MIT/202107/ts/NoDeps/inactive
  - https://github.com/yjose/reactjs-popup
  - https://react-popup.elazizi.com/
  - React Popup Component - Modals, Tooltips and Menus —  All in one
  - 👀️ Function as children pattern to take control over your popup anywhere in your code
  - 支持嵌套Popup
  - 示例和文档都很详细
  - [proposal: Render tooltip popup programmatically](https://github.com/yjose/reactjs-popup/issues/185)

- react-laag /824Star/MIT/202204/ts/NoDeps
  - https://github.com/everweij/react-laag
  - https://storybook.react-laag.com/?path=/docs/text-selection--page
  - Hooks to build things like tooltips, dropdown menu's and popovers in React
  - 提供了很多示例，包括tooltip、popover、context-menu、autocomplete

- https://github.com/daangn/stackflow
  - Mobile-first stack navigator framework with composable plugin system
  - Stackflow is a project that implements Stack Navigation UX, which is mainly used in mobile devices (iOS/Android, etc.) in a JavaScript environment
  - Since the core logic and integration layers are separated, it can be integrated with various front-end frameworks. (Now only supports React)

- react-element-popper /2Star/MIT/202109/js/NoDeps
  - https://github.com/shahabyazdi/react-element-popper
  - https://shahabyazdi.github.io/react-element-popper/
  - A small React component to create a variety of elements that require Popper, such as dropdowns, modals, multi selects, and more.
  - 提供了portal、tooltip、dropdown的示例，但示例很简单
  - 支持多层嵌套

- react-atmosphere /6Star/MIT/202104/ts/inactive
  - https://github.com/paulshen/react-atmosphere
  - https://react-atmosphere.netlify.com/
  - React building blocks for UI layers (tooltips, dialogs, etc).
  - 依赖popperjs/core.v2、react-focus-lock
  - 提供了无限嵌套layer的示例

 

- react-layer-stack /MIT/152Star/201903
  - https://github.com/chain-police/react-layer-stack
  - https://github.com/fckt/react-layer-stack
  - https://fckt.github.io/react-layer-stack/
  - Layering system for React. 
  - Useful for popover/modals/tooltip/dnd application

- react-layers-manager /MIT/107Star/201904 
  - https://github.com/giuseppeg/react-layers-manager
  - Manage layers and z-index in React applications using context and createProtal
  - render your layers as siblings of your application root
  - This way layers are guaranteed to always be on top of your application
- https://github.com/sdgluck/react-z-index
  - Manage zIndex values in one place
  - wrap Modal component with ZIndex component
- https://github.com/pieterv/react-layers
  - inspired by the work done on the react-bootstrap's [Overlay](https://react-bootstrap.github.io/components/overlays/)
  - Overlays rely on the third-party library Popper.js

- https://github.com/iamhosseindhv/notistack
  - https://notistack.com/
  - customizable notification snackbars (toasts) that can be stacked on top of each other
# examples-menu-toolbar
- toolbar/button-group
  - https://www.radix-ui.com/docs/primitives/components/toolbar
  - https://carbondesignsystem.com/patterns/text-toolbar-pattern/
  - https://github.com/carbon-design-system/carbon/tree/v10/packages/react/src/components/Toolbar
  - https://v7-react.carbondesignsystem.com/?path=/story/deprecated-toolbar--default
  - https://codepen.io/team/carbon/pens/public
  - v11已移除，v10可访问，效果偏向带filter的表格工具条
  - Deprecate Header, Shell, and Toolbar in favor of UNSTABLE__Shell
  - toolbar is a set of buttons and menus that allows users to edit text, search keywords, attach files, and embed links

- context-menu
  - https://react.carbondesignsystem.com/?path=/story/experimental-unstable-menu-contextmenu--context-menu

- https://github.com/szhsin/react-menu /js
  - https://szhsin.github.io/react-menu/
  - for building accessible menu, dropdown, submenu, context menu and more

- https://github.com/fkhadra/react-contexify /ts
  - https://fkhadra.github.io/react-contexify/
  - Add a context menu to your react app with ease

- https://github.com/pacocoursey/cmdk
  - https://cmdk.paco.me/
  - unstyled command menu React component.
  - 依赖 @radix-ui/react-dialog
# modal/portal
- https://github.com/wellyshen/react-cool-portal
  - hook for Portals, which renders modals, dropdowns, tooltips etc. to `<body>` or else.

- react-usePortal /826Star/MIT/202107/ts/inactive
  - https://github.com/alex-cory/react-useportal
  - provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component 
  - 源码单文件，功能和实现都过于简单，不支持控制顺序
# popover
- https://github.com/everweij/react-laag /NoDeps
  - Hooks to build things like tooltips, dropdown menu's and popovers in React

- https://github.com/alexkatz/react-tiny-popover
  - A lightweight, highly customizable, non-intrusive, and Typescript friendly popover react HOC
# focus-management
- https://github.com/greena13/react-hotkeys
  - Declarative hotkey and focus area management for React

- https://github.com/Palmaswell/focus-manager
  - a Keyboard and Focus manager context provider that allows you to implement keyboard navigation flows in React applications. 
  - It registers, tracks, and delegate events to DOM elements or React components.

- https://github.com/focus-trap/focus-trap
  - Trap focus within a DOM node.
  - to trap focus within a DOM node — so that when a user hits Tab or Shift+Tab or clicks around, she can't escape a certain cycle of focusable elements.

- https://github.com/andreasbm/focus-trap
  - A lightweight web component that traps focus within a DOM node

- https://github.com/theKashey/react-focus-lock
  - Modal dialogs. You can not leave it with "Tab", ie do a "tab-out".

- https://github.com/vovacodes/react-sunbeam
  - Spatial navigation and focus management system for React apps

- https://github.com/evanminto/react-use-focus-management
  - hook allowing for programmatic control over the currently focused element.
# repos-layer
- layerJS /MIT/1.8kStar/202010/js/inactive
  - https://github.com/layerJS/layerJS
  - https://layerjs.org/
  - https://github.com/layerJS/layerJS/wiki
  - Javascript UI composition framework
  - No dependencies.

- layer-for-layui /MIT/7.9kStar/201712/长时间停更+突然更新
  - https://github.com/sentsin/layer
  - https://layer.layui.com/
  - 丰富多样的Web弹出层组件
  - [layui](https://github.com/sentsin/layui)
# examples

# more
