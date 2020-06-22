---
tags: [charting]
title: note-viz-lib-svg-canvas
created: '2019-08-01T05:10:56.452Z'
modified: '2020-06-22T09:15:44.476Z'
---

# note-viz-lib-svg-canvas

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

## svg-grammar

- transform  
  - translate(x,y)  
  不提供y时，默认y为0  
- 坐标变换    
  - 在每个SVG元素对象上，都有一个getScreenCTM()的方法，它会返回一个SVGMatrix来表示元素的坐标系所做过的变换。  
  - 此外SVG还有一种SVGPoint类型，它有x和y两个属性可以表示任一一个点，同时它还有一个matrixTransform()方法可以将点跟某个SVGMatrix相乘得到相应矩阵变换后的点。  
  - 通过这些再加上一些线性代数的知识，就可以轻松的进行坐标系的变换了。  
  - 要注意的是SVGPoint只能通过svg元素对象的createSVGPoint()来创建，不能用new SVGPoint()这样的方式。

- viewBox 视图框  
  - `<svg width="500" height="200" viewBox="0 0 50 20" >`
  - 500x200像素视口的<svg>元素内部使用从0,0到50,20的坐标系。  
  - <svg>内的图形上的坐标系每一个单位对应于宽度上的500/50=10像素和高度上的200/20=10像素。

- preserveAspectRatio  
  - 属性采用由空格分割的两个值，告诉视图框如何在视口内对齐，这个值本身由两部分组成    
  - 第二个值（如果有的话）指示如何保留宽高比，可选值meet, slice, none  
