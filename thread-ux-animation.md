---
title: thread-ux-animation
tags: [animation, thread, ux]
created: '2021-01-06T14:39:01.923Z'
modified: '2021-01-06T14:40:55.495Z'
---

# thread-ux-animation

- ## Reasons why you should scale a pseudo-element on hover and not the element itself
- https://twitter.com/ericwaetke/status/1346791180940566528
  - you don't have these annoying hover glitches
- Just put all the styles you want to animate/transition in a pseudo-element!
  - doesn't really matter if you choose ::before or ::after, you need to adjust the z-index anyway!
- Just in case you don't know what "Boop" is yet, it's basically a fancier hover animation
  - [Boop! - A whimsical twist on hover transitions](https://www.joshwcomeau.com/react/boop/)
