---
title: thread-web-animation-opinions
tags: [animation, opinions, thread, web]
created: '2021-01-08T19:15:15.849Z'
modified: '2021-01-08T19:16:04.471Z'
---

# thread-web-animation-opinions

# opinions

# pieces

 - ## 

- CSS animation and Web Animation API won't be stalled by CPU intensive JavaScript, whereas other libs will start getting janky.

- Web Animations API Super Powers
  - you can easily sequence animations with WAAPI. 
    - Chaining animations is simple and robust (something you can't currently do in CSS).
    - No plugins needed, no library code to learn. It's part of the spec!
    - WAAPI is a W3C standard, no plugins needed — in browsers now!
  - you can easily fire a function when an animation ends

- Although Web Animations API superior for many use cases.. 
  - There's situations where HTML5 requestAnimationFrame() needs full Hz access & self-detect single framedrop stutter.
  - 120Hz TestUFO still unsupported on 120 Hz iPads. 

- Ionic uses the Web Animations API where it's available and automatically falls back to CSS where it's not. 
  - It's not something I've really looked into, but I don't there is enough support to use WAAPI alone yet. 
  - The good news: the API will be available to use without Ionic soon.
  - We dropped support for IE11 and Edge Legacy recently. That means that Web Animations are supported everywhere:

- Ionic animation is a high level abstraction of web animations api. 
  - You can see it in action on every ionic component.. 
  - I love their approach and syntax, pretty straight (but simpler) when compared with another libs, like greensock.. go for it!
  - https://github.com/ionic-team/ionic-framework/tree/master/core/src/utils/animation

- We are adopting Framer Motion as the standard for @godaddy but still need to figure out bundling (its quite large w/out tree shaking)
  - I believe Framer Motion 2 already supports tree-shaking or will support it soon with Popmotion 9

- For shoelace, Here’s an early prototype of declarative animations using the Web Animation API. 
  - Over 500 are already built in.

- CSS Keyframes are underrated
  - Coupled with CSS custom properties and web animation API, not sure we really need those fancy JS libraries. 
    - Tried quite a few and keep having to ditch them due to performance issues. 
    - Just wish there was a good tool for spring/physics with CSS.
  - Yup! (although interrupt-able animations probably need JS, as well as springs)
  - Would be great for there to be a performant browser primitive for spring animations

- We'd like to see the Web Animations API do all that GSAP can do
  - True, WAAPI can't do much without a lot of code, but in most of the apps, GSAP is way overkill. CPU and memory consumption-wise
  - Just saying from a performance standpoint. Still, Greensock rocks. And don't let anyone deny the fact that GSAP SVG Animations are super

 
