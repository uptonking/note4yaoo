---
title: thread-algs-usecase
tags: [algorithms, thread, usecase]
created: '2021-02-20T07:29:08.660Z'
modified: '2021-02-20T07:30:23.867Z'
---

# thread-algs-usecase

# pieces

- ## 

- ## Algorithm question (I have no idea). Given a rectangular plane and a set of rectangles on it, find the “nicest” place for a new rectangle with a given size. 
- https://twitter.com/mourner/status/1362885034085146628
  - By “nicest” I mean “where you would place it” — ideally in the middle of the largest free space. Can’t move other rects.
- this is at least similar to the "pole of inaccessibility"
  - https://github.com/mapbox/polylabel
  - A fast algorithm for finding polygon pole of inaccessibility, 
  - the most distant internal point from the polygon outline (not to be confused with centroid), implemented as a JavaScript library. 
  - Useful for optimal placement of a text label on a polygon.

- ## Given an array of length n, how would you select m ≤ n evenly-spaced samples from the array? Surprise: you can use Bresenham’s line algorithm.
- https://twitter.com/mbostock/status/1380708254586609664
- [Evenly-Spaced Sampling](https://observablehq.com/@mbostock/evenly-spaced-sampling)
