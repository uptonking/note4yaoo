---
title: lib-notebook-observablehq-community
tags: [community, observablehq]
created: '2021-05-14T14:54:41.440Z'
modified: '2021-05-14T14:55:00.191Z'
---

# lib-notebook-observablehq-community

# discuss

- ## One great thing about using @observablehq is that I am not "locked in". 
- https://twitter.com/steren/status/1525226330039521280
  - notebooks can be exported in idiomatic JavaScript, and later loaded on my own website:

- ## To help investigate userspace bugs in long running @observablehq notebooks, I used @mootari 's access-runtime notebook to create a notebook state snapshot function. 
- https://twitter.com/tomlarkworthy/status/1508384106937303043
  - Now you get a readout of all the cells and their current state, and value is availible.

- ## Anyone seen any good patterns for running automated tests in an @observablehq notebook?
- https://twitter.com/simonw/status/1495094294851428352
- If ya looking for more end-to-end or integration tests: https://github.com/asg017/observable-prerender
  - Otherwise, abstracting your JS code into a separate package is always cool, or moving your data processing into a node script is also helpful

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
- What I'm talking about is editing code with Vim-like keys INSIDE the cells. An implementation of the Ace Editor or something similar would be amazing.
  - We use CodeMirror and are considering the vim bindings, but it’d probably be something we launch at the same time as user-configurable key bindings.
