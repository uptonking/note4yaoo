---
title: toc-viz-chart-flow
tags: [flowchart, toc, viz]
created: 2020-07-13T01:43:34.873Z
modified: 2020-10-22T10:22:55.878Z
---

# toc-viz-chart-flow

# guide

- usecase
  - 自动化任务
# flowchart
- mermaid /32.1kStar/MIT/202009/js
  - https://github.com/mermaid-js/mermaid
  - Generation of diagram and flowchart from text in a similar manner as markdown
  - [Poll - next diagram type addition: PlantUML](https://github.com/mermaid-js/mermaid/issues/177)

- jsplumb /7.3kStar/MIT/202302/ts
  - https://github.com/jsplumb/jsplumb
  - https://jsplumbtoolkit.com/
  - https://jsplumbtoolkit.com/features
  - Visual connectivity for webapps
  - dev/4.x branch is a rewrite in Typescript
  - 基于dom实现
  - [automatic layout](https://github.com/jsplumb/jsPlumb/issues/205)
    - available in paid edition

- react-flow /2.8kStar/MIT/202103/ts
  - https://github.com/wbkd/react-flow
  - https://reactflow.dev/
  - https://pro.reactflow.dev/
  - https://reactflow.dev/docs/examples/layout/auto-layout/
    - One using d3-hierarchy and the other one using dagre.js as a layout engine.
  - core依赖 react, d3-drag, d3-selection, d3-zoom, zustand
  - library for building interactive node-based UIs, editors, flow charts and diagrams
  - React Flow Pro is not an additional library, it is a paid subscription around the React Flow

- LogicFlow /4.5kStar/apache2/202305/ts
  - https://github.com/didi/LogicFlow
  - https://docs.logic-flow.cn/examples/#/gallery
  - 专注于业务自定义的流程图编辑框架，支持实现脑图、ER图、UML、工作流等各种图编辑场景
  - core依赖preact、mousetrap
  - 视图层依赖preact，但使用时不要求react环境，通过instance.render()执行
  - 兼容各种产品自定义的流程编辑需求，绝大部分模块以插件的形式实现，支持各模块自由插拔
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

- joint /3.9kStar/MPL/202305/js
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
# uml
- https://github.com/jgraph/mxgraph
  - /6.1kStar/Apache2/202011/archived
  - mxGraph is a fully client side JavaScript diagramming library that uses SVG and HTML for rendering.
  - [Future of types after mxgraph EOL announcement](https://github.com/typed-mxgraph/typed-mxgraph/issues/12)
# node-graph
- https://github.com/awslabs/diagram-maker
  - https://awslabs.github.io/diagram-maker
  - https://awslabs.github.io/diagram-maker/explore/demos.html
  - framework-agnostic
  - 基于svg实现，没有canvas
  - 提供了layout、circular、theming等多种示例
  - A library to display an interactive editor for any graph-like data.
- https://github.com/reaviz/reaflow
  - Node-based Visualizations for React
  - REAFLOW is a modular diagram engine for build static or interactive editors. 

- https://github.com/dagrejs/dagre /201801/js/deprecated
  - Directed graph layout for JavaScript
  - This project does not have a maintainer or active project members
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
# more
- https://github.com/aislelabs/react-flowchart-editor
  - http://data.aislelabs.com/demo/index.html
  - A windowed flow chart editor in React
  - 只依赖react
