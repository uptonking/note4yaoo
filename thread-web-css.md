---
title: thread-web-css
tags: [css, thread, ux, web]
created: '2021-01-08T17:14:57.157Z'
modified: '2021-01-08T17:15:13.906Z'
---

# thread-web-css

# compatibility

- [Is Houdini ready yet？](https://ishoudinireadyyet.com/)
  - 各浏览器兼容性表格，标准状态、支持时间
- [WebKit Feature Status](https://webkit.org/status/)
  - CSS Typed OM Level 1: under dev
  - web animations api: supported since 14.0
  - CSS Animation Worklet API: under consideration
  - [WebKit CSS Feature Status](https://webkit.org/css-status/#)
  - [Features in Safari](https://developer.apple.com/safari/features/)

- clipboard only fully supported by Safari
- Typed OM & CSS Paint API only fully supported in Chrome
- bitmaprenderer, feature policy, & web locks experimental

# pieces

 

- ## You can use the `:target` pseudo-class to create modals with zero JavaScript.
- https://twitter.com/denicmarko/status/1350761109360414721
- Only problem is accessibility. 
  - You still need JavaScript (I believe) to close the modal by pressing escape or clicking outside of it.
- you can't use anchors inside modals and you don't have control on it. 
  - For example updating aria attributes or activating the focus trap, because you don't know when it's open/closed
  - I made this long time ago to test this approach.
