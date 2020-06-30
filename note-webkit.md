---
tags: [web, webkit, webview]
title: note-webkit
created: '2019-10-17T09:05:43.329Z'
modified: '2020-06-28T17:29:32.465Z'
---

# note-webkit

## 浏览器的渲染过程

- 浏览器将HTML，CSS，JavaScript代码转换成屏幕上所能呈现的实际像素，这期间所经历的一系列步骤，叫做关键渲染路径（Critical Rendering Path）
1. DOM Tree的构建
  - 从网络或者磁盘下读取的HTML原始字节码，通过设置的charset编码，转换成相字符
  - 通过词法分析器，将字符串解析成Token，Token中会标注出当前的Token是开始标签，还是结束标签，或者文本标签等。
  - 浏览器会根据Tokens里记录的开始标签，结束标签，将Tokens之间相互串联起来（带有结束标签的Token不会生成Node）
  - Node包含了这个节点的所有属性
  - 事实上，在构建DOM树时，不是要等所有的Tokens都转换成Nodes后才开始，而是一边生成Token一边采取深度遍历算法消耗Token来生成Node
  - 从bytes到Tokens的这个过程，浏览器都可以交给其他单独的线程去处理，不会堵塞浏览器的渲染线程。但是后面的部分就都在渲染线程下进行了，也就是我们常说的js单线程环境
2. CSSOM Tree的构建
  - CSSOM的生成过程和DOM十分相似，也是：1. 解析，2. Token化，3. 生成Nodes并构建Tree
3. Render Tree的构建
  - Render Tree上的每一个节点被称为：RenderObject。
  - RenderObject跟DOM节点几乎是一一对应的，当一个可见的DOM节点被添加到DOM树上时，内核就会为它生成对应的RenderOject添加到Render Tree上。
  - 其中，可见的DOM节点不包括：
    - 一些不会体现在渲染输出中的节点（如 `<html><script><link>…` ），会直接被忽略掉。
    - 通过CSS隐藏的节点。例如上图中的span节点，因为有一个CSS显式规则在该节点上设置了 `display:none` 属性，那么它在生成RenderObject时会被直接忽略掉。
  - Render Tree是衔接浏览器排版引擎和渲染引擎之间的桥梁，它是排版引擎的输出，渲染引擎的输入
  - 浏览器渲染引擎并不是直接使用Render树进行绘制，为了方便处理Positioning, Clipping, Overflow-scroll, CSS Transfrom/Opacrity/Animation/Filter, Mask or Reflection, Z-indexing等属性，浏览器需要生成另外一棵树：RenderLayer
  - 浏览器会为一些特定的RenderObject生成对应的RenderLayer，其中的规则是：
    - 是否是页面的根节点 It’s the root object for the page
    - 是否有css的一些布局属性（relative absolute or a transform) It has explicit CSS position properties (relative, absolute or a transform)
    - 是否透明 It is transparent
    - 是否有溢出 Has overflow, an alpha mask or reflection
    - 是否有css滤镜 Has a CSS filter
    - 是否包含一个canvas元素使得节点拥有视图上下文 Corresponds to canvas element that has a 3D (WebGL) context or an accelerated 2D context
    - 是否包含一个video元素 Corresponds to a video element
  - 当满足上面其中一个条件时，这个RrenderObject就会被浏览器选中生成对应的RenderLayer。
  - 至于那些没有被命运选中的RrenderObject，会从属与父节点的RenderLayer。
  - 最终，每个RrenderObject都会直接或者间接的属于一个RenderLayer。
  - 浏览器渲染引擎在布局和渲染时会遍历整个Layer树，访问每一个RenderLayer，再遍历从属于这个RenderLayer的 RrenderObject，将每一个RenderObject绘制出来。
  - 可以理解为：RenderLayer树决定了网页绘制的层次顺序，而从属于RenderLayer的 RrenderObject决定了这个Layer的内容，所有的RenderLayer和RrenderObject一起就决定了网页在屏幕上最终呈现出来的内容。
4. Layout
  - 布局最后的输出是一个“盒模型”：将所有相对测量值都转换成屏幕上的绝对像素
5. Paint
  - 将渲染树中的每个节点转换成屏幕上的实际像素
  - 浏览器通过发出“Paint Setup”和“Paint”事件，将渲染树转换成屏幕上的像素
- 浏览器内部实现了Render Object
  - 每个Render Object和DOM节点一一对应。
  - Render Object上实现了将其对应的DOM节点绘制进位图的方法，负责绘制这个DOM节点的可见内容如背景、边框、文字内容等等。
  - 同时Render Object也是存放在一个树形结构中的。
- 如果有层叠、半透明等等情况的元素（具体哪些情况请参考无线性能优化：Composite）就会从Render Object提升为Render Layer
  - 不提升为Render Layer的Render Object从属于其父级元素中最近的那个Render Layer
  - 根元素HTML自己要提升为Render Layer
- 浏览器渲染引擎遍历Layer树，访问每一个RenderLayer，然后递归遍历negZOrderList里的layer、自己的RenderObject、再递归遍历posZOrderList里的layer。就可以将一颗 Layer树绘制出来。
- Layer树决定了网页绘制的层次顺序，而从属于 RenderLayer 的 RenderObject 决定了这个 Layer 的内容，所有的 RenderLayer 和 RenderObject 一起就决定了网页在屏幕上最终呈现出来的内容。
- 上面的过程可以搞定绘制过程。但是浏览器里面经常有动画、video、canvas、3d的css等东西。这意味着页面在有这些元素时，页面显示会经常变动，也就意味着位图会经常变动。
- 每秒60帧的动效里，每次变动都重绘整个位图是很恐怖的性能开销。
- 因此浏览器为了优化这一过程，引出了Graphics Layers和Graphics Context，前者就是我们常说的合成层(Compositing Layer)
- 每个合成层Graphics Layer 都拥有一个 Graphics Context，Graphics Context会为该Layer开辟一段位图，也就意味着每个Graphics Layer都拥有一个位图。
- Graphics Layer负责将自己的Render Layer及其子代所包含的Render Object绘制到位图里。然后将位图作为纹理交给GPU。所以现在GPU收到了HTML元素的Graphics Layer的纹理，也可能还收到某些因为有3d transform之类属性而提升为Graphics Layer的元素的纹理。
- 现在GPU需要对多层纹理进行合成(composite)，同时GPU在纹理合成时对于每一层纹理都可以指定不同的合成参数，从而实现对纹理进行transform、mask、opacity等等操作之后再合成，而且GPU对于这个过程是底层硬件加速的，性能很好。最终，纹理合成为一幅内容最终draw到屏幕上。
- 所以在元素存在transform、opacity等属性的css animation或者css transition时，动画处理会很高效，这些属性在动画中不需要重绘，只需要重新合成即可。

## 浏览器的渲染过程 - Composite

- DOM Tree：浏览器将HTML解析成树形的数据结构。
- Style Rules：浏览器将CSS解析成树形的数据结构，对应我们的CSSOM。
- Render Tree：DOM和CSSOM合并后生成Render Tree。
- Layout： 布局。有了Render Tree，浏览器已经能知道网页中有哪些节点、各个节点的CSS定义以及他们的从属关系，从而去计算出每个节点在屏幕中的位置。
- Paint： 渲染。按照算出来的规则，通过显卡，把内容画到屏幕上。
- Reflow（回流/重排）：当浏览器发现某个部分发生了点变化影响了布局，需要倒回去重新渲染，这个回退的过程叫reflow。
- Dirty位系统
  - 为了避免所有细小的更改都要从根节点进行整体布局，浏览器采用了一种“dirty 位”系统。
  - 如果某个RenderTree上的Node发生了更改，便将自身标注为“dirty”，表示需要进行布局
  - 有两种标记：“dirty”和“children are dirty”。“children are dirty”表示尽管呈现器自身没有变化，但它至少有一个子代需要布局reflow时，浏览器会对Render Tree进行遍历，而仅仅只对标注了“dirty “的Node进行布局。
- repaint（重绘）：改变某个元素的背景色、文字颜色、边框颜色等等不影响它周围或内部布局的属性时，屏幕的一部分要重画，但是元素的几何尺寸没有变
- Chrome拥有两套不同的渲染路径：硬件加速路径和旧软件路径。
- 硬件加速路径会将一些图层的合成交给GPU处理，比CPU处理更快，而我们的RenderLayer（有些地方又称作PaintLayers）并不能作为GPU的输入，这里会将RenderLayer转换成GraphicsLayers
- 与RenderObject转换成RenderLayer一样，浏览器也是根据“某些规则”，选中一些特殊的RenderLayout节点（天选之子），这些节点将被称为Compositing Layers，Compositing Layers与其他的普通节点不一样的是他们拥有自己的GraphicsLayer，而那些没有被选中的节点，会和父层公用一个GraphicsLayer。
- 每个GraphicsLayer都拥有GraphicsContext，GraphicsContext输出的位图会作为纹理上传到GPU中。
- 什么是纹理？可以把它想象成一个从主存储器(例如 RAM)移动到图像存储器(例如 GPU 中的 VRAM)的位图图像(bitmapimage)
- Chrome 使用纹理来从GPU上获得大块的页面内容。通过将纹理应用到一个非常简单的矩形网格就能很容易匹配不同的位置(position)和变形(transformation)。这也就是3DCSS的工作原理，它对于快速滚动也十分有效
- 提升到合成层后合成层的位图会交GPU处理，但请注意，仅仅只是合成的处理（把绘图上下文的位图输出进行组合）需要用到GPU，生成合成层的位图处理（绘图上下文的工作）是需要CPU。
- 当需要repaint的时候可以只repaint本身，不影响其他层，但是paint之前还有style， layout, 那就意味着即使合成层只是repaint了自己，但style和layout本身就很占用时间。
- 仅仅是transform和opacity不会引发layout和paint，那么其他的属性不确定。

## reflow

- reflow
  - 如果引起reflow，样式首先必须重新计算，因此重排会触发两种操作
  - force reflow 
    - https://gist.github.com/paulirish/5d52fb081b3570c81e3a
- 当在js中调用（requested/called）以下所有属性或方法时，浏览器将会同步地计算样式和布局，进行重排( `reflow` 或layout thrashing)，通常是性能瓶颈
- element
  - 盒子计算
      - elem.offsetLeft/offsetTop, elem.offsetWidth/offsetHeight
      - elem.offsetParent
      - elem.clientLeft/clientTop, elem.clientWidth/clientHeight
      - elem.getClientRects(), elem.getBoundingClientRect()
  - frame/image
      - height, width
  - 滚动相关
      - elem.scrollBy(), elem.scrollTo()
      - elem.scrollIntoView(), elem.scrollIntoViewIfNeeded()
      - elem.scrollWidth/scrollHeight, elem.scrollLeft/scrollTop

  -焦点

      - elem.focus() 可以引起两次重排
  - 获取其他属性
      - elem.computedRole, elem.computedName
      - elem.innerText
- window.getComputedStyle()
  - 通常会引起样式重新计算
  - 元素在shadow tree中
  - 使用了media queries（viewport相关的一种），特别是以下某一属性
      - width, height
      - aspect-ratio,device-pixel-ratio, resolution, orientation
  - 获取以下的某一种属性
      - width, height，top, right, bottom, left
      - margin,padding
      - transform, translate, rotate, scale
      - x, y, rx, ry
- window
  - window.scrollX, window.scrollY, scrollBy(), scrollTo(), scrollX/Y
  - window.innerHeight, window.innerWidth
  - window.getMatchedCSSRules() 仅重新计算样式
  - webkitConvertPointFromNodeToPage(), webkitConvertPointFromPageToNode()
- form
  - inputElem.focus()
  - inputElem.select(), textareaElem.select()
- mouse
  - mouseEvt.layerX/layerY, mouseEvt.offsetX/offsetY
- document
  - doc.scrollingElement 仅重新计算样式
- range
  - range.getClientRects(), range.getBoundingClientRect()
- svg
  - computeCTM(), getBBox()
  - getCharNumAtPosition(), getNumberOfChars()
  - getComputedTextLength(), getSubStringLength(), selectSubString()
  - instanceRoot
  - 很多
- contenteditable
  - 非常多，包含复制图片到剪切板
- 如何避免reflow
  - for循环里触发重排或改变DOM性能最差
  - 使用DevTools Timeline分析性能问题的位置
  - 合并读写DOM操作，参考[FastDOM](https://github.com/wilsonpage/fastdom)，或使用虚拟DOM
- ref
  - https://jinlong.github.io/2015/09/30/what-forces-layout-reflow/
  - https://www.zcfy.cc/article/fastersite-how-not-to-trigger-a-layout-in-webkit
