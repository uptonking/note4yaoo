---
title: lib-viz-flowchart-logicflow-dev
tags: [flowchart, logicflow, node-edge]
created: 2024-05-14T19:37:39.990Z
modified: 2024-05-14T19:38:08.626Z
---

# lib-viz-flowchart-logicflow-dev

# guide

- features
  - 支持多种绘图实现，默认支持html和svg, 支持缩放
  - 🔌 支持插件
  - 提供了流程引擎的后端实现Turbo，仅5张表
  - 示例丰富
    - edge-animation, auto-layout
    - bpmn
    - [提供了执行任务动画的示例](https://docs.logic-flow.cn/demo/dist/bpmn-and-engine)
      - [内置了基础的动画效果, 在定义边的时候，可以将属性isAnimation设置为 true 就可以让边动起来](https://site.logic-flow.cn/tutorial/intermediate-edge#%E5%8A%A8%E7%94%BB)

- pros
  - 支持undo/redo
  - 支持pause/resume
  - 支持minimap

- cons
  - LogicFlow目前不支持移动端的touch事件，所以会出现无法移动画布、节点
  - 似乎不支持transaction ?

- who is using #logicFlow
  - didi/xiaoju-survey

- tips
  - 主要用于流程图，不必在支持任意图形编辑和pdf编辑上花费过多精力
# dev

# examples

- https://github.com/Teamlinker/Teamlinker /GPL/202407/ts/inactive
  - Teamlinker is a team collaboration platform that integrates multi-functional modules, such as contact, task management, meeting, IM, Wiki and file management.
  - Completely developed using TypeScript, using Node.js on the backend and Vue3 on the frontend.
  - 依赖logicFlow

## apps-flow

- https://github.com/1Panel-dev/MaxKB /15.5kStar/GPL/202504/python/ts/vue
  - https://maxkb.pro/
  - 基于大模型和 RAG 的开源知识库问答系统
  - it is a ready-to-use RAG chatbot that features robust workflow and MCP tool-use capabilities. 
  - 依赖django、langchain、pgvector、Vue
  - Flexible Orchestration: Equipped with a powerful workflow engine, function library and MCP tool-use, enabling the orchestration of AI processes to meet the needs of complex business scenarios.
# docs

# more
