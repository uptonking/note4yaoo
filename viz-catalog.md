---
title: viz-catalog
tags: [intro, viz]
created: '2020-08-03T09:11:08.024Z'
modified: '2020-12-21T07:47:09.103Z'
---

# viz-catalog

## 三种绘图技术比较 SVG、Canvas、WebGL 

- [三种绘图技术SVG、Canvas、WebGL 3D比较](https://zhuanlan.zhihu.com/p/81226852)

- svg
  - 一种使用XML描述的2D图形的语言
  - SVG基于XML意味着，SVG DOM中的每个元素都是可用的，可以为某个元素附加Javascript事件处理器。
  - 在SVG中，每个被绘制的图形均被视为对象。如果SVG对象的属性发生变化，那么浏览器能够自动重现图形。

- canvas
  - 通过Javascript来绘制2D图形。
  - 是逐像素进行渲染的。
  - 其位置发生改变，会重新进行绘制。
  - 优点
    - 适合以图片的形式导出预览图、导出截图、导出图表，图片通用性强

- webgl
  - 基于Canvas的3D框架
  - 主要用来做 3D 展示、动画、游戏

## svg vs canvas

- overview
  - SVG is vector based and Canvas is a bitmap you draw on. Scaling with SVG is natural and with Canvas it requires a redraw.
  - SVG is built with elements, like DOM elements, and therefore you can draw a circle and attach mouse *events* to it very naturally with Javascript.  Canvas does not give you this ability natively, requiring much more work.
- visual-xp
  - with blinks, offset, ...
- interaction
- animation
  - When it comes to animation it is tempting to go along HTML5 canvas but if your need is complex animations or require more control and quality, SVG is the way to go.
- performance
- use case
  - analyze the size of dataset first
- misc
  - Canvas is suitable for graphic-intensive games while SVG is not suitable for gaming.
- ref
  - https://blogs.msdn.microsoft.com/ie/2011/04/22/thoughts-on-when-to-use-canvas-and-svg/
  - http://jack-kelly.com/html5_canvas_versus_svg_for_interactive_charts_and_graphical
