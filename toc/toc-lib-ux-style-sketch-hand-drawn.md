---
title: toc-lib-ux-style-sketch-hand-drawn
tags: [hand-drawn, sketch, toc, ux]
created: 2020-08-09T09:04:58.352Z
modified: 2021-01-13T19:30:59.508Z
---

# toc-lib-ux-style-sketch-hand-drawn
- search
  - paper, reading, reader, document

- whiteboard-solutions
  - 🆚️ 技术栈基于svg容易实现缩放，基于dom不容易缩放
  - [Excalidraw白板调研文档](http://wangxiang.website/docs/work/excalidraw.html)
    - npm 包目前不支持：多人协作、共享链接等，不过 Excalidraw 团队已经在规划当中，不久就会以插件的形式支持。
# popular
- tldraw /5.8kStar/MIT > NonCommercial/202202/ts
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

- excalidraw /15.3kStar/MIT/202101/ts
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


- https://github.com/phedkvist/whiteboard
  - https://whiteboard-umber.vercel.app/
  - a simple whiteboard application.
  - 只依赖react
  - 画板元素都是svg元素

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

- https://github.com/antfu/drauu /MIT/202402/ts
  - https://drauu.netlify.app/
  - Headless SVG-based drawboard in browser.
  - built with Vanilla JavaScript
  - Built for Slidev.

- https://github.com/mohitkumartoshniwal/whiteboard-konva-react /202402/js
  - Code for the Youtube video on building excalidraw clone using React and Konva.js
  - [Excalidraw or Figma Clone using React and Konva - YouTube](https://www.youtube.com/watch?v=LXlE1y5PQsk)
# canvas-drawing
- https://infinitecanvas.tools/gallery/
  - 画板类产品列表
  - The infinite canvas is the foundation of a new class of apps from design tools, to code editors, and workspaces.

- https://github.com/dlemrry/editor /202109/js/inactive
  - real time collaborative documents using web socket
  - Web application for editing texteditor and painting canvas in real-time collaboration.
  - 展示了 quill、draftjs、canvas+mousemove 几个示例
  - 提供了client+server，可作为通用协作方案
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
# typesetting
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

## cn/汉字与排版

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
# latex/printing
- overleaf /10.5kStar/AGPLv3/202211/js/latex/ace>codemirror
  - https://github.com/overleaf/overleaf
  - https://github.com/overleaf/overleaf/wiki
  - https://github.com/overleaf/overleaf/tree/main/services/web/frontend/js/features/source-editor
  - A web-based collaborative LaTeX editor
  - source-editor支持codemirror6、ace
  - https://github.com/overleaf/ace /Ajax.org Cloud9 Editor
  - [Compile Error and PDF Download Notifications](https://github.com/overleaf/overleaf/issues/1031)
    - migrate from ACE to CodeMirror 6. Yes, the CM6 work will be coming to CE soon._202206

  - https://github.com/overleaf/ace
  - https://github.com/amitness/open-in-overleaf
    - Open latex of any arxiv.org paper on overleaf

- https://github.com/fiduswriter/fiduswriter /js/python
  - https://fiduswriter.org/
  - an online collaborative editor especially made for academics who need to use citations and/or formulas.

- https://github.com/michael-brade/LaTeX.js /livescript
  - https://latex.js.org/
  - https://latex.js.org/playground.html
  - a LaTeX to HTML5 translator written in JavaScript using PEG.js. 
  - LaTeX.js tries to be absolutely and uncompromisingly exact and compatible with LaTeX. 
  - If you need a LaTeX to HTML translator that also understands TeX to some extent, take a look at: tex4ht、latex2html

- https://github.com/manuels/texlive.js /inactive
  - http://manuels.github.com/texlive.js/
  - Compiling LaTeX (TeX live) in your browser
  - This is a port of TeX live 2016 to Javascript. It is based on the port of the pdftex TeX compiler to Javascript using emscripten. It creates PDF files from LaTeX code and supports packages.

- https://github.com/SaswatPadhi/pseudocode.js /js
  - https://saswatpadhi.github.io/pseudocode.js
  - a JavaScript library that typesets pseudocode beautifully to HTML.
  - Pseudocode.js takes a LaTeX-style input that supports the algorithmic constructs from LaTeX's algorithm packages
  - The HTML output produced by pseudocode.js is (almost) identical with the pretty algorithms printed on publications that are typeset by LaTeX.
  - pseudocode.js can render math formulas using either KaTeX, or MathJax.

- https://github.com/James-Yu/LaTeX-Workshop
  - an extension for Visual Studio Code, aiming to provide core features for LaTeX typesetting with Visual Studio Code.

## tex-markdown

- https://github.com/susam/texme /js
  - a lightweight JavaScript utility to create self-rendering Markdown + LaTeX documents.

- https://github.com/parpalak/upmath.me
  - Markdown and LaTeX online editor - create text for web with equations and diagrams
# math
- https://github.com/cortex-js/compute-engine /ts
  - https://cortexjs.io/
  - An engine for symbolic manipulation and numeric evaluation of math formulas expressed with MathJSON
  - MathJSON is a lightweight mathematical notation interchange format based on JSON.
  - The Cortex Compute Engine can parse LaTeX to MathJSON, serialize MathJSON to LaTeX, format, simplify and evaluate MathJSON expressions.

- https://github.com/KaTeX/KaTeX /js/NoDeps
  - https://katex.org/
  - Fast math typesetting for the web.
  - KaTeX renders its math synchronously and doesn't need to reflow the page. See how it compares to a competitor in this speed test.
  - KaTeX's **layout** is based on **Donald Knuth's TeX**, the gold standard for math typesetting.
  - support ssr
  - KaTeX supports much (but not all) of LaTeX and many LaTeX packages.

- https://github.com/pyramation/LaTeX2JS /js
  - Author interactive math equations and diagrams online using LaTeX and PSTricks
  - thanks to MathJax
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
