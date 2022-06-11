---
title: thread-viz-d3-notebook-examples
tags: [d3, examples, notebook, thread, viz]
created: '2021-05-25T09:14:09.194Z'
modified: '2021-05-25T09:14:28.879Z'
---

# thread-viz-d3-notebook-examples

# guide

# creators
- Eric Lo
  - https://github.com/analyzer2004
  - https://observablehq.com/@analyzer2004
  - https://ericlo.dev/

- We created a collection of curated datasets for our community to get started
- https://observablehq.com/@observablehq/curated-datasets
  📊Google Merchandise Sales Data
  📈Bandcamp Sales Data
  ⚡️EIA Electricity Data
  🌤NOAA Hourly Weather Data
  💹Plot Test Data
  🌍U. S. Geographic Data

# discuss
- ## 

- ## 

- ## I updated my @observablehq example of how to combine @d3js_org and @Mapbox to make it more reusable, using the D3 examples format.
- https://observablehq.com/@john-guerra/mapbox-d3
  - Just give it some topoJSON features and it will draw them with D3, letting Mapbox do the zoom and panning

- ## The new hexbin transform aggregates 2D points into hexagonal bins (true hexagons in screen space)
- https://observablehq.com/@observablehq/plot-hexbin

- ## Using scale to animate images between different aspect ratios will distort(使变形、扭曲) them. 
- https://twitter.com/mattgperry/status/1534885775086604290
  - My advice is usually to use two elements, an image and an outer div to clip it. 
  - Here's a new approach that uses one element, applying scale correction to backgroundSize
  - https://codesandbox.io/s/framer-motion-scale-correction-for-transformed-images-ude0np?file=/src/App.js
- The downside to the background-size approach is you lose `<img>` semantics. 
- Here's a hacky version using the upcoming `object-view-box ` rule, which is viewBox for images.
  - (Chrome Canary required)

- How are you handling layout changes if you're using transforms.
  - The CSS changes the layout (in this case width/height/margin) and the transforms animate the change
  - So what the point if using transforms if you still animate height and margin, etc...
  - You don't - you change width/height once, this changes the layout (the expensive operation). Then you undo the change using a transform, which you then animate back down to zero.
  - Here's a good write up of the general approach
  - [FLIP Your Animations](https://aerotwist.com/blog/flip-your-animations/)

- ## Render sketchy styled barchart with D3 & @antv/g
- https://observablehq.com/@xiaoiver/d3-rough-barchart

- ## We are using @observablehq notebooks and @vega_vis in our non-majors Intro to Data Vis course this quarter. 
- https://twitter.com/jonfroehlich/status/1520149034421219328
  - I've enjoyed learning both platforms and creating some educational materials

- ## This is DependenTree! A dependency graph visualization library built on top of D3.
- https://observablehq.com/@amogh/dependentree

- ## We created a few datasets for our community to get started with on @observablehq . First up is Google Merchandise Sales Data.
- https://twitter.com/observablehq/status/1514753644700344321

- ## Check out my observable notebook exploring COVID cases and deaths over time within the US
- https://observablehq.com/@amdaccache/u-s-covid-19-confirmed-and-probable-cases-deaths-by-state-rep

- ## It's the end of the year. I have worked with @observablehq for the entirety of 2021 and here are what I think are some of the best notebooks were, 
- https://dev.to/tomlarkworthy/100-beautiful-and-informative-notebooks-of-2021-23lg
  - curated into topics covering "dataviz", "maths", "art", "design", "dev", "apps", "tutorials" and "tools"

- ## A zoomable, point-based embedding of 1-million plus papers in the @arxiv using embeddings from the cartolabe project
- https://twitter.com/benmschmidt/status/1428763715827023874
  - [The Arxiv in WebGL](https://observablehq.com/@bmschmidt/arxiv)

- ##[ Visualizing The New York Times’s Mini Crossword](https://observablehq.com/@observablehq/nyt-minis)
