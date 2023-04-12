---
title: thread-web-animation-waapi
tags: [animation, thread, waapi]
created: 2021-09-22T04:12:55.839Z
modified: 2021-09-22T04:13:22.341Z
---

# thread-web-animation-waapi

# discuss

- ## 

- ## 

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
