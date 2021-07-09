---
title: spec-format-office-math
tags: [format, math, office, spec]
created: '2020-12-16T12:41:16.245Z'
modified: '2021-01-14T13:21:12.375Z'
---

# spec-format-office-math

# spec

- LaTex
# faq

- 

# guide

# pieces

# discuss
- ## Does MathLive use KaTeX or MathJax for rendering?
- https://github.com/arnog/mathlive/issues/402
- MathLive includes its own rendering engine. 
  - MathLive can be used to render static math as well, although it was optimized for editing.
- Editing and displaying text (and math formulas) are vastly different problems.
- Imagine that you are dealing with `"\sin x"`. 
  - Now, to display it you must parse that string, build a tree that represent its content (a "sin" operator and a "x" symbol next to each other), 
  - then generate some rendering abstraction (probably another tree) that represents what must be displayed (a "sin" string in a certain font, an "x" in another font), 
  - then actually render that to your target rendering environment (HTML for example, as a set of `<span>` tags with appropriate attributes and classes). 
  - That's basically what KaTeX and MathJax do, although they each have their own way of doing it (they use different intermediate representations, and can target different final rendering models, for example).
- For editing, you still need to do the first part, parsing the string and having an abstract representation of it. 
  - But now, you must also be able to handle editing operations on that, for example if the backspace key is pressed when the cursor is after "sin". 
  - You must have a way of not only "going down", but also "going back up", that is reconstructing the input, which now would be just "x". 
  - In addition to all the logic necessary to handle the editing (responding to keyboard input, keeping track and displaying a selection, handling mouse input), you also need data structures that can support being modified and still reconstruct TeX input.
- It might have been possible to start with KaTeX or MathJax, and heavily modify them to do this, but this would have been a much bigger effort. And I was kinda curious what it would take to implement an engine to do the TeX rendering as well

- ## MathJax Turns 3.0
- https://news.ycombinator.com/item?id=22582343
- MathJax 3 is about twice as fast as MathJax 2, but still slower than KaTeX.
- One relatively clear thing is that MathJax supports more features
- One thing I remember reading is that MathJax takes a fundamentally different approach, and that a lot of the time it spends is in measuring things on the page to get things exactly right, while KaTeX is looser about things. 
- Both MathJax and KaTeX support server-side rendering, and the speed differences vanish(消失) (for the reader at least) when nothing is being done client-side.

- [Switching From MathJax to KaTeX](https://www.xaprb.com/blog/switching-mathjax-katex)
  - MathJax is sophisticated(复杂巧妙的，先进的；水平高的), but it’s large and has a lot of dependencies. It’s not slow, but KaTeX is a lightweight drop-in replacement that’s even faster.
  - MathJax is simple to install with a one-line `<script>` tag
  - KaTeX is slightly more involved. js, css, setup
# ref
