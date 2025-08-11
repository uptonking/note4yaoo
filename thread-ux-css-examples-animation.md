---
title: thread-ux-css-examples-animation
tags: [animation, codepen, examples, thread, ux]
created: 2022-11-21T15:25:52.884Z
modified: 2022-11-21T15:27:20.974Z
---

# thread-ux-css-examples-animation

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## Animating from `scale(0)` usually feels "off". Try animating from a higher initial scale instead (0.9+).
- https://x.com/emilkowalski_/status/1954891053032755560
  - It helps it feel more gentle and elegant.
  - Here's the difference between initial `scale(0)` and `scale(0.93)`

- It's combined with a fade in/out animation right?
  - Yes, custom `ease-out` easing, 125ms duration, opacity 0 → 1. 
  - @lochieaxon has made a nice site with easings that can help you make your animations look great - https://easing.dev.

- After several tries, I agree 0.9+ is the sweet spot! ~0.95+ for larger modals/windows

- 0.7 would be even better imho
# examples-loading/progress
- ## 

- ## 

- ## 4 lines of JavaScript. Zero dependencies.
- https://x.com/crutchcorn/status/1774695605455224871
- stroke-dashoffset from 0% to 100%?
  - Yup! Tied to scroll via CSS variable and a JS listener

- ## one way to animate borders with CSS: animate an element along the border of another and mask it
- https://x.com/httpfleck/status/1894866501049430457
  - offset-path: border-box; 
  - https://codepen.io/andrewf3009/pen/oNrxXKP

- ## Steps animation
- https://x.com/ln_dev7/status/1928457950152077492

- ## A mix of clip path and CSS transitions
- https://x.com/emilkowalski_/status/1901689149154869746
  - here's a path animation variant

- ## Animated hero
- https://x.com/lostdoesart/status/1902386317889098066
  - 流程图的连线会显示流动动画

- ## animate an element along the border of another and mask it 
- https://x.com/jh3yy/status/1894787364762812778
  - `@​keyframes trail { to { offset-distance: 100%; }}`

- ## 🚝 css Marquee 火车移动效果
- https://x.com/anatudor/status/1832819142061154486
  - requires knowing number of items + all items having same width with a fixed minimum
  - uses an SVG filter and doesn't have any of the restrictions above, but hits 
  - [Marquee! - Ko-fi](https://ko-fi.com/post/Marquee-M4M0132D70)
  - https://codepen.io/thebabydino/pen/bGPzdaM
  - https://codepen.io/t_afif/pen/MWZxXWB

- ## Conic gradients can be so beautiful.
- https://twitter.com/JoshWComeau/status/1367492015836049413
  - This wonderful tool shows us a few dozen great examples, and features 1-click CSS copy-to-clipboard 
- https://conic.style/

- ## CSS conic-gradient borders 
- https://twitter.com/argyleink/status/1282889809782927360
- https://codepen.io/argyleink/pen/pogZxaZ

- ## Create this beautiful button with SVG animation using HTML and CSS
- https://x.com/davidm_ml/status/1835613558664495571
  - 围绕边框的亮线动画

- https://x.com/Ibelick/status/1843236886636265601
  - Just added the classic Border Trail to motion-primitives.
  - An animated border that adapts to any container, easy to stylize, update the transition, and more.

- ## 💫 I love this cool effect with CSS Conic gradients
- https://x.com/wesbos/status/1828528779544719707
  - https://codepen.io/wesbos/pen/PoraMVV
  - 围绕边框的亮线动画
- No need for any nesting/ pseudos. Make the `conic-gradient()` relative to `border-box` and restrict main button background layer to `padding-box` .

- ## progress bar, infinite
- https://codepen.io/LauraBizzle/pen/wvEMqVN
- https://codepen.io/artboardartisan/pen/VLzKVN

- non-infinite
  - https://codepen.io/pixelsultan/pen/ZKqvyx
# ux-examples
- ## 

- ## 

- ## You can use spring animations with vanilla CSS, no JS motion library needed. Browser support is solid, around 90%. 
- https://x.com/serhii_be/status/1915850431990821093
- Only downside is they’re not interruptible.

- ## tooltip timing - a button concept
- https://x.com/argyleink/status/1824479024254685308
  - 先出现hover动画，结束后再出现tootlip，纯css实现
  - https://codepen.io/argyleink/pen/bGPaxVp
  - animated conic gradients with at-property

- ## 多列卡片分别滚动
- https://x.com/lostdoesart/status/1821491304192229720
  - I made it with @jittervideo
  - Jitter to make a proof of concept, then I'll use Rive to add it to the site

- ## 滑块滑动跳跃
- https://codepen.io/ste-vg/pen/OEbYqZ

- ## 💫 Staggered Animation - CSS 逐行显示动画
- https://x.com/alirdev/status/1817923525002530819
- I once recorded a video for a text reveal usiwng this same approach
  - [JS Text Reveal Effect - YouTube](https://www.youtube.com/watch?v=PMiVFXZpYQo&t=140s)
- I made a video a while ago that explains this technique
  - [Css: Scoped variables - YouTube](https://www.youtube.com/watch?v=cXM0SZeWjd4)

- ## fab 浮动菜单按钮 
- https://x.com/Ibelick/status/1799787095462236612
  - Made in the browser with SVG filters, linear() easing function, and (Tailwind) CSS  
  - [Gooey Menu](https://www.ibelick.com/lab/gooey-menu)

- ## 💫 4 lines of JavaScript. Zero dependencies.
- https://twitter.com/crutchcorn/status/1774695605455224871
  - 渐变的彩色边框线
  - https://gist.github.com/crutchcorn/e97804c1061d07d18df5e7a7110ef450

- ## Pacman loader con SVG y CSS
- https://twitter.com/carmenansio/status/1773032297303835006
  - https://codepen.io/carmenansio/pen/RwLvxEr
  - 圆脸张嘴吃弹珠的动画，无js

- ## Make your CSS animations stand out by using the `linear()` easing function to create more complex animation curves that can mimic bounce and spring effects.
- https://twitter.com/joyofcodedev/status/1772639782553669673

- ## 💫 combine it with CSS scroll-driven animation
- https://twitter.com/jh3yy/status/1770603402923225175
  - 图片挤压文字的动画效果
- https://twitter.com/jh3yy/status/1772702339389923355
  - https://codepen.io/jh3y/pen/ZEZJYVe

- https://twitter.com/jh3yy/status/1772705093546107377
  - The CSS trick here is using custom properties to drive your CSS animation behavior
  - Doesn't have to be a scroll animation

- https://twitter.com/jh3yy/status/1771294048889786389
  - Custom property powered responsive scroll animations with CSS
  - https://codepen.io/jh3y/pen/JjVRGwR

- ## Create this beautiful sound wave using just HTML and CSS 
- https://twitter.com/davidm_ml/status/1763530731337257266
  - https://github.com/atherosai/ui/tree/main/animation-01

- ## 🌰 You can do blobs with CSS filter but it only works as black or white as far as I know but you can use SVGs to achieve the result you want.
- https://twitter.com/joyofcodedev/status/1754218335405736273
  - As a Svelte component
  - 颜色渐变，通过blur来渐变形状、文字
  - https://svelte-ux.techniq.dev/docs/components/Gooey
- You can gradient them & all as in this talk I gave four years ago
  - https://codepen.io/thebabydino/project/full/ZjwjBe

- ## Create this SVG animation using just HTM and CSS 动态边框线
- https://twitter.com/davidm_ml/status/1753015956119449862
  - https://github.com/atherosai/ui/tree/main/animation-02

- ## You can create this sparkly backdrop with a single element using mask-composite whilst animating the mask-position
- https://twitter.com/jh3yy/status/1722397114532048959
  - https://codepen.io/jh3y/pen/ExrWOJe

- ## Here’s a quick tutorial on how to create the popular shimmer effect on the @linear website using @framer .
- https://twitter.com/jurrehoutkamp/status/1630213441901264903
  - https://www.youtube.com/watch?v=HDYoDRg-nGA
  - https://shimmer.framer.wiki/

- ## A grid rotation concept
- https://codesandbox.io/s/grid-rotation-concept-lnuld6?file=/src/index.tsx

- ## Turn any content into an infinite grid! @framer-motion @chakra_ui
- https://twitter.com/austin_malerba/status/1609915292095860740
  - https://codesandbox.io/s/infinitegrid-rtuh7b

- ## I have a thing for day/night demos
- https://twitter.com/WalterStephanie/status/1533690417736306690
  - https://codepen.io/TurkAysenur/pen/bGawdKv?utm_source=swlinks-tw

- ## We can use % values for positioning animations on timelines.
- https://twitter.com/cassiecodes/status/1405254957507428353
  - https://codepen.io/GreenSock/pen/PopXddg
  - 依赖gsap、vue，实现刻度进度的显示

- ## Infinity Squares 
- https://twitter.com/jh3yy/status/1368647671381188608
  - https://codepen.io/jh3y/pen/xxRaoKP
  - 方形旋转一圈回原点，基于GSAP
- This would be perfect for a loader

- ## Skateboard-Like Preloader
- https://twitter.com/jonkantner/status/1502270615998369793
  - https://codepen.io/jkantner/pen/abEoyeK

- ## 流星雨扑面而来的效果
- https://codepen.io/danwilson/pen/qGdJGq

- ## Segmented Progress Bar
- https://twitter.com/jonkantner/status/1418182789493571587
  - https://codepen.io/jkantner/pen/poPWVbV
