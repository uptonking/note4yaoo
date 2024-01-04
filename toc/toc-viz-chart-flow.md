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

- resources
  - [diagram-js vs gojs vs jointjs vs jsplumb vs mxgraph | npm trends](https://npmtrends.com/diagram-js-vs-gojs-vs-jointjs-vs-jsplumb-vs-mxgraph)
  - [流程图制作: BPMN流程图在线绘制](https://segmentfault.com/a/1190000019385581)
# flowchart
- mermaid /32.1kStar/MIT/202009/js
  - https://github.com/mermaid-js/mermaid
  - Generation of diagram and flowchart from text in a similar manner as markdown
  - [Poll - next diagram type addition: PlantUML](https://github.com/mermaid-js/mermaid/issues/177)

- maxGraph /500Star/apache2/202305/ts
  - https://github.com/maxGraph/maxGraph
    - https://jgraph.github.io/mxgraph/
  - https://jgraph.github.io/mxgraph/docs/manual.html
  - https://jgraph.github.io/mxgraph/docs/js-api/files/view/mxGraph-js.html
  - https://github.com/gelvidge/maxGraph
  - maxGraph is a fully client side JavaScript diagramming library
  - It provides many of the diagramming features which would be expected by a piece of presentation software like Microsoft® PowerPoint™ or LibreOffice® Impress such as being able to resize, move or rotate nodes, but has a stronger focus on automatic layout algorithms and applications of Graph Theory.
  - [mxgraph 系列【2】：项目结构说明 - 掘金](https://juejin.cn/post/6844904153873924110)
  - [mxgraph 系列【4】：事务管理 - 掘金](https://juejin.cn/post/6844904193094860808)
  - https://github.com/jgraph/mxgraph
    - https://jgraph.github.io/mxgraph/javascript/examples/autolayout.html
    - Development on mxGraph has now stopped, this repo is effectively end of life.
    - We created mxGraph in 2005, we moved onto commercial activity around draw.io
    - mxGraph is pretty much feature complete, production tested in many large enterprises and stable for many years.
    - [mxGraph - Known Issues](https://jgraph.github.io/mxgraph/docs/known-issues.html)

- drawio /36.5kStar/apache2/202310/js
  - https://github.com/jgraph/drawio
  - https://www.drawio.com/
  - draw.io, this project, is a configurable diagramming/whiteboarding visualization application
  - draw.io is not suitable as a framework for building other products from. For this try either Tldraw or Excalidraw.
  - It is not an SVG editing app, the SVG export is designed only for embedding in web pages, not for further editing in other tools.
  - Additional minified JavaScript files and Java libraries are used in this project. All of the licenses are deemed compatible with the Apache 2.0, nothing is GPL or AGPL
  - draw.io is also closed to contributions.

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
  - `const instance = jsPlumb.newInstance({container});` 初始化
  - Toolkit Edition 专属功能
    - undo/redo, Graph Operations, layout, search
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

- diagram-js /1.4kStar/MIT/202305/js
  - https://github.com/bpmn-io/diagram-js
  - A toolbox for displaying and modifying diagrams on the web.
  - [支持Redo/Undo](https://github.com/bpmn-io/diagram-js/issues/9)
  - examples
    - https://github.com/bpmn-io/bpmn-auto-layout
    - https://github.com/bpmn-io/diagram-js-examples

- xyflow/react-flow /18.6kStar/MIT/202311/ts/d3
  - https://github.com/xyflow/xyflow 
  - https://github.com/wbkd/react-flow
  - https://xyflow.com/
  - https://reactflow.dev/
  - https://pro.reactflow.dev/
  - https://reactflow.dev/docs/examples/layout/auto-layout/
    - One using d3-hierarchy and the other one using dagre.js as a layout engine.
  - open source libraries for building node-based UIs with React or Svelte
  - core依赖 react, d3-drag, d3-selection, d3-zoom, zustand
  - library for building interactive node-based UIs, editors, flow charts and diagrams
  - React Flow Pro is not an additional library, it is a paid subscription around the React Flow
  - [is Dynamic auto layouting using dagre possible?](https://github.com/wbkd/react-flow/issues/1113)
    - Dynamic auto layout with dagre is possible. As explained you need to re-layout your graph when you add a node. The easiest way is to have pre-defined dimensions for your nodes. If that's not possible you need to wait for the first render and then do a re-calculation of the layout.

- LogicFlow /4.5kStar/apache2/202305/ts
  - https://github.com/didi/LogicFlow
  - https://docs.logic-flow.cn/examples/#/gallery
  - 专注于业务自定义的流程图编辑框架，支持实现脑图、ER图、UML、工作流等各种图编辑场景
  - core依赖preact、mobx、mousetrap
  - 视图层依赖preact，但使用时不要求react环境，通过instance.render()执行
  - 部分使用class组件
  - 兼容各种产品自定义的流程编辑需求，绝大部分模块以插件的形式实现，支持各模块自由插拔
  - 支持undo/redo
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
# uml
- https://github.com/jgraph/mxgraph
  - /6.1kStar/Apache2/202011/archived
  - mxGraph is a fully client side JavaScript diagramming library that uses SVG and HTML for rendering.
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

- https://github.com/tgdwyer/WebCola /1.9kStar/MIT/202307/ts/NoDeps
  - http://marvl.infotech.monash.edu/webcola/
  - an open-source JavaScript library for arranging your HTML5 documents and diagrams using constraint-based optimization techniques.
  - The core layout is based on a complete rewrite in Javascript of the C++ libcola library.
  - It works well with libraries like D3.js, svg.js, and Cytoscape.js. 
  - Note: While D3 adaptor supports both D3 v3 and D3 v4, WebCoLa's interface is styled like D3 v3.

- https://github.com/jacomyal/sigma.js /ts
  - https://www.sigmajs.org/
  - JavaScript library aimed at visualizing graphs of thousands of nodes and edges
  - Since version v2,  `sigma.js` focuses on the management of graph display: rendering, interaction... 
  - The graph model is managed in a separate library called `graphology`.
  - Sigma.js uses WebGL to render graphs. It is also possible to customize rendering, but it is harder than it would be with SVG or Canvas based solutions.
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

- https://github.com/cytoscape/cytoscape.js /js
  - Cytoscape.js is a fully featured graph theory library. 
  - Cytoscape.js contains a graph theory model and an optional renderer to display interactive graphs. 

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
# more
- https://github.com/aislelabs/react-flowchart-editor
  - http://data.aislelabs.com/demo/index.html
  - A windowed flow chart editor in React
  - 只依赖react
