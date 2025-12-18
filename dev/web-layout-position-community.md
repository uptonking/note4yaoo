---
title: web-layout-position-community
tags: [community, layout]
created: 2024-11-29T08:23:21.219Z
modified: 2024-11-29T08:23:36.849Z
---

# web-layout-position-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## CSS tip: Use `svh` to stop the mobile address bar from hiding your UI. It guarantees a perfect fit within the visible screen.
- https://x.com/denicmarko/status/2000919855877513483
  - Works in all modern browsers.
- For us Tailwind users: Always take in account safezones, just so you can stop hitting your head against the mobile UI perks

- There's the "small viewport" (svh = height, svw = width) or 'the usable real estate within the browser's chrome' ('chrome' being the term that indicates widgets that are part of the browser itself, not the page) There's "The Viewport" (which is the entire surface of the browser window below the title bar) (vh/vw) and there's the Large Viewport (aka 'full screen size') which are referred to by 'lvh and lvw'. There's also the 'dynamic viewport' (whose respective dimensions are dvh and dvw) which is just the visible section of the small viewport.

- `dvh` is also pretty cool it auto switch between svh (small view height) and lvh (large view height) for a more Dynamic content when web ui appears / disappears

- ## 🤔 [css - Why does an absolute position element wrap based on its parent's right bound? - Stack Overflow](https://stackoverflow.com/questions/24307922/why-does-an-absolute-position-element-wrap-based-on-its-parents-right-bound)
- The width of an element always respects its containing block. 
  - If the element is absolutely positioned, then its dimensions can be constrained by top, right, bottom and left, 
  - but as long as its width is `auto` then it must still be constrained to the width of its containing block (making it no different from in-flow block boxes in that respect), which in your case is its absolutely-positioned parent. 
  - There isn't really any other element whose constraints the absolutely-positioned element could size itself with respect to without compromising the flow of its text.

- ## 💡 [width: 100% of an absolute positioned element is bigger than the parent - Stack Overflow](https://stackoverflow.com/questions/49209970/width-100-of-an-absolute-positioned-element-is-bigger-than-the-parent)
- 📌 absolute定位元素的width若为百分比，则其width相对于第一个positioned祖先元素计算百分比，而不是相对直接父元素计算百分比
- By making any element `position: absolute;` means: place me to the first parent that is `position: relative;` (to the first ancestor positioned (relative, absolute or fixed)) which is not always equal to its parent element.

- In the child element, instead of using height:100% use top:0; bottom:0; to fill up height, and left:0; right:0; to fill width up.
