---
title: lib-react-preact-community
tags: [community, preact, react]
created: '2021-04-24T15:07:05.237Z'
modified: '2021-04-24T15:07:50.479Z'
---

# lib-react-preact-community

# repeat

- ## Preact works with both React and Web Component toolkits.
- https://twitter.com/munawwarfiroz/status/1378223550226653185
- We've been working on the second half of the rewrite of Preact's renderer. 
  - It adds support for pluggable component models (+better compat), improves average & worst-case performance, and provides a foundation for first-class asynchrony (+suspense) and new diffing modes.
  - Time is already being split between this large effort and WMR, which is a larger project than it seems at first glance (it includes what is essentially a light implementation of babel+JSX+rollup).
- I didn't check WC toolkits (duh, didn't think of that). Then the only way is to try them out. 
  - They don't explicitly write preact compatibility. 
  - Some toolkits like react-spectrum has documented the bugs with preact.
- afaiu spectrum is pretty new, so that may change. Though its size makes it a bit of an odd choice for preact apps (each spectrum component is larger than preact itself).
  - Seriously though, I think that’s how it should be. Preact is really just a thin layer on top of the DOM. Building actual components takes a lot of code, no matter the framework.
  - But also that’s not entirely true. Our components have a lot of overlapping pieces. One component may look large on bundlephobia, but most of the big pieces are shared between many different components, so it evens out in real apps.

# pieces

- ## 

- ## 

- ## 
