---
title: lib-notebook-observablehq-community
tags: [community, observablehq]
created: '2021-05-14T14:54:41.440Z'
modified: '2021-05-14T14:55:00.191Z'
---

# lib-notebook-observablehq-community

# discuss

- ## 

- ## 

- ## Observable’s Not JavaScript_201906
- https://news.ycombinator.com/item?id=20184181
- I kinda want Observable to be it's own language that can compile to JS
  - And it kinda is. We provide a parser¹ and a runtime², and you can download a copy of any notebook compiled to a JavaScript module
  - That said, we’re explicitly designing for the reactivity of the notebook environment. 
- What's the rationale for results above code?
  - On Observable, each cell is a unit that can be evaluated independently, with two sides to it — you have the source code editor, and you have the rendered display (either a chunk of DOM or canvas that you’ve drawn, or an interactive inspector for JS values).
  - Now, the important thing is that the code half of the cell is often collapsed. 
  - If the code is on top, the entire cell jumps when it opens and closes, pushing the rendered display up and down. 
  - If the code is on the bottom, it emerges from the half of the cell that is always there, and the display is stable.
  - the rendered value as primary and the source code as secondary.
- Non-linear is a plus. Why force an order. Spreadsheet is non-linear and it works pretty well
- Clicking to reveal can be simply addressed with a global Expand-All toggle.


