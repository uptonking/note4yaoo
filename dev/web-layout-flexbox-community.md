---
title: web-layout-flexbox-community
tags: [community, flexbox, layout]
created: 2020-08-17T13:31:05.254Z
modified: 2024-06-18T02:45:42.107Z
---

# web-layout-flexbox-community

# guide

# examples
- Quick little prototype that animates a flex layout as you change configuration options for it
  - https://twitter.com/argyleink/status/1735369407961153655
  - https://codepen.io/argyleink/pen/rNPEOxM
  - wrapping the style updates with `document.startViewTransition()`.
  - i could write some custom view transition styles to make it stretch to the new position, but i was lazy.
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
# discuss-min-width/height-0
- ## 

- ## [Use text-overflow: ellipsis and flexbox align-items: center in combination - Stack Overflow](https://stackoverflow.com/questions/48545178/use-text-overflow-ellipsis-and-flexbox-align-items-center-in-combination)
- text-overflow: ellipsis won't work on flex container (display: flex).
  - The main reason is that the text node becomes a anonymous flex child and needs `min-width: 0` to behave (or else it won't shrink beyond its content size), but as one can't target a text node with CSS, we need to wrap it, here done with a span.

# discuss
- ## 

- ## 

- ## [Absolutely positioned flex item is not removed from the normal flow in IE11 - Stack Overflow](https://stackoverflow.com/questions/32991051/absolutely-positioned-flex-item-is-not-removed-from-the-normal-flow-in-ie11)
- 💡 an absolutely-positioned child of a flex container does not participate in flex layout

- ## Basically every layout overflow bug ever boils down to some flex or grid child needing `min-width: 0` ; 
- https://twitter.com/adamwathan/status/1734696245015494711
- And basically every layout underflow bug ever boils down to some flex child needing `flex-shrink: 0` .
- For those asking, it's likely because of `min-width` defaulting to `auto` .
  - [Defensive CSS - Minimum Content Size In CSS Flexbox](https://defensivecss.dev/tip/flexbox-min-content-size/)

- 📝 [An Interactive Guide to Flexbox in CSS](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/)
  - After a few years of practice, I actually feel like setting `flex-shrink: 0` is the more straightforward/direct solution to this particular problem. Though,  `min-width` still has an important role to play in the Flexbox algorithm! 
  - flex-shrink has a default value of 1, and we haven't removed it, so the search input should be able to shrink as much as it needs to! Why is it refusing to shrink?
  - The Flexbox algorithm refuses to shrink a child below its minimum size. The content will overflow rather than shrink further, no matter how high we crank flex-shrink!
  - Text inputs have a default minimum size of 170px-200px (it varies between browsers). That's the limitation we're running into above.
  - In other cases, the limiting factor might be the element's content. For an element containing text, the minimum width is the length of the longest unbreakable string of characters.
  - By setting min-width: 0px directly on the Flex child, we tell the Flexbox algorithm to overwrite the “built-in” minimum width. Because we've set it to 0px, the element can shrink as much as necessary.
  - It's worth noting that the built-in minimum size does serve a purpose. It's meant to act as a guardrail, to prevent something even worse from happening. 比如min-width设为0后这个flex-item的内容会被相邻flex-item盖住部分

- Yes please. Would love `min-height: 0` as well. My full-screen flex-based layouts are plagued(折磨, 烦扰) by this.

- ## Do you ever not want `min-width/height: 0` to prevent Grid/Flex children from spilling out? 
- https://twitter.com/souporserious/status/1427404212531458054
  - Seems like it should be in a reset. 
  - I did this in a system before and don't recall having any issues 
  - [Preventing a Grid Blowout](https://css-tricks.com/preventing-a-grid-blowout/)
- Hmm, I don’t ever set min dims to 0. My approach is usually to conform to content flow and avoid fixed containers that would allow contents to spill. Am I missing something?
- Yeah there's a difference, here, where min-height:0 causes children to shrink, probably unexpectedly
  - Sometimes you do want your children content to be the min-height, if you _want_ them to overflow their scrollable containe
  - Ohh, this is a perfect example! 🙏 So maybe it could be automatically set based on the parent overflow (and could be overridden if needed). Just thinking what the best happy path could be
