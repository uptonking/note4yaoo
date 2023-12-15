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

- ## 🤔 How do you control the children tabindex?
- https://twitter.com/devongovett/status/1735457449199419758
  - We don’t! The toolbar keeps track of its last focused child and marshals(带领；引领) focus back to it when tabbing in from the outside. There's also a Tab key handler that moves focus out of the whole toolbar.
- Have you noticed any drawbacks with that method compared to using roving tabindex?
  - One more theoretical drawback would be if there was hardware that didn't send Tab key events but still used tabindex for navigation, we wouldn't know about this and the browser couldn't handle it for us. But we haven't encountered this situation yet. 
  - We've used the same approach in our tables/grids to allow arbitrary focusable children for a few years now and haven't had any complaints.

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
