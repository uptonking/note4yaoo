---
title: thread-ux-css-examples
tags: [css, examples, thread, ux]
created: '2021-02-05T13:56:42.396Z'
modified: '2021-02-05T14:00:02.922Z'
---

# thread-ux-css-examples

# ux-dev-examples

- css firework

- ## 

- ## - You can create carousel using 2 lines of CSS
- https://twitter.com/Prathkum/status/1370185869127249921
  - https://codepen.io/prathamkumar/pen/bGBOzXj
- The :hover selector changes the CSS when a mouse hovers over the element. I had issues too so I used JS to help. 

- ## This is my implementation of @AndrewGlassner 's glob shape
- https://twitter.com/steveruizok/status/1369756871041683457
  - https://4qr7f.csb.app/
  - https://codesandbox.io/s/glob-4qr7f
- I think this is the strategy used by @GoodNotesApp for their lines (which are great btw). Those look like globs to me. 👀 And they erase well—glob by glob.
- The first challenge: the points of a glob need to be far enough away from each-other to allow us to draw tangents between them. (If the handles end up inside of the circles, the glob breaks.) We'll need to lose points, but we still may need those points to inform the curve.
- TIL about Glob! Thinking of using them in your drawing tool? What's the application? Other than being somehow adorable
  - Yeah, I think we can link them together to create dynamic lines! (Also, you can spin those circles and curves if you want to try this in 3D! See the link at the bottom of the demo.)

- ## For those unfamiliar with negative margin magic, check out the comparison
- https://twitter.com/hexagoncircle/status/1288510365756612608
  - Flexbox gap = less HTML elements, less CSS tricks, and cleaner, easier to manage code to get the job done
  - https://codepen.io/hexagoncircle/pen/oNbrbjP

- ## Infinity Squares 
- https://twitter.com/jh3yy/status/1368647671381188608
  - https://codepen.io/jh3y/pen/xxRaoKP
  - 方形旋转一圈回原点，基于GSAP
- This would be perfect for a loader

- ## Conic gradients can be so beautiful.
- https://twitter.com/JoshWComeau/status/1367492015836049413
  - This wonderful tool shows us a few dozen great examples, and features 1-click CSS copy-to-clipboard 
- https://conic.style/

- ## there is an excellent reason to use #CSS Position Sticky with top and bottom combined if the sticky element is stacked in the middle
- https://twitter.com/eladsc/status/1367047171078582273
- https://codepen.io/elad2412/pen/ExNKLbrz

- ## Pure CSS Wardrobe using `<details>` && `<summary>` .
- https://twitter.com/jh3yy/status/1365782898662662147
  - css实现开门关门
  - https://codepen.io/jh3y/pen/BaQrKxp

- ## Just a couple of floating squares playing Table tennis with pure CSS.
- https://codepen.io/amit_sheen/full/PobQjMX

- ## Opposing corner radial gradients look softer than angled linear gradients:
- https://twitter.com/argyleink/status/1295745027063218176
  - https://codepen.io/argyleink/pen/ExKyMeZ
  - [linear vs radial](https://codepen.io/obvi_as/pen/abNmvoz?editors=1100)
-  I've been loving https://uigradients.com recently 
- omg this is so true and i never thought of it! so simple! 
  - i made a comparison based off your pen

- ## CSS 404 Concept Page
- https://twitter.com/jh3yy/status/1363238109413052423
  - Using "at-property" to animate background clipped text
  - https://codepen.io/jh3y/pen/MWbvzKb

- ## 4 layouts for the price of 1, thanks flex
- https://twitter.com/argyleink/status/1217213431947747328
  - https://codepen.io/argyleink/pen/LYEegOO
- You may also like CSS Grid for such responsive permutations
  - https://codesandbox.io/s/responsive-form-fikwv

- ## Digging this fluid-type implementation
- https://twitter.com/JoshWComeau/status/1362128684639940608
  - [Fluid typography with CSS clamp](https://piccalil.li/tutorial/fluid-typography-with-css-clamp)
- I’m a big fan of clamp()
  - it’s decent at doing what I like to do the most with CSS: 
  - let the browser do its job with some hints at how to do it. 
  - It also provides just the right amount of control, which is handy for layout elements, too.

- ## A table that has a sticky header *and* a sticky first-column. 
- https://twitter.com/JoshWComeau/status/1361741382759636993
  - Pure CSS solution too, via `position: sticky` and some clever stacking orders. No JS required!
  - [A table with both a sticky header and a sticky first column](https://css-tricks.com/a-table-with-both-a-sticky-header-and-a-sticky-first-column/)
- I used this solution in a project with a large table for mobile. It’s a little difficult to use, but do the job.

- ## Generate abstract geometric art using a delightful free tool. Includes 11 different styles and a ton of customization.
- https://twitter.com/JoshWComeau/status/1359399954347929604
  - https://tabbied.com/select-artwork 
  - 源码基于nextjs，超级适合用来制作logo
- That is cool. But I hoped for an svg export though.
-  I poked at it and it’s built using standard HTML nodes rather than SVG, so it makes sense that it can only export png

- ## Properties like `z-index` can be used in your transitions and keyframe animations! 
- https://twitter.com/JoshWComeau/status/1358128488071507969
  - They'll step between values at the right time, helping you orchestrate effects like this.
  - [The Surprising Things That CSS Can Animate](https://codersblock.com/blog/the-surprising-things-that-css-can-animate/)
  - https://codepen.io/uptonking/pen/OJbNgLd
  - 卡片切换时使用图层交错的效果

- ##  Tweak numbers to create neat-o shapes, and then nab the CSS to generate them.
- https://twitter.com/JoshWComeau/status/1357033108898410496
  - https://codepen.io/yuanchuan/pen/QWGWXPz
- Because it's `clip-path` , it can be applied to your images, HTML nodes, anything!
  - No more weird border hacks for basic shapes

- ##  Focus outlines are important for accessibility, but they can't be rounded. Simulate 'em with box-shadow!
- https://twitter.com/JoshWComeau/status/1356713502954635274
  - https://codepen.io/joshwcomeau/pen/LYbEQMa
- Don't forget a little dash of `border: 2px solid transparent` for Windows High Contrast Mode support!
- I remember hearing from @adamwathan this wasn't great for accessibility (in high-contrast mode on Windows or something?)
  - It’s totally ok but just have to make sure you don’t use `outline: none` to hide the browser focus style. 
  - Use something like `outline: 2px dotted transparent` instead, invisible to regular users but WHC will ignore transparent and show a real color 

- ## Pure CSS/SVG Tic Tac Toe 2021 
- https://twitter.com/jh3yy/status/1355625929968640000
  - https://codepen.io/jh3y/pen/KKNwpzN

- ## I made a new piece with just #css & html - Ring Doorbell. 
- https://twitter.com/KassandraSanch/status/1336789953821478913
  - Can you tell which one is code and which one is an image?
  - https://codepen.io/kassandrasanch/pen/oNzzMjr?editors=0100
- And I figured out one little difference between A and B. 
  - B have a rounded corners on bottom! 
  - so i check on your code, you made that rounded corner. 
  - So I guess B is Art and A is image

- ## New scroll-animations demo: A (contact) list where items that come into view fly-in.
- https://twitter.com/bramus/status/1352506087304540161
- [CSS-only with @​scroll-timeline](https://codepen.io/bramus/full/bGwJVzg)
  - 需要chrome 89，并且开启特性
- [JavaScript Web Animations API (WAAPI) + ScrollTimeline](https://codepen.io/bramus/full/ExgJPjM)
- Key part is setting `endScrollOffset` to edge `end` + offset `1`

- ## an interactive CSS box model experience
- https://twitter.com/argyleink/status/1355161023221813250
  - 显示box model的三维效果
  - https://codepen.io/argyleink/pen/BaLedvd

- ## [Do you have a portfolio website? Share it below](https://twitter.com/study_web_dev/status/1349218005406916608)
- https://www.colecaccamise.com/
  - theming-黑白，基于bootstrap，但视觉上难以察觉
- https://sosplush.github.io/
  - theming-淡黄
- theming-黑暗
  - https://usmahm.github.io/
  - https://tutul.netlify.app/
  - https://www.rahulmahesh.me/
  - https://ishaan28malik.github.io/champion-runner-home/
  - https://divymr.tech/
  - https://abdulsalam.netlify.app/
