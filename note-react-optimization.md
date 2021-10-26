---
title: note-react-optimization
tags: [optimization, react]
created: '2020-08-07T09:03:40.736Z'
modified: '2020-12-08T13:38:59.914Z'
---

# note-react-optimization

# yet

- 只渲染指定或默认范围内visible的元素

# summary

- Stop worrying if rerenders happen and instead start worrying about how fast your renders are
  - Slow could mean a lot of things.
  - React is fast. But rendering non visible elements, computing expensive things that don’t change often, triggering infinite render loops are all terribly slow.
