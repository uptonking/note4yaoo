---
title: toc-lib-editor-text-canvas
tags: [canvas, lib, text-editor, toc]
created: 2021-05-19T08:31:35.173Z
modified: 2021-05-19T08:32:28.120Z
---

# toc-lib-editor-text-canvas

# guide

- tips
  - 还可以复用主流业务组件的canvas渲染逻辑，如 echarts-zrender, Fabric, pixi, dropflow, LeaferJS
  - 基于dom的组件比canvas组件对agent更友好

- ref
  - https://www.npmtrends.com/primrose-vs-carota-vs-@creately/carota
# popular
- https://github.com/WaiSiuKei/neditor /MIT/202308/ts/inactive
  - https://waisiukei.github.io/neditor/
  - rich text editor aimed at running in Canvas.
  - 在事件模型和 DOM 模型都准备好之后，移植 ProseMirror 就非常容易了。
  - [从浏览器源码开始实现 Canvas 富文本编辑器 - 知乎 _202307](https://zhuanlan.zhihu.com/p/642703113)

- onlyoffice-sdkjs /190Star/AGPLv3/202302/js
  - https://github.com/ONLYOFFICE/sdkjs
  - https://personal.onlyoffice.com/
  - https://api.onlyoffice.com/docbuilder/spreadsheetapi
  - 💡 word/excel/ppt都基于canvas实现
  - Contains API for all the included components client-side interaction.
  - 通过TypedArray，将表格数据以二进制格式存储，通过字段压缩+共享字符串表来优化内存空间
  - [精读onlyoffice在线表格存储设计](https://juejin.cn/post/7202252704978386999)
  - repos
    - https://github.com/ONLYOFFICE/document-editor-react-samples
      - 示例依赖server api，本地无法运行
    - https://github.com/ONLYOFFICE/document-editor-react
      - 示例依赖server api，本地无法运行

- canvas-editor /72Star/MIT/202211/ts/几乎无依赖
  - https://github.com/Hufe921/canvas-editor
  - https://hufe.club/canvas-editor/
  - rich text editor by canvas/svg
  - The render layer by svg is under development, see feature/svg
  - The export pdf feature is available now, see feature/pdf
  - [一个开源可分页的富文本编辑器_202212](https://zhuanlan.zhihu.com/p/592004147)
  - https://gitee.com/wfeng0/canvas-editor /202402/ts
    - [Canvas-Editor 实现类似 Word 协同编辑 - 掘金 _202401](https://juejin.cn/post/7326979670485925926)
    - 此次的重点是实现协同部分的代码，难免会修改源码部分，实现协同。
    - Yjs 的基本使用中，通过Map设置数据，observe观察器实现数据获取
    - 用户闪烁的光标目前还没有思路实现，后面会攻克技术难点，但是用户选取可以通过API实现

- https://github.com/WindRunnerMax/CanvasEditor /MIT/202603/ts
  - https://windrunnermax.github.io/CanvasEditor/
  - Canvas 简历编辑器
  - 🐛 未实现原位置编辑，需要在弹窗或右侧面板编辑文字

- https://github.com/karpov-kir/canvas-block-editor /ts
  - A block based canvas text editor.

- primrose /506Star/MIT/202011/js
  - https://github.com/capnmidnight/Primrose
  - https://www.primrosevr.com/
  - A source code text editor that renders in an HTML5 canvas. 
  - useful for texturing 3D objects in WebGL apps.
  - Primrose is a syntax highlighting text editor that renders into an HTML5 Canvas element. 
    - This is particularly useful for texturing 3D objects in WebGL apps.
    - Here is a basic example that creates an editor in a 2D web page.
    - Here is a basic example that creates an editor in a 3D WebGL app, using Three.js.
  - While Primrose can manage most input events on its own, in WebGL contexts, it's not able to figure out what the user's pointer is pointing at. 
  - Grammars are collections of RegExps that define rules for performing the necessary tokenization to be able to achieve syntax highlighting. 

- carota /553Star/MIT/201605/js
  - https://github.com/danielearwicker/carota
  - https://earwicker.com/carota/
  - Simple, flexible rich text rendering/editing on HTML Canvas
  - active forks
    - https://github.com/creately/carota

- https://github.com/cfu288/canvas-text-editor
  - https://cfu288.github.io/canvas-text-editor/
  - A proof of concept text editor implemented with HTML5 Canvas
  - Currently this editor uses an array of **Gap Buffer** s to represent and manipulate the file data. 
  - Internal benchmarks show it is more performant than a javascript simple array or another implementation of Gap Buffer using javascript Typed Arrays.

- https://github.com/makepad/makepad /rust
  - https://makepad.dev/
  - Makepad is a creative software development platform for Rust that compiles to wasm/webGL, osx/metal, windows/dx11 linux/opengl
  - This is the repository for Makepad, a new way to build UIs in Rust for both native and the web.
  - DOM-less GPU-based text editor

- https://github.com/R-Neville/canvas-line-editor
  - https://r-neville.github.io/canvas-line-editor/
  - HTML canvas based text editor written in TypeScript
  - Canvas Line Editor is my (ongoing) attempt at creating a plaintext editing interface for an IDE I'm building with Electron.js.

- https://github.com/markusmoenig/richtextjs
  - http://richtextjs.com/
  - /25Star/MIT/201711/js
  - RichTextJS is inspired by (but does not share any code with) Carota.

- https://github.com/cqdlhjpdml/jditor
  - http://www.jditor.com/debug.html
  - this js project is aimed to help myself to draw a similar ms visio graph in web browser canvas. 
  - all symbols are svg vector symbol.

- textor /108Star/MIT/201905/ts
  - https://github.com/lutzroeder/textor
  - https://lutzroeder.github.com/textor
  - Experimental text editor control written in TypeScript using HTML5 canvas.
  - Supports syntax highlighting for JavaScript, HTML and CSS.
# custom-layout
- https://github.com/ritzyed/ritzy /201509/js/inactive
  - Ritzy editor is a rich text, real-time character-by-character collaborative embeddable browser-based editor. 
  - It shuns(避免) use of the `contentEditable` attribute in favor of a custom editor surface and layout engine, exactly like the approach implemented by Google Docs.
  - Ritzy is built with real-time collaborative editing support from the ground up, underlying mechanism for this is a causal tree CRDT.
# canvas-text-editor
- https://github.com/grassator/canvas-text-editor-tutorial
  - Simple text editor using html5 canvas
# canvas-examples
- https://github.com/ahungrynoob/canvas-text
  - https://ahungrynoob.github.io/canvas-text/index.html
  - a simple paragraph editor implemented by canvas.
# canvas-engine
- https://github.com/youtube/cobalt /BSD/202501/cpp
  - https://cobalt.dev/
  - https://developers.google.com/youtube/cobalt
  - Cobalt is a lightweight HTML5/CSS/JS application container that is designed to provide a rich application development environment with minimal resource consumption (deployment size, RAM, CPU, GPU). 
  - 为在极少资源条件下播放视频而设计，支持audio/video标签，不支持img/p，对文本排版支持有限
  - Cobalt is a single-process application and does not rely on the ability to spawn multiple processes.
  - Cobalt is optimized to run on single-core CPUs, resulting in better input latency since the renderer and resource loader do not compete with layout operations.
  - Cobalt produces consistent 60FPS animations by only supporting animation of properties that don't affect layout, like transform, and always running animations on a separate thread.
  - On platforms that support GLES2, Cobalt avoids CPU painting by performing almost all rendering operations on the GPU.
# more
