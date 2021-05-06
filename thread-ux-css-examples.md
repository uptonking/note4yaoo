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


- ## I've been enjoying playing with some variable fonts this eve.
- https://twitter.com/piccalilli_/status/1390053832814563330
  - https://codepen.io/piccalilli/pen/XWMWpzy
  - 字体变化

- ## HSL Palette Generator: Generate CSS custom properties for a color palette
- https://twitter.com/jh3yy/status/1387153018764898312
  - https://codepen.io/jh3y/pen/rNjbmBQ
  - 通过滑动条选择范围，批量生成hsl和steps
  - This is an update to my "50 Shades of Hue" demo that now allows you to configure a "Hue" range too

- ## make focus a little more engaging
- https://twitter.com/argyleink/status/1387072095159406596
  - prefers-reduced-motion: no-preference
  - https://codepen.io/argyleink/pen/JjEzeLp
  - 使用按键移动焦点时，元素外框出现波纹动画
- Is there a way to preserve the nicely rounded corners when supplying your own outline style (e.g. to compensate for a background color) in Chrome or am i just out of luck?
  - FocusRing: The discord accessibility team built a library so we could use another element to position and style focus rings correctly. It’s solved a number of issues and it looks great for users who need them

- ## I made a Mac mini with HTML & CSS.
- https://twitter.com/_georgemoller/status/1388528849600847874
  - https://codepen.io/george2106/pen/MWJdQYV?editors=1100
- Neither are real. They are both just pictures produced by pixels on our screens. To see a real one, you need to see it in real life.

- ## I tried making the purple iPhone with CSS: Mine vs the real pic
- https://twitter.com/ece_minaa/status/1386335568548831237
  - https://codepen.io/ece_mina/pen/poRGeKO?editors=1100

- ## Tuggable Lamp
- https://twitter.com/jh3yy/status/1385764359490703366
  - Playing with animated SVG on today's stream
  - @greensock (Draggable && MorphSVG)
  - https://codepen.io/jh3y/pen/mdRaNgM
  - 拉亮台灯的效果

- ##  `<datalist>` HTML element - useful for adding input suggestions with 0 javascript
- https://twitter.com/swyx/status/1260199927856001024
- I learned “the opposite”. 
  - I once tried to render ~100.000 options in a datalist using nextjs. 
  - Only to see each key press taking 5 secs to show 😂. 
  - Then I thought “maybe I need something else”. 
  - But datalist is awesome (in fact I would find it a lot harder to do that in js).
- Now try to put a image!!!... Don't work!
- `<datalist>` is well supported on mobile too. The only downside is that they are hard to style
- This is a similar idea to the `<optgroup>` tag

- ## Made a 10 line polyfill for flexbox gap.
- https://twitter.com/devongovett/status/1244679626162450432
  - You can use it just like normal CSS properties. No extra wrappers around each item, or spacer elements needed. 
  - https://codesandbox.io/s/gallant-monad-p8jpv
  - CSS custom properties are super powerful!
  - `<div class="flex" style="--gap: 10px; ">`

- ## Evening Lanterns
- https://twitter.com/BraydonCoyer/status/1291085918183489537
  - https://codepen.io/braydoncoyer/pen/NWqaBmK
  - 放孔明灯的效果

- ## The `--var: ;` Hack to Toggle Multiple Values With One Custom Property
- https://twitter.com/MiriSuzanne/status/1380635887705284613
  - https://codepen.io/mirisuzanne/pen/qBRpard?editors=1100
- I made a quick demo sometime ago that demonstrates how you can change a property's value depending on whether or not a custom property was space-toggled.
  - https://codepen.io/uptonking/pen/poRazzY
  - 若css vars为空，则含有该值的属性也无效

- ## Menu Button Interaction
- https://twitter.com/aybukeceylan/status/1380920082822524937
  - https://codepen.io/aybukeceylan/pen/zYNpWdj
  - 类似fab圆形浮动菜单

- ## full-screen scroll-snap starter? 
- https://twitter.com/argyleink/status/1380552877467336710
  - https://codepen.io/argyleink/pen/qBRpdEr
  - 竖向多个满屏内容，自动滚动到满屏状态
- one suggestion: make it `min-block-size: 100vh` , so you don't get scrollbars on every section on short screens/large user font settings.

- ## The Impossible Checkbox 🐻
- https://twitter.com/jh3yy/status/1295782167977615361
  - @reactjs && @greensock
  - https://codepen.io/uptonking/pen/xxgrpgL
  - /amazing/超级可爱

- ## In 2021 it's Easier to designed #HTML native Checkboxes while using
- https://twitter.com/eladsc/status/1378640452807704582
  - "::before" pseudo-element of the checkbox
  - 'all: unset' on the checkbox for resetting to the base styles of #CSS
  - https://codepen.io/elad2412/pen/jOymRJy

- ## Swag 卡通人走路
- https://twitter.com/rolivaalonso/status/1375439896756813825
  - https://codepen.io/ricardoolivaalonso/pen/bGgEQLL

- ## 50 Shades of Hue. Generate monochromatic HSL color palettes for your CSS 
- https://twitter.com/jh3yy/status/1374499978039631879
  - Made some updates to that color picker
  - Built with @reactjs , @prismjs , && @skypackjs
  - https://codepen.io/jh3y/pen/xxgbvPz

- ## Use HSL to generate shades. Store in CSS variables 
- https://twitter.com/jh3yy/status/1374142406023610369
  - https://codepen.io/jh3y/pen/JjEjJjN
- Often times HWB and LCH can be more intuitive, hue-centric representations of color and are a part of the CSS4 Color spec. So coming soon.
- https://github.com/caub/color-tf
  - Color transforms between RGB, HSL, HSV and HWB, and more
- LCH
  - https://css.land/lch/

- ## Color picker animation 
- https://twitter.com/mironcatalin/status/1374306238499061761
- Done using Moti by @FernandoTheRojo powered by Reanimated2 by @swmansion & @kzzzf , built with @expo .

- ## project || prototype starter styles:
- https://twitter.com/argyleink/status/1371850967822520333
  - normalize box sizing
  - zero out margins
  - document & body fill viewport
  - use OS system font
  - https://codepen.io/uptonking/pen/QWGRyrX
  - 简单的落地页，文字水平竖直居中
- there's more to reset and/or normalize in a page, but it can get complex quickly and tradeoffs start to happen. 
  - the above is generically stable for my projects; a sturdy foundation.
- Not fond of the `position: relative` by default 
  - because I’ve often needed to break out of 2-3 ancestors to absolutely position something relative to their 3th or 4th ancestor. 
  - In React Native you can’t do that, so you have to change your structure significantly instead.

- ## New CSS @​scroll-timeline demo!
- https://twitter.com/bramus/status/1370466149536763905
  - Experimental technology: Chrome with “Experimental Web Platform Features” enabled only for now
  - https://codepen.io/bramus/pen/GRNNjqz
- While we translate the `<figure>` elements on scroll, they're not the drivers of the animation. Instead, it's the position of their parent `<section>` that controls their animation progress (e.g. “Element-based Offsets”)

- ## You can create carousel using 2 lines of CSS
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

- ## 实现div-border-collapse效果的方法
- https://stackoverflow.com/questions/17915865/how-to-make-borders-collapse-on-a-div
- 不要使用display:table-cell，表格布局在频繁操作动态样式时性能差
- 使用负值margin
  - http://jsfiddle.net/6eGdN
  - 通过父边框挡住子边框实现，或全部显示子边框

``` css
    div.gridcontainer {
      width: 7/86px;
      line-height: 0;
    }

    div.griditem {
      display: inline-block;
      border: 1px solid black;
      width: 18px;
      height: 18px;
      margin-left: -1px;
      margin-bottom: -1px;
    }
```

- 使用父边框上左，使用子边框右下，也可交换

``` css
  div.gridcontainer {
    width: 76px;
    line-height: 0;
    border: solid black;
    border-width: 1px 0 0 1px;
  }

  div.griditem {
    display: inline-block;
    border: solid black;
    border-width: 0 1px 1px 0;
    width: 18px;
    height: 18px;
  }
```

- use box-shadow instead of using border 
  - https://codepen.io/savehansson/pen/rsIEp
- add a left and bottom border to the ul and drop it from the li
