---
title: thread-web-ui-foundation
tags: [components, pattern, thread, ui, web]
created: '2021-04-23T09:23:02.552Z'
modified: '2021-04-23T09:24:19.873Z'
---

# thread-web-ui-foundation

# pieces

- ## 

- ## 

- ## 

- ## How to implement a tooltip positioning engine
- https://twitter.com/lihautan/status/1352431000559607809
  - positioning in 12 directions
  - move as you scroll
  - flip as it hits the edge
  - constrained within a boundary
  - hide when the target leaves the screen
  - https://www.youtube.com/watch?v=tBn0lVUzUbA
- oh i'm an idiot i used `position:absolute` ..
  - Well, if your immediate scrollable parent is also the nearest positioned parent, then setting `position: absolute` would be some sort of optimisation where you wouldn't need to repositioned every time it is scrolled.
