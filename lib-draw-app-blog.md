---
title: lib-draw-app-blog
tags: [blog, drawing, whiteboard]
created: 2023-09-07T04:18:49.697Z
modified: 2023-09-07T04:19:18.677Z
---

# lib-draw-app-blog

# guide

# blogs-collab

# blogs

## 🚀 [从零打造现代化绘图框架 Plait - 知乎 _2022](https://zhuanlan.zhihu.com/p/609592474)

- 我们基于自研的绘图框架初步完成了一个脑图组件并成功集成到我们 PingCode Wiki 中
- Canvas 还是 SVG 其实社区中也没有一个明确的答案，我们参考了一些知名产品的方案选型，SVG 和 Canvas 都有并且实现的效果都不差，
  - 比如语雀的白板使用的是 SVG，ProcessOn 使用的是 Canvas，Excalidraw 使用的是 Canvas，drawio 使用的是 SVG 等等。
  - 因为我们没有 Canvas 的使用经验，加上我们的思维导图节点希望支持富文本内容，所以暂时选定对 DOM 更友好的 SVG
- 我们整体是 SVG + Richtext 的方案。
  - 绘图使用 SVG ，目前我们脑图节点、节点连线、展开收起图标等等都是基于 SVG 绘制的。
  - 节点内容使用 foreignObject 包括嵌入到 SVG 中，这种方案使节点内容支持富文本。

- Plait 框架「插件机制」的部分，这部分的灵感来源于富文本编辑器框架 Slate。

- 
- 
- 

## [plait - Web画图技术之画布滚动方案 - 知乎 _202403](https://zhuanlan.zhihu.com/p/688702380)

- 主流的画板的滚动有两种交互，暂且把他们命名为：无限画布和有限画布
  - Excalidraw 、BlockSuite 算是无限画布，言外之意时画布是没有区域限制的，可以无限滚动到任何区域，也就是因为无限滚动的原因，整个画布是没法显示确切的滚动条，用户也就无法明确的知道那个区域有绘图元素。
  - 语雀、XMind、ProcessOn 等产品是采用有限画布的形态，有限画布有一个优点就是可以显示滚动条 - 能直观的展示看出内容区域的大小，并且滚动区域会跟随绘图元素及其位置而动态更新。
- 我们最终选择了「有限画布」的交互形态。

- 画布的缩放是通过改变 SVG 元素的宽高实现，就是保持 viewBox 映射区域计算逻辑不变，让真实 SVG DOM 的宽高放大/或者指定比例实现绘图元素的缩放。

- 
- 
- 

# more
