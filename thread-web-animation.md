---
title: thread-web-animation
tags: [animation, thread, ux]
created: '2021-01-06T14:39:01.923Z'
modified: '2021-01-08T17:14:34.841Z'
---

# thread-web-animation

# pieces

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## I love react-spring, but does anyone know of anything with a smaller bundle size? 
- https://twitter.com/tannerlinsley/status/1415457202794500097
  - I'm looking for something *microscopic* (like 4kb for react-motion), but still performs the animation loop outside of React.
- Curious how folks handle the “outside of React” part. Any good reads on explanations?
  - Collect a `ref` on the element and directly manipulate the DOM element’s properties and style using DOM APIs.
  - It’s funny how fast things can be when you aren’t running a reconciler with every frame.
- Did a quick create vite app and compared before/after adding a basic spring animation. Ended up adding 15kb so I will eat my words here

- ## From what I understand, JavaScript animations are limited to 60fps, even on devices that support higher refresh rates—but CSS animations can go higher. What about these?
- https://twitter.com/steveruizok/status/1415223404022714368
- Eh? JS is doing perfectly fine going to 120hz on my 4k 120hz display. rAF should always be going up to the displays refresh rate unless the device has performance issues. Maybe some devices browsers have rAF crippled but it's fine on desktop at least.
  - Ah right, this is a Safari issue (where raf is limited to 60fps)
  - Depends on the browser: iPad Safari for example maxes out at 60

- ## Interesting jank(闪烁) test here pitting Motion Concept C animating transform, background-color and x (as a CSS variable) against Popmotion.
- https://twitter.com/mattgperry/status/1415214004465700866
  - The reason for this is **WAAPI can run opacity and transform (and filter?) completely on the compositor thread**. All other animations play on the main thread, just like your regular JavaScript animation library.
  - This is a shame for the performance of animating transforms individually but it does reaffirm my feelings that off-thread performance is just one of the benefits we get from WAAPI (Popmotion's animate function is about 5kb and needs `"style.transform ="` boilerplate)
- Another nice thing about WAAPI too is that you don't incur the cost of injecting a `<style>` tag to create a custom animation 🎉; that was a surprising bottleneck for my spring-keyframes library

- ## For the second time in my life I’ve attempted to write a book about animation and ended up making a library instead
- https://twitter.com/mattgperry/status/1412121262449627140
  - Every time I tried to explain a non-obvious behaviour of the browser's built-in animation API (WAAPI) I couldn't help but try and fix it with code instead.
- For instance, WAAPI's default behaviour is to leave your element in its *initial* state once the animation has finished.
  - There's an option called "fill" that you can set to "forwards" to fix it... except even the spec warns about memory leaks
  - The recommended method (read: fix) is to make a promise handler that explicitly sets the the styles you were animating to.
  - It's this kind of just-annoying-enough behaviour that can kill the adoption of an API. Or at least give value to an opinionated API built around it.
  - These fixes progressed into experiments to see how close I could get to an GSAP or Anime.js-style library, but for a much smaller bundlesize. 
- Problem is, you bite a ton of limitations when dealing with WAAPI. Many of these could be unsurmountable(无法解决/克服的). But not all.
  - For instance, I thought you can't animate transforms individually, or use velocity-based springs. But I realised that was not true when making this prototype
- Unfortunately it is rather hard to add spring easing, custom transforms, attribute tweens, etc... at a small size as I later realized 😢, 
  - if you choose to use spring easing with @okikio/animate the file size is 11kb but without spring easing it is 5kb, 1kb less than animejs.
  - I noticed some of the problems with WAAPI, so I built @okikio/animate as a way to make it easier to make animations with the WAAPI.
  - I based the animation format off of animejs, so, using it shouldn't be too different from animejs.
- You may want to use Animation Worklet's, instead of just WAAPI. 
  - You can apparently create custom easing using animation worklets.

- ## Kicking the tires on a 1kb, WAAPI-powered animation API
- https://twitter.com/mattgperry/status/1408688475973488640
  - https://codesandbox.io/s/react-waapi-library-sketch-wh09l
  - 例子依赖motion
- Are we getting a framer-motion-svelte? 
  - No probably not! it’s already got a fairly good in-built animation system and I’ve been looking into how possible it’d be to do layout animations and it looks pretty tricky to do without layout thrashing
- Is the WAAPI GPU-accelerated by default, say, if we use the left or top property to animate?
  - No these are still layout-triggering properties. The performance improvements come from running animations off the main JS thread

- ## Finally got a grip on how I want to handle animations with @shoelace_style components. 
- https://twitter.com/claviska/status/1395873208063217668
  - Going with the Web Animations API and a thin animation registry instead of [unreliable] CSS transitions.
  - This took me more time than I’d like to admit. I really wanted to allow animation customizations to happen with CSS, but this is the next best thing.
- There’s also a method to set the default animation(s) for all components.

- ## You might not need all those keyframes! 
- https://twitter.com/jh3yy/status/1373417544200171529
  - Repeating keyframes at different points? You can group them.
  - Keyframe putting an element in its default position? You might not need it.
  - https://codepen.io/jh3y/pen/poNMVYG
- Woah! I for sure thought you’d need the “reset” state.

- ## What’s your biggest animation pain point?
- https://twitter.com/mattgperry/status/1373252112298225667
- Triggering viewport scroll animations below the fold. Such a massive pain in the arse!
- Mount/unmount animations still usually end up buggy for me even with animate presence.
- Animating only once in view. Easy enough with intersection observer but also ends up with buggy edge cases.
- Animating for multiple media queries.
- Getting animations to fire in sequence

- ## The future of CSS: Scroll-Linked Animations 
- https://twitter.com/bramusblog/status/1364016209516232709
  - In this post we dig into CSS @​scroll-timeline to create Scroll-Linked Animations between two absolute scroll-offsets, and how we can tweak them.
  - [The Future of CSS: Scroll-Linked Animations](https://www.bram.us/2021/02/23/the-future-of-css-scroll-linked-animations-part-1/)

- https://twitter.com/bramusblog/status/1367259964683739141
  - In this 2nd part covering @​scroll-timeline we turn things up a notch and dig into creating Scroll-Linked Animations using Element-based Offsets

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
