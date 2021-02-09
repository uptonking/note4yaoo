---
title: thread-web-animation
tags: [animation, thread, ux]
created: '2021-01-06T14:39:01.923Z'
modified: '2021-01-08T17:14:34.841Z'
---

# thread-web-animation

# pieces

- ## 

- ## An Interactive Guide to CSS Transitions
- https://twitter.com/JoshWComeau/status/1359162874707533825
  - It's a deep dive into `transition` , the CSS motion workhorse. 
  - We'll discover different timing functions, learn about UX and performance best-practices, and more! 
- [An Interactive Guide to CSS Transitions](https://www.joshwcomeau.com/animation/css-transitions/)

- ## If I am let down by any Web API, it's gotta be the Web Animations API._201906
- https://twitter.com/maxlynch/status/1138501067451355138
  - The (only?) benefit it brings is stepping and pause/play. 
  - No spring animations, no physics, no frame-by-frame callback. 
  - Likely you'll need a 3rd party JS animation library for anything serious.
- Speaking of which, can anyone tell me why this CSS animation with (seemingly) the exact same config as a Web Animation both run differently? The Web Animation is faster and less fluid
  - Because they have different default easing. 
  - Web Animations allows you to apply easing across the *whole* animation iteration /or/ between two keyframes or both. 
  - CSS Animations only allows easing between keyframes.
  - In your example you are applying easing across the whole iteration for the Web Animations but CSS animations can't do that. 
  - It's a common problem authors encounter.
- As Rob points out, all that is coming. 
  - For now the main benefits are being able to generate async (i.e. smooth) animations from script, sync animations, composite them, and manipulate CSS animations/transitions (that's how the synchronized Firefox tab animation works fwiw).
- WebAnim's composite: add will allow retargeting animations smoothly. 
  - Complex easing functions for css-easing-2 enable declarative spring anims 
  - CSS Animation Worklet allows frame-by-frame customization 
  - 新特性都在draft阶段

- ## CSS transition won’t trigger when class is applied on a DOM element via custom elements ‘connectedCallback’ but calling ‘animate’ w/ Web Animations API works 100% in the same lifecycle hook
- https://twitter.com/iplayitofflegit/status/1338273190049562625
  - This is what `requestAnimationFrame(() => requestAnimationFrame(() => this.classList.add('new-class')))` should help

- ## Reasons why you should scale a pseudo-element on hover and not the element itself
- https://twitter.com/ericwaetke/status/1346791180940566528
  - you don't have these annoying hover glitches
- Just put all the styles you want to animate/transition in a pseudo-element!
  - doesn't really matter if you choose ::before or ::after, you need to adjust the z-index anyway!
- Just in case you don't know what "Boop" is yet, it's basically a fancier hover animation
  - [Boop! - A whimsical twist on hover transitions](https://www.joshwcomeau.com/react/boop/)

- ## Introducing Popmotion 9
- https://twitter.com/Patriopro/status/1316352484504461314
  - The motion library behind the Motion library, the lodash of animation.  
  - Popmotion 9 is simple, powerful, low level, stable, and tiny.
- Simple
  - When I wrote version 8, I'd just fallen in love with functional programming, reactive streams, and composability.
  - Popmotion 9 is an animate function and a bag of helper functions. You call them how you want. Not a pipe in sight.
- Powerful
  - The animate function handles numbers, colors and complex strings with keyframes and spring animations.
  - Framer Motion features like duration-based springs, repeatable springs, iOS-style momentum scrolling via the inertia function are all here too.
- Low level
  - Popmotion ships with no renderer. Do with these values as you please!
  - Animations use `rAF` by default, but you can use a synchronous loop (for pre-calculated frames) or an XR headset.
  - The underlying keyframes, spring and decay Iterators are also available directly.
- Stable
  - Written in TypeScript and now with 95% test coverage.
- Tiny
  - The animate function itself is less than 5kb, and all easing and utility functions are individually importable.
  - This is the animator's JavaScript toolbox.
- Is the Web Animations API more performant than popmotion?
  - In heavy load situations, probably.
  - 9 is designed to be portable to a worklet architecture, so this won't be true forever. 
  - 9 is also far more flexible than WAAPI, which is bound to the DOM. 

    - Can't use it with Three, or innerHTML, or XR devices etc, no springs either
