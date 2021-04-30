---
title: thread-web-ui-foundation
tags: [components, pattern, thread, ui, web]
created: '2021-04-23T09:23:02.552Z'
modified: '2021-04-23T09:24:19.873Z'
---

# thread-web-ui-foundation

# pieces

- ## 

- ## I have to admit that I thought I would be using CSS Grid a lot more when I learned it. 
- https://twitter.com/andrewbaisden/status/1386999817444986883
  - However with both React Native and Flutter using Flexbox for layout I am using it much more.

- ## have a design system taking advantage of CSS named template areas | lines for layout?
- https://twitter.com/argyleink/status/1366894892404809728
  - layout type (container) creates a grid with named areas, then elements claim them (slots)? or do you assign them to a slot? have tooling? have typed layouts!? tokens? tell me everything!
  - or maybe y'all have a 12 | 16 column grid, and children span based on token values!? get that art direction right into the CSS from an API Nerd face
- I like the slot technique used in React Spectrum - similar to WC
  - It’s all CSS grid under the hood.
- Largely using named areas for page layout, attaching the styles to a `data` attribute. 
  - This way the grid area is not dependent on semantic containers like `<main>` . 
  - `data-grid-area` can be applied to any element. You can even nest layouts this way.

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
