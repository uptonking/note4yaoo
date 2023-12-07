---
title: thread-web-a11y
tags: [a11y, keyboard-event, web]
created: 2023-12-02T09:28:16.180Z
modified: 2023-12-02T09:28:47.243Z
---

# thread-web-a11y

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## Checking if an element has `visibility: hidden` with `checkVisibility()` , but not if the opacity is 0:
- https://twitter.com/RogersKonnor/status/1732066220348735681
  - `el.checkVisibility({ checkOpacity: false, checkVisibilityCSS: true });` .
  - Why? Tab order. 
  - An element with `visibility: hidden;` is removed from the tab order. 
  - An element with `opacity: 0` is left in the tab order. 
  - Focus traps are fun.

- ## If you do `<slot tabindex="-1"></slot>` , all slotted children are no longer focusable.
- https://twitter.com/RogersKonnor/status/1730697107231617073
  - But if you do: `<span tabindex="-1"> <slot></slot> </span>` , Everything works as expected
  - the "bug" / "issue" exists across the 3 browsers: Chrome / FF / Safari
