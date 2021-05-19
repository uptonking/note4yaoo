---
title: toc-lib-ux-style-sketch-hand-drawn
tags: [hand-drawn, sketch, toc, ux]
created: '2020-08-09T09:04:58.352Z'
modified: '2021-01-13T19:30:59.508Z'
---

# toc-lib-ux-style-sketch-hand-drawn

- search
  - paper, reading, reader, document

# popular

- excalidraw /15.3kStar/MIT/202101/ts
  - https://github.com/excalidraw/excalidraw
  - https://excalidraw.com/
  - Virtual whiteboard for sketching hand-drawn like diagrams
  - https://twitter.com/Vjeux/status/1292706657663762432
    - Excalidraw stores everything into a giant variable "AppState" and whenever it changes, we re-draw the canvas and optionally the UI if needs be.
    - We don't use requestAnimationFrame, we respond to DOM events directly. 
    - History is implemented pushing JSON.stringify(appState) to an array. It's pretty memory heavy, we need to optimize this at some point! 

- roughViz /MIT/5.4kStar/202006
  - https://github.com/jwilber/roughViz
  - https://github.com/rough-stuff/rough
  - a reusable JavaScript library for creating sketchy/hand-drawn styled charts in the browser, based on D3v5, roughjs, and handy.
- wired-elements /8.4kStar/MIT/202006/ts
  - https://github.com/rough-stuff/wired-elements
  - https://wiredjs.com/
  - Collection of custom elements that appear hand drawn. Great for wireframes or a fun look.
  - https://wiredjs.com/
- https://github.com/wiredjs/designer
  - Mockups and wire-framing tool built using web components. Uses hand-drawn sketchy controls.
  - https://wiredjs.github.io/designer

- https://github.com/gangtao/sketchify
  - turn svg graph into sketchy visualization
  - a js tool that turns svg graph into sketchy visualization. It is based on Rough.js

- https://github.com/timqian/chart.xkcd
  - a chart library that plots “sketchy”, “cartoony” or “hand-drawn” styled charts.
  - https://timqian.com/chart.xkcd/

- https://github.com/fxaeberhard/handdrawn.css /201606
  - http://fxaeberhard.github.io/handdrawn.css/
  - Handdrawn.css lets you prototype your web site with a hand drawn look and feel.

# paper

- https://github.com/papercss/papercss /字体变成手写体
  - https://www.getpapercss.com/
  - The Less Formal CSS Framework
- NES.css /MIT/15kStar/202006
  - https://github.com/nostalgic-css/NES.css
  - https://nostalgic-css.github.io/NES.css/
  - a NES-style(8bit-like) CSS Framework
  - 像素风格的文字和组件

- https://github.com/BafS/Gutenberg
  - https://bafs.github.io/Gutenberg
  - Modern framework to print web pages correctly
  - Gutenberg.css is the base stylesheet but there are themes available in the themes folder.
- https://github.com/ethantw/Han /2kStar/MIT/201903/js
  - https://hanzi.pro/
  - Han.css: the CSS typography framework optimised for Hanzi.
  - 「汉字标准格式」是一套支援各种印刷效果的Sass + JavaScript排版框架
  - 集成「语意样式标准化」「文字设计」「高级排版功能」三大模组，并为繁体中文、简体中文及日文配置的本地化设计
- https://github.com/KyleAMathews/typography.js
  - http://kyleamathews.github.io/typography.js/
  - /3.5kStar/MIT/202008/js
  - Typography is a complex system of interrelated styles. 100s of style declarations on dozens of elements must be in harmonious order. Trying one design change can mean making dozens of tedious recalculations and CSS value changes. Creating new Typography themes with CSS feels hard.
  - You can provide configuration to the Typography.js JS api and it uses its Typography engine to generate CSS for block and inline elements.
  - Typography.js themes are simple Javascript objects. As such they're easy to share across projects

# wireframe

- https://github.com/tsx/shireframe
  - http://rawgit.com/tsx/shireframe/master/examples/doodle.html
  - Declarative wireframes for programmers

- https://github.com/mydraft-cc/ui
  - https://mydraft.cc/
  - 依赖react, redux, antd, typescript
  - The goal of this project is to create an open source wireframing tool. 

# more

- https://github.com/steveruizok/perfect-freehand
  - https://perfect-freehand-example.vercel.app/
  - a library for creating freehand paths 
