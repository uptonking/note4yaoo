---
title: web-style-css-blog
tags: [blog, css, styling, web]
created: '2020-12-24T17:15:58.938Z'
modified: '2021-01-07T16:44:56.296Z'
---

# web-style-css-blog

# guide

# blog

## [Debugging CSS: Some Tips and Tricks](https://dev.to/sheelah_b/debugging-css-some-tips-and-tricks-bek)

- In this article I'll provide some strategies I've used for troubleshooting CSS when things are not working as expected
- **Generic Layout Issues**
- One of my most commonly used strategies when facing any kind of layout issue is 
  - to add an outline around a parent element's children. 
  - This lets me see whether the children are where I thought they would be and whether they have the expected dimensions. 
- If the layout issue is more complex and you need to debug the layout of the entire page, you can add outlines for every element on the page using different colors.
- An alternative strategy for debugging the layout of the entire page is to place a background color on all elements

``` CSS
.element {
  outline: 1px solid red;
}

[].forEach.call($$("*"), function(a) {
    a.style.outline="1px solid #"+ (~~(Math.random() * (1 << 24))).toString(16)
  }

) *:nth-child(n) {
  background-color: rgba(255, 0, 0, 0.2);
}
```

- **CSS Grid or Flexbox Issues**
- I like to take advantage of Firefox or Chrome's developer tools to help with these issues
- you can use the layout tab to inspect a grid or flex parent.
- Doing this can help you also discover any bugs caused by adding an extra wrapper div or element between your parent and child elements which can break your grid or flex layout.

- **Page Overflow Issues**
- For debugging an unexpected horizontal scrollbar, my favorite strategy is outlined here
  - [Finding/Fixing Unintended Body Overflow](https://css-tricks.com/findingfixing-unintended-body-overflow/)

- **Browser or Mobile-Only Bugs**
- It's worth testing the page out on other browsers and on a mobile device (especially on Safari mobile!) if you can. 
- If you're only seeing the issue on one browser, then you can narrow down the source of the bug.
- For example, I've regularly ran into flexbox issues that are Safari-specific. I
  - 've discovered these by testing in other browsers and confirming that the issue only shows up in Safari. 
  - A good reference of Flexbox browser-specific bugs is Philip Walton's flexbugs repo.

- **Typos**
- A useful strategy here is to use your browser developer tools to inspect the element of the page where you're seeing the bug. 
- If you see your rule there and it's crossed out, it's not getting applied.
- A preventative strategy here is to use a code editor that includes syntax highlighting for CSS, like VS Code.

- **Markup Issues**
- you can use your browser developer tools to inspect the element's markup and then verify that the expected class is applied to the element.

- **Animation and Transition Issues**
- my first strategy is always to greatly slow down the timing of the animation or transition. 
- That way I can watch as it runs, and it makes it easier to see both the start, end, and intermediate states.
- For animations, I also like to verify that I've specified the animation shorthand properties for time values in the right order
  - If the animation rule is crossed out, you'll know that there's likely a typo
- Another issue I've hit in the past is typos in animation keyframes which then cause the animation not to get applied.
- For animation debugging, I also like 
  - [Debugging CSS Keyframe Animations](https://css-tricks.com/debugging-css-keyframe-animations/)
