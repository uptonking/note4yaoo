---
title: lib-viz-flowchart-mxgraph-community
tags: [community, flowchart, mxgraph]
created: 2023-05-29T15:09:38.281Z
modified: 2023-05-29T15:09:48.766Z
---

# lib-viz-flowchart-mxgraph-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## [Migration of mxGraph GraphEditor Demo to MaxGraph · maxGraph/maxGraph · Discussion _202502](https://github.com/maxGraph/maxGraph/discussions/695)
  - 将类似 drawio 的界面迁移到 maxgraph

- ## 🎨 [Feasibility of using canvas or webgl to replace SvgCanvas2D _202302](https://github.com/maxGraph/maxGraph/issues/180)
  - I understand that mxGraph was designed to use svg from the beginning. From a technical standpoint, I'm wondering if it's possible to implement `AbstractCanvas2D` using canvas or webgl instead of `SvgCanvas2D` ?
- [Implementing AbstractCanvas2D using canvas · maxGraph/maxGraph · Discussion _202303](https://github.com/maxGraph/maxGraph/discussions/182)
  - I have implemented the drawing of blocks and lines using canvas

- AFAIK, it is feasible to extend AbstractCanvas2D to implement what you suggest. It is clearly designed for this purpose. 
  - Previously, mxGraph was able to manage `VML` rendering with a dedicated `AbstractCanvas2D`. It also involved some flags in the code to choose the `Canvas2D` implementation at runtime. 
  - Both the VML and flags have been removed from maxGraph in version 0.1.0.
  - So, if we want to implement alternative Canvas2Ds, we will have to implement again the logic that will allow us to choose the type of Canvas2D we want to use. Reviewing the former mxGraph code will help here.
- In the past, I participated in a experiment with mxGraph on adding sketch support to the SvgCanvas2D. This involved having a new Canvas2D class but also modify some prototypes from the original mxGraph implementation. As this was already a kind of SvgCanvas2D, there was no need for a dedicated flag, so the changes to mxGraph prototypes were limited. This may help for investigations.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## ComfyUI 这种交互形式有名字吗？macOS/iOS 有实现好的库吗吗？
- https://twitter.com/s1ntone/status/1769908843323240871
- 前端的还有 React Flow / Rate.js / BaklavaJS

- ## Have someone tried to build a graph like this in HTML and CSS?
- https://twitter.com/hhg2288/status/1727836911899676856
- I'd consider constructing this kind of thing with SVG. Also, it might end up being easiest to actually measure locations of the adjacent history parts rather than trying to predict them.
- Drawing this is only part of the problem. And indeed I think you gotta need SVG at least.
  - But before starting the drawing you’d need to compute the layout of the DAG first, and figure out the minimum number of columns and how to pack the nodes onto them.

- ## 💡 [Performance on loading \ inserting \ zooming in mxgraph](https://github.com/jgraph/mxgraph/issues/265)
- The main issue here is manipulating a large SVG DOM takes time. The change for zooming involved SVG zoom, to avoid the SVG DOM API.
  - as @Diaskhan points out, mxGraph isn't the right library if you looking to draw 10, 000 shapes.
  - You're better off with a WebGL or canvas based library that is written for high performance.
- 👉🏻 If you still pick mxGraph for a large diagram, you'll need to implement some application level of detail (LOD) functionality. 
  - That is, when a huge graph is zoomed out, rather than try to render everything, render some summary of groups of cells, instead.
- 👉🏻 The LOD example demonstrates showing different views based on zoom level. 
  - [Level of detail(LOD) example for mxGraph](https://jgraph.github.io/mxgraph/javascript/examples/lod.html)
  - That said, I haven't checked whether this would actually solve performance issues at scale.
  - It might be that you would need to create a "shadow model" of cells removed from the graph and add/remove depending on the viewpoint and zoom to keep the number of cells to a certain limit.
- We've made improvements to the zoom. If the performance problems are elsewhere, I'd suggest a different library or some level of detail implementation.

- I make 2 steps
  - Set SVG display none before zooming
  - I draw the only cells. I delete methods redrawLabel and redrawControl
