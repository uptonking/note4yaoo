---
title: thread-viz-base-svg
tags: [svg, thread, viz]
created: '2021-03-11T11:17:49.598Z'
modified: '2021-03-11T11:26:06.670Z'
---

# thread-viz-base-svg

# pieces

- ## Too Many SVGs Clogging Up Your Markup? Try `use`.
- https://css-tricks.com/too-many-svgs-clogging-up-your-markup-try-use/
- Recently, I had to make a web page displaying a bunch of SVG graphs for an analytics dashboard. I used a bunch of `<rect>, <line>, <text>` elements on each graph to visualize certain metrics.
- This works and renders just fine, but results in a bloated DOM tree, where each shape is represented as separate nodes. 
  - Displaying all 50 graphs simultaneously on a web page results in 5, 951 DOM elements in total, which is far too many.
- This is not optimal for several reasons:
  - A large DOM increases memory usage, longer style calculations, and costly layout reflows.
  - It will increases the size of the file on the client side.
  - Lighthouse penalizes the performance and SEO scores.
  - Maintainability is a nightmare — even if we use a templating system — because there’s still a lot of cruft and repetition.
  - It doesn’t scale. Adding more graphs only exacerbates these issues.
- The solution? The SVG element.
  - The `<use>` element takes nodes from within the SVG document, and duplicates them somewhere else. 
    - The effect is the same as if the nodes were deeply cloned into a non-exposed DOM, then pasted where the `use` element is.
