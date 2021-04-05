---
title: thread-geo-mapping
tags: [geo, mapping, thread]
created: '2021-03-26T11:27:57.480Z'
modified: '2021-03-26T11:28:29.993Z'
---

# thread-geo-mapping

# pieces

- ## 

- ## Voronoi polygons for hover interactivity of points are popular and make sense to dataviz practitioners but maybe we should have been teaching people how to use quadtrees instead? 
- https://twitter.com/Elijah_Meeks/status/1378880759713333252
  - Familiarity with quadtrees is more valuable in the long-term and gives greater dataset flexibility.
  - As far as flexibility, you can do the same radius-constrained lookup, but you can also use quadtree hierarchies for clustering. 
  - As for long-term value, understanding quadtrees and spatial search is better than proficiency with an otherwise seldom-used visualization approach.
- voronoi/quadtree hover overlays look cool, but i don't think there's any number of points where they're actually the best choice
  - low n: just check every point onmousemove instead
  - high n: computing a voronoi locks up the browser
- Any reference for beginners?
  - The quadtree from #d3js is something I'm most familiar with and is well-documented and easy to use. I have never written any tutorials about it and haven't seen any, though.
