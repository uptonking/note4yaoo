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

- ## 
- ## Did you know that you can make any element resizable, just like `<textarea>`?
- https://twitter.com/denicmarko/status/1351431494733062145
- it won't work without `p {overflow: auto;}`


- ## I remember hearing that it was safer to use numbered font-weights (eg. font-weight: 700 instead of font-weight: bold) because of a browser rendering bug.
- https://twitter.com/JoshWComeau/status/1351179391938813963
  - Does anyone remember what this was? Has it been fixed?
- That's because if a bold variant is not part of the font-face, the browser will try to make it bold by itself (Sometimes making the text look really ugly). 
  - But if the browser cannot find a numbered variant, it will just skip it and render the text at normal weight.
- Both tachyons and tailwind still use numbers for font-weights. I do, too.

- ## You can use the `:target` pseudo-class to create modals with zero JavaScript.
- https://twitter.com/denicmarko/status/1350761109360414721
- Only problem is accessibility. 
  - You still need JavaScript (I believe) to close the modal by pressing escape or clicking outside of it.
- you can't use anchors inside modals and you don't have control on it. 
  - For example updating aria attributes or activating the focus trap, because you don't know when it's open/closed
  - I made this long time ago to test this approach.
