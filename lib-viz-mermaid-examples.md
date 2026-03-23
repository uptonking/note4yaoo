---
title: lib-viz-mermaid-examples
tags: [charting, examples, flowchart, mermaid]
created: 2025-11-19T17:58:52.718Z
modified: 2025-11-19T17:59:15.580Z
---

# lib-viz-mermaid-examples

# guide

# popular
- https://github.com/xicilion/chart_for_markdown /202511/md
  - 本库整理了典型的图表应用案例，涵盖 Vega、Vega-Lite、Mermaid 和 HTML+CSS 四种主流可视化技术。
  - Vega 高级可视化图表 5 个图表类型
  - Vega-Lite 数据驱动图表 22 个图表类型
  - Mermaid 流程与关系图 19 个图表类型
  - HTML+CSS 自定义架构图 1 个图表类型
  - 📡 roadmap
    - xychart
  - https://x.com/xicilion/status/1991503023475228784
    - 写文档的时候，把图表库 clone 到文档目录，把图表库路径告诉 agent，让它根据文档内容，自由选择最合适的图表。
    - 如果有特殊需求， 可以将指定图表的文件给 agent 要求它用。
    - 如果 agent 绘制图表出错， 可以把样本文件给它让它照抄。
  - https://github.com/xicilion/markdown-viewer-extension
    - 把前阵子写的 markdown 渲染工具改写成 chrome 插件发布出来了。支持浏览器阅读 markdown，并一键保存为 word

- https://github.com/gotoailab/modern_mermaid /MIT/202512/ts
  - https://modern-mermaid.live/
  - modern, beautiful Mermaid.js editor with live preview, multiple themes, and high-quality export. 
  - [I built a modern Mermaid.js editor with custom themes + beautiful exports — looking for feedback! : r/Markdown _202512](https://www.reddit.com/r/Markdown/comments/1pc7e0p/i_built_a_modern_mermaidjs_editor_with_custom/)
    - Nice work! Good selection of themes, backgrounds, fonts, example charts, etc.

- https://github.com/lukilabs/beautiful-mermaid /2.9kStar/MIT/202601/ts
  - Render Mermaid diagrams as beautiful SVGs or ASCII art
  - Ultra-fast, fully themeable, zero DOM dependencies. Built for the AI era.
  - When you're working with an AI coding assistant, being able to visualize data flows, state machines, and system architecture—directly in your terminal or chat interface—makes complex concepts instantly graspable.
  - 5 diagram types — Flowcharts, State, Sequence, Class, and ER diagrams
  - Dual output — SVG for rich UIs, ASCII/Unicode for terminals
  - Mermaid is the de facto standard for text-based diagrams. It's brilliant. But the default renderer has problems:
    - No terminal output — Can't render to ASCII for CLI tools
    - Heavy dependencies — Pulls in a lot of code for simple diagrams
    - We built beautiful-mermaid at Craft to power diagrams in Craft Agents
    - The ASCII rendering engine is based on mermaid-ascii by Alexander Grooff. We ported it from Go to TypeScript
    - https://github.com/AlexanderGrooff/mermaid-ascii /MIT/202601/go
      - Render mermaid diagrams in your terminal

- https://github.com/u14app/mindmap /apache2/202603/ts/svg/NoDeps
  - https://mindmap.u14.app/
  - A beautiful, interactive mind map component for React.
  - Natively supports AI stream output with Markdown list syntax and iOS-style UI.
  - [【开源】Open MindMap 更轻量级的思维导图，自创 Markdown-Like 语法，MindNode 风格  _202603](https://linux.do/t/topic/1800074)
    - 原生 AI 支持，Markdown-Like 语法，好看的 UI，轻量级（gzip 16.8k）。
    - 基于文本的思维导图，目前最主流的还是mermiad, 我觉得没必要另起炉灶自定义一套
    - 并不是没考虑过，mermiad 大而全，但对于思维导图的支持存在以下几个问题：
      - 1、思维导图语法过于生涩，用户不学习的情况下，无法直接编写
      - 2、mermiad 的思维导图更像是知识图谱的样式，而非传统的思维导图
      - 3、mermiad 适合展示，无法直接对思维导图进行图形界面的编辑
      - 4、mermiad 太重了，不适合轻量级的 web app 使用
      - 5、AI 其实对 mermiad 支持度一般，在输出语法时经常出错，之前做过的几个项目，我需要反复修改提示词才能勉强保住 AI 对 mermiad 输出可以被正常渲染
      - 6、mermiad 没有天然的 AI 支持，勉强可以流式输出，但无内置 AI 输入框，需要额外开发。
# examples
- https://github.com/skovy/llm-markdown /MIT/202309/ts/inactive
  - https://llm-markdown.vercel.app/
  - A Nextjs app demonstrating how to display rich-text responses from Large Language Models (LLMs) by prompting and rendering Markdown formatting, Mermaid diagrams, and LaTeX equations.

- https://github.com/jgordley/MermaidGPT /202405/python/inactive
  - simple ChatGPT and Mermaid.js integration that allows you to generate diagrams using natural language
# utils
- https://github.com/1jehuang/mermaid-rs-renderer /MIT/202601/rust/NoDeps
  - A fast native Rust Mermaid diagram renderer. No browser required. 500-1000x faster than mermaid-cli.
  - mmdr renders diagrams 100-1800x faster than mermaid-cli by eliminating browser overhead.
# integrations
- https://github.com/apache/echarts-from-mermaid /202503/ts/inactive
  - A plugin that enables Apache ECharts to render charts using Mermaid-like syntax.
  - This plugin is particularly useful when you want to generate charts from text/markdown, especially in LLM applications. 
    - Instead of having LLMs generate complex ECharts options directly, you can use this plugin to convert simpler Mermaid-like syntax into ECharts options. 
    - This approach is more reliable since Mermaid syntax is much simpler than ECharts' option structure.
# text-charting
- https://github.com/BlueprintLabIO/markdown-ui /412Star/MIT/202509/ts/inactive
  - https://markdown-ui.blueprintlab.io/
  - https://markdown-ui.com/
  - An open standard for rendering interactive widgets in plain Markdown
  - Readable everywhere: Preview rich UI, but if unsupported, it's still legible Markdown
  - Zero lock-in: Pure spec—works with any Markdown parser + any UI framework
  - [Show HN: Turn Markdown into React/Svelte/Vue UI at runtime, zero build step | Hacker News _202508](https://news.ycombinator.com/item?id=45024532)
# more
