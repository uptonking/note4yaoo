---
title: lib-viz-mermaid-community
tags: [charting, community, flowchart, mermaid]
created: 2025-11-19T17:50:48.482Z
modified: 2025-11-19T17:51:33.509Z
---

# lib-viz-mermaid-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 推荐一个 Mermaid.js的开源替代：Graphviz（内部使用dot 文本语言）
- https://x.com/LinearUncle/status/2076110243000631526
  - https://graphviz.org
  - AI 写 Mermaid 常因特殊符号渲染失败，AI 写 dot 语言几乎不会失败
  - 语法 30 年零变更，不存在版本兼容坑
  - 工业级布局引擎，几百节点也不乱
  - 表达能力更强，支持Html-like语法，特别是表格渲染
  - 不依赖浏览器，不用学，直接让AI出图

- 其实 Mermaid.js 的布局引擎就是 Graphviz.js。

- https://x.com/LinearUncle/status/2076660411349491831
  - https://play.d2lang.com
  - 推荐另外一个开源继任者：D2。同样是"文本 → 架构图"
  - 语法比 dot 更简洁直观，AI 生成几乎零失败，人也能直接读懂
  - 默认出图颜值高：内置多套主题，还有手绘风 sketch 模式，支持自定义icon
  - 三种布局引擎可切换（dagre / ELK / TALA），大图不乱，还能手动微调
  - 原生支持时序图、SQL 表结构、类图、图标、甚至动画——不用像 dot 那样靠 HTML-like 语法硬凑
  - 单个二进制 + watch 模式：改一行文本，图实时刷新，依然不依赖浏览器
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-flowchart
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## [Render a table from CSV/TSV _202203](https://github.com/mermaid-js/mermaid/issues/2858)
  - Table syntax in markdown is abhorrent. It's difficult to write, even more difficult to maintain. Plethora of conversion tools exist to help users to convert various data into markdown tables, but the process of converting and maintaining changes over time is clunky.
- mermaid block diagrams allow some simple tables to be rendered from tsv, or space-separated, data.(though they also need to include a line specifying the number of rows or columns)

# discuss
- ## 

- ## 

- ## 

- ## 
