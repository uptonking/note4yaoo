---
title: lib-notebook-starboard-codebase
tags: [codebase, starboard]
created: '2021-05-13T04:03:03.627Z'
modified: '2021-05-13T04:03:25.717Z'
---

# lib-notebook-starboard-codebase

# guide

- starboard的主要编辑区和预览区都在`<iframe>`里面

- `<starboard-editor>`是最外层web components组件
  - `<starboard-source-viewer>`展示了整篇笔记的源码
  - `<iframe>`是一篇笔记主要的内容编辑和预览区
    - `<starboard-cell>`作为每个区块的容器
      - `<starboard-text-editor>`是每个区块的源代码编辑区
      - `<starboard-console-output>`是每个区块的运行预览区
    - `<starboard-insertion-line>`作为区块间的空行，放置了 `Insert Cell` 的操作图标

# discuss

- ## 

- ## 

- ## 

- ## Feature request- Reset, Reset & Run all cells
- https://community.starboard.gg/t/feature-request-reset-reset-run-all-cells/81
- As long as the notebook runs in its own iframe with no further sandboxing, the equivalent of resetting the kernel would be refreshing that iframe.
- Jupyter Notebook has the top bar with global controls (such as Run all cells), Starboard has no equivalent for that. 
  - I tried to avoid it as long as possible, but it’s looking like it’s inevitable. 
  - We’ll need some buttons for global actions (e.g. download as text file, or run all cells). 
  - I still want people to also be able to use a Starboard notebook as a small embed too, so it shouldn’t be too prominent (perhaps it should be hidden by default).
