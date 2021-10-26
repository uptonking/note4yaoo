---
title: thread-web-animation-waapi
tags: [animation, thread, waapi]
created: '2021-09-22T04:12:55.839Z'
modified: '2021-09-22T04:13:22.341Z'
---

# thread-web-animation-waapi

# discuss

- ## 

- ## 

- ## 

- ## 

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
