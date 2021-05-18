---
title: lib-notebook-observablehq-dev
tags: [d3, notebook, observablehq]
created: '2021-05-06T09:42:52.668Z'
modified: '2021-05-14T14:44:14.720Z'
---

# lib-notebook-observablehq-dev

# guide

- tips
  - observable-notebook的使用体验，感觉像为d3语法设计的文档ide

- [Making Your Code Citable](https://guides.github.com/activities/citable-code/)
  - 提出了一种基于zenodo发布与引用代码或网页的方法
  - 类似arxiv、biorxiv、figshare、peerage of science、peerj preprints

# pros

- cell的执行顺序不按照书写顺序，而按照依赖顺序
  - 自动生成尾部的appendix
- reactive document，适合用来做展示文档
- import named cells from other notebooks
  - `import` cell `with` data `from` other-notebook
- 可以修改和探索任何发布的notebook

# cons

- ## 文档编辑类
- 不支持图文混排，如水平分栏，只能上下堆叠单元格
- @username会另起一行

- ## 文档编辑-markdown
- markdown的code block的样式与observablehq的代码样式相同，易混淆文档和实际执行的代码

- ## 导航浏览类
- 快捷键冲突
- 文档不支持自动生成目录toc

- ## syntax
- import的来源无法区分来自npm，还是来自其他observable notebook
  - observablehq对于导入npm包使用`require()`，默认基于cdn.jsdelivr.net，需要AMD
  - `import()`需要手动指定cdn.skypack.dev，需要es6
  - `d3-require` is the module that powers Observable’s `require`.
- 跳转到声明处，未实现

# faq-not-yet

- 如何不显示cell name，同时又能通过cell name引用这个cell

# faq

# examples-stars

- [新型冠状病毒患者行为数据分析与可视化](https://observablehq.com/@zhangwenjia-pku/untitled)
  - 展示了随时间动态变化的条形图

# examples

- ref
  - search: 数据 site:observablehq.com

# ref

- [How to: Embed a Notebook in a React App](https://observablehq.com/@observablehq/how-to-embed-a-notebook-in-a-react-app)

- [HQ](https://askubuntu.com/questions/627516) means Headquarters.
  - It's the name given to the website, not the software project per se(本身，自身，本质上).
