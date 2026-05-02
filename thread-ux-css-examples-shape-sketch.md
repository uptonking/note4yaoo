---
title: thread-ux-css-examples-shape-sketch
tags: [codepen, examples, shape, sketch, thread, ux]
created: 2022-11-21T15:25:52.884Z
modified: 2022-11-21T15:27:20.974Z
---

# thread-ux-css-examples-shape-sketch

# guide

# ux-examples
- ## 

- ## 

- ## 

- ## the new CSS border-shape API makes this possible: 手绘/草稿风格边框线条
- https://x.com/wesbos/status/2050252606501457958

- ## 常见的为 DOM 设置平滑圆角的方案大多使用的 mask，我来分享一种利用 superellipse 并在数学上对齐顶点，并支持多重方案低成本使用 
- https://x.com/xiaolinbythesea/status/2039644145044824305
- chrome 不久前实现了border shape，任意形状的边框都可以了

- ## 你现在可以轻松用纯 css 实现小米 logo 的圆角，gemini logo，以及曾经让你头疼的优惠券挖凹角效果
- https://x.com/dongnaebi/status/1988794318539354505
- 兼容性
  - 没事，样式问题不会导致崩溃，只是回退到普通圆角

- ## 3个box在hover时切换布局的示例
- https://twitter.com/nanxiaobei/status/1719748228483330462
  - 纯 CSS 实现 https://codepen.io/nanxiaobei/pen/NWEWBra
  - JS 版本 https://codepen.io/nanxiaobei/pen/dyaXwgK

- ## This is my implementation of @AndrewGlassner 's glob shape
- https://twitter.com/steveruizok/status/1369756871041683457
  - https://4qr7f.csb.app/
  - https://codesandbox.io/s/glob-4qr7f
- I think this is the strategy used by @GoodNotesApp for their lines (which are great btw). Those look like globs to me. 👀 And they erase well—glob by glob.
- The first challenge: the points of a glob need to be far enough away from each-other to allow us to draw tangents between them. (If the handles end up inside of the circles, the glob breaks.) We'll need to lose points, but we still may need those points to inform the curve.
- TIL about Glob! Thinking of using them in your drawing tool? What's the application? Other than being somehow adorable
  - Yeah, I think we can link them together to create dynamic lines! (Also, you can spin those circles and curves if you want to try this in 3D! See the link at the bottom of the demo.)

- ## 60° Gradient Morphing Blob
- https://twitter.com/HiTw93/status/1593816335594684416
  - https://codepen.io/georgedoescode/pen/oNzamjV
  - 动态水滴的效果，渐变形状和颜色
  - 水滴采用科幻风格的渐变色
  - 基于svg实现
