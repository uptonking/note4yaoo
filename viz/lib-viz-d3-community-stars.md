---
title: lib-viz-d3-community-stars
tags: [community, d3, viz]
created: 2021-05-29T21:06:19.728Z
modified: 2021-05-29T21:07:03.556Z
---

# lib-viz-d3-community-stars

# guide

- 时间变化条形图
  - [Make bar chart races without coding](https://flourish.studio/visualisations/bar-chart-race/)
  - [most popular backend frameworks 时间变化条形图 基于d3实现](https://statisticsanddata.org/data/most-popular-backend-frameworks-2012-2021/)
# pieces
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [flat Naming of exports · Issue #67 · codemirror/dev](https://github.com/codemirror/dev/issues/67)
- I've been leaning towards using as flat as possible a namespace within each package—everything goes into the top exports, except for the occasional static method that reads better when tacked onto a class.

- This reminds me of "the great namespace flattening" that happened in D3.js at v4.
  - The context comes after the names, so alphabetical ordering results in logical tree ordering.

- I think I've just accepted that some inconsistencies (EditorView but ViewPlugin, not EditorViewPlugin) are unavoidable if we don't want the interface to feel like it was written by computers, for computers. 
  - Also, nesting just doesn't work well with TypeScript, so that's out.
