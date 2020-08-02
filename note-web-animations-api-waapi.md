---
title: note-web-animations-api-waapi
tags: [animation, waapi, web]
created: '2020-08-02T13:35:01.695Z'
modified: '2020-08-02T13:39:54.869Z'
---

# note-web-animations-api-waapi

## Web Animations API (WAAPI)

- https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API
- https://caniuse.com/#feat=web-animation
  - some browsers may support only level 1
- WAAPI-Powered GSAP? Unlikely.
  - https://greensock.com/waapi/
  - WAAPI is a native browser technology that's similar to CSS animations, but for JavaScript.
  - It's much more flexible than CSS animations 
  - and it taps into the same mechanisms under the hood so that the browser can maximize performance.
  - WAAPI has some critical weak spots that make it virtually impossible for GSAP to leverage it under the hood
    - WAAPI only supports cubic-bezier() for custom easing, meaning it's limited to one segment with two control points.
      - It can't support eases like Bounce, Elastic, Rough, SlowMo, wiggle, ExpoScaleEase, etc
    - The most commonly animated values are translation (x/y position), rotation, and scale (all transform-related)
      - but you cannot control them independently with CSS or WAAPI.
    - WAAPI doesn't let you animate arbitrary properties of generic objects, like {myProperty:0}.
  - WAAPI has a performance advantage because it can leverage a separate thread whereas JavaScript always runs on the main thread, right? 
    - Well, sort of. 
    - The only time a separate thread can be used is if transforms and/or opacity are the only things animating on a particular element (or else you run into synchronization issues). 
    - Plus there's overhead involved in managing that thread which can also get bogged down. 
    - There are tradeoffs either way. 
    - Having access to a different thread is fantastic even if it only applies in certain situations. 
    - That's probably the biggest reason I wanted to leverage WAAPI originally, but the limitations and tradeoffs are pretty significant 
  - The main benefit I see in using WAAPI inside GSAP is to get the off-the-main-thread-transforms juice 
    - but even that only seems useful in relatively uncommon scenarios, and it comes at a very high price.
  - Why use GSAP even if/when WAAPI gets full browser support?
    - Browser bugs/inconsistencies
    - Lots of extra features like morphing, physics, Bezier tweening, text tweening, etc.
    - Infinite easing options (Bounce, Elastic, Rough, SlowMo, ExpoScaleEase, Wiggle, Custom)
    - Independent transform components (position, scale, rotation, etc.)
    - Animate literally any property of any object (not just DOM)
    - Timeline nesting (workflow)
    - GSDevTools
    - Relative values and overwrite management
    - from() tweens are much easier - you don't need to get the current values yourself
  - Why WAAPI might be worth a try
    - always 
  - The goal of this article is NOT to criticize WAAPI. I think it's a great step forward for browsers.
    - Brian Birtles, one of the primary authors of the WAAPI spec, reached out and offered to work through the issues and try to find solutions
    - 2020 EDIT: Now Brian Birtles is the only one working on WAAPI and he does so on a volunteer basis, so further development of WAAPI has understandably slowed down in recent times
