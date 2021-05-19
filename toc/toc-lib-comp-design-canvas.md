---
title: toc-lib-comp-design-canvas
tags: [canvas, components, design-system, lib, toc]
created: '2021-05-19T13:53:40.087Z'
modified: '2021-05-19T13:54:12.338Z'
---

# toc-lib-comp-design-canvas

# canvas-based-components

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

- revas /80Star/MIT/202102/ts
  - https://github.com/pinqy520/revas
  - https://pinqy520.github.io/demo/revas-pwa/
  - 交互操作只支持触摸touch，不支持鼠标click；样式非常友好
  - 依赖自研的开源布局工具yoga-layout-wasm
  - Use React and CSS to build UI interfaces on canvas

- https://github.com/SensormaticFirmware/FlexCanvasJS
  - RIA Web Application Framework for HTML5 Canvas inspired by Adobe Flex/Flash.
  - Style-able, skin-able, customize-able Javascript UI component set, from shapes to color pickers to data grids. 
  - Relative and dynamic layouts, automatic redraw regions, composite effects, and much more.
  - Great for everything 2D, complex web forms to games.

- https://github.com/ericdrowell/concrete
  - Html5 Canvas framework that enables hit detection, layering, multi-buffering for lightning fast performance, pixel ratio support, and download support
  - As the creator of KineticJS, author of HTML5 Canvas Cookbook, I've identified a handful of features that just about every HTML5 Canvas project needs. 

# more-canvas-ui

- https://github.com/andrepxx/pure-knob
  - Canvas-based JavaScript UI element implementing touch, keyboard, mouse and scroll wheel support.
