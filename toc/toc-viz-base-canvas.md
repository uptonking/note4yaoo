---
title: toc-viz-base-canvas
tags: [canvas, toc, viz]
created: 2020-08-02T08:59:13.271Z
modified: 2020-10-05T06:17:42.467Z
---

# toc-viz-base-canvas

# guide

- 没必要执着于render agnostic
  - 具体场景需求不同，如ui组件、图表、动画
  - 跨平台的差异
  - react-canvas/webgl，在一定程度也是将vdom渲染到不同平台

- tips
  - 还可以复用主流业务组件的canvas渲染逻辑，如 echarts-zrender, Fabric, pixi, dropflow, LeaferJS
# popular
- canvas-engines-comparison
  - https://github.com/slaylines/canvas-engines-comparison
  - https://benchmarks.slaylines.io/
  - 渲染5000个矩形的性能：PixiJS > Two.js >> konva.js/fabric.js/paper.js
  - [Show HN: Canvas engines performance comparison – PixiJS, Two.js, and Paper.js](https://news.ycombinator.com/item?id=23083730)
    - The comparison was unfair it was only moving the positions of the rectangles each frame for paper.js, and two.js 
    - but for pixi.js it was redrawing them from scratch which means it had to retesselate everything every frame.

- konva /12.4kStar/MIT/202503/ts/NoDeps
  - https://github.com/konvajs/konva
  - http://konvajs.org/
  - JS framework that extends the 2d context by enabling canvas interactivity for desktop and mobile applications.
  - began as a fork of ericdrowell/KineticJS
  - In order to run konva in nodejs environment, you also need to install `canvas` package manually. Konva will use it for 2d canvas API.
  - https://github.com/ericdrowell/KineticJS
    - /MIT/3.9kStar/201404
  - https://github.com/konvajs/react-konva
    - provides declarative and reactive bindings to the Konva Framework.

- https://github.com/fabricjs/fabric.js /29.8kStar/MIT/202503/ts/NoDeps
  - http://fabricjs.com/
  - Javascript Canvas Library, SVG-to-Canvas (& canvas-to-SVG) Parser
  - Out of the box interactions such as scale, move, rotate, skew, group...
  - Built in shapes, controls, animations, image filters, gradients, patterns, brushes...
  - Typed and modular
  - See browser modules for using es6 imports in the browser or use a dedicated bundler.
  - Fabric.js depends on `node-canvas` for a canvas implementation (HTMLCanvasElement replacement) and jsdom for a window implementation on node. 
- https://github.com/nihaojob/vue-fabric-editor
  - 基于fabric.js和Vue的图片编辑器，可自定义字体、素材、设计模板。

- react-canvas /12.5kStar/BSD/201703/inactive
  - https://github.com/Flipboard/react-canvas
  - High performance canvas rendering for React components
  - https://github.com/Flipboard/react-canvas/issues/138
    - This is a Cairo graphics library with HTML5 Canvas and a react bindings. 
    - Its a pretty straight forward wrapper around Cairo.
    - Cairo has been wrapped many times by many different libraries, 
    - this one is just the same as all the others, except maybe that its used by Flipboard, but they don't say much about it other than their one Wiki article.

- https://github.com/GuptaSiddhant/recanvas
  - Build and render an image using canvas, yoga-layout and react in node environment.

- two.js /7.1kStar/MIT/202105/js
  - https://github.com/jonobr1/two.js
  - https://two.js.org/
  - A renderer agnostic two-dimensional drawing api for the web.
  - It is renderer agnostic enabling the same api to render in multiple contexts: webgl, canvas2d, and svg.
  - 依赖 Underscore.js(以前也依赖raf、@codemirror/next)
  - Focus on Vector Shapes: aims to make the creation and animation of flat shapes easier and more concise.
  - At its core two.js relies on a scenegraph.
    - This means that when you draw or create an object (a Two.Path or Two.Group), two actually stores and remembers that. 
  - Two.js has a built in animation loop. 
  - Two.js features a Scalable Vector Graphics Interpreter

- spritejs /4.5kStar/MIT/202105/js/inactive/周边项目都没有更新了
  - https://github.com/spritejs/spritejs
  - https://spritejs.org/#/zh-cn/index
  - 依赖 gl-matrix、sprite-animator
  - OffscreenCanvas and Web Worker.
  - Work with d3.
  - It is renderer agnostic enabling the same api to render in multiple contexts: webgl2, webgl, and canvas2d.
  - Manipulate the sprites in canvas as you do with the DOM elements.
  - https://github.com/qcharts/core
    - https://github.com/spritejs/q-charts
    - 基于 spritejs 封装的图表库

- paper.js /12.2kStar/MIT/202401/js
  - https://github.com/paperjs/paper.js
  - http://paperjs.org/
  - Scriptographer ported to JavaScript and the browser, using HTML5 Canvas.
  - paper-full.js – The full version for the browser, including PaperScript support and Acorn.js
  - paper-core.js – The core version for the browser, without PaperScript support nor Acorn.js. 
- react-ape /1.2kStar/MIT/202012/js
  - https://github.com/raphamorim/react-ape
  - https://raphamorim.io/react-ape/
  - a react renderer to build UI interfaces using canvas/WebGL. 
  - React Ape was built to be an optional React-TV renderer. 
  - It's mainly a renderer focused on creating things for TV, PS4, Nintendo Switch, PS Vita, PS3 and low memory devices.
  - https://github.com/raphamorim/react-tv
    - deprecated for react-ape

- https://github.com/leaferjs/leafer /MIT/202404/ts
  - https://www.leaferjs.com/
  - HTML5 Canvas 2D 图形渲染引擎，可结合 AI 绘图、生成界面。
  - Leafer 定义了图形渲染引擎的核心功能，可以瞬间创建 100 万个图形，与具体 UI、业务场景无关
  - 提供了性能优化和可扩展的空间，遵循 Leafer 接口之上开发的渲染器、布局器、UI 框架之间可以互通有无。
  - [leaferjs，全新的 Canvas 渲染引擎 - 掘金](https://juejin.cn/post/7256386855721074747)
    - 以前做过类似的大数据量下的canvas渲染，优化思路收益最大的也无非就是可视区渲染 + buff区缓存，移动画布动态渲染。
    - 基于这个逻辑来讲，性能比较都不成立，因为其他方案确实渲染了 100 万个节点，而你这个只渲染了可视区有限个，可能是百十来个。 这没有比较的意义。
  - https://github.com/leaferjs/in
    - 官方增强功能插件中心
  - https://github.com/leaferjs/ui
    - 提供了常用的 UI 绘图组件，和开箱即用的功能，方便与 Figma、Sketch 等产品进行数据交换，并为跨平台开发提供了统一、丰富的交互事件，如拖拽、旋转、缩放手势等。
    - 逐步稳定，正式版即将到来

- easy-canvas /106Star/MIT/202010/js/NoDeps
  - https://github.com/Gitjinfeiyang/easy-canvas
  - https://gitjinfeiyang.github.io/easy-canvas/example/ui.html
  - 支持文档流，参照 web，无需设置 x、y 以及宽高
  - 提供了一套比较完整的组件库
  - 使用render函数在canvas中创建文档流布局。Tag: 海报图、小程序朋友圈分享图。
  - [easyCanvas实现原理解析](https://juejin.im/post/6871124987550531592)
  - 之前做dom截图用过 html2canvas 发现太慢了，然后换成 dom-to-image 好很多。foreignObject 是真香啊
  - https://github.com/Gitjinfeiyang/vue-easy-canvas
    - 将 easy-canvas 封装成vue组件进行使用 注意：内部实现是将vue节点转换成目标节点，转换过程中会有性能损失，渲染与转换时间大概4:1

- https://github.com/karasjs/karas
  - A declarative JavaScript framework on Canvas/Svg/Webgl.
  - karas实现了一个微型浏览器引擎，同时扩充CSS/WAA在样式/动画上的标准，增强类似SVG的矢量标签描述语法，结合JSX/React的开发方式，形成一个对前端友好的RIA框架。

- https://github.com/pikasojs/pikaso /MIT/202402/ts
  - https://pikaso.app/
  - Fully-typed and Fully-tested HTML5 Canvas Library
  - Pikaso is built on top of `Konva` to provide a couple of advanced features that Konva doesn't support out of the box.
  - Pikaso comes with support for NodeJs out of the box
  - https://github.com/pikasojs/pikaso-react-hook

- https://github.com/cburgmer/rasterizeHTML.js /js
  - http://cburgmer.github.io/rasterizeHTML.js
  - Renders HTML into the browser's canvas
  - it is possible by embedding the HTML into an SVG image as a `<foreignObject>` and then drawing the resulting image via `ctx.drawImage()`.
  - SVG is not allowed to link to external resources and so rasterizeHTML.js will load external images, fonts and stylesheets and store them inline via data: URIs (or inline style elements respectively).

- https://github.com/samizdatco/skia-canvas
  - Skia Canvas is a browser-less implementation of the HTML Canvas drawing API for Node.js. 
  - While the primary goal of this project is to provide a reliable emulation of the standard canvas API
  - It is based on Google’s Skia graphics engine and, accordingly, produces very similar results to Chrome’s `<canvas>` element.

- https://github.com/eKoopmans/html2pdf.js
  - Client-side HTML-to-PDF rendering using pure JS.
  - html2pdf.js converts any webpage or element into a printable PDF entirely client-side using html2canvas and jsPDF.
# canvas-designer-builder
- react-design-editor /556Star/MIT/202009/inactive
  - https://github.com/salgum1114/react-design-editor
  - https://salgum1114.github.io/react-design-editor/
  - 画布区是canvas，其余地方是dom
  - developed direct manipulation of editable design tools like Powerpoint
  - We've developed it with reactjs, antd3, fabricjs4, echarts4
# canvas-extensions
- https://github.com/udevbe/react-canvaskit
  - Experiment in creating a custom react renderer using an offscreen webgl canvas on top of Skia CanvasKit
  - This implementation allows you to use all familiar React concepts like hooks and contexts, in conjunction with JSX elements that closely match the existing Skia CanvasKit API. 
  - Everything is drawn to a hardware accelerated WebGL canvas.
  - [CanvasKit](https://skia.org/docs/user/modules/canvaskit/) 
    - WebGL context encapsulated as an SkSurface, allowing for direct drawing to an HTML canvas

- https://github.com/wcandillon/canvaskit-lite
  - A polyfill of CanvasKit that uses browser APIs

- https://github.com/Automattic/node-canvas
  - a Cairo-backed Canvas implementation for Node.js.

- https://github.com/spritejs/sprite-flex-layout
  - 无依赖
  - a layout engine which implements flex, can use in canvas/node-canvas
- https://github.com/miguelpeixe/react-flexcanvas
  - Canvas grid system built with flexboxes for React
# canvas-animation
- https://github.com/jeremyckahn/rekapi
  - Rekapi is a keyframe animation library for JavaScript. 
  - It gives you an API for: Defining keyframe-based animations, and Controlling animation playback.
  - Rekapi is renderer-agnostic. 
  - At its core, Rekapi does not perform any rendering. 
  - However, it does expose an API for defining renderers, and comes bundled with renderers for the HTML DOM and HTML5 2D `<canvas>` .

- https://github.com/CreateJS/EaselJS
  - /7.7kStar/MIT/202010/js
  - a library for building high-performance interactive 2D content in HTML5
  - It provides a feature-rich display list to allow you to manipulate and animate graphics. 
  - It also provides a robust interactive model for mouse and touch interactions.
- https://github.com/CreateJS/EaselJSRenderers
  - Runtime pluggable renderers for EaselJS (Canvas 2D, WebGL, HTML DOM, SVG).
  - an experiment that aims to provide runtime pluggable renderers for a subset EaselJS content
# examples
- https://github.com/snelsi/smart-canvas
  - https://smart-canvas.vercel.app/
  - 依赖react-router, three, react-three/fiber, zustand, chakra-ui/react, emotion/react, framer-motion
  - 依赖很多，但示例效果较好，左侧菜单配置，右侧画布编辑
  - demo with a bunch of cool interactive stuff and smart, dynamic shell

- https://github.com/doodlewind/freecube
  - Freecube renders and animates Rubik's Cube with raw WebGL, plus a tiny rule-based solver showing how CFOP works.
  - 魔方打乱还原动画

- https://github.com/datavized/morph /201809
  - 5 steps to create generative art from tabular data (e.g. spreadsheets and comma-separated values).
# utils
- https://github.com/yinguangyao/canvas-flex /ts
  - Canvas 结合 Yoga 实现的一个 Flex 布局，支持部分 Flex 语法

- https://github.com/KaliedaRik/Scrawl-canvas /MIT/202410/js
  - https://scrawl-v8.rikweb.org.uk/
  - a Javascript library for working with the HTML5 `<canvas>` element
  - Includes an adaptable - yet easy to use - protocol for positioning, displaying and animating artefacts and effects across the canvas.
  - Adds functionality to make `<canvas>` elements responsive, adapting their size to their surrounding environment while remaining fully interactive.
  - Helps make canvas elements more accessible for both keyboard and AT users.
# more-repos
- https://github.com/c-zhuo/easycanvas /2019
  - 一个同时支持2D和3D渲染、轻量、高效、MVVM模式的渐进式canvas渲染库

- https://github.com/limboy/canvasdraw
  - `CanvasRenderingContext2D` is powerful on drawing, but it's API is not user friendly, especially if you want to draw a bunch of stuff. 
  - this library make it easier to draw.
  - 依赖node-canvas

- https://github.com/ahdinosaur/virtual-canvas
  - canvas element for virtual-dom

- https://github.com/jarenchow/janvas
  - 未开源源码，目前 janvas.min.js 仅使用 uglifyjs --compress 简单压缩无混淆
  - 基于 HTML5 Canvas 2d 绘图上下文的 JavaScript 绘图库，不仅便于 拓展，拥有极佳的 灵活度 和超越原生 canvas API 开发的 性能
# ref
- [Best low level canvas library for making interactive animations?](https://stackoverflow.com/questions/24468958/best-low-level-canvas-library-for-making-interactive-animations)
  - KineticJS, Greensock
