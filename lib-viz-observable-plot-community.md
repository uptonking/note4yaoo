---
title: lib-viz-observable-plot-community
tags: [community, d3, observable-plot, viz]
created: '2021-05-05T07:41:39.016Z'
modified: '2021-05-05T07:43:12.792Z'
---

# lib-viz-observable-plot-community

# guide

- ref
  - [Plot Spec design, function chaining & semantics](https://github.com/observablehq/plot/discussions/392)
# pieces
- ## 

- ## 

- ## 

- ## I am obsessed with Plot
- https://twitter.com/enjalot/status/1398009942070661122
  - I'll do this with some anecdotes and examples along with pointers to currently available resources. 
  - It's a very young library but it's already changing the way I make #dataviz dramatically
- the first thing is speed. I cannot emphasize this enough, when you can make visualizations an order of magnitude faster it qualitatively changes how you approach data.
  - it takes a little getting used to, but the API is pretty quick to remember and you don't need to type much to get a ton of power. my current obsession is stacking things.
- [Hands-on Data Visualization with Observable Plot](https://www.youtube.com/watch?v=SnLBbbQzK1E)

- ## Observable Plot 
- https://news.ycombinator.com/item?id=27036768
- I didn't see any mention of this, but does Observable Plot support interactive charts? E.g. detailed summary on data point hover?
- Yes, in a variety of ways. 
  - All marks currently support native tooltips (the title channel), and in the near future we’ll be releasing more interactions that you can compose into the chart, e.g. for brushing or pointing. 
  - As I mentioned in another comment here, Plot is designed to leverage Observable’s language-level interactivity (dataflow) — so all plots are reactive by default, and plots can expose an interactive selection to the rest of the notebook.
- Plot is designed to leverage Observable’s language-level interactivity (dataflow) rather than design a new interaction system that is limited to within the visualization.
- 
