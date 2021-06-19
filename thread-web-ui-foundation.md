---
title: thread-web-ui-foundation
tags: [components, pattern, thread, ui, web]
created: '2021-04-23T09:23:02.552Z'
modified: '2021-04-23T09:24:19.873Z'
---

# thread-web-ui-foundation

# guide

- ## The most useful piece of advice I’ve heard for designing reusable React components: Use popular libraries as inspiration.
- https://twitter.com/housecor/status/1406224388442177542
  - Before implementing my own Table, Select, Tabs, etc, I look at the APIs of popular libraries like MaterialUI, Ant Design, and Spectrum.
  - These libraries have been used by 1000's. Their APIs have been carefully thought through, and heavily vetted.
  - So while the API may not be perfect for my team's needs, it's likely a solid starting point.
- I have been doing the same with Angular 
# pieces
- ## 

- ## When people learn ARIA, overuse is a common mistake. 
- https://twitter.com/housecor/status/1390295213659279360
- [Notes on ARIA Use in HTML](https://www.w3.org/TR/using-aria/)
  - If you can use a native HTML element or attribute with the semantics and behavior you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so.
  - Do not change native semantics, unless you really have to.
  - All interactive ARIA controls must be usable with the keyboard.
  - Do not use `role="presentation"` or `aria-hidden="true"` on a focusable element .
  - All interactive elements must have an accessible name.

- ## how do you solve this problem: I often have SVG files I load in img tags. 
- https://twitter.com/bradwestfall/status/1389724773077315584
  - I want to control the width and height with CSS only. 
  - Sometimes the SVG will load HUGE for a split second until the CSS loads and shapes it down to size.
  - my solution: Right now I do a style tag that looks for all img's with file names ending in svg, display none those. Wait until the CSS loads to give it it's size and also reset omg/svg to display:inline
  - [SVG Style Inheritance and the ‘Flash Of Unstyled SVG’](https://www.sarasoueidan.com/blog/svg-style-inheritance-and-fousvg/)
- If the original SVG has viewBox defined, you can size them inline with the image tag, and further resize them using CSS. 
  - On the img tag, I usually size them for mobile and scale them up as needed with CSS for larger viewports. 
  - A lot of compressors remove the viewBox.
- You can set the size of the SVG I believe, so perhaps you can set the initial size of the resource to be smaller

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
  - Yeah most likely I just need repaint and/or re-composition instead of relayout
