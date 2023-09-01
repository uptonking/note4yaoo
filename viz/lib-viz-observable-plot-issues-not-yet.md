---
title: lib-viz-observable-plot-issues-not-yet
tags: [issues, not-yet, observable-plot]
created: 2021-05-31T18:12:17.654Z
modified: 2021-05-31T18:13:54.087Z
---

# lib-viz-observable-plot-issues-not-yet

# issues-not-yet

- ## [Sort a scale’s domain according to a channel, or other scale?](https://github.com/observablehq/plot/issues/388)
- It is common to have to sort marks according to another channel: vertical or horizontal bars sorted by decreasing size for example.
  - Vega-Lite offers a very simple syntax to do this: `sort("-y")`, to sort for example markBars according to channel y, 
  - and ggplot2 offers a similar syntax `(x = reorder(...))`.
  - With Plot, it's more complex, especially in the context of grouping, with domain specifications via d3.groupSort() that require a fine-grained knowledge of these advanced D3 functions, and I'd rather avoid this kind of dependency to D3.
- We did a lot of previous exploration on this topic; 
  - I’m supportive of continuing this effort, but I don’t think it’s easy. 
  - I have two fairly strong opinions here. 
  - First, it **should be explicit and opt-in**: you have to declare which mark channel is driving the sort order (or possibly which other scale, and perhaps in either case you have to specify how to aggregate multiple values). 
  - Second, we should **avoid a stringDSL** like "-y" or "median(y)" because we want this to be extensible with JavaScript.




