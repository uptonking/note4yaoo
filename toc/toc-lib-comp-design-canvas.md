---
title: toc-lib-comp-design-canvas
tags: [canvas, components, design-system, lib, toc]
created: 2021-05-19T13:53:40.087Z
modified: 2021-05-19T13:54:12.338Z
---

# toc-lib-comp-design-canvas

# guide

- tips
  - 还可以复用主流业务组件的canvas渲染逻辑，如 echarts-zrender, Fabric, pixi, dropflow, LeaferJS
# canvas-based-components
- easy-canvas /544Star/MIT/202208/js/NoDeps
  - https://github.com/Gitjinfeiyang/easy-canvas
  - https://gitjinfeiyang.github.io/easy-canvas/example/ui.html
  - easy-canvas is a powerful tool helps us easy to layout with canvas.
  - 使用 render 函数，在 canvas 中创建文档流，快速实现布局.
  - 支持文档流，参照web，无需设置 x、y 以及宽高
  - 提供了一套比较完整的组件库
  - [easyCanvas实现原理解析](https://juejin.im/post/6871124987550531592)
  - 之前做dom截图用过 html2canvas 发现太慢了，然后换成 dom-to-image 好很多。foreignObject 是真香啊
  - https://github.com/Gitjinfeiyang/vue-easy-canvas
    - 将 easy-canvas 封装成vue组件进行使用
    - 注意：内部实现是将vue节点转换成目标节点，转换过程中会有性能损失，渲染与转换时间大概4:1
    - 兼容小程序以及 web，无第三方依赖

- revas /80Star/MIT/202102/ts
  - https://github.com/pinqy520/revas
  - https://pinqy520.github.io/demo/revas-pwa/
  - Use React and CSS to build UI interfaces on canvas
  - 交互操作只支持触摸touch，不支持鼠标click；样式非常友好
  - 依赖开源布局工具yoga-layout-wasm

- FlexCanvasJS /MIT/201909/inactive
  - https://github.com/SensormaticFirmware/FlexCanvasJS
  - RIA Web Application Framework for HTML5 Canvas inspired by Adobe Flex/Flash.
  - Style-able, skin-able, customize-able Javascript UI component set, from shapes to color pickers to data grids. 
  - Relative and dynamic layouts, automatic redraw regions, composite effects, and much more.
  - Great for everything 2D, complex web forms to games.

- concrete /232Star/MIT | GPLv2/202006/js
  - https://github.com/ericdrowell/concrete
  - Html5 Canvas framework that enables hit detection, layering, multi-buffering for lightning fast performance, pixel ratio support, and download support
  - As the creator of KineticJS, author of HTML5 Canvas Cookbook, I've identified a handful of features that just about every HTML5 Canvas project needs. 

- https://github.com/c7js/c7
  - C7 is a canvas-based UI toolkit.
  - C7 re-implements the key technology of modern front-end development based on HTML `<canvas>` (without any third-party libraries)10 commonly used components described in XML (e.g. `<button>, <image>, <input>`)
  - Flex layout and commonly used CSS
  - MVVM
  - Scaffolding and development server out of the box (supports hot reload)

- https://github.com/pikasojs/pikaso /MIT/202402/ts
  - https://pikaso.app/
  - Fully-typed and Fully-tested HTML5 Canvas Library
  - Pikaso is built on top of `Konva` to provide a couple of advanced features that Konva doesn't support out of the box.
  - Pikaso comes with support for NodeJs out of the box
  - https://github.com/pikasojs/pikaso-react-hook
# render-to-canvas
- Crosskit /3Star/MIT/202004/js/archived
  - https://github.com/steria773-archive/Crosskit
  - 4 Renderers: CANVAS, WEBGL, SVG, DOM
  - Rendering engine that can renders graphics in CanvasRenderingContext2D, WebGLRenderingContext, SVG, DOM
  - Lightweight and simple with size of 75kb (Smaller than Two.js and Hilo)

- https://github.com/plantain-00/composable-editor-canvas
  - https://plantain-00.github.io/composable-editor-canvas/
  - A composable editor canvas library.
  - 基于svg实现的图形编辑器
  - 提供了多种编辑场景示例
  - 实现了多种react-render-target: canvas, svg, webgl

- https://github.com/LibertyGlobal/ReactLiberty /201705/archived
  - choose between WebGL/Canvas/DOM/Native or any other UI renderer
  - a React library designed to abstract renderer by presenting three kinds of entities. 
  - They are Image, Text and Container.
  - React Liberty uses Yoga CSS Layout for laying components out, ReactMotion for declarative animations and Sunbeam for focus management.

- https://github.com/benboba/canvas-render
  - 使用HTML5 Canvas模拟DOM，解析CSS并在Canvas中渲染。

- https://github.com/ksandin/react-surface
  - A custom react renderer utilizing yoga-layout targeting pixi.js.
# more-canvas-ui
- https://github.com/andrepxx/pure-knob
  - Canvas-based JavaScript UI element implementing touch, keyboard, mouse and scroll wheel support.
