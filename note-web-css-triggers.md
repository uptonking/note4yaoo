---
tags: [css, web]
title: note-web-css-triggers
created: '2020-06-28T16:00:42.392Z'
modified: '2020-06-28T16:02:57.664Z'
---

# note-web-css-triggers

## CSS Triggers

- transform
  - Changing `transform` does not trigger any geometry changes or painting, which is very good. 
  - This means that the operation can likely be carried out by the compositor thread with the help of the GPU.
- opacity
  - Changing `opacity` does not trigger any geometry changes, which is good. But since it is a visual property, it will cause painting to occur. Painting is typically a super expensive operation, so you should be cautious.
  - Once any pixels have been painted, the page will be composited together.
- width
  - Changing `width` alters the geometry of the element. 
  - That means that it may affect the position or size of other elements on the page, both of which require the browser to perform layout operations.
  - Once those layout operations have completed, any damaged pixels will need to be painted, and the page must then be composited together.
