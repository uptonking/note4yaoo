---
title: toc-viz-chart-flow
tags: [flowchart, toc, viz]
created: 2020-07-13T01:43:34.873Z
modified: 2020-10-22T10:22:55.878Z
---

# toc-viz-chart-flow

# guide

- requirements
  - **auto-layout**
  - undo/redo
  - transaction(like prosemirror/mxgraph)

- usecase
  - 自动化任务

- workflow/automation/pipeline/**rpa**
  - workflow/flowchart progress animation
  - ⚖️ workflow specification: bpmn, MCP, JSON Canvas
    - n8n/activepieces/trigger 对bpmn的讨论度都不高
  - workflow-backend/engine: logicFlow-server
  - 与外部系统通信可考虑使用统一workflow平台, 内部模块间通信优先events/rpc

- tips
  - 🆚️ 技术栈基于svg容易实现缩放，基于dom不容易缩放

- resources
  - [diagram-js vs gojs vs jointjs vs jsplumb vs mxgraph | npm trends](https://npmtrends.com/diagram-js-vs-gojs-vs-jointjs-vs-jsplumb-vs-mxgraph)
  - [流程图制作: BPMN流程图在线绘制](https://segmentfault.com/a/1190000019385581)
# flowchart
- mermaid /83.5kStar/MIT/202510/ts
  - https://github.com/mermaid-js/mermaid
  - https://mermaid.js.org/
  - https://www.mermaidchart.com/
  - https://mermaid.live/
  - Generation of diagram and flowchart from text in a similar manner as markdown
  - [Poll - next diagram type addition: PlantUML](https://github.com/mermaid-js/mermaid/issues/177)
- https://github.com/mermaid-js/mermaid-live-editor /5.8kStar/MIT/202510/ts/svelte
  - https://mermaid-js.github.io/mermaid-live-editor/
  - https://mermaid.live/
  - Edit, preview and share mermaid charts/diagrams. 
  - New implementation of the live editor.
  - 左侧代码，右侧流程图，整体类似markdown编辑器
  - 依赖@mermaid-js/layout-elk、@mermaid-js/mermaid-zenuml、monaco-editor、@codemirror/lang-markdown、svg2roughjs、svg-pan-zoom
  - Edit and preview flowcharts, sequence diagrams, gantt diagrams in real time.
  - Save the result as a svg
  - Get a link to a viewer of the diagram so that you can share it with others.
  - https://github.com/mermaid-js/zenuml-core
    - The ZenUML renderer
    - DSL 解析器和渲染器都在这个代码库中。
    - DSL 解析器是基于 Antlr4 构建的。其定义文件位于src/g4。生成的解析器位于 src/generated-parser。 对解析器的增强相关的代码位于src/parser文件夹。
    - 所有其他的文件基本上都是跟渲染器相关的。渲染器是基于 VueJs 2.x 开发的。

- maxGraph /500Star/apache2/202504/ts
  - https://github.com/maxGraph/maxGraph
    - https://maxgraph.github.io/maxGraph/
    - https://jgraph.github.io/mxgraph/
  - https://jgraph.github.io/mxgraph/docs/manual.html
  - https://jgraph.github.io/mxgraph/docs/js-api/files/view/mxGraph-js.html
  - https://jgraph.github.io/mxgraph/javascript/index.html
  - https://github.com/gelvidge/maxGraph
  - maxGraph is a fully client side JavaScript diagramming library
  - 基于svg实现, [连线支持动画](https://maxgraph.github.io/maxGraph/demo/?path=/story/effects-animation--default)
  - 支持 [auto-layout](https://maxgraph.github.io/maxGraph/demo/?path=/story/layouts-autolayout--default)
  - 支持 [LoD(在缩放时仅显示部分元素)](https://maxgraph.github.io/maxGraph/demo/?path=/story/zoom-offpage-lod--default)
  - 支持dynamic-loading
  - 支持off-page渲染
  - 支持print时设置page-breaks/footer
  - 支持overlay/float元素的宽高设置
  - 支持bpmn
  - It provides many of the diagramming features which would be expected by a piece of presentation software like Microsoft® PowerPoint™ or LibreOffice® Impress such as being able to resize, move or rotate nodes, but has a stronger focus on automatic layout algorithms and applications of Graph Theory.
  - `maxGraph` APIs are not fully compatible with `mxGraph` APIs. The concepts are the same, so experienced mxGraph users should be able to switch from mxGraph to maxGraph without issues.
  - 🐛 未提供开箱即用的app，如编辑形状属性和文本
    - 似乎不支持 pause/resume ?
  - [mxgraph 系列【2】：项目结构说明 - 掘金](https://juejin.cn/post/6844904153873924110)
  - [mxgraph 系列【4】：事务管理 - 掘金](https://juejin.cn/post/6844904193094860808)
  - https://github.com/jgraph/mxgraph
    - https://jgraph.github.io/mxgraph/javascript/examples/autolayout.html
    - Development on mxGraph has now stopped, this repo is effectively end of life.
    - We created mxGraph in 2005, we moved onto commercial activity around draw.io
    - mxGraph is pretty much feature complete, production tested in many large enterprises and stable for many years.
    - [mxGraph - Known Issues](https://jgraph.github.io/mxgraph/docs/known-issues.html)

- drawio /36.5kStar/apache2(NonOpen)/202310/js
  - https://github.com/jgraph/drawio
  - https://www.drawio.com/
  - draw.io, this project, is a configurable diagramming/whiteboarding visualization application
  - draw.io is not suitable as a framework for building other products from. For this try either Tldraw or Excalidraw.
  - 🐛 部分代码未开源，是压缩过的，如mxClient.js
    - The minified code authored by us in this repo is licensed under an Apache v2 license, but the sources to build those files are not in this repo. 
    - This is not an open source project. We do not accept PRs unless one of the maintainers specifically says it's OK (basically never).
  - It is not an SVG editing app, the SVG export is designed only for embedding in web pages, not for further editing in other tools.
  - Additional minified JavaScript files and Java libraries are used in this project. All of the licenses are deemed compatible with the Apache 2.0, nothing is GPL or AGPL
  - draw.io is also closed to contributions.
  - https://github.com/jgraph/drawio-desktop /apache2/202503/js
    - Official electron build of draw.io
    - drawio-desktop is a diagramming desktop app based on Electron that wraps the core draw.io editor.
    - draw.io Desktop is designed to be completely isolated from the Internet, apart from the update process.
    - draw.io is closed to contributions (unless a maintainer permits it, which is extremely rare).
    - If we were to receive a PR, we'd have to basically throw it away and write it how we want it to be implemented.

- https://github.com/nicoespeon/gitgraph.js /2.9kStar/MIT/202209/ts/inactive
  - https://www.nicoespeon.com/gitgraph.js
  - https://www.nicoespeon.com/gitgraph.js/stories/
  - A JavaScript library to draw pretty git graphs in the browser
  - core无依赖，支持vanillajs、React
  - @gitgraph/core contains the main logic for manipulating git-like API and compute the graph that should be rendered.

- jsplumb /7.3kStar/MIT/202302/ts/NoDeps
  - https://github.com/jsplumb/jsplumb
  - https://jsplumbtoolkit.com/
  - https://jsplumbtoolkit.com/features
  - Visual connectivity for webapps
  - 基于dom实现
  - dev/4.x branch is a rewrite in Typescript
  - In 5.x, the undo/redo functionality was pulled into the Toolkit core
  - Toolkit Edition 专属功能
    - undo/redo, Graph Operations, layout, search
  - `const instance = jsPlumb.newInstance({container});` 初始化
  - [automatic layout](https://github.com/jsplumb/jsPlumb/issues/205)
    - available in paid edition
    - [jsPlumb Community Edition with Dagre layout](https://codepen.io/viswesh/pen/ejrLPx)
    - [dg-jsplumb.js](https://gist.github.com/michiel/2e632cd50c435594cc44)
    - [Pan and Zoom in jsPlumb Community Edition with Dagre and jQueryUI Draggable](https://gist.github.com/archetana/b11d1a3712c2761f2c45cafd2bcb9b50)
  - [Is that possible to undo dragging and revert it to original position in some condition?](https://github.com/jsplumb/jsplumb/issues/628)
    - in pro
    - the short answer is you'd have to do this manually right now. but a "can drop in group" callback is something we could think about adding if you were interested.
  - https://twitter.com/jsplumblib/status/1716839513903776034
    - 3 reasons to choose jsPlumb over Jointjs
    1. jsPlumb is not limited to SVG but JointJS is
    2. jsPlumb integrates with Angular, React, Vue (2/3) and Svelte
    3. jsPlumb has no external dependencies. JointJS has 3. And more if you want touch events.
  - [前端可视化建模技术概览](https://leungwensen.github.io/blog/2015/frontend-visual-modeling.html)
  - examples
    - https://github.com/jsplumb-toolkit-demonstrations/flowchart-builder
    - https://github.com/jsplumb-toolkit-demonstrations/react-database-visualizer
- https://gitee.com/openEA/FlowDesigner
  - FlowDesigner来源于Linkey BPM中的流程设计器，作用于流程运行过程中的图形描述

- https://github.com/eclipse-sprotty/sprotty /EPLv2/202501/ts/svg
  - https://sprotty.org/
  - A diagramming framework for the web
  - This is the client part of Sprotty, a next-generation, open-source diagramming framework built with web technologies.
  - Fast, scalable SVG rendering that is compatible with all modern browsers and stylable with CSS
  - Animations built into the core
  - Support for a distributed runtime with client and server
  - Fast, reactive client architecture implemented in TypeScript
  - Java or Node.js based server architecture
  - Configuration via dependency injection
  - Integrations with Xtext, Langium, the Language Server Protocol, VS Code and Theia
  - Can be run as rich-client as well as in the browser
  - sprotty (this repository) contains the client code (sprotty), shared code for Node.js servers (sprotty-protocol), ELK layout integration (sprotty-elk) and examples.
  - https://github.com/eclipse-sprotty/sprotty-server /EPL/202411/java
    - Server implementation for the Sprotty diagramming framework
    - contains server code for Java and includes server-side diagram layout, the extension of the Language Server Protocol, and the integration with the Xtext framework

- diagram-js /1.4kStar/MIT/202501/js
  - https://github.com/bpmn-io/diagram-js
  - A toolbox for displaying and modifying diagrams on the web.
  - [支持Redo/Undo](https://github.com/bpmn-io/diagram-js/issues/9)
  - examples
    - https://github.com/bpmn-io/bpmn-auto-layout
    - https://github.com/bpmn-io/diagram-js-examples

- xyflow/react-flow /18.6kStar/MIT/202410/ts/d3
  - https://github.com/xyflow/xyflow 
  - https://github.com/wbkd/react-flow
  - https://xyflow.com/
  - https://reactflow.dev/
  - https://pro.reactflow.dev/
  - https://reactflow.dev/docs/examples/layout/auto-layout/
    - One using d3-hierarchy and the other one using dagre.js as a layout engine.
  - open source libraries for building node-based UIs with React or Svelte
  - core只依赖3个: d3-drag, d3-selection, d3-zoom
  - react依赖zustand，postcss
  - library for building interactive node-based UIs, editors, flow charts and diagrams
  - React Flow Pro is not an additional library, it is a paid subscription around the React Flow
  - 🐛 似乎不支持 pause/resume ?
  - [Undo and redo operations _202211](https://github.com/xyflow/xyflow/issues/656)
    - This is basically how I did it
  - [is Dynamic auto layouting using dagre possible?](https://github.com/wbkd/react-flow/issues/1113)
    - Dynamic auto layout with dagre is possible. As explained you need to re-layout your graph when you add a node. The easiest way is to have pre-defined dimensions for your nodes. If that's not possible you need to wait for the first render and then do a re-calculation of the layout.

- LogicFlow /4.5kStar/apache2/202404/ts
  - https://github.com/didi/LogicFlow
  - https://docs.logic-flow.cn/examples/#/gallery
  - http://logic-flow.org/examples/
  - 专注于业务自定义的流程图编辑框架，支持实现脑图、ER图、UML、工作流等各种图编辑场景
  - core依赖preact、mousetrap, mobx-react似乎是可选依赖
  - engine是一个可以在JavaScript环境执行的流程引擎
  - 视图层依赖preact，但使用时不要求react环境，通过instance.render()执行
  - 部分使用class组件
  - 🔌 兼容各种产品自定义的流程编辑需求，绝大部分模块以插件的形式实现，支持各模块自由插拔
  - 本地开发时，使用node.v16
  - 支持minimap
  - ⌛️ 支持undo/redo
  - 支持pause/resume
    - [feat(engine): add the ability to pause and resume workflows _202307](https://github.com/didi/LogicFlow/commit/7c4e3855ad0a7af4121de6552be61f690b4e0e6c)
  - https://github.com/didi/Turbo /apache2/202412/java
    - 一款Java实现的轻量级流程引擎，是公司内多个低代码平台的核心后端服务。
    - 提供“定义流程，并根据流程定义，执行流程”的核心能力
    - 支持流程回滚操作
    - 依赖spring-boot、MySQL
    - Turbo的定位是兼容BPMN2.0的轻量级流程引擎（而非平台），支持可重入交互，主要负责提供稳定而高效的核心能力：流程定义、流程驱动，而节点的具体执行由接入方实现
    - 当前市面上大部分是Activiti、Flowable、Camunda等面向OA场景，功能强大且有比较完整的生态的工作流引擎（平台），同时因为OA复杂的场景，库表关联操作非常多，但是对于其它业务场景，引擎运维以及学习成本较高，性能不可避免有一定损失，不适用于C端场景
    - 还有部分专注于纯内存执行、无状态的流程引擎，比如阿里的Compileflow，这类引擎中断后不可重入，不适用于人机交互场景，适用于执行业务规则
    - [turbo test _202308](https://github.com/didi/LogicFlow/discussions/1320)
  - [LogicFlow案例分享](https://github.com/didi/LogicFlow/issues/716)
  - [perf: 优化layout](https://github.com/didi/LogicFlow/pull/518)
    - 自动布局这个功能后来发现有很多不足，所以放弃了，我先合并进来，但是这个插件暂时不提供对外文档。
    - 也欢迎您参考或者直接使用d3/d3-hierarchy，对logicflow的自动布局进行优化。
  - [希望能支持优化布局排版的功能，类似自动布局的能力_202212](https://github.com/didi/LogicFlow/issues/946)
    - 目前我们并没有找到完美的布局方案
- https://github.com/hsole/layoutFlow
  - https://hsole.github.io/layoutFlow/
  - 脑图和自动布局一键美化
  - 自动布局的不足：首先能用的业务场景有限，一般用于树型结构（如脑图）或者布局有规律的场景。
  - 树布局直接使用了https://github.com/antvis/hierarchy 
  - 流程图会存在环这种结构。这个时候直接用树布局是不合适的，所以我们使用dagre布局。发现https://github.com/antvis/layout提供的dagre布局最好用（G6里面的dagre布局也是用的这个）
  - **一键美化的实现思路和自动布局类似，都是把LogicFlow中的图数据传给布局库，然后再把得到的新的图数据重新使用LogicFlow渲染**
  - 由于一键美化这种纯系统布局的不够人性化，我们增加了一种半系统半人工的布局方式，也就是选区美化。
  - [流程图布局在项目中的实践 - 掘金](https://juejin.cn/post/7145653979119091720)
- https://github.com/towersxu/draft-flow
  - 基于LogicFlow和rough.js实现的手绘风格流程图

- https://github.com/bytedance/flowgram.ai /MIT/202505/ts/功能全面
  - https://flowgram.ai/
  - https://flowgram.ai/examples/playground.html
  - a node-based flow building engine that helps developers quickly create workflows in either fixed layout or free connection layout modes.
  - 基于dom实现的节点图方案
  - 支持plugin、物料
  - core依赖inversify、@phosphor/messaging、@@tweenjs/tween.js、reflect-metadata
  - runtime支持js/nodejs, 其中nodejs依赖@fastify/websocket、@trpc/server
  - Fixed layout: where nodes can be dragged to specified positions, with support for compound nodes like branches and loops.
  - Free layout: where nodes can be placed anywhere and connected using free-form lines.
  - Motion 动画在 Web 端应用可追溯到 Material Design，里边提到元素的变化如宽高或位置需要一个过渡过程，画布引擎会把线条和节点拆分单独绘制，使实现 Motion 过渡动画成本大大降低
  - 💫 https://flowgram.ai/en/examples/fixed-layout/fixed-feature-overview.html
    - 提供了执行进度的示例动画
  - 线上应用: 扣子工作流、飞书多维表格工作流、飞书低代码平台工作流
  - 官方物料目前底层基于 Semi Design 实现，业务如果有底层组件库的诉求，可以通过 CLI 复制源码进行替换

- https://github.com/alibaba/butterfly /js
  - 基于JS的数据驱动的节点式编排组件库
  - 利用DOM/REACT/VUE来定制元素；灵活性，可塑性，拓展性优秀
  - 依赖jquery、lodash、antv/hierarchy、d3-force、dagre、ml-matrix、dom-to-image
  - 在issues里面反馈的bugs超多

- kroki /1.1kStar/MIT/202109
  - https://github.com/yuzutech/kroki
  - https://kroki.io/
  - Convert plain text diagrams to images !
  - it takes a text diagram as input and returns an image.
  - Kroki provides a unified HTTP API with support for BlockDiag (BlockDiag, SeqDiag, ActDiag, NwDiag, PacketDiag, RackDiag), BPMN, Bytefield, C4 (with PlantUML), Ditaa, Erd, Excalidraw, GraphViz, Mermaid, Nomnoml, Pikchr, PlantUML, SvgBob, UMLet, Vega, Vega-Lite and WaveDrom…​ and more to come!

- react-flow-chart /MIT/719Star/202006
  - https://github.com/MrBlenny/react-flow-chart
  - https://mrblenny.github.io/react-flow-chart/index.html
  - A flexible, stateless, declarative flow chart library for react
  - 依赖react-draggable、react-zoom-pan-pinch
  - [Automatic layout](https://github.com/MrBlenny/react-flow-chart/issues/61)

- joint /3.9kStar/MPL/202305/js/svg-only
  - https://github.com/clientIO/joint
  - http://www.jointjs.com/
  - SVG-based JavaScript diagramming library powering exceptional UIs

- G6 /7kStar/MIT/202009
  - https://github.com/antvis/g6
  - https://g6.antv.vision/
  - a graph visualization engine
  - 依赖d3-force、darge有向图、ml-matrix矩阵计算、各种工具@antv/g-base
- GGEditor /MIT/2.5kStar/202007
  - https://github.com/alibaba/GGEditor
  - https://ggeditor.com/
  - A visual graph editor based on G6 and React
- graphin /368Star/MIT/202009
  - https://github.com/antvis/graphin
  - https://graphin.antv.vision/
  - A React toolkit for graph analysis based on G6
- X6 /288Star/MIT/202009
  - https://github.com/antvis/X6
  - JavaScript diagramming library
  - core无依赖
  - [前端图可视化引擎antv的g6和x6区别是什么，如何选择？ - 知乎](https://www.zhihu.com/question/435855401)
    - 如果你想做一个像 draw.io 那样的图编辑器，特别是流程图编辑，用 X6。
    - 如果你想做一个像 gephi、keylines 的几个应用那样的分析场景，用 G6。
- wfd-g6 /519Star/MIT/202006
  - https://github.com/guozhaolong/wfd
  - https://guozhaolong.github.io/wfd/
  - flowable workflow designer base on @antv/g6, react

- XChart /1kStar/Apache2/202009/java
  - https://github.com/knowm/XChart
  - XChart is a Java library for plotting data
- imove /943Star/MIT/202101/ts
  - https://github.com/imgcook/imove
  - https://www.yuque.com/imove/docs/hvu0md
  - iMove 是一个逻辑可复用的，面向函数的，流程可视化的 JavaScript 工具库。
  - 感谢 蚂蚁 X6 团队 提供的绘图引擎
- https://github.com/egoist/flowkit
  - https://flowkit.vercel.app/
  - /45Star/NALic/202104/ts
  - 依赖react-flow-renderer, preact, tailwindcss
  - A simple online flow chart editor.
- react-diagrams /MIT/3kStar/201908/ts/canvas
  - https://github.com/projectstorm/react-diagrams
  - http://projectstorm.cloud/react-diagrams
  - diagramming library written in react

- https://github.com/emilwidlund/nodl
  - framework for visual node graphs. 
  - It has a core library & a React-library as of now, runs on MobX and leverages the power of RxJS & Zod for computational magic. 

- https://github.com/alyssaxuu/flowy
  - The minimal javascript library to create flowcharts

- https://github.com/plantain-00/composable-editor-canvas
  - https://plantain-00.github.io/composable-editor-canvas/
  - A composable editor canvas library.
  - 基于svg实现的图形编辑器
  - 提供了多种编辑场景示例
  - 实现了多种react-render-target: canvas, svg, webgl

- https://gitee.com/wfeng0/svg-flow-editor-mvp /apache2/202402/ts
  - 一款自研流程图编辑器，提供了一系列流程图交互、编辑所必需的功能，计划支持前端研发自定义开发各种逻辑编排场景，如流程图、ER 图、BPMN 流程等
  - 项目使用typescript与svg、canvas等技术进行搭建，脱离vue、react等框架的限制
  - 底层依赖了svg对项目元件库的基础元件进行创作，同时使用了canvas对背景网格、水印等进行绘制，使用html进行页面布局
# mindmap
- https://github.com/wanglin2/mind-map /MIT/202405/js/vue/NoDeps
  - https://wanglin2.github.io/mind-map/#/index
  - 一个简单&强大的 Web 思维导图
  - 一个 js 思维导图库，不依赖任何框架
  - 基于思维导图库、Vue2.x、ElementUI 开发，可以操作电脑本地文件，可以当做一个在线版思维导图应用使用，也可以自部署和二次开发。
  - 也提供了客户端可供下载使用，支持Windows、Mac及Linux
  - [我开源了一个思维导图 - 掘金 _202307](https://juejin.cn/post/7257922419319406648)
# bpmn
- https://github.com/paed01/bpmn-engine /MIT/202410/js
  - BPMN 2.0 execution engine. Open source javascript workflow engine.
  - The engine only support elements and attributes included in the BPMN 2.0 scheme, but can be extended to understand other schemas and elements.
  - The aim is to, at least, have BPMN 2.0 core support.
  - The bpmn-engine resides upon the excellent library bpmn-io/bpmn-moddle developed by bpmn.io
# uml
- https://github.com/jgraph/mxgraph /6.1kStar/Apache2/202011/archived
  - mxGraph is a fully client side JavaScript diagramming library that uses SVG and HTML for rendering.
  - 基于svg实现
  - [Future of types after mxgraph EOL announcement](https://github.com/typed-mxgraph/typed-mxgraph/issues/12)

- https://github.com/hikerpig/pintora /MIT/ts
  - An extensible text-to-diagrams library that works in both browser and node.js
  - Heavily inspired by Mermaid.js and PlantUML.
# node-graph
- https://github.com/awslabs/diagram-maker /apache2/202304/ts/NoDeps/archived
  - https://awslabs.github.io/diagram-maker
  - https://awslabs.github.io/diagram-maker/explore/demos.html
  - framework-agnostic
  - 基于svg实现，没有canvas
  - 提供了layout、circular、theming等多种示例
  - A library to display an interactive editor for any graph-like data.
  - 可选依赖dagre
- https://github.com/reaviz/reaflow /202311/ts
  - Node-based Visualizations for React
  - REAFLOW is a modular diagram engine for build static or interactive editors. 
  - 依赖d3-shape、elkjs、kld-affine、framer-motion、rdk、undoo
  - [Huge bundle size](https://github.com/reaviz/reaflow/issues/224)
    - ELK.js is the core layout library - i will investigate if there is a better way to bundle it
    - Ya, ELK is not fun to work with either but it has the best layout engine that I've found.

- https://github.com/dagrejs/dagre /201801/js/deprecated
  - Directed graph layout for JavaScript
  - This project does not have a maintainer or active project members

- https://github.com/jagenjo/litegraph.js /7.5kStar/MIT/202401/js/NoDeps/inactive
  - https://tamats.com/projects/litegraph/editor
  - A library in Javascript to create graphs in the browser similar to Unreal Blueprints. 
  - A graph node engine and editor written in Javascript similar to PD or UDK Blueprints, comes with its own editor in HTML5 Canvas2D. 
  - Nodes can be programmed easily and it includes an editor to construct and tests the graphs.
  - The engine can run client side or server side using Node. It allows to export graphs as JSONs to be included in applications independently.
  - Renders on Canvas2D (zoom in/out and panning, easy to render complex interfaces, can be used inside a WebGLTexture)
  - Optimized to support hundreds of nodes per graph (on editor but also on execution)
  - Subgraphs (nodes that contain graphs themselves)
  - Live mode system (hides the graph but calls nodes to render whatever they want, useful to create UIs)
  - Highly customizable nodes (color, shape, slots vertical or horizontal, widgets, custom rendering)
  - Easy to integrate in any JS application (one single file, no dependencies)
  - https://github.com/Comfy-Org/litegraph.js /233Star/MIT/202508/ts
    - https://github.com/Comfy-Org/ComfyUI_frontend/tree/main/src/lib/litegraph /MIT
    - As of August 5, 2025, Comfy-Org/litegraph.js is now part of the ComfyUI Frontend monorepo
    - This is the litegraph version used in ComfyUI_frontend.
    - It is a fork of the original litegraph.js. Some APIs may be unchanged, however it is largely incompatible with the original.
    - Sort node based on ID on graph serialization

- https://github.com/tgdwyer/WebCola /1.9kStar/MIT/202307/ts/NoDeps
  - http://marvl.infotech.monash.edu/webcola/
  - an open-source JavaScript library for arranging your HTML5 documents and diagrams using constraint-based optimization techniques.
  - The core layout is based on a complete rewrite in Javascript of the C++ libcola library.
  - It works well with libraries like D3.js, svg.js, and Cytoscape.js. 
  - Note: While D3 adaptor supports both D3 v3 and D3 v4, WebCoLa's interface is styled like D3 v3.

- https://github.com/jacomyal/sigma.js /ts/WebGL
  - https://www.sigmajs.org/
  - JavaScript library aimed at visualizing graphs of thousands of nodes and edges
  - Since version v2,  `sigma.js` focuses on the management of graph display: rendering, interaction... 
  - The graph model is managed in a separate library called `graphology`.
  - Sigma.js uses WebGL to render graphs. It is also possible to customize rendering, but it is harder than it would be with SVG or Canvas based solutions.

- https://github.com/emilwidlund/nodl
  - A framework for computational node graphs.
  - https://x.com/emilwidlund/status/1900181498135011398
    - In 2022, I created Alma — An interactive playground for generative graphics, by combining nodes & logic into WebGL shaders. All through an intuitive no-code interface.
    - what the flow diagram library you used?
      - I made it myself

- https://github.com/inngest/workflow-kit /apache2/202504/ts
  - The quickest and easiest way to add a Zapier-like workflow UI experience to your product. 
  - Define actions in your backend and expose a Workflow UI using pre-built React components.
  - Workflow Kit enables you to build user-defined workflows with Inngest by providing a set of workflow actions to the Workflow Engine while using the pre-built React components to build your Workflow Editor UI.
# dataflow
- jerosoler/Drawflow /3.2kStar/MIT/202206/js/inactive
  - https://github.com/jerosoler/Drawflow
  - https://jerosoler.github.io/Drawflow/
  - Drawflow allows you to create data flows easily and quickly.
  - Data sync on Nodes
  - Vanilla javascript (No dependencies)
  - [A simple example showing execution of the flow created using drawflow](https://github.com/jerosoler/Drawflow/issues/543)

- https://github.com/fibo/flow-view
  - a visual editor for Dataflow programming
  - Nodes and edges can be created via API
# auto-layout
- https://github.com/kieler/elkjs /js
  - ELK's layout algorithms for JavaScript
  - The Eclipse Layout Kernel (ELK) implements an infrastructure to connect diagram editors or viewers to automatic layout algorithms. 
  - This library takes the layout-relevant part of ELK and makes it available to the JavaScript 
  - Note that elkjs is not a diagramming framework itself - it computes positions for the elements of a diagram.
  - elkjs is the successor of klayjs.
  - https://github.com/kieler/elk-live
    - A web page with a text editor for ELK Graph and a synchronized graphical view.
  - https://github.com/kieler/klayjs
    - a layer-based layout algorithm that is particularly suited for node-link diagrams with an inherent direction and ports (explicit attachment points on a node's border)  

- https://github.com/iVis-at-Bilkent/cytoscape.js-fcose
  - a faster version of our earlier compound spring embedder algorithm named CoSE, implemented as a Cytoscape.js extension

- https://github.com/cytoscape/cytoscape.js /MIT/202401/js
  - https://js.cytoscape.org/demos/tokyo-railways/
  - a fully featured graph theory library. 
  - Cytoscape.js contains a graph theory model and an optional renderer to display interactive graphs. 
  - Created at the University of Toronto and published in Oxford Bioinformatics (2016, 2023).

- https://github.com/mapbox/potpack /js
  - https://mapbox.github.io/potpack/
  - fast JavaScript library for packing boxes of varying size into a near-square container, which is useful for generating CSS sprites and WebGL textures.
  - Similar to shelf-pack, but static (you can't add items once a layout is generated), and aims for maximal space utilization.
# math/statistics
- https://github.com/jsxgraph/jsxgraph /994Star/LGPLv3/202310/js
  - https://jsxgraph.org/wp/about/index.html
  - a cross-browser library for interactive geometry, function plotting, charting, and data visualization in a web browser.
  - Dynamic Mathematics with JavaScript

- https://github.com/jcoglan/sylvester /201302/js
  - http://sylvester.jcoglan.com/
  - a vector, matrix and geometry library for JavaScript, that runs in the browser and on the server side

- https://github.com/eurostat/gridviz /EUPL/202311/js
  - https://eurostat.github.io/gridviz/
  - a JavaScript library to visualise gridded data (or any tabular dataset with x/y position) in the browser in a large variety of advanced cartographic styles
  - a JavaScript library to visualise gridded data (or any tabular dataset with x/y position) in the browser in a large variety of advanced cartographic styles
# flow-ai
- https://github.com/yunshenwuchuxun/smart-drawio-next /MIT/202511/js
  - https://smart-drawio-next.vercel.app/
  - 用自然语言生成专业 Draw.io 图表
  - [分享一个AI科研绘图神器 ](https://linux.do/t/topic/1171836)

- https://github.com/liujuntao123/smart-excalidraw-next /202511/js
  - https://smart-excalidraw-next.vercel.app/
  - [新的excalidraw画图神器来了 ](https://linux.do/t/topic/1119379)
    - 之前开发了一个 smart-mermaid，可以轻松的通过自然语言进行 mermaid 和 excalidraw 的绘制，获得了很多人的认可。
    - 经过一段时间的使用和用户反馈，依然存在了一些问题： 
      - 由于 mermaid 本身的限制，生成的图表类型受限，图表的灵活性也不够高; 
      - mermaid 转化为 excalidraw 后，经常出现一些莫名其妙的箭头折向问题，美观性实在堪忧
    - 出于灵活性和美观性这两方面的原因，诞生了一个新的项目：smart-excalidraw。
    - 采用了独创的箭头连接算法，能够很好的修正 AI 绘制过程中出现的箭头乱飘的现象。
    - 除了箭头连接算法和提示词是我自己研究出来的外。 其他的功能均为 vibe-coding 所得，难免会有 bug

- https://github.com/Tiledesk/tiledesk-dashboard /MIT/202406/ts
  - https://www.tiledesk.com/
  - full-stack Open Source Live Chat with built-in Chatbots, written in Node.js and Angular.
  - This repository is dedicated to the WebApp dashboard to manage Tiledesk

- https://github.com/receptron/graphai /MIT/202410/ts
  - GraphAI is an asynchronous data flow execution engine, which allows developers to build agentic applications by describing agent workflows as declarative data flow graphs in YAML or JSON.
  - agentic applications require making multiple asynchronous API calls (e.g., OpenAI's chat-completion API, database queries, web searches) and managing data dependencies among them
  - GraphAI allows developers to describe dependencies among those agents (asynchronous API calls) in a data flow graph in YAML or JSON, which is called declarative data flow programming
# task-scheduler
- https://github.com/openworkflowdev/openworkflow /apache2/202511/ts
  - https://openworkflow.dev/
  - a TypeScript framework for building durable, resumable workflows that can pause for seconds or months, survive crashes and deploys
  - Workflows are durable functions. They can contain multiple steps, make external API calls, query databases, and perform complex logic
  - Steps are the building blocks of workflows. Each step is executed exactly once and its result is memoized. 
  - Workers are long-running processes that poll your database for pending workflows and execute them. You can run multiple workers for high availability and scale.

- https://github.com/hatchet-dev/hatchet /6.1kStar/MIT/202510/go
  - https://hatchet.run/
  - Hatchet is a platform for running background tasks, built on top of Postgres. 
  - Instead of managing your own task queue or pub/sub system, you can use Hatchet to distribute your functions between a set of workers with minimal configuration or infrastructure.
  - Hatchet is a full-featured background task management platform, with built-in support for chaining complex tasks together into workflows, alerting on failures, making tasks more durable, and viewing tasks in a real-time web dashboard.
  - Hatchet is built on a durable task queue that enqueues your tasks and sends them to your workers at a rate that your workers can handle.
  - 依赖sqlc、cobra、viper、tink-go、otel
  - [Migrating to sqlc for better performance _202411](https://github.com/hatchet-dev/hatchet/blob/main/frontend/docs/pages/blog/migrating-off-prisma.mdx)
    - we're removing Prisma entirely from Hatchet's codebase in favor of sqlc.
  - [refactor: separate api and engine repositories, change ticker logic _202403](https://github.com/hatchet-dev/hatchet/pull/281)
    - This refactor removes the dependency on the Prisma ORM for the engine
    - We did this for a number of reasons - to reduce query load on the database and have more control over query latency, and because connections pools were unpredictable and spiking with Prisma.
    - We will still be modeling all database changes via the Prisma DSL, and running migrations through Prisma.

- https://github.com/riverqueue/river /4.5kStar/MPL/202510/go
  - https://riverqueue.com/
  - River is a robust high-performance job processing system for Go and Postgres.
  - Being built for Postgres, River encourages the use of the same database for application data and job queue.
  - River was in large part inspired by our experiences with other background job libraries over the years, most notably: Oban in Elixir; Que, Sidekiq, Delayed:: Job, and GoodJob in Ruby; Hangfire in . NET.
  - db操作似乎使用sqlc
  - [Gorm integration _202311](https://github.com/riverqueue/river/issues/58)
    - River now has a database/sql driver. Here’s the doc on using that with GORM: riverqueue.com/docs/gorm
# more
- https://github.com/aislelabs/react-flowchart-editor
  - http://data.aislelabs.com/demo/index.html
  - A windowed flow chart editor in React
  - 只依赖react

- [flowith - Node-Based GPT-4o and Claude-3 Opus Driven AI Productivity Tool](https://flowith.io/)
