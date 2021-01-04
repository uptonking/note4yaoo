---
title: viz-base-canvas
tags: [canvas, viz]
created: '2020-07-17T13:36:32.433Z'
modified: '2020-12-21T07:46:54.190Z'
---

# viz-base-canvas

# 在Canvas中实现动画

- ## [实战：在 Canvas 中实现动画](https://www.zhihu.com/market/pub/119647264/manuscript/1182364509212303360)

- 在Canvas中，动画是通过一系列连续的画面按顺序呈现的。
- 而这些连续的画面是即时绘制出来的，为了让动画更加流畅，可能需要在很短的时间内重新绘制动画很多次。
- 动画的大致实现流程可以分为以下几个步骤
  - 清空画布。
  - 改变绘图的状态，包括变换坐标系统、修改各种属性等。
  - 重新绘制图形。
  - 回到第一步。
- 在上面几个步骤的轮回中，需要将绘制动作放在一个定时器里。JavaScript提供了两个定时器方法，分别是 `setInterval` 和 `setTimeout`
- 为了方便绘制图像，可能需要频繁修改绘图的状态，及时保存和恢复状态可以让你方便许多。

- ## [Canvas 动画简介](https://www.zhihu.com/pub/reader/119583977/chapter/1058119929794027520)

- Canvas 动画实际上就是一个「不断清除、重绘、清除、重绘的过程」。也就是说，想要实现 Canvas 动画，也就只有两步。

# ref

- [canvas动画](https://zhuanlan.zhihu.com/p/73561191)
  - canvas动画原理：快速切换的静态画面
  - 动画步骤：绘制 - 清空 - 绘制 - 清空 - 绘制...
  - 控制函数：setTimeout, setInterval, requestAnimationFrame
  - 运动效果：线性、变速、函数运动如正弦、环形
- [SpriteJS —— Canvas动画从未如此简单](https://zhuanlan.zhihu.com/p/38265264)
  - SpriteJS是一款由360奇舞团开源的跨终端canvas绘图库，可以基于canvas快速绘制结构化UI、动画和交互效果，并发布到任何支持canvas环境的平台上（比如浏览器、小程序和node）
  - Sprite为图形创建类似于DOM的对象模型，因此我们可以像创建DOM元素一样，创建Sprite元素，并将它们append到layer上，从而将元素呈现到画布上
  - 如果只是绘制静态图形，SpriteJS还体现不出优势，但如果要给图形增加动画效果，那么SpriteJS内置了Transition API和标准的Web Animation API
