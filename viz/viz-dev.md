---
title: viz-dev
tags: [intro, viz]
created: 2020-08-03T09:11:08.024Z
modified: 2021-01-01T20:21:10.887Z
---

# viz-dev

# guide
- 可视化输出报告时，技术上更依赖图形编辑器

# svg

- 是一种使用XML描述2D图形的语言。
- SVG基于XML，这意味着SVG DOM中的每一个元素都是可用的。您可以为某个元素附加Javascript事件处理器。
- 在SVG中，每个被绘制的图形均被视为对象。如果SVG对象的属性发生变化，那么浏览器能够自动重现图形。

- 基于对象模型（SVG元素与HTML元素类似）
- 多个图形元素，是文档对象模型 (DOM) 的一部分
- 视觉呈现使用标记创建并通过CSS或通过脚本以编程方式修改
- 事件模型/用户交互基于对象，是在原语图形元素上的 – 线条、矩形、路径
- SVG 标记和对象模型直接支持可访问性

- svg特点
  - 不依赖分辨率
  - 支持事件处理器
  - 最适合带有大型渲染区域的应用程序（比如谷歌地图）
  - 复杂度高会减慢渲染速度（任何过度使用DOM的应用都不快）
  - 不适合游戏应用

- usecase
  - 交互式图表和图形
  - 用于查看和打印的高保真度文档
  - 静态图像

## pieces

- SVG结构更像是html的dom结构，它的每一块图形元素都是一个“dom”元素，每一个元素可以通过属性和样式去控制
  - 它比较有优势的地方是动画能力，一方面可以直接在dom上去表现动画，借助`<animate />`和<`transformAnimate />`这两个元素去实现，除此之外它仍然可以通过css3和javascript方式等去实现动画
  - 我认为，svg适合去做一些插入html中的有动画要求的展现，特别是富文本中去实现一些动画（可以不借助css3和js实现）; 
# canvas
- 通过Javascript来绘制2D图形。
- 是逐像素进行渲染的。
- 在canvas中，一旦图形被绘制完成，它就不会继续得到浏览器的关注，如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

- 基于像素（Canvas在本质上是一个具有绘图API的图像元素）
- 单个HTML元素，在行为上类似于 `<img>`
- 视觉呈现通过脚本以编程方式创建和修改
- 事件模型/用户交互是粗粒度的 – 仅在画布元素上，交互必须根据鼠标坐标手动编程
- API不支持可访问性，除了画布，还必须使用基于标记的技术

- canvas特点
  - 依赖分辨率
  - 不支持事件处理
  - 弱的文本渲染能力
  - 能够以.png和.jpg格式保存结果图像
  - 最终适合图像密集型的游戏，其中有许多对象会被频繁重绘
- canvas pros
  - 适合以图片的形式导出预览图、导出截图、导出图表，图片通用性强

- usecase
  - 实时高容量数据表示（大规模数据）
  - 高性能（滤镜、光线跟踪器）
  - 2D休闲游戏

- webgl
  - 基于Canvas的3D框架
  - 主要用来做 3D 展示、动画、游戏

## pieces

- canvas则是一个html的dom元素，通过js在获得canvas文本上下文之后，通过canvas提供的API去画元素，如圆（arc），矩形（strokeRect）等，
  - 绘制过程中的样式需要提前设置后再去执行绘画命令，相对于svg比较生硬一些
  - 其动画的实现上也只能通过js里的计时器，设置好绘制间隔去一遍遍重绘来达到动画的效果。
  - canvas适合去做一些复杂丰富的数据可视化展示的，如图表等，配合当前一些插件EchartJs等，能够快速实现很多复杂多样的数据展示。
# svg vs canvas
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

## for svg/html

- https://twitter.com/steveruizok/status/1572613782006018049
  - Placing native web content in a customer renderer (i.e. something built with HMTL Canvas) is virtually impossible. Figma has a great system for writing widgets in React, but those are rendering with its primitives rather than HTML/CSS—something closer to React Native.
# canvas vs webgl
- canvas(cpu) vs webgl(gpu)

- ## [What's better: Canvas vs. WebGL](https://hashnode.com/post/whats-better-canvas-vs-webgl-for-a-newbie-cje7kxq2n046tiqwu94uv44lu)
- Depends on you goal. 
- If you have low-level graphics programming in mind, with the eventual aim to develop a render engine, then, in my opinion, it is a lot easier to start out with the HTML5 Canvas API. 
  - It abstracts away a lot of low-level details you do not need in order to create visuals. 
  - Also, in the beginning, it is rather likely, that performance is not an issue. 
  - I believe that it is far more important to first study the concept of 2D programming and how to manage things, like assets, states, input handling, etc.
- If you feel comfy with those things, switching over to WebGL is pretty easy. Everything will stay nearly the same, but become a lot more complicated. 
  - That allows you to do things you were not able to, before, with a great deal of control, like 3D scenes with shaders and instancing, etc.
- However, if you do not want to learn the exact implementation stuff, but just have fun creating content, like a game, it is advisable, that you use an available engine. 
  - WebGL, just like OpenGL or Direct2D/3D, Vulkan and Metal, is a very sophisticated API, which takes a lot of time to learn. 
  - Even if you know it by heart take a lot of time to use and optimize.
  - WebGL is not always available, so fallbacks have to put in place. 
  - As such, it ususally makes more sense to use a library, which raises the abstraction level to something manageable, pre-optimized and purposed. 
  - In that case, you should not study the low-level stuff for too long, but get on reading the docs of your renderer or engine.

- If you want fast prototypes with less than 100 sprites, some basic shape primitives, filters with globalAlpha and sheer image/pixel manipulation, go for canvas.
- If you have a lot of sprites and many layers choose WebGl. WebGl will offer better performance. 2 key points where WebGl will beat any other approach: shaders + sprite count
- If you want a lot of easy to implement interactivity with less than ~30000 elements, you can also in principle venture into SVG. In principle you can also get very nice and interesting effects with combining SVGFilter, linearGradient and masks so you might want to give it a try.
# ref
- [SVG 与 HTML5的canvas各有什么优点，哪个更有前途？](https://www.zhihu.com/question/19690014/answers/updated)
- [三种绘图技术SVG、Canvas、WebGL 3D比较](https://zhuanlan.zhihu.com/p/81226852)
