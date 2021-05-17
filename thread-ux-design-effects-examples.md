---
title: thread-ux-design-effects-examples
tags: [examples, thread, ux]
created: '2021-03-26T09:10:52.255Z'
modified: '2021-05-10T04:06:02.843Z'
---

# thread-ux-design-effects-examples

# pieces

- ## 

- ## I‘ve made a mini playground project to walk you through our new Variant updates. 
- https://twitter.com/benjaminnathan/status/1392486734311694342
  - https://t.co/0PYB9pApAA?amp=1
  - 组件背景会自动变宽或变窄

- ## Inspired by @peduarte I also made changes to the code highlight UI: muted color 
- https://twitter.com/pveyes/status/1391641615295385603
  - I'm still keeping highlight color & indicator on hover because main use case is exploring code through twoslash
  - 默认只高亮部分代码，鼠标移动时高亮全部代码

- ## themed window
- https://twitter.com/jsngr/status/1391503528443711490
  - 软件窗口的主题

- ## Really happy with how the coded version of this Pricing Page design by @jamesm turned out for an upcoming Tailwind UI update
- https://twitter.com/david_luhr/status/1390407355733577735
  - Lots of interesting semantic markup and responsive design considerations for the pricing tiers and feature comparison sections.
  - 屏幕由宽变窄时ui变化的过程
- Many feature comparison sections in the wild aren't actually accessible. 
  - To do thing properly, we use a well-structured `<table>` on larger screens and a `<dl>` (definition list) on smaller screens to present this dense content in a semantic way.
- Another detail: in the feature comparison, the "cards" are faked to work around `<table>` and `<dl>` limitations. 
  - Semantics always come first. 
  - They're backgrounds, followed by the content, followed by borders, which scale with the content, all hidden from the accessibility tree.

- ## glob style looks perfect for Chinese/Japanese characters.
- https://twitter.com/lomography1996/status/1389525442227413003

- ## Mini Fruit Carousels built with greensock
- https://twitter.com/jh3yy/status/1383548575972352006
  - 环状走马灯，可以循环播放
  - https://codepen.io/jh3y/pen/mdRjKgr

- ## I've improved reCAPTCHA.
- https://twitter.com/defaced/status/1381939949843406856
  - 验证码的形式是类似移动方块将九宫格(少1块)拼成一幅图，真的难
  - after 5 minutes of failing: "damn, guess I'm not human"
  - You monster.

- ## Our design team lead Andrey O. has become a judge 
- https://twitter.com/ZajnoCrew/status/1382001079181787138
  - 黑白卡片能传达出一直庄重感

- ## Control the size and color of a 16x16 dot matrix with a single JavaScript function. 
- https://twitter.com/aemkei/status/1323399877611708416
  - 一个矩阵全是点，可批量调整大小、颜色
  - https://tixy.land/

- ## I spend too much time building a #threejs preloader animation that nobody sees because it's on screen for just a second.
- https://twitter.com/marquizzo/status/1380580369515220992
  - 碎屑先拼接再破碎的效果，作为loading

- ## Took me 10+ hours to make this waterDroplet simulation with pressure.
- https://twitter.com/tdinh_me/status/1378995883090452481
  - 模拟水往下流的过程，可添加漂浮的船
- https://github.com/trungdq88/summer

- ## Scroll up to navigate router history?
- https://twitter.com/raunofreiberg/status/1379069069303947265
  - 界面历史的展示，使用堆叠层次的缩略图

- ## my latest project in solo "Mont Saint Michel 3D"
- https://twitter.com/VIGNEAurelien/status/1375114346905358346
  - 界面产生类似红旗随风飘扬小起伏的效果
