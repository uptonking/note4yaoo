---
title: lib-viz-flowchart-mxgraph-examples
tags: [examples, mxgraph]
created: 2023-05-29T17:33:23.012Z
modified: 2023-05-29T17:33:33.600Z
---

# lib-viz-flowchart-mxgraph-examples

# guide

- examples
  - 还可以在相关issues的引用issues里面找示例
  - [Level of detail(LOD) example for mxGraph](https://jgraph.github.io/mxgraph/javascript/examples/lod.html)
  - [mxgraph入门解析 - 入门示例分析](https://gcgligoudan.github.io/mxgraph/)
# popular
- maxGraph /500Star/apache2/202305/ts
  - https://github.com/maxGraph/maxGraph
    - https://jgraph.github.io/mxgraph/
  - https://jgraph.github.io/mxgraph/docs/manual.html
  - https://jgraph.github.io/mxgraph/docs/js-api/files/view/mxGraph-js.html
  - https://github.com/gelvidge/maxGraph
  - maxGraph is a fully client side JavaScript diagramming library
  - 图形默认渲染为svg
  - It provides many of the diagramming features which would be expected by a piece of presentation software like Microsoft® PowerPoint™ or LibreOffice® Impress such as being able to resize, move or rotate nodes, but has a stronger focus on automatic layout algorithms and applications of Graph Theory.
  - [mxgraph 系列【2】：项目结构说明 - 掘金](https://juejin.cn/post/6844904153873924110)
  - [mxgraph 系列【4】：事务管理 - 掘金](https://juejin.cn/post/6844904193094860808)
- https://github.com/jgraph/mxgraph /202011/js/archived
  - https://jgraph.github.io/mxgraph/javascript/examples/autolayout.html
  - Development on mxGraph has now stopped, this repo is effectively end of life.
  - We created mxGraph in 2005, we moved onto commercial activity around draw.io
  - mxGraph is pretty much feature complete, production tested in many large enterprises and stable for many years.
  - [mxGraph - Known Issues](https://jgraph.github.io/mxgraph/docs/known-issues.html)

- https://github.com/process-analytics/bpmn-visualization-js /245Star/apache2/202503/ts
  - https://process-analytics.github.io/bpmn-visualization-js/
  - a TypeScript library for visualizing process execution data on BPMN diagrams
  - 依赖mxgraph4、fast-xml-parser，依赖很少
  - True opensource license without watermark display
  - Highly customizable rendering in a simple way
  - Strong identity: the only BPMN viewer with a woman icon in the User Tasks
  - [[INFRA] Evaluate the Replacement of `mxGraph` with `maxGraph` _202501](https://github.com/process-analytics/bpmn-visualization-js/issues/3238)
    - maxGraph, as a fork of mxGraph, retains feature parity (including similar extension points) with its predecessor.
    - Tests are added progressively to maxGraph. On 2025-02-04, there were 143 tests covering 29.21% ( 7109/24334 ) of statements
    - maxGraph appears to have limited adoption, and there are no active maintainers outside of the Process-Analytics project and Bonitasoft.
  - [[INFRA] Evaluate the Replacement of `mxGraph` with `JointJS` _202504](https://github.com/process-analytics/bpmn-visualization-js/issues/3315)
    - jointjs has been rejected. because some key features are missing, especially zooming and keyboard interaction, which are critical for bpmn-visualization.
  - [[INFRA] Evaluate the Replacement of `mxGraph` with a New Library _202501](https://github.com/process-analytics/bpmn-visualization-js/issues/3237)
    - Libraries often include editing features that are unnecessary for bpmn-visualization; these features should be easily removable.
    - mxGraph library is not tree-shakable, but maxgraph is tree-shakable

- https://github.com/WindrunnerMax/FlowChartEditor
  - https://windrunnermax.github.io/FlowChartEditor/
  - 流程图编辑器，支持独立的流程图编辑器包以及DrawIO嵌入通信方案

- https://github.com/mortalYoung/graph-react
  - https://mortalyoung.github.io/graph-react/introduction
  - graph-react 是基于 mxGraph 打造, 为组件开发场景而生的开发工具。该项目的接口实现参考于 AntV
  - 在配置对应的数据和类型就会根据数据渲染出对应的 vertexs、edges、ports

- https://github.com/process-analytics/mxgraph-sketch
  - Add sketch style to mxGraph thanks to roughjs

- https://github.com/hp100277/mxGraph-worker-render /js
  - 基于mxGraph生成的图形使用webwroker进行解析并渲染为canvas
  - 依赖promise-worker, zrender

- https://github.com/kristianmandrup/react-mxgraph-typescript-starter /ts
  - React 16 mxgraph-js and typescript starter template 

- https://github.com/kristianmandrup/mxgraph-app /ts
  - Components for building a Diagram App based on MxGraph 4.1+

- https://github.com/kristianmandrup/mxgraph-editor
  - Contains the main Editor and Editor UI classes for building an MxGraph based Graph Editor app.
- https://github.com/kristianmandrup/mxgraph-base
  - provides base functionality including factories and resources for building an mxgraph app
- https://github.com/kristianmandrup/mxgraph-extensions
  - extracted from the main mxgraph editor app

- https://github.com/kristianmandrup/software-diagram-app
  - AutoCAD for software development
  - mxgraph 4.1+, mxgraph-toolkit
  - https://github.com/kristianmandrup/mxgraph-toolkit
  - Toolkit for mxgraph built with ts-mxgraph

- https://github.com/QOLQA/vanilla-mxgraph /js
  - https://github.com/aire-ux/mxgraph
  - Aire-UX project relies on mxgraph, and this is its official fork. 

- https://github.com/convergencelabs/mxgraph-demo /202107/js
  - This project demonstrates collaborative diagram editing using the mxGraph open source diagraming framework integrated with Convergence
- https://github.com/convergencelabs/mxgraph-adapter /202107/ts
  - An adapter between mxGraph and Convergence
# utils
- https://github.com/jwyGithub/maxGraph-composition-api
  - Building web with composite api

- https://github.com/SciumoTech/mxgraphdata
  - Parses Draw.io or diagrams.net file that may be compressed into pure JSON.
  - You must include Pako

- https://github.com/shiddo-tech/mxgraph-import-export-adapter /js
  - import and export mxgraph, 基于xml-js

- https://github.com/WolfScholle/mxgraph-canvas-spike
  - a spike on how to add canvas drawing functionality to mxGraph

- https://github.com/b1f6c1c4/draw.io-export
  - Convert draw.io xml to pdf/png within command line.

- https://github.com/Sispeks/mxgraph2pptx
  - mxgraph2pptx

- https://github.com/phaze-phusion/svg-to-stencil
  - Convert SVG paths to MXGraph syntax used in DrawIO stencils
  - SVGs containing groups `<g>`, definitions `<def>` or transform attributes are not supported.
# integrations
- https://github.com/QuantStack/jupyterlab-drawio /js
  - A standalone embedding of the FOSS drawio / mxgraph package into jupyterlab
# examples
- https://github.com/tbouffard/mxgraph-javascript-example-bundled-with-rollup /js
  - Vanilla Javascript mxGraph integration example

- https://github.com/tripplen23/mxGraph-electron-helloWorld
  - /js
- https://github.com/cd-yang/mxGraphElectron /js
  - Demo for mxGraph library with electron
  - https://github.com/cd-yang/mxgraph-react-demo

- https://github.com/pwcong/bpm /ts
  - BPM Components written in React for Business.

- https://github.com/wewoor/mxgraph-demo /js/react
  - some mxGraph usage examples
  - Hierarchical Layout
- https://github.com/korbinzhao/mxgraph-editor /js/react
  - A mxGraph editor support 3 types of shapes, svg/image/card.

- https://github.com/ksc-fe/king-diagram /js
  - A diagram editor based on mxGraph

- https://github.com/Jason-chen-coder/Mxgraph-EasyFlowEditor
  - https://jason-chen-coder.github.io/Mxgraph-EasyFlowEditor
  - 基于mxGraph+vue设计的流程图编辑器

- https://github.com/ekoz/vue-mxgraph-samples
  - 在 vue2 中使用 mxgraph 的一些用例 

- https://github.com/coco-w/coco-mxgraph-editor
  - 基于 mxgraph，vue3，typescript 的 editor 组件
  - https://github.com/coco-w/mxgrapheditor
# more
- https://github.com/jsoliz064/mxGraph_server_node
  - /js
