---
title: pm-office-data-analysis-viz
tags: [data-analysis, documentation, office, pm, viz]
created: '2021-04-16T15:06:09.060Z'
modified: '2021-07-11T08:25:40.112Z'
---

# pm-office-data-analysis-viz

# guide

- more-data-notebooks
  - observable
  - streamlit
  - grid
  - jupyter for python

- more-notebooks
  - starboard-notebook

- more-notebooks
  - vscode notebook api

# faq

- ## 文档打开慢
- 考虑code splitting

- ## 文档不能离线编辑，缺少标准的交互式文档格式
- 离线的响应速度和性能应该要快一点

- ## 编辑文档时，菜单少图标多，一不小心就不知道点到了哪里，很焦虑
- 帮助文档弹出提示
- easy undo-redo

# ideas

- app in notebook
  - mini-program

# discuss

- ## 导出图片
- https://github.com/asg017/observable-prerender
  - Pre-render Observable notebooks with Puppeteer! Inspired by d3-pre
- https://github.com/fivethirtyeight/d3-pre
  - pre-renders d3 visualizations into inline SVG elements
  - The pre-rendering tool uses a headless browser to turn d3 code into its resulting SVG

- ## Grid is like a no-code version of Observable d3 notebooks
- https://twitter.com/benlcollins/status/1374398481381478414
- https://grid.is/
  - GRID is a no-code productivity tool that enables you to transform your #spreadsheets into shareable, interactive web documents.
  - GRID enables you to leverage your existing spreadsheet skills to build smart, interactive calculators, reports and scenario analyses.

- ## Can you run your own Observable notebook server
- https://talk.observablehq.com/t/noob-can-you-run-your-own-observable-server/757/9
- https://github.com/observablehq/runtime
  - Observable runtime lets you run Observable notebooks as true reactive programs in any JavaScript environment
- Embeddable notebooks are now available. 
  - You can download your compiled notebooks and upload them to your server, 
    - or load them directly from api.observablehq.com with your provided access key. 
  - With the first method, you’re completely independent of observablehq.com, 
  - but with the latter, you can get live updates to your (for example, dynamic programming tutorial) every time you hit “Publish” again.
- The notebook-runtime is the same codebase that observablehq.com uses to run your notebooks, and has the same browser support targets: 
  - the evergreen browsers — Chrome, Firefox, Safari, Edge and Node.js. 
  - That said, if you need wider browser support, we’d certainly be happy to look at pull requests against notebook-runtime that enable it.
- We may offer some on-premise (self-hosted) enterprise solution in the future, 
  - but our current focus is on developing cloud-hosted private collaboration for teams.

# ref

- [Why We're Building Observable](https://observablehq.com/@observablehq/why-were-building-observable)
  - https://news.ycombinator.com/item?id=25161409
