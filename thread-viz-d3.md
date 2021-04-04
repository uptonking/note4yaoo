---
title: thread-viz-d3
tags: [d3, thread, viz]
created: '2021-02-28T08:06:23.552Z'
modified: '2021-02-28T08:06:41.340Z'
---

# thread-viz-d3

# pieces

- ## I figured out how to use d3 and TopoJSON to render an animated SVG map of vaccinations by US county
- https://twitter.com/simonw/status/1378583374235717637
  - [US county vaccinations choropleth map](https://observablehq.com/@simonw/us-county-vaccinations-choropleth-map)
- Turn it into an mp4 with observable-prerender!
  - [Introducing observable-prerender - Pre-render Observable notebooks with Puppeteer!](https://observablehq.com/@asg017/introducing-observable-prerender)

- ## I wrote up a guide for combining React & d3
- https://twitter.com/Wattenberger/status/1375063666840772615
  - [react + d3.js](https://wattenberger.com/blog/react-and-d3)
- The rules definitely extend to all other Javascript frameworks. I've used very similar code many times, especially in Svelte 
  - https://github.com/Wattenberger/Wattenberger-2019/tree/master/src/components/Blog/posts/D3AndReact
- I'm curious: How well does React scale vs D3, for doing the rendering of many components? Could you take the "Creating Many D3 elements" example and scale it, add mutation and corresponding animation, and profile the render?
  - since every SVG element is a DOM element, there's a good amount of overhead and things can get slow, in my experience ~1000 elements. I'll often use SVG by default and switch to Canvas (imperative code, no mouse events) if I need better perf
- WRT React vs D3 for rendering: Both can output same DOM, but their approaches for manipulating/updating are different. I *suspect* React might be slower because it's creating a Component wrapper around each, but I also wonder if its DOM-diffing approach offsets that overhead.
  - Yeah, it can be a bit slower, with all of the overhead. I'll sometimes go down the rabbit hole of perf checking and memoizing components, when a viz would still be snappy with vanilla js & d3. But I much prefer working with a js framework
  - Totally agree! Tho sometimes you don't have a choice. While React (or any framework) helps make things more readable and manageable (and testable!!), it's important to realize there might be tradeoffs as well.
- Very nice! I definitely advocated for this approach before, but I've found that both react-spring and framer-motion cause a lot of slowdowns when there are a lot of circles to animate (~500). Switching to d3-transition made it much smoother. Any thoughts on this?
  - there's definitely overhead with React that could require paying attention to perf, I'll always default to css animations when possible. but I'll take the tradeoffs for being able to use a framework any day

- ## Typically the voronoi-polygons of Lloyd's Algorithm closely resemble hexagons, but aren't quite perfect.
- https://twitter.com/MattDzugan/status/1359706810400276480
- [Lloyd's Algorithm ➡️ Regular Tilings](https://observablehq.com/@mattdzugan/lloyds-algorithm-regular-tilings)
