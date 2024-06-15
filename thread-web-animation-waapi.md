---
title: thread-web-animation-waapi
tags: [animation, thread, waapi]
created: 2021-09-22T04:12:55.839Z
modified: 2021-09-22T04:13:22.341Z
---

# thread-web-animation-waapi

# guide

# discuss-stars
- ## 

- ## 

- ## This test file demonstrates a pre-generated `keyframe` animation performing (literally) 100x slower in Chrome when it runs concurrently to another WAAPI animation or one running via `requestAnimationFrame` .
- https://twitter.com/mattgperry/status/1746173512669073680
  - [Pre-generated keyframes performance issues in Chrome](https://gist.github.com/mattgperry/454158ed97d5abeb3f4ed511264cbb64)
  - By JS animation I mean one that calculates a new value every rAF like GSAP. Adding a WAAPI animation on `opacity` was fine. But then adding a WAAPI animation on `background-color` with precalculated Keyframes triggered the poor performance. 
  - But then turning off either the JS animation or the opacity WAAPI animation made things normal again. 
  - the performance returns to normal when you remove either the `requestAnimationFrame` animation OR the second `WAAPI` animation. But when both are running performance tanks.

# discuss-comparison 🆚️
- ## 

- ## 

- ## Left: Web Animations API (21 FPS) vs Right: Anime.js v4 (59 FPS)
- https://x.com/JulianGarnier/status/1801603790719562047
  - Running animations on the main thread isn't always as bad as it may seem.

- In my tests I found that performance is generally fine as long as you only create a fixed amount of looped animations. But if you keep creating new animations with new values (like in the video) the performance drops considerably.
  - Might be related to parsing the values of the previously running animation 

- WAAPI seems to struggle after a certain amount of animations have been created. But I don't really know what exactly causes this performance drop.

- https://x.com/JulianGarnier/status/1801983161892475390
# discuss
- ## 

- ## 

- ## 

- ## JS animations can do things CSS can't, like animate independent transform axes with spring animations. 
- https://twitter.com/mattgperry/status/1733091360809304375
  - The problem is they need JS to download first. 
- In Framer, we inline a tiny script that can generate these spring keyframes and animate them on the GPU via WAAPI.
  - When React hydrates, Framer Motion creates animations for each transform. These can all be interrupted independently by hover effects etc
- We run the WAAPI animation for an extra frame that is meant to "paste over" the very heavy lifting that tends to happen in useEffect but this isn't always enough. So with v2 we carry on playing the WAAPI animation **and** create the independent JS animations. Why?
  - WAAPI animations override any changes to style so this animation is completely smooth even during a busy hydration. 
  - The key is, when we want to interrupt one of these transforms, only then do we cancel the WAAPI animation
- Any tiny mismatch in timing is much less noticeable here as it's a point of user interaction where some (or all) values are being interrupted.
  - Also by popping off the WAAPI animation to simply "reveal" the other transform animations we don't need any big changes in Motion

- ## Did you know @Framer Motion isn't just a React animation library? 
- https://twitter.com/mattgperry/status/1645797584999682058
  - I've quietly been building out a subset of APIs that can be used universally, on any page.
- I love http://motion.dev and just out of curiosity, is there anything that using framer on a vanilla JS @vite project can achieve that can't be done with motion one? Also, is there any possibility that in the feature, both projects will be merged?
  - It’s more likely Framer Motion will be a superset of Motion One with a filesize that reflects that. The latter will always be limited by WAAPI E.g spring animations, SVG etc

- Would you recommend using Framer motion over http://motion.dev for new non-react projects?
  - If you’ve not hit any WAAPI-based limitations then no!

- what's the difference between this project and http://motion.dev ?
  - Less and less as a lot from Motion One has now been absorbed into Framer Motion.
  - However, Motion One relies fully on WAAPI. It can do less in most ways. As a result its animate() function is 3.8kb (soon 2.5kb).
  - VS Framer Motion's animate() which is 15.5kb.

- we still need a API to animate SVG attribute changes with Framer. Currently only CSS stuff can be animated (i think)🙂
  - “Yeah it’s cool that it can be used cross-platform but can it animate the feDisplacementMap scale attribute”
  - Having said that we do have attrX/Y for this same reason so it’s probably easy enough to extend this to scale too
  - SVGs animate attributes by default. It’s the conflict with transform names

- I love both framer-motion and motion one, thank you! question on scroll-linked animations — am I right to think using motion one’s API will allow more work to be done up front than passing a MotionValue in to the style prop? then the lib just “scrubs” at run-time?
- 

- ## Motion One doesn’t have layout animations so no changes need
- https://twitter.com/mattgperry/status/1623204503003471872

- ## Motion One's new custom animations let you hook it up to an external library like Flubber to perform these morphing SVG animations
- https://twitter.com/mattgperry/status/1487701600529534979
  - https://codesandbox.io/s/motion-one-morph-svg-paths-qldsz?file=/src/index.js

- ## Hardware-accelerated CSS and WAAPI animations should be considered *progressive enhancement*, rather than mandatory. 
- https://twitter.com/mattgperry/status/1488076336958738432
  - Why? One word, that you're probably sick of hearing: Safari.
- Safari uses Apple's Core Animation for accelerated animations, the API that powers animations across iOS and macOS.
  - This means that if Core Animation doesn't support a feature, Safari bails the animation out of acceleration.
- The list of unsupported features is extensive:
  - 🙅🏾‍♀️ playbackRate !== 1
  - 🙅‍♂️ alternate/reverse playback direction
  - 🙅🏻 step easing
  - 🙅🏿‍♂️ cubic-bezier easing with overshoot (pictured)
  - 🙅🏼‍♀️ filter in iOS
- Usually when a bug is encountered with accelerated animations their go-to bugfix is to just add another bail-out.
- Over time the list of bail-outs has grown into an unknowable mishmash. However, getting accelerated animations to work is only half the battle.
- Success leads to synchronisation issues, timing issues and rendering oddities
- This is why Motion One disables acceleration in Safari by default
  - The Safari team contacted me about fixing this and then ghosted. Apple doesn't allow 3rd party browsers so we're stuck in this situation until the richest company in the world adequately supports their browser

- Out of curiosity, how do you disable hardware acceleration in Safari? I didn't think it was possible when animating properties like opacity and transform 
  - We trigger a bail-out, currently by setting playbackRate to something imperceptibly small like 1.00000001. I've been assured this won't be fixed (so we can continue to exploit) until sync/render/timing bugs have been squashed.

- ## Declarative animations are returning to vanilla JavaScript via Motion One!
- https://twitter.com/mattgperry/status/1455443495032967169
  - Springs, inView, stagger, and an API thats even simpler than CSS.

- ## Introducing Motion One. The smallest fully-featured animation library for the web.
- https://twitter.com/mattgperry/status/1440341298582523904
  - Built on the Web Animations API, it offers hardware accelerated animations, timelines and more, all for less than a fifth of the size of Greensock.
- How would you compare it to framer motion?
  - I mean currently this is an imperative JS library along the lines of Anime.js, Greensock, Popmotion etc so they're not really comparable.
  - Will you also make a declarative/React version of this library?
  - Declarative 100%. I don't know about libraries yet, there's a React library mostly in the can (and used on the homepage!) but I'd rather start over vanilla first
- Will you be updating framer-motion to use this under the hood?
  - I would love to, but we'll have to see. Framer Motion was  designed without any of the restrictions in WAAPI and there's a whole bunch of main thread functionality you'd have to bounce back to Popmotion for anyway.
- Can I ask if you compared the performance against @LottieFiles recently released player jLottie?
  - I've just had a quick look and I think it's a different use-case. jLottie is 15kb and for Lottie files, but you wouldn't make these yourself. Likewise Motion One is 3kb and can't animate Lottie files. They're almost mutually(相互地) exclusive(独家的，独占的) (几乎是互斥的)
  - Having said that Motion One uses WAAPI so Firefox and soon Chrome can run hardware accelerated animations for SVG. So if we could get it to animate Lottie files the performance would be better
  - jLottie is a player that animates Lotties, whereas Motion One is an animation library - which can be used to build a Lottie player. Yes, two entirely different use cases at a paradigmatic level. One can always take the innards of jLottie and render Lotties via Motion One...
- How do you animate something when in view? Like the bar charts on your homepage
  - For that I'm actually using a private Motion One React library that does in viewport animations
