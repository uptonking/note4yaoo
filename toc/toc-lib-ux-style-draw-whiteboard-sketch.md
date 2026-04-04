---
title: toc-lib-ux-style-draw-whiteboard-sketch
tags: [drawing, hand-drawn, sketch, toc, ux, whiteboard]
created: 2020-08-09T09:04:58.352Z
modified: 2025-03-22T18:23:37.602Z
---

# toc-lib-ux-style-draw-whiteboard-sketch
- search
  - paper, reading, reader, document

- whiteboard-solutions
  - 🆚️ 技术栈基于svg容易实现缩放，基于dom不容易缩放
  - [Excalidraw白板调研文档](http://wangxiang.website/docs/work/excalidraw.html)
    - npm 包目前不支持：多人协作、共享链接等，不过 Excalidraw 团队已经在规划当中，不久就会以插件的形式支持。
# popular
- tldraw /5.8kStar/MIT > Free+watermark/202202/ts
  - https://github.com/tldraw/tldraw
  - https://www.tldraw.com/
  - https://tldraw.substack.com/archive
  - 基于svg实现
  - [License updates for the tldraw SDK - by Steve Ruiz _20231220](https://tldraw.substack.com/p/license-updates-for-the-tldraw-sdk)
    - Under our new license, you are permitted to use the tldraw SDK for non-commercial purposes.
    - The pre-release 2.x versions released until Apache-2.0 will remain licensed under Apache-2.0.
    - The 1.x version of tldraw will remain licensed under MIT forever. 
    - We’ve discussed selling a hosted collaboration service, similar to TipTap Collab, or splitting the library into free features and premium features like AgGrid, pricing based on usage like MapBox, or even turning tldraw.com into a teams-based SaaS app like Excalidraw+.
  - [Change licenses to tldraw _20231219](https://github.com/tldraw/tldraw/pull/2167)
  - packages/tldraw contains the source for the @tldraw/tldraw package. 
    - 依赖 radix-ui、@stitches/react、@tldraw/core、zustand
    - This is an editor as a React component named `<Tldraw>`.
    - You can use this package to embed the tldraw editor in any React application
  - packages/core contains the source for the @tldraw/core package. 
    - 依赖 mobx-react-lite、@use-gesture/react
    - This is a renderer for React components in a canvas-style UI. 
    - It is used by @tldraw/tldraw as well as several other projects.
  - core-example is a simple example for @tldraw/core
    - 示例使用mobx-react-lite作为状态管理
  - https://github.com/justjake/tlshot
    - Take screenshots and edit them with tldraw.
  - 🍴 forks
  - https://github.com/DallasCarraher/compound
    - This fork of tldraw is focused on providing a free-for-commercial-use white boarding tool

- excalidraw /94.6kStar/MIT/202503/ts/canvas
  - https://github.com/excalidraw/excalidraw
  - https://excalidraw.com/
  - 基于canvas实现
  - Virtual whiteboard for sketching hand-drawn like diagrams
  - https://twitter.com/Vjeux/status/1292706657663762432
    - Excalidraw stores everything into a giant variable "AppState" and whenever it changes, we re-draw the canvas and optionally the UI if needs be.
    - We don't use `requestAnimationFrame`, we respond to DOM events directly. 
    - History is implemented pushing `JSON.stringify(appState)` to an array. It's pretty memory heavy, we need to optimize this at some point! 
  - [产品经理：客户想要个画板，你们前端能不能做？ | 学习笔记](http://wangxiang.website/docs/work/excalidraw-use.html)
  - https://github.com/UreekaBiz/svg-poc
    - An Excalidraw-like SVG Proof-of-Concept

- https://github.com/plait-board/drawnix /MIT/202503/ts/svg
  - https://drawnix.com/
  - 开源白板工具（SaaS），一体化白板，包含思维导图、流程图、自由画等
  - 基于插件机制 - 可灵活扩展
  - 导出为 PNG, JPG, JSON(.drawnix)
  - 编辑特性：撤销、重做、复制、粘贴等
  - 无限画布：缩放、滚动
  - Drawnix 的定位是一个开箱即用、开源、免费的工具产品，它的底层是 Plait 框架，Plait 是我司开源的一款画图框架，代表着公司在知识库产品上的重要技术沉淀。
  - Drawnix 是插件架构，能够支持多种 UI 框架（Angular、React），能够集成不同富文本框架（当前仅支持 Slate 框架），在开发上可以很好的实现业务的分层
- https://github.com/worktile/plait /MIT/202503/ts/svg
  - https://plait.pages.dev/
  - A completely customizable framework for building all-in-one drawing whiteboard
  - core依赖roughjs、immer, 通过rxjs的Subject将状态放入context(仅一个文件使用rxjs)
  - 对于形状绘制如circle/line/rectangle依赖RoughSVG
  - 代码架构几乎完全模仿slate
  - Plait does not rely on any frontend UI framework at its core, but it provides solutions for integrating with mainstream frontend UI frameworks 
  - Text rendering in the plait is based on the Slate framework, Plait was inspired by the Slate framework in its design

- https://github.com/phedkvist/whiteboard
  - https://whiteboard-umber.vercel.app/
  - a simple whiteboard application.
  - 只依赖react
  - 画板元素都是svg元素

- https://github.com/typsusan-zzz/canvas-drawing-editor /496Star/MIT/202512/ts/canvas/NoDeps
  - https://typsusan-zzz.github.io/canvas-drawing-editor/
  - https://typsusan-zzz.github.io/canvas-drawing-editor/demo.html
  - 强大的 Canvas 画布编辑器 Web Component，零依赖，支持 Vue 2/3、React、Angular 和原生 HTML
  - 图片支持 - 导入和编辑图片，支持亮度/对比度/模糊等滤镜
  - 撤销/重做 - 完整的历史记录支持（Ctrl+Z / Ctrl+Y）
  - 图层管理 - 图层上移/下移/置顶/置底，可见性和锁定控制
  - 更多形状 - 星形、心形、三角形、菱形、贝塞尔曲线
  - 富文本 - 支持部分加粗、部分改色、部分斜体
  - 移动端支持 - 单指拖拽、双指缩放/旋转、长按选择、响应式布局
  - 轻量级 - gzip 后约 33KB

- https://github.com/gezilinll/blitz /202404/ts/vue
  - [Blitz：可以实时聊天的多人协同白板 _202307](https://zhuanlan.zhihu.com/p/643903971)
    - 无限画布 目前我是直接使用 Pixi 作为渲染引擎，因此只需要将视图中的 传递给 Pixi 的 Application 即可
    - 编辑器用户界面框架是基于 Vue3 落地的，在 UI 组件和风格上采用的是 Element-Plus 为主
    - 协同编辑我采用的是 Hocuspocus 的解决方案，其除了提供客户端的 Provider 外，也提供了对应服务端的 SDK

- https://github.com/LHRUN/paint-board /MIT/202309/ts
  - https://songlh.top/paint-board/
  - 基于canvas的多功能画板
  - 依赖react-dnd、daisyui
  - Canvas based drawing board, including free drawing, eraser, text, select, layer, undo, redo, clear, save, drag

- https://github.com/mirayatech/NinjaSketch /202401/ts
  - https://ninja-sketch.vercel.app/
  - Excalidraw clone built with React and TypeScript.
  - Rough.js is used for the sketchy, hand-drawn style.

- roughViz /MIT/5.4kStar/202006
  - https://github.com/jwilber/roughViz
  - a reusable JavaScript library for creating sketchy/hand-drawn styled charts in the browser, based on D3v5, roughjs, and handy.
- https://github.com/rough-stuff/rough /MIT/202311/ts/inactive
  - https://roughjs.com/
  - https://github.com/rough-stuff/rough/wiki
  - a small (<9kB gzipped) graphics library that lets you draw in a sketchy, hand-drawn-like, style.
  - Rough.js works with both Canvas and SVG.
  - RoughCanvas or RoughSVG provides the main interface to work with this library
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

- https://github.com/rocicorp/replidraw
  - https://replidraw.herokuapp.com/
  - A tiny Figma-like multiplayer graphics editor.
  - Built with Replicache, Next.js, Pusher, and Postgres.
    - pusher: create and maintain complex messaging infrastructure

- https://github.com/plantain-00/composable-editor-canvas /MIT/202404/ts
  - https://plantain-00.github.io/composable-editor-canvas/
  - A composable editor canvas library.
  - 提供了多种编辑场景示例
  - 提供了多种render target:react, react-canvas, react-svg, react-webgl
  - 实现了2种undo: undo, patch-based-undo-redo

- https://github.com/antfu/drauu /1.4kStar/MIT/202502/ts
  - https://drauu.netlify.app/
  - Headless SVG-based drawboard in browser.
  - built with Vanilla JavaScript
  - Built for Slidev.
  - Stylus / Touch pressure support
  - Undo / Redo stacks

- https://github.com/mohitkumartoshniwal/whiteboard-konva-react /202402/js
  - Code for the Youtube video on building excalidraw clone using React and Konva.js
  - [Excalidraw or Figma Clone using React and Konva - YouTube](https://www.youtube.com/watch?v=LXlE1y5PQsk)

- https://github.com/SarthakRawat-1/sketchbook-ui /MIT/202604/ts
  - https://sarthakrawat-1.github.io/sketchbook-ui/
  - A hand-drawn React component library with a sketchy, notebook aesthetic.
# canvas-drawing
- https://github.com/ZimengXiong/ExcaliDash /AGPL/202511/ts
  - A self-hosted dashboard and organizer for Excalidraw with live collaboration features.
  - 提供了一个清爽的管理界面（仪表盘），永久保存你画的每一张图。你可以搜索、整理文件一样，把不同的画稿拖拽到“收藏夹”里分类

- https://infinitecanvas.tools/gallery/
  - 画板类产品列表
  - The infinite canvas is the foundation of a new class of apps from design tools, to code editors, and workspaces.

- https://github.com/dlemrry/editor /202109/js/inactive
  - real time collaborative documents using web socket
  - Web application for editing texteditor and painting canvas in real-time collaboration.
  - 展示了 quill、draftjs、canvas+mousemove 几个示例
  - 提供了client+server，可作为通用协作方案

- https://github.com/JessYan0913/pictode /MIT/202409/ts/vue/inactive
  - https://pictode.com/
  - 最方便集成的绘图工具
  - [Pictode：十分钟 DIY 图形编辑器 _202310](https://fast.v2ex.com/t/979389)
# styling
- https://github.com/imrishabh18/text-to-handwriting
  - https://imrishabh18.github.io/text-to-handwriting
  - convert text copied or typed into handwriting, which can be downloaded in images making it look real.

- https://github.com/papercss/papercss /字体变成手写体
  - https://www.getpapercss.com/
  - The Less Formal CSS Framework
  - https://github.com/gouflv/react-papercss-ui
    - A React UI components made with PaperCSS

- NES.css /MIT/15kStar/202006
  - https://github.com/nostalgic-css/NES.css
  - https://nostalgic-css.github.io/NES.css/
  - a NES-style(8bit-like) CSS Framework
  - 像素风格的文字和组件

- https://github.com/BafS/Gutenberg
  - https://bafs.github.io/Gutenberg
  - Modern framework to print web pages correctly
  - Gutenberg.css is the base stylesheet but there are themes available in the themes folder.

- https://github.com/KyleAMathews/typography.js
  - http://kyleamathews.github.io/typography.js/
  - /3.5kStar/MIT/202008/js
  - Typography is a complex system of interrelated styles. 100s of style declarations on dozens of elements must be in harmonious order. Trying one design change can mean making dozens of tedious recalculations and CSS value changes. Creating new Typography themes with CSS feels hard.
  - You can provide configuration to the Typography.js JS api and it uses its Typography engine to generate CSS for block and inline elements.
  - Typography.js themes are simple Javascript objects. As such they're easy to share across projects
# typesetting-font
- https://github.com/Myriad-Dreamin/typst.ts /907Star/apache2/202512/rust/ts
  - https://myriad-dreamin.github.io/typst.ts
    - 示例渲染为html元素，文字可选择，但没有视觉上的分页线
  - a project dedicated to bring the power of typst to the world of JavaScript
  - 效果类似付费版 [Typst: The new foundation for documents](https://typst.app/play)
    - 此示例右侧预览pdf渲染为`<canvas>`元素
  - [Use typst as library in browser? · Issue · typst/typst _202304](https://github.com/typst/typst/issues/909)
    - Typst can be compiled to WASM, but no JS glue is available, you'd have to write that yourself. It's not as simple as compile(string) because you also need to provide fonts, and if you want a multi-file setup of course also files.

- https://github.com/davidmerfield/Typeset
  - https://typeset.lllllllllllllllll.com/
  - An HTML pre-proces­sor for web ty­pog­ra­phy
  - Typeset does not re­quire any client-side JavaScript and uses less than a kilo­byte of CSS. 
  - Processed HTML & CSS works in Internet Explorer 5 and with­out any CSS. 
  - pro­vides ty­po­graphic fea­tures used tra­di­tion­ally in ﬁne print­ing which re­main un­avail­able to browser lay­out en­gines.
    - Real hang­ing punc­tu­a­tion
    - Optical mar­gin align­ment
    - Small caps de­tec­tion
    - Soft hy­phen in­ser­tion
    - Punctuation sub­sti­tu­tion

- https://github.com/bramstein/typeset /js
  - TeX line breaking algorithm in JavaScript
  - This is an implementation of the Knuth and Plass line breaking algorithm using JavaScript.

- https://github.com/palantir/typesettable /ts/inactive
  - a library for measuring, wrapping, and writing text on Canvas, SVG, and HTML.
  - developers often want wrapped text to auto-hyphenate and truncate with ellipses when overflowing the bounding box. Typesettable aims to make this entire process easier.
  - Typesettable works with native browser APIs and has no external dependencies.

- https://github.com/exogen/react-typesetting /js/inactive
  - https://exogen.github.io/react-typesetting/
  - React components for creating beautifully typeset designs.
  - `TightenText` component is intended to give short runs of text (like titles, labels, etc.) some “give” before wrapping.
  - `PreventWidows` component instead works by actually measuring the widths of lines, and can thus support many different ways to specify the desired minimum width
  - `Justify` component solves this by conditionally setting text as justified only when there is enough room
# cn/汉字与排版
- tips
  - [The Type — 文字 / 设计 / 文化 » 中文排版网格系统的五大迷思](https://www.thetype.com/2020/01/16565/)

- https://github.com/ethantw/Han /2kStar/MIT/201903/js/inactive
  - https://hanzi.pro/
  - Han.css: the CSS typography framework optimised for Hanzi.
  - 「汉字标准格式」是一套支援各种印刷效果的Sass + JavaScript排版框架
  - 集成「语意样式标准化」「文字设计」「高级排版功能」三大模组，并为繁体中文、简体中文及日文配置的本地化设计

- https://github.com/sivan/heti
  - https://sivan.github.io/heti/
  - 专为中文网页内容设计的排版样式增强。 
  - 预置多种排版样式（行间注、多栏、竖排等）；
  - 中英文混排优化：无论你的输入习惯是否在中西文间留有空格，都会统一成标准间距（¼字宽的空白）；
  - 标点挤压：自动对中文标点进行½字宽的挤压（弯引号和间隔符挤压¼字宽）
  - https://github.com/crazyurus/ancient-heti
    - https://ancient-heti.vercel.app/
    - 古文，采用 heti.css 排版

- https://github.com/sparanoid/chinese-copywriting-guidelines
  - https://sparanoid.com/note/chinese-copywriting-guidelines/
  - 统一中文文案、排版的相关用法，降低团队成员之间的沟通成本

- https://github.com/sofish/typo.css
  - 目标：一致化浏览器排版效果，构建最适合中文阅读的网页排版。包括桌面和移动平台。
  - 强制换行：添加 .textwrap 到文本所在的容器，如果是 table 测还需要 .textwrap-table

- https://github.com/CoffeeIO/TypesetBot /ts/GPLv3
  - https://coffeeio.com/typesetbot/
  - bringing TeX level typesetting to the web

- https://github.com/harttle/md-padding
  - https://harttle.land/md-padding/
  - 修复 Markdown 中的混排空格：中英文、数字、链接等。

- https://github.com/Haixing-Hu/typesetting-standard
  - 中文书刊排版相关标准和规范

- https://github.com/satouriko/copywriting-correct
  - 中英文文案排版纠正器。
  - 本项目是 ricoa/copywriting-correct 的 JavaScript 实现。
  - 基于 中文文案排版指北（简体中文版） 进行纠正，帮助解决中英文混排的排版问题，提高文案可阅读性。

- https://github.com/huacnlee/autocorrect /rust
  - AutoCorrect 是一个基于 Rust 编写的工具，用于「自动纠正」或「检查并建议」文案，给 CJK（中文、日语、韩语）与英文混写的场景，补充正确的空格，纠正单词，同时尝试以安全的方式自动纠正标点符号等等。

### 支持中文的字体

- https://github.com/Warren2060/Chillkai
  - 寒蝉正楷体，为优化中西文排版的楷体项目
  - 由中文字体 全字库正楷体 和西文字库 Gentium 整合优化

- https://github.com/heangfat/cjk-math-type
  - 中華數碼之排版工具與方法
  - 本庫提供一款可變字型，包含筭籌、花碼、筮數，並簡述其基本用法。
# wireframe
- https://github.com/tsx/shireframe
  - http://rawgit.com/tsx/shireframe/master/examples/doodle.html
  - Declarative wireframes for programmers

- https://github.com/mydraft-cc/ui
  - https://mydraft.cc/
  - 依赖react, redux, antd, typescript
  - The goal of this project is to create an open source wireframing tool. 
# ink 水墨画
- https://github.com/BloodmageThalnos/ShadowInk
  - 基于深度学习的水墨画创作与分享平台
# more
- https://github.com/steveruizok/perfect-freehand
  - https://perfect-freehand-example.vercel.app/
  - a library for creating freehand paths 

- https://github.com/szimek/signature_pad
  - http://szimek.github.io/signature_pad/
  - Signature Pad is a JavaScript library for drawing smooth signatures. 
  - It's HTML5 canvas based and uses variable width Bézier curve interpolation based on Smoother Signatures post by Square. 
  - It doesn't depend on any external libraries.

- https://github.com/MyScript/iinkJS
  - https://developer.myscript.com/
  - integrate rich handwriting recognition features in your webapp.
  - Get your keys and the free monthly quota to access MyScript Cloud at developer.myscript.com

- d3-canvas
  - https://observablehq.com/@d3/draw-me

- d3-svg
  - [Build a free-hand drawing app with React Hooks](https://reactfordataviz.com/articles/mouse-events-with-d3v6-react-hooks/)
# discuss-typesetting
- ## 中式排版必须先计算栏宽定下版心之后，再把版心摆放到页面上，
- https://twitter.com/Kongque_Chinese/status/1682265824076402689
  - 至于页边距的数值，是页面减去版心之后计算出来的；
  - 也就是说，并非事先「定」出来、而是之后「余」出来的，这与西式排版正相反。
