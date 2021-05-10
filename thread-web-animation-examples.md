---
title: thread-web-animation-examples
tags: [animation, examples, thread, web]
created: '2021-04-21T15:00:50.996Z'
modified: '2021-04-21T15:01:12.882Z'
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

# pieces

- ## 

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
