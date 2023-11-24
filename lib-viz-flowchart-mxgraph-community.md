---
title: lib-viz-flowchart-mxgraph-community
tags: [community, flowchart, mxgraph]
created: 2023-05-29T15:09:38.281Z
modified: 2023-05-29T15:09:48.766Z
---

# lib-viz-flowchart-mxgraph-community

# guide

# discuss
- ## 

- ## 

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
