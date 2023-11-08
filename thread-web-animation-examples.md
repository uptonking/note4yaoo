---
title: thread-web-animation-examples
tags: [animation, examples, thread, web]
created: 2021-04-21T15:00:50.996Z
modified: 2021-04-21T15:01:12.882Z
---

# thread-web-animation-examples

# repeat

- ## Proof of concept: Spring animations with WebAnimations API
- https://twitter.com/mattgperry/status/1385937499478974465
  - This is driven synchronously by Popmotion, although there's downsides there's also a lot gained from this kind of approach. 
  - Pros/cons in the sandbox comments 
  - https://codesandbox.io/s/proof-of-concept-spring-animations-using-webanimations-api-2x6b5?file=/src/index.js
- pros
  - Minimal JS overhead, single animation to drive multiple values
  - Leverage browser interpolation rather than BYO (smaller bundle size)
  - Fallback to off-thread WebAnimations API for normal animations
- cons
  - No synchronous access the values makes this no good for useTransform or layout animations
  - No transferring velocity between animations. What is velocity anyway without direct access to the current interpolated values
  - Unclear how to support overshoot for more complex values (eg calc(50vw - 50%))
  - Synchronous JS. Less overhead than Framer Motion (1 animation per value) but not off-thread like WAAPI.
  - Every con is also currently true of Animation Worklet .
- Have you tried animation worklets?
  - Yeah there's some experimental code in Popmotion from my hacking around.if we're going off-thread I'd rather a very low level, Reanimated 1-style API to start
- Great work! Such a shame there's no perfromant physics animation API baked into the platform.
- Interesting. WAAPI is great because literally no work is happening on the main thread. Repeatedly setting currentTime on the main thread looks no different from just using JS for everything. Why would I want to do it this way?

- ## The Math behind animations is a new series that explores the simple and yet powerful mathematical tools that are used in everyday apps. 
- https://twitter.com/wcandillon/status/1418810474045583366
  - 动画中的数学，以react native动画为例，
  - 动画示例做得很棒
# discuss
- ## 

- ## Responsive login form with fun animation Using HTML, CSS and JS.
- https://twitter.com/viki_code/status/1721979187127353709
  - https://codepen.io/viki-code/pen/rNPjzpX
  - 眼睛跟随鼠标的动画

- ## Animating clip-paths on layers of images makes really interesting page transitions!
- https://twitter.com/crnacura/status/1719413040947372420
  - [Image Layer Animations with Clip-Path | Codrops](https://tympanus.net/codrops/2023/10/31/image-layer-animations-with-clip-path/)

- ## Today we have some ideas for speedy layered image animations for page transitions using clip paths
- https://twitter.com/codrops/status/1719374467548242383
  - [Image Layer Animations with Clip-Path](https://tympanus.net/codrops/2023/10/31/image-layer-animations-with-clip-path/)

- ## Polishing case study transitions with all plain JavaScript
- https://twitter.com/michalzalobny/status/1718922552523866426
  - https://github.com/michalzalobny/plain-page-transition
  - [Case Studies](https://zesty-cocada-b5eb44.netlify.app/)

- ## 🌰 How does Stripe do that really cool morphing animation with their menus?
- https://twitter.com/Steve8708/status/1719083969931882597
  - See how to easily replicate it with React, Tailwind, and AI
  - [Make an Animated Menu like Stripe with React, Tailwind, and AI](https://www.builder.io/blog/stripe-menus)

- ## You can use @sveltejs crossfade to transition item from 1 layout to another
- https://twitter.com/lihautan/status/1274876595170238465

- ## What are the best examples of web apps you've used that have great, thoughtful animations/motion design?
- https://twitter.com/DavidKPiano/status/1524477381288812544

- ## Animated effect, but a square mask! 
- https://twitter.com/argyleink/status/1437769098742538242
  - This mask is fit dynamically to a hovered || tapped DOM element 
  - https://codepen.io/argyleink/pen/jOwwWOb
  - 长按时会聚焦到当前元素，其他所有元素都会被mask蒙版样式覆盖

- ## You can actually achieve spring animations using the WAAPI. 
- https://twitter.com/okikio_dev/status/1415314400253206528
  - https://codepen.io/okikio/pen/abJMWNy
- The demo uses [@okikio/animate](https://github.com/okikio/native/tree/master/packages/animate), but you don't really need it to creative spring animations
  - https://okikio.github.io/native/demo/animate.html
  - It utilizes the Web Animation API to deliver butter smooth animations at a small size, it weighs ~11.6 KB
  - In @okikio/animate, I create tweenAttr which used WAAPI together with rAF to emulate individual transforms for svg and other attribute transforms

- ## Animated draggable playing cards stack made with @framer motion.
- https://twitter.com/kaestner_felix/status/1391470242338164737
  - https://codesandbox.io/s/framer-motion-cards-4bqbn

- ## A map of the best  animation Libraries of #javascript and #css3
- https://twitter.com/Lindsey_design/status/1388244530831446017
  - Where is AnimeJS and Framer motion?

- ## This is how we created “Traveloop”. Animating basic shapes in After Effects and then creating the 3D look inside Cinema 4D
- https://twitter.com/MestreMotion/status/1387125087871062020
  - 同一对象运动动画的3d版和2d版，主要是形状渐变

- ## I'm *thrilled* to announce I'm joining @greensock as the 'Lead bestower of animation superpowers'.
- https://codepen.io/cassie-codes/pen/ExZpRwO
- 袜子出口处的撒花庆祝效果
