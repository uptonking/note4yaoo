---
title: lib-viz-flowchart-mxgraph-dev
tags: [flowchart, mxgraph, viz]
created: 2023-05-29T15:08:59.025Z
modified: 2023-05-29T15:09:30.865Z
---

# lib-viz-flowchart-mxgraph-dev

# guide

- features
  - 示例丰富

- cons
  - 不适合绘制大量图形元素
  - 代码不够模块化

- tips
  - 主要用于流程图，不必在支持任意图形编辑和pdf编辑上花费过多精力
# dev
- 插入图形的一般流程
  - graph.insertVertex
  - graph.insertEdge
# codebase
- 都是EventSource实例
  - graphManager, graphModel, graphSelection, graphView
# more
