---
title: toc-lib-editor-builder-window-manager
tags: [builder, layout, toc]
created: 2021-01-08T10:48:16.590Z
modified: 2021-01-08T11:48:16.590Z
---

# toc-lib-editor-builder-window-manager

# guide

- sidebar
  - 使用场景包括dashboard、doc、book、site...
  - 可以直接从使用场景的角度来分析解决方案
  - 侧边栏过于复杂时可以考虑用窗口来代替实现(侧边栏 vs 浮动面板)
  - 主流的库会碰到各种需求，可以在issues中搜索 two sidebar 查看讨论过的方案

- ref
  - 几乎所有的窗口布局组件的例子，整体最外层布局都是不能下滑滚动的，但窗口内部内容可以滚动
    - 比较适合做表格，做文档要考虑跳转到锚点
# panel-window-manager
- ref
  - 可拖动
  - 可缩放
  - 是否支持dock
  - 卡片是否可重叠或遮挡
  - 是否支持split view
  - [search: window manager](https://github.com/search?o=desc&p=1&q=window+manager+language%3Ajavascript+language%3Atypescript&s=updated&type=Repositories)

- react-grid-layout /16.9kStar/MIT/202202/js
  - https://github.com/react-grid-layout/react-grid-layout
  - https://strml.github.io/react-grid-layout/examples/0-showcase.html
  - A draggable and resizable grid layout with responsive breakpoints, for React.
  - 卡片能随意拖动和缩放
  - 静止状态时，卡片不可重叠遮挡
  - 🍴 forks
  - https://github.com/DEXAGA/react-grid-layout-hooks /202105/ts
    - Migration to Hooks
    - Migration to Typescript

- golden-layout /5.8kStar/MIT/202209/ts
  - https://github.com/golden-layout/golden-layout 
  - https://golden-layout.com/
  - A multi window layout manager for webapps
  - 主要用于传统分栏布局，窗口不可重叠遮挡
  - 适合实现类似vscode、notable这类编辑器或文件管理器

- rc-dock /411Star/Apache2/202212/ts+js
  - https://github.com/ticlo/rc-dock
  - https://ticlo.github.io/rc-dock/examples
  - Dock Layout for React Component
  - 卡片能随意拖动和缩放
  - 静止状态时，卡片能遮挡
  - 支持 Popup panel as new browser window

- https://github.com/jupyterlab/lumino /ts/PhosphorJS/jupyter
  - https://lumino.readthedocs.io/en/latest/examples.html
  - a set of JavaScript packages, written in TypeScript, that provide a rich toolkit of widgets, layouts, events, and data structures. 
  - 提供了3个经典示例: accordion、data-grid with merged-cell、dock-panel
  - These enable developers to construct extensible high-performance desktop-like web applications, such as JupyterLab. 
  - Lumino was formerly known as PhosphorJS.
  - https://github.com/jupyterlab/lumino/tree/main/packages/datagrid
    - 表格自研

- https://github.com/node-projects/dock-spawn-ts
  - https://node-projects.github.io/dock-spawn-ts/
  - a Typescript Docking Framework to create a Visual Studio like IDE in HTML
  - a Typescript fork of Dock Spawn, a Docking Framework for HTML.
  - 提供了ide的示例，复刻visual studio
  - 支持多实例

- https://github.com/caplin/FlexLayout  /ts
  - https://rawgit.com/caplin/FlexLayout/demos/demos/v0.7/demo/index.html
  - A multi-tab layout manager
  - 功能非常丰富，提供了类似vscode的左右侧边栏tabs，主内容区tabs，底部tabs
  - 样式陈旧

- https://github.com/hlhielkema/elara 
  - https://hlhielkema.github.io/elara/
  - /5Star/MIT/202009/js/NoDeps
  - 卡片能随意拖动和缩放
  - 静止状态时，卡片能部分遮挡；样式非常友好，demo设计很棒
  - 注意，例子都很好看，但都没有显示竖直滚动条
  - split平铺窗口后，无法拖拽改变两边大小，不能下滑查看更多窗口
  - Elara enables creating a Windows/MacOS like window manager experience inside a web browser. 
  - No third-party libraries or frameworks are needed to use Elara.

- https://github.com/mathuo/dockview
  - https://dockview.dev/#live-demo
  - A zero dependency layout manager built for React

- https://github.com/aeagle/react-spaces
  - https://allaneagle.com/projects/react-spaces
  - An easy to understand and nestable layout system, React Spaces allow you to divide a page or container into anchored, scrollable and resizable spaces enabling you to build desktop type user interfaces in the browser.
- https://github.com/rlamana/Ventus
  - /300Star/MIT/201812/js/只依赖lodash
  - http://www.rlamana.com/ventus/code/examples/simple/
  - http://www.rlamana.com/ventus/code/examples/desktop/
  - 卡片能随意拖动和缩放，经典例子expose可以一次预览所有窗口
  - 静止状态时，卡片能部分遮挡
  - A window manager written in Javascript, HTML5 and CSS3.
- https://github.com/davidfig/window-manager
  - https://davidfig.github.io/window-manager/
  - /32Star/MIT/202007/Ventus
  - 明显感觉比Ventus更卡顿
  - A javascript-only Window Manager
  - I used Ventus to build internal tools and editors, but I wanted a more configurable solution with a better event model that didn't rely on CSS.
- https://github.com/nextapps-de/winbox
  - https://nextapps-de.github.io/winbox/
  - /3.7kStar/Apache2/202105/js
  - 功能简单，但文档示例丰富
  - outstanding performance, no dependencies, fully customizable
- https://github.com/Knossys/Proscenium 
  - /1Star/202011
  - A web based window manager and user interface toolkit for cloud based applications
- https://github.com/cezarykluczynski/simone
  - http://cezarykluczynski.github.io/simone/demos/functional/basic.html
  - /27Star/MIT/201810/js
  - 缩放窗口时有动画渐变，明显地给人流畅感
  - 样式非常传统陈旧
  - It's built on top of the jQuery and jQuery UI.
  - window manager consisting of two widgets: taskbar and window, providing a desktop-like experience
- https://github.com/UbiCastTeam/overlay-display-manager
  - JS overlay window manager to display iframes, images and html content.
  - /3Star/202101
- https://github.com/ColinEspinas/wwm
  - customizable windows manager for the web
  - /2Star/202101
- https://github.com/acdra1n/wm.js
  - window manager for the web.
  - /2Star/LGPLv3/202101

- https://github.com/projectstorm/react-workspaces
  - http://projectstorm.cloud/react-workspaces/
  - /90Star/202006/ts
  - 基于dom实现
  - 可以显示侧边小窗
  - 不能拖拽改变panel大小
  - help you build super-modern desktop-grade applications that have window management similar to Adobe/Jetbrains and Netbeans
  - https://github.com/projectstorm/react-canvas
    - 基于canvas实现
    - A pluggable layout and graphics system aimed at powering desktop publishing as well as storm-react-diagrams
- https://github.com/nomcopter/react-mosaic 
  - https://nomcopter.github.io/react-mosaic/
  - /2.6kStar/Apache2/202005/ts
  - A React tiling window 
  - 可以拖拽改变panel大小，支持自动平铺
- https://github.com/arqex/react-tiles /46Star/201804
  - https://react-tiles.firebaseapp.com/
  - a window manager component to display more than one app route at the same time dividing your browser in tiles.
- https://github.com/masesk/webapp-interface-manager
  - https://masesk.github.io/webapp-interface-manager/
  - /1Star/NALic/202004/js
  - 依赖react-bootstrap
  - React application to mange and display multiple web pages and/or React components in their own window on a single browser tab
- https://github.com/stayradiated/reactwm /33Star/201409
  - http://stayradiated.github.io/reactwm/
  - A minimal window manager built using React.
- https://github.com/zzarcon/react-cristal /26Star/201902/ts
  - https://zzarcon.github.io/react-cristal/
  - window manager for React. Convert any component into a window
- https://github.com/BradDunagan/react-paneless /5Star/201909
  - A minimal window manager that may be included in your ReactJS app.
- https://github.com/openopus/ng-pane-manager2
  - Angular version of the AngularJS version of the web window management system.

- https://github.com/idealjs/layout-manager
  - Building Multi-Window Application's Frameworkless Library

- https://github.com/davidjbradshaw/iframe-resizer
  - This library enables the automatic resizing of the height and width of both same and cross domain iFrames to fit their contained content. 

- https://github.com/tamkeen-tms/electron-window-manager
  - A NodeJs module for Electron (Atom Shell, previously) that will help you create, control, manage and connect your application windows very easily.
  - Most of the applications created using Electron are one-window applications
  - if you are to build a multi-window Electron application, then you may want to have a look at this package module.
# dockable(sidebars)
- https://github.com/ColorlibHQ/AdminLTE
  - https://adminlte.io/
  - https://adminlte.io/themes/v3/
  - 左侧是可折叠到只显示图标的sidebar，右侧是可勾选配置项的浮动sidebar
  - Free admin dashboard template based on Bootstrap 4

- https://github.com/balloob/react-sidebar
  - http://balloob.github.io/react-sidebar/example/
  - a sidebar component for React.
  - Dock the sidebar next to the content
  - Sidebar and content passed in as PORCs (Plain Old React Components)
  - Only dependency is React
  - 侧边栏宽度会随着内容宽度变化
  - 不直接支持同时打开多个sidebar，但可创建多个实例
  - [Enable window scrolling in v3](https://github.com/balloob/react-sidebar/pull/161)
    - This PR fixes most of the scrolling issues. 
    - It basically enables using the body as the scroll container instead of using the content-div as the scrolling container. 
  - https://github.com/MilllerTime/react-sidebar
    - only support mobile
    - [Architecture Proposal: Avoid rendering all app content in a nested scrolling container](https://github.com/balloob/react-sidebar/issues/86)

- slideout /8kStar/MIT/201803/js/NoDeps
  - https://github.com/Mango/slideout
  - https://slideout.js.org/
  - 实现左右2个sidebar的缺点是不能同时显示，一次只能显示一个，并且最左边或最右边的内容会被遮挡
  - [Is it possible to have two slideout menus - one to the left and one to the right - at the same time?](https://github.com/Mango/slideout/issues/208)
    - yes
    - [Two Slideouts](https://codepen.io/pazguille/pen/GNEzZv)
  - [support 2 menu in page](https://github.com/Mango/slideout/issues/127)
    - [Slideout.js - Left & Right Menu](https://codepen.io/egmalt/pen/PGbWRq)

- https://github.com/Kamona-WD/starter-dashboard-layout
  - https://kamona-wd.github.io/starter-dashboard-layout/
  - tarter responsive dashboard layout built with tailwindcss & alpinejs
  - 左边侧边栏显示一级菜单，右边可显示浮动侧边面板
  - 样式超级友好
  - https://github.com/Kamona-WD/starter-dashboard-layout-vue/
- https://github.com/Kamona-WD/kwd-dashboard
  - https://kamona-wd.github.io/kwd-dashboard/
  - Fully responsive dashboard template built with tailwindcss & alpinejs
  - 只有左边有侧边栏，左右两边都有浮动面板

- https://github.com/goodoldneon/react-drag-and-dock
  - https://codepen.io/goodoldneon/pen/WPraLE
  - Create free-floating panels that "dock" into designated docks. 
  - Panel docking does not cause its children to remount.
  - When a Panel docked, the position of the Dock is determined using `Element.getBoundingClientRect()`. Then the Panel height, width, and position are changed. All positions are relative to `document.body`.
  - To the user, the Panel appears to be inside the Dock. In reality, the Panel is actually on top of the Dock.

- more-dock
  - 操作的ui不一定是panel，可能是toolbar、floating-action-button
  - https://github.com/onitecsoft/smarti.dock.js
    - JQuery floating dock panel. Native configuration, custom layout and css style
# split-panels
- react-resizable-panels /452Star/MIT/202212/ts
  - https://github.com/bvaughn/react-resizable-panels
  - https://react-resizable-panels.vercel.app/
  - React components for resizable panel groups/layouts.
  - panel 不重叠，不可悬浮

- https://github.com/nathancahill/split /js/NoDeps
  - https://split.js.org/
  - Unopinionated utilities for resizeable split views
  - No overhead or attached window event listeners, uses pure CSS for resizing.
  - Split.js - The original library, maintained since 2014, works with float and flex layouts
  - Split Grid - Successor to Split.js, for grid layouts. 基于display-grid实现

- https://github.com/devbookhq/splitter /ts
  - a React component that allows you to split views into resizable panels. Similar to vscode
  - inspired by Split.js and written as 100% functional component
  - All size calculation is done through CSS using `calc` with minimal JS

- https://github.com/johnwalley/allotment /ts
  - https://allotment-storybook.netlify.app/
  - React component for resizable split views
  - 提供了复刻vscode界面的示例
  - Like VS Code's split view implementation? You're in luck! This component is derived from the same codebase.

- https://github.com/b-zurg/react-collapse-pane /ts
  - https://storybook-collapse-pane.netlify.app/
  - The splittable, draggable, collapsible panel layout library
  - 依赖mui

- https://github.com/xcfox/react-tile-pane /ts
  - https://xcfox.github.io/react-tile-pane/demo/
  - A React tiling pane manager
  - use @use-gesture/react, react-use-measure as peerDependencies

- https://github.com/bokuweb/react-sortable-pane /ts
  - http://bokuweb.github.io/react-sortable-pane
  - Sortable and resizable pane component for react.
  - 支持uncontrolled和controlled

- https://github.com/tomkp/react-split-pane /3kStar/MIT/201911/js/inactive
  - https://tomkp.github.io/react-split-pane
  - Split-Pane component, can be nested or split vertically or horizontally!
# resize-grid-layout
- muuri /10.6kStar/MIT/202107/js/inactive
  - https://github.com/haltu/muuri
  - https://muuri.dev/
  - a JavaScript layout engine that allows you to build all kinds of layouts 
  - and make them responsive, sortable, filterable, draggable and/or animated.
  - https://github.com/paol-imi/muuri-react
    - React implementation of the amazing Muuri layout engine.
    - All Muuri features are implemented in a React-friendly way, with custom components and hooks

- https://github.com/naver/egjs-grid /185Star/MIT/202209/ts
  - https://naver.github.io/egjs-grid/
  - A component that can arrange items according to the type of grids
- https://github.com/naver/egjs-infinitegrid /1.5kStar/MIT/202211/ts
  - https://naver.github.io/egjs-infinitegrid/storybook
  - https://naver.github.io/egjs-infinitegrid/
  - A module used to arrange card elements including content infinitely on a grid layout.
  - 支持4种，masonry、justified、frame、packing
  - 不支持拖拽

- https://github.com/RyoSogawa/react-resizable-layout /202210/ts
  - https://ryosogawa.github.io/react-resizable-layout/
  - accessible headless React component and hook for drag-and-drop resizable layouts.
# examples
- https://github.com/EikosPartners/windowmanagerjs /20Star/201802
  - https://github.com/aesalazar/windowmanagerjsdemo
  - A framework to manage multiple dockable HTML windows.
  - Runtimes supported: modern browsers, electron, openfin
- https://github.com/soupy-developer/auroraOS
  - A window manager/desktop environment in your browser.

- https://github.com/i3/i3
  - i3 is a tiling window manager for X11.
  - 基于c, perl
- https://github.com/material-shell/material-shell
  - A modern desktop interface for Linux extending GNOME Shell.
- https://github.com/aliyun/oss-browser
  - 提供类似windows资源管理器功能, Windows 7 above, Linux and Mac.
- https://github.com/nashaofu/dingtalk
  - 钉钉桌面版，基于electron和钉钉网页版开发，支持Windows、Linux和macOS

- https://github.com/MichalBures/electron-simple-window-manager
  - Easily manage (open, hide, move, ...) your Electron windows.
# more
- https://github.com/krishpranav/js-os
  - js-os is an open-source web desktop platform with a window manager, application APIs, GUI toolkit, filesystem abstractions and much more.

- https://github.com/alexkuz/react-dock
  - http://alexkuz.github.io/react-dock/demo/
  - Resizable dockable react component

- https://github.com/antimatter15/breadloaf
  - draggable, dockable, notebook-style layout engine for React
