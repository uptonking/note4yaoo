---
title: thread-pm-base-office-whiteboard-draw
tags: [office, whiteboard]
created: 2023-05-30T21:36:19.919Z
modified: 2023-05-30T21:36:55.391Z
---

# thread-pm-base-office-whiteboard-draw

# guide

- [Rendering like Butter - a Confluence Whiteboards Story - Atlassian Engineering_202308](https://www.atlassian.com/engineering/rendering-like-butter-a-confluence-whiteboards-story)
  - Great insight into building high performance whiteboard for the Web
  - Finite State Machine
  - Entity Component System
  - WebGL
  - Tiling
  - While the essay concluded that the most efficient way to render things was using WebGL, the benchmark also showed that DOM+React was not that bad (3~4x slower than Raw WebGL)—small products and personal projects may not need the burden of WebGL.

- [Figma已被替代, Miro还会远吗？——无限白板大全 - 知乎 _202205](https://zhuanlan.zhihu.com/p/512318494)
# discuss-stars
- ## 

- ## 

- ## What if a graph view and text editor were just two ends of a continuous spectrum? 
- https://twitter.com/OrionReedOne/status/1790263523857019227
  - You get consistent semantics, intermediate views, and some other benefits by blending structurally-compatible representations.
  - Here's a 'semantic zoom' in @tldraw
  - 类似大纲视图作为网状节点图的节点
- This could be a great alternative to the outliner as a notetaking system ... Incidentally, I've also been playing with defining graph models from within the text itself, and linking them together ...

- i want all of my code editing to be like this
  - we are not in the stage of editing yet, currently only for code navigation, but we will be full blown editor ultimately
  - [Spectral Beta - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=SenecaFron.spectral-beta)
- Yes I need this in my ide
- If only something like @orgpad_official had a free version that i could run as an app offline or sync manually, that wouldn't cost me lifetime decency on non-trustable company.

- Knowledge graph? Or token linkage based on similarity?

- ## 有朋友问我Miro好在什么地方。
- https://twitter.com/PenngXiao/status/1739195961199800601
  - Miro有一个非常难用的地方，比如Table只难看有点不可思议。除此之外，完全没有一个地方支持Markdown也有点令人费解。
  - 除此之外，Miro的每个细节都完美的符合我的预期。
- 这样的产品单独说它好很难解释，就拿BoardOS做个对比，我用了几分钟发现的几个细节差距（不称为问题）：
  1. Sticky note里面的换行
  2. 触摸板移动无限画布不符合直觉
  3. 缩放速度太快、太敏感
  4. Mindmap选中之后不能独立缩放
  - BoardOS是一个非常优秀的产品，以上完全可能是我习惯了Miro之后的不适，并非产品的问题。

# discuss
- ## 

- ## 

- ## 

- ## 

- ## We've shipped follow mode
- https://twitter.com/excalidraw/status/1737130730587603053
  - 适合画板类应用，当一个人操作时，另一个人的可见区域和focus跟随主要操作人

- ## 请考究派同学帮忙解释一下这个现象——为啥用户放着正规的图不用，喜欢手写风格。这个值得做成一个收费的特性吗？
- https://twitter.com/PenngXiao/status/1735204643138134241
- 不想为了几个像素的对齐，来回折腾。
  - diagram as code类产品没有这个问题，反正也不是用户控制布局
- 常用 plantuml，但这类工具和贴图里面所见即所得的画图工具是两种产品形态。
- 涂鸦符合人性。人就喜欢这种符合直觉但不准确的表达方式。
- 手写风格的ui设计图是有价值的， 不是喜欢而已，因为图是拿来沟通的，你的沟通对象可能是用户（客户）或其他非专业人士， 手写风格潜移默化给对方灌输 和强化 “这是草稿” 的概念，避免讨论沟通时跑题到当前不需要关注的细节去。 
  - 举个例子，讨论功能时，面对一个精美的按钮，有些客户会说按钮太大了
  - 但是面向一个手绘风格的按钮，讨论对象都知道最终ui肯定不是这样，所以不会提出样式上的建议意见而浪费大家讨论的时间。

- 自由，不受限制，才有创意产生。

- ## Added a timeline view to the @remix_run DevTools! (WIP) made with @vite_js
- https://twitter.com/aryan__deora/status/1725909619644461144
  - A neat way to visualize link prefetches too!
  - 页面fetch时序动画
  - 上面是页面，下面是devtools

- ## new discovery! use numbered figures (e.g. fig 1, fig 2) to describe different stages of an interaction
- https://twitter.com/tldraw/status/1726047257403830736
- Wait until I can import my figma into this
  - just copy a screenshot and paste it in 

- ## What if @figma had a cursor video chat?
- https://twitter.com/alexeinars/status/1706333517242618342
  - 鼠标光标移动时，光标旁显示用户视频界面而不是偷笑

- ## Do you prefer @tldraw to @excalidraw ?
- https://twitter.com/jitl/status/1643764436660899840
  - Excalidraw is ahead on features, TLDraw is ahead in my heart
- I like the code a lot more than the Excalidraw code, and I've learned a ton from following @steveruizok's work over the years

- ## meeting Steve and spending the day understanding @tldraw ’s vision (not as “another excalidraw”, but an embeddable canvas for everyone) 
- https://twitter.com/swyx/status/1598558782388256768

- ## A tangent thread is about how spatial canvases come into play. 
- https://twitter.com/chrisshank23/status/1663296920150999040
  - Particularly thinking about @tldraw 's early vision to provide a platform for other to build spatial canvases...
- I see a gap between unstructured spatial canvases and meaningful, structured diagramming tools. Spatial canvases nudge you to create your own conceptual framework for a task. Diagramming tools are domain-specific and have little extensibility.
  - The unstructured nature of a spatial canvas likely manifests in its implementation of a bunch of lines/shapes with coordinates that you move around. These shapes have no inherent relationship or meaning in the data representation only the human perceiving the canvas.

- What's cool is that the "nextgen" spatial canvases like @excalidraw and @tldraw are starting to explore this a little. 
  - For example, both have the first-class concept of arrows/lines connecting shapes together!
