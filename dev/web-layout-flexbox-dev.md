---
title: web-layout-flexbox-dev
tags: [flexbox, layout]
created: 2020-08-17T13:31:05.254Z
modified: 2020-12-21T07:46:20.408Z
---

# web-layout-flexbox-dev

# faq

- ## `margin: auto` vs `justify-content/align-items:center`

```CSS
/* 第一种 */
.outer {
  display: flex;
}

.inner {
  margin: auto;
}

/* 第二种 */
.outer {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

- In the first example `auto` margin applies only to the flex item and centers that one flex item within the container.
- In the second example, you are centering items from the container level. This code will center all items.
- Also, keep in mind, if you use both methods at the same time `margin: auto` should prevail(战胜).
  - From CSS Flexbox spec 8.1:
  - Prior to alignment via `justify-content` and `align-self` , any positive free space is distributed to auto margins in that dimension
  - If free space is distributed to auto margins, the alignment properties will have no effect in that dimension because the margins will have stolen all the free space left over after flexing.
- But the most important difference, for practical purposes, may be the behavior when a flex item exceeds the size of the container. 
  - When this happens, you lose access to parts of the item when using the container-level code. 
  - The item disappears from the screen and is not accessible via scroll.
  - To overcome this problem, use `margin: auto` for centering to work properly.
- ref
  - [What's the difference between margin:auto and justify-content/align-items center?](https://stackoverflow.com/questions/44244549/whats-the-difference-between-marginauto-and-justify-content-align-items-cent)

- ## What's the diff on a position:absolute el btw `{top:0;right:0;bottom:0;left:0;}` and `{top:0;left:0;height:100%;width:100%;}` ?

- [Width and Absolute Positioning](https://keithjgrant.com/posts/2016/01/width-and-absolute-positioning/)

- “That’s easy”, I thought. “They often seem the same in practice, but width and height are based on the parent (or nearest block-level ancestor). Top, right, bottom, and left are based on the nearest positioned ancestor. Those aren’t necessarily the same element.”

- But my codepen showed me an absolutely positioned element whose width and height are derived from the positioned ancestor, not the immediate container.

- With right: 0; bottom: 0, the margin is contained inside the positioned descendant; they will shrink the size of the element.
  - So what does this mean? It seems to me that `top: 0; right: 0; bottom: 0; left: 0` is probably the one to favor, as it's a little more predictable, unless you have a particular reason to use height or width instead.
# discuss
- ## Do you ever not want `min-width/height: 0` to prevent Grid/Flex children from spilling out? 
- https://twitter.com/souporserious/status/1427404212531458054
  - Seems like it should be in a reset. 
  - I did this in a system before and don't recall having any issues 
  - [Preventing a Grid Blowout](https://css-tricks.com/preventing-a-grid-blowout/)
- Hmm, I don’t ever set min dims to 0. My approach is usually to conform to content flow and avoid fixed containers that would allow contents to spill. Am I missing something?
- Yeah there's a difference, here, where min-height:0 causes children to shrink, probably unexpectedly
  - Sometimes you do want your children content to be the min-height, if you _want_ them to overflow their scrollable containe
  - Ohh, this is a perfect example! 🙏 So maybe it could be automatically set based on the parent overflow (and could be overridden if needed). Just thinking what the best happy path could be
