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

- ## Braid uses arrays for responsive props, but I've realised objects are much better:
- https://twitter.com/markdalgleish/status/1362779695683543041
  - No need to plug holes with null, e.g. ['small', null, 'large']
  - Adding new breakpoints between existing ones isn't a breaking change
  - Types are simpler, e.g. `Partial<Record<Breakpoint, Space>>`

- Once you add it all up, I feel like it's tough to argue for responsive prop arrays over objects.
- I've been leaning on a more CSS approach recently either through a mediaQueries/variants prop:

``` jsx
<Stack
  direction="column"
  mediaQueries={{ 'medium': { direction: 'row'  } }}
/>
```

  - More typing, but when you have a lot going on it's easier to discern IMO.

- Yeah, I believe Chakra supports both so you get the simplicity of the array for simple cases and the advantages you mention for the more complex ones. 
  - Loses some of the typing simplicity benefit though.
- We use them in our custom component system.
  - Btw braid inspired us a lot when we started to draft layout components API, so thank you very much
- Agreed. We swapped early on and never looked back.
  - Objects are much easier to parse and read too imp
- A related question: Do you define those breakpoints in Braid, or do consumers define those? Or I suppose you could provide defaults they override in the theme.
  - They're defined in Braid.

- ## CSS question, for folks with a deeper understanding of browser mechanics than me: Is there a difference between “layers” and “stacking contexts”?
- https://twitter.com/JoshWComeau/status/1362073864495370240
  - As far as I can tell, they're synonyms used in different contexts — layers are mentioned in terms of animation performance, stacking contexts in terms of layout and z-index. But are they actually discrete concepts? If so, what's the distinction?
- Yes, any transform (or non-0 opacity) (i.e. on the h1) creates a stacking context which would normally stack above the list. 
  - However, `position: relative` explicitly stacks the list above the in-flow content (including that implicit context).
- I think stacking contexts don't get browser's GPU acceleration like composite layers
- it seems like if there is a difference, stacking contexts could refer to more rules than just layers. 

- ## The lesson: only use comma-separated selectors when those selectors have broad browser support. 
- https://twitter.com/JoshWComeau/status/1359213597331763200
  - When using browser-prefixed things, or cutting-edge stuff like `:focus-within` , you should repeat the rules instead.
- Here's what's going on: 
  - the comma operator is used to apply the same CSS rule to multiple selectors, but in order for it to work, *all selectors must be valid*.
  - When Chrome sees `-moz-range-track` , it doesn't recognize it, and it invalidates the *entire rule*.
- Firefox ignored but not fails on `-webkit-*` for compatibility reasons, since devs are/were littering their CSS with it and it was breaking sites in Firefox.

- ## print-to-pdf is almost good enough. Are there CSS tricks you can use to improve page breaks?
- https://twitter.com/Swizec/status/1358589201495728129
- There are a few things, you can force page breaks or try to prevent them inside specific elements (if possible) with "page-break-after" and "page-break-before"
- There is also "widows" and "orphans", which might come in handy
  - [Orphans and Widows in CSS](https://tosbourn.com/orphans-widows-css/)
  - Orphans are the lines of text that get left behind on an old page should a paragraph of text get split onto a new page.

- ## For an LTR layout, positioning an element outside its parent on the left side does not cause a horizontal scroll. 
- https://twitter.com/shadeed9/status/1358664786867798017
  - However, positioning the element on the right side does.

- ## Browsers have a built-in Dark Mode color scheme. 
- https://twitter.com/bramus/status/1358093784001740801
  - If you don’t change any of the default colors, you can have Dark Mode support by adding only this little piece of CSS:
  - `:root { color-scheme: dark light; }` .
  - To prevent a FOUC(flash of unstyled content), its recommended to use a meta tag for it though.
- [Improved dark mode default styling with the color-scheme CSS property](https://web.dev/color-scheme/)

- ## I got a question asking what I thought about CSS frameworks like Bootstrap.
- https://twitter.com/JoshWComeau/status/1357709670325059592
  - My answer: I do not suggest using them. Nor do I suggest using fully-styled component libraries like Material UI.
  - TL; DR — unless you’re building a short-term project (prototype, hackathon), CSS frameworks can be harmful, *increasing* the amount of time you need to spend on the UI. 
  - I recommend using a style-agnostic tool like Reach UI instead. 
  - Use third-party functionality, not styles.
  - A design is more than the sum of its parts. I can take a bunch of really-nicely-designed components and still wind up with a poorly-designed product. 
  - It’s been said that only Google can produce nice-looking Material Design apps, since their designers understand how to use it.
  - I teach at a bootcamp, and we strongly discouraged students from using fully-styled component libraries. 
  - Invariably, students would hit a point where they’d spend longer trying to override the styles/get it to work than they would have spent building it from scratch
  - Now there is one HUGE caveat here. I’m talking specifically about “styled” component libraries. 
  - Style-agnostic libraries like Reach UI, which focus purely on functionality, are a godsend and you should absolutely use them. 
  - Please don’t build your own modal from scratch.
  - I think if you’re a solo dev maker, investing in your design skills is the best thing you can do.
- 100 % agree. I think this is exactly why Material-UI is working on Unstyled Components in v5.
  - [[RFC] Material-UI v5:  Unstyled components](https://github.com/mui-org/material-ui/issues/20012)

- ## Today I looked into the performance of different layout modes in CSS. 
- https://twitter.com/JoshWComeau/status/1356377422925541377
  - I was curious if it takes the browser longer to lay out elements in a grid vs. Flexbox vs. flow layout.
  - TL: DR; they're all plenty fast, but there are small differences.
- For the benchmark, I created an app that renders 1000 random items, with a couple HTML tags in each one. I trigger a re-render, and measure how long it takes to recalculate layout.
- Regular flow layout. No CSS on the container.
  - I imagine this is the lowest it could be, since each element fills the available width. No "interplay" between children.
  - This will be our baseline!
- A flex column.
  - Very similar layout to the last element, except that margins don't collapse anymore.
- A flex row, with `flex-wrap: wrap` , and min/max sizes on children
  - This one requires a bit more computation, since the browser has to decide where the lines wrap.
- A 5-column grid.
  - I remember reading that CSS Grid could be slower in some circumstances, but it doesn't make a HUGE difference.
- I've seen a couple "CSS Grid is slow, use Flexbox instead" takes, 
  - and I feel much more comfortable now saying that you should ignore them Smiling face with open mouth and cold sweat the folks working on browsers are super smart 
  - and they wouldn't ship a layout method with huge performance problems.
- My takeaway: there is a cost when it comes to using dynamic layouts, but that cost is quite small in absolute terms.
  - Even on a low-end device, using Grid layout probably won't increase render times by a noticeable amount

- ## I'm working on a UI for a client project and wanted to share some CSS and SVG goodness.
- https://twitter.com/shadeed9/status/1353047713256882177
  - The requirement is to implement a dynamic tape element that can be colored, rotated, and sized. 
  - This is a very good use case for CSS and SVG. Isn't it?
  - https://codepen.io/shadeed/pen/OJRYaZK
- (1) I used Adobe Illustrator to group the tape into three layers. The base, white areas, and black areas. All of the layers have a semi-transparent background. This will help in making them *blend* with elements underneath them.
- (2) Then, I exported the SVG and placed the content within an `<def>` . This will help me in reusing the SVG in other pages without duplicating the code each time. Also, I used `fill: currentColor` to pass a custom color to each tape.
- (3) To make it easy to customize the tapes, I will use CSS variables as inline styles.
- (4) That's it. We created a dynamic tape that can be colored, sized, and rotated very easily. Thanks to CSS and SVG!

- ##  `--bg: ; /* with a space */` vs `--bg:; /* no space */` .
- https://twitter.com/MiriSuzanne/status/1352055999771787264
  - for `body { background: var(—bg, green); }` .
  1. A value of ‘ ‘ is valid but not a color, no background
  2. No value (eg ‘guaranteed-invalid’), fallback to green
- `--bg:;` is not a valid declaration, and is *ignored*

- ## CSS conic-gradient borders 
- https://twitter.com/argyleink/status/1282889809782927360
- https://codepen.io/argyleink/pen/pogZxaZ

- ## Did you know that you can make any element resizable, just like `<textarea>` ?
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
