---
title: thread-web-animation
tags: [animation, thread, ux]
created: 2021-01-06T14:39:01.923Z
modified: 2021-01-08T17:14:34.841Z
---

# thread-web-animation

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🎯 After 5 years in the making, I'm very happy to finally release Anime.js v4 _202504
- https://x.com/JulianGarnier/status/1907817228168257854
  - New modular API
  - Draggables
  - WAAPI support

- ## 🌰 What is the Figma of motion design?
- https://x.com/_CryptoDesigner/status/1812785446063329593
- Adobe After Effects is still THE king for traditional, non-interactive motion design. New tools come and gone, but tbh nothing beats AE in terms of possibilities
- The best for straight up motion design is @fable_motion . Jitter is pretty good. @rive_app is cool because it is motion and interactive - different thing, and I'm just getting started with it (exciting!).

- ## Learn how to make your own layout animation library using the FLIP animation technique and the Web Animations API to create impossible layout animations.
- https://twitter.com/joyofcodedev/status/1773817479019593914
  - [Make Your Own Layout Animation Library Using The FLIP Animation Technique - YouTube](https://www.youtube.com/watch?v=idD9DA9eR_A)

- ## animating numbers? use a monospace font or `font-variant-numeric: tabular-nums` to avoid layout shifts
- https://twitter.com/JohnPhamous/status/1721954437839872383
- Also great for tables to keep numbers nice and neat across rows

- https://twitter.com/jh3yy/status/1715409590320288041
  - font-variant: tabular-nums; Is shorthand for font-variant-numeric.
- This can be used anywhere you want to align numbers
# discuss-raf
- ## 

- ## 

- ## @googlechrome currently contains a bug where the timestamp provided to `requestAnimationFrame` is roughly the time when rAF was invoked, *not* when the provided callback is triggered.
- https://twitter.com/mattgperry/status/1688509448120082432
  - This means if the main thread is blocked in the meantime, the timestamp provided will not represent the current frame but some time in the distant past.
  - Will ship a fix for Framer Motion today that uses http://performance.now() instead

# discuss-svg-anime
- ## 

- ## 

- ## 

- ## One of the tricky things to get right in SVG path animations is picking the right `stroke-dasharray` , so I made this visual to help understand
- https://x.com/nandafyi/status/1839319314220146753

# discuss
- ## 

- ## 

- ## 

- ## Framer Motion 11.11 introduces object animations.
- https://x.com/mattgperry/status/1841842701215437115
  - animate() can now accept and animate *any* object. Be it Three.js Object3Ds, Pixi.js Graphics... anything.
  - You can even mix different object types and HTML/SVG elements within animation sequences.

- Check out the sandbox, based on the classic React Three Fiber x Spline demo

- ## In Framer we're making an animation engine to animate anything a designer throws at us.
- https://twitter.com/mattgperry/status/1788296976997478689
  - It's not 100% optimal for everything but fantastic for most and always getting better.
  - I would be genuinely curious to see a FLIP or WAAPI implementation of this
  - It looks simple-ish but it's deceptive. The layouts are all being animated with transforms. With the mixed spring/time transitions, rotating children, undistorted radius, interruption. I think the way we do it is the only way possible. But perhaps there's a more performant way?
- When you say less powerful device, do you have specs? Because it could be we do things like frame rate detection that throttles or disables animations on slow devices

- ## 💫 implementing text animations with framer-motion is so fun
- https://twitter.com/consolerod/status/1770819569654870318
- is it motionValue that’s being animated?
  - that could be a an approach but i'm actually just animating motion.divs with initial and exit properties, since i already know the values and the edges of the selection window i just pass them to the tooltip, as new values comes in when scrolling they replace the previous ones

- ## Framer Motion 11.0.11 is a quantum leap in animation library performance.
- https://twitter.com/mattgperry/status/1767532370792427577
  - Introducing deferred keyframe resolution. 2.5x faster than 10.0 and GSAP animating from a cold start and 6x faster animating between unit types 
  - This is about to become super important for SEO.

- Why? Google is introducing the Interaction to Next Paint (INP) score. This means sites will be penalised the longer it takes for a page to become interactive and the longer between events and animation start. I've created two new benchmarks to improve the times for both.
- Motion 11 batches all reads and writes on the next animation frame. This saves an incredible amount of work - no more red marks!

- ## Like mixing JS animations and WAAPI seems to have no performance impact *until* there's a WAAPI animation on the main thread.
- https://twitter.com/mattgperry/status/1735665781784916216
  - Reaffirms my belief in only running select animations via WAAPI and will be removing backgroundColor to start.
  - I don't really understand why this would be happening but it's specifically when we pre-generate keyframes for a WAAPI animation for any of the values (so not a specific problem with backgroundColor or main thread animations). Good argument to support linear() where possible

- ## morphing tip prototype with View Transitions
- https://twitter.com/argyleink/status/1720550871300493541
  ✅ fixed position tip
  ✅ animates display: none
  ✅ just set innerText and left/top
  - https://codepen.io/argyleink/pen/GRzNZNe
  - i mouse into squares causing a tip to move to the center with some text. the tip morphs and moves to position!

- ## Scroll-driven animations coming in Safari
- https://twitter.com/anatudor/status/1719012021398589824
  - [scroll-driven animations – Bram.us](https://www.bram.us/tag/scroll-driven-animations/)
- Most of those fall deeply into the "just because you can doesn't mean you should" territory. Otoh the flip book example is divine.

- ## It’s actually weird to me that the View Transitions API accepts an async function. 
- https://twitter.com/mattgperry/status/1710630573339787561
  - startViewTransition shouldn’t be fired until anything asynchronous has finished and we’re ready to start a single sync job - updating the DOM. 
  - Because this function freezes the whole UI anyway.
- So allowing the encapsulation of jobs that could normally be discarded, interrupted, or persisting animations etc while they happen, is encouraging bad practise
- Although I am reminded of the example where you await fonts requested on the new page - that’s pretty nice.

- ## Preact Signals-inspired API for useTransform
- https://twitter.com/mattgperry/status/1691442096279064576
  - Subscribes to MotionValues used within the provided callback, rather than having to pass them in manually.
  - `useTransform( () => x.get() * 2 )`

- I kinda like the explicit dep array, but I guess at this point people are probably accustomed enough to seeing implicit subscriptions that it wouldn’t be confusing

- The thing that annoys me about it is having to rename the latest values(in old solution with deps). latest- is a convention but you’d probably choose to call them the same thing you called the MotionValues

- ## 💡 framer motion had signals five years ago 
- https://twitter.com/steveruizok/status/1635197073078513664
  - `MotionValue` provide reactive composable atomic state that provided a second channel for data that didn’t cause React to re-render (essential for animations). They can be computed via “transform” hooks.

- I wonder what @mattgperry you’ve learned after this time with such a system? Has MotionValue matured, any changes to its API that came out of long use?
  - These have roots in the Popmotion value API which as you can see in the opening summary "A multicast reaction that tracks the state of a number and allows velocity queries" I wrote when I was shitfaced on Rx
  - The API has remained the same since day 1. Easily my favourite part of Framer Motion and imo the most underused power feature. No notes
  - The only thing that's changed is I occasionally add a "naughty" method to make my life easier somewhere like `setWithVelocity`, which I basically use to force a new value and velocity to transfer a value from WAAPI back to the main thread. 
  - It would be great to have signals that you could pass straight into React's style but honestly I trust my render loop/render functions to be optimised for this

- This is the reason for stuff like animated.* out of react-spring.
  - Something I've wanted between signals & concurrency is a way to accumulate per-frame changes and apply them synchronously outside of React's scheduler. This is something I'd do in a game engine or renderer as mutating shared or WIP GPU memory can have severe perf ramifications.
- Exactly this, non of these data models efficiently support constant changing of values ala game engines from physics, game play, and AI control. Double goes for multiplayer except for netcode style. The rate of change and amount of entities would break all of the de jour app state/reactivity solutions. Rejecting simulation/emergent change isn't the not the end game.
- We’re halfway there with Theatre’s “signals” implementation. It’s a few years old but battle tested at this point.

- react-spring has had this for a long time as well,  `SpringValues` are observables that can omit events to their animated nodes.

- ## I realized recently that Framer Motion values are actually signals. 
- https://twitter.com/devongovett/status/1658573125125312512
  - They update outside React's render cycle. 
  - Good for performance, but I find the API a bit cumbersome compared to plain React. 
  - Hoping the React compiler finally enables animations without special wrappers.
- The challenge is locality of reactivity. Like components are the thing that changes. It makes easy bounds but is at odds with the cross-cutting independence you want. A compiler can "fix" this but only through masking the decoupling. Hooks already suggest this solution
- I think framer motion exists before "signals" were named that way so perhaps signals are motion values ; ) But yeah they work in a similar fashion

- ## @framer Motion 9.1 adds more hardware accelerated animations!
- https://twitter.com/mattgperry/status/1628738974096261121
  - Its unique hybrid engine now supports `opacity` , `clipPath` , `filter` , and `transform` . 
  - Smoother animations, longer-lasting batteries.
- https://codesandbox.io/s/framer-motion-hardware-accelerated-values-b01wfc
  - This animation runs with zero CPU overhead. To prove this, you can click the "block main thread" button to block JS for two seconds while the animation carries on.
- clipPath and backgroundColor have been promised for years in Chrome but aren't in yet. (We don't yet support backgroundColor as Motion's interpolation is nicer than browsers)

- ## A very useful CSS property for animations is transition timing function 
- https://twitter.com/davidm_ml/status/1617098718343475201

- ## Just released an interesting bug fix for mixing rotation and layout animations in Framer Motion.
- https://twitter.com/mattgperry/status/1534465693336363008
  - In this video, the grey container is animating height via scale, which distorts its children. We usually correct for this, but these rotating children are still stretching.

- ## I'm looking for the absolutely smallest implementation of a smooth-scroll animation loop powered by nothing more than request animation frame + some measurements at each tick. Anyone seen anything like that in the wild?
- https://twitter.com/tannerlinsley/status/1532422987277668353
- https://github.com/stipsan/smooth-scroll-into-view-if-needed

- ## There's a little left to do before we release Framer Motion 5 
- https://twitter.com/mattgperry/status/1432728000710184967
- Previously, we maintained a "projection target", a viewport-relative bounding box that described where an element should appear on screen.
- Now, when a layout changes, we figure out the transform required to make an element revert to the old layout, and animate that to zero
  - This sounds like FLIP but in reality we are calculating the projection target once a frame from applying this transform to the measured layout.
  - This means we can still calc a transform that will get two different elements into the same box to create shared element animations.
  - The transform we actually apply to an element is calculated to ensure it's free from any distortion from parent transforms, just like before.
  - But doing all this from a transform animating to zero is more stable than from a projection target that could become out of date.
- Additionally, we now measure layout relative to the page, and considering all `overflow: scroll` elements.
  - This means that measured layouts don't become out of sync if they're measured at different scroll offsets.
- Finally, `AnimateSharedLayout` was created to remove layout thrashing 
  - but we use layout animations extensively in Framer so if you nested these or had many siblings, layout thrashing would resurface.
  - It took a lot of work, some sensible trade-offs and some outright cheats 
  - but now we've removed layout thrashing completely and removed the need for you as a developer to add `AnimateSharedLayout` . 
  - Just add `layoutId` and away you go!

- ## CSS variables can be used *within CSS keyframe animations*!
- https://twitter.com/JoshWComeau/status/1422921859021131779
- Although I think the way you propose is going to perform better as the browser can eval the variable at the start of the animation and only animate transform off the main thread. **CSS variable animation performance is still bound to the main thread**.
- He's applied `will-transform` which is a more polite way of saying `translateZ(0)` . The browser will most likely put these on GPU layers as in your approach
  - I'm guessing framer motion already has this baked in?
  - Yeah but we use translateZ(0) still as it has better old browser support.
- I built a whole animation system on this core concept! CSS variables allow for composable and fully customizable animations.
  - Thank you! Next steps are to make it purgeable or use a JIT compiler to reduce overall file size. We took some inspiration/learnings from your dark mode article as well!
- https://github.com/ingram-projects/animxyz
  - The first truly composable CSS animation library. 
  - Powered by CSS variables to allow a nearly limitless number of unique animations without writing a single keyframe. 
- I've found if you don't predefined the CSS variables the performance is abysmal(极坏的), I can't properly tell why, but it lags and stutters quite a bit.

- ## I'm surprised by how much more energy efficient animating transform is with WAAPI than GreenSock JavaScript.
- https://twitter.com/mattgperry/status/1421789054669033473
- However, at least in Safari by far the the worst battery-life offender is animating CSS variables. 
  - If @webkit drags its heels supporting ` CSS.registerProperty` , I might extend the individual transform polyfill to set transform on an element directly.
- The WAAPI uses less memory and CPU in general, so, it can produce super smooth animations with little to no worry about sustained performance. 
  - Note, **infinitely looping animations will accumulate memory and if left running for too long will lead to a memory overflow**
  - Stateless animations would be one way to address this, where frame to render is determined by time instead of internal state.
  - Most libraries work this way already though, even Popmotion’s spring
- Measuring energy efficiency is so interesting! I’d love to profile @astrodotbuild . What tool is this?
  - Safari/WebKit dev tools I think.

- ## experimenting with a way to visualize the frames of a framer-motion animation
- https://twitter.com/siddharthkp/status/1420424243007922179
  - the controls UI is by @pmndrs
  - fun fact, that's also how we visualise easing (that was all @davidbismut) in Leva, it gives a really good idea of what's going to happen
  - https://github.com/siddharthkp/tracer-motion

- ## a feature comparison guide for Motion Concept C.
- https://twitter.com/mattgperry/status/1419753685207429121
  - where it will shine is bundlesize and perf for those users where any missing features isn't a problem.
- The main missing features are custom easing functions, path morphing, and animating raw strings/numbers. These might be showstoppers in some projects. But we also get incredible interpolation and off-thread animations.
- How do you consider Motion Concept C and Motion Framer future? 
  - No this is separate although having written both it does share a similar API on the React side. In that sense jumping between the two is easy enough if you don’t need the full Framer Motion capabilities

- ## One of my endlessly repeated animation tips is 'let easing do the heavy lifting for you' 
- https://twitter.com/cassiecodes/status/1418863372112736258
  - i.e. don't write unnecessary code if you can use an easing curve instead. 

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
