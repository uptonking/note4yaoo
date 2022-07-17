---
title: thread-web-animation-opinions
tags: [animation, opinions, thread, web]
created: 2021-01-08T19:15:15.849Z
modified: 2021-01-08T19:16:04.471Z
---

# thread-web-animation-opinions

# opinions

# pieces

 - ## 

 - ## 

 - ## 

 - ## 

 - ## A standing issue with CSS transitions/animations is that you can't apply two or more transforms to a single DOM node with independent timing functions. 
 - https://twitter.com/sebmarkbage/status/1409897461146165258
   - It's an issue for 2D physics animations like springs when the starting velocity is an angle (fling).
   - You end up having to add extra DOM nodes to this which makes it a lot harder to do as a universal library. Unless you hide a bunch of extra nodes in a shadow DOM I guess. That's one reason many pick JS animations today.
   - CSS worklets doesn't seem to have a solution to this neither. Built-ins like the spring() proposal doesn't neither. Is there any proposal that I've missed that aims to solve this?
 - I was under the impression that individual transform properties would solve this?
   - [CSS Individual Transform Properties](https://webkit.org/blog/11420/css-individual-transform-properties/)
   - I completely missed that! It looks like a good start but unfortunately doesn't seems like it would fully solve it. Since there's no individual X and Y properties. You could hack for 2D by using transform and individuals giving you two dimensions, but you'd run out for Z.
 - But I’ve managed to solve it with a JS-driven animation as a polyfill
   - I'm profiling to see if I can understand what you meant by this but registered CSS variables seem to animate on the animation thread like any other and the performance impact is whatever you apply them to.

 - ## Why aren’t you using WebAnimations API?
 - https://twitter.com/mattgperry/status/1387990910043140098
 - I mostly work with React and React Native. I can use Animated/Reanimated on both, but I can't use WebAnimation API on React Native. Would be cool if I could though.
 - if i have to call useRef one more time i’ma lose it is the main reason.in all seriousness though CSS animations+framer motion when needed seems like the simplest (fewest LoC) way to accomplish my motion needs

 - ## vote: To animate, I primarily use css vs WAAPI vs js
 - https://twitter.com/mattgperry/status/1387667723405103106
   - css : WAAPI :js = 0.497 : 0.12: 0.491(165votes)
 - I default to CSS as much as possible, but when the animation has the potential to burn out your whole career, I use libs like framer motion or popmotion

 - ## I dislike most animations on the web since they just slow things down. 
 - https://twitter.com/BenNadel/status/1374691082978660353
   - An example that has bugged me for a while: the change in size, shape, color, and location is _sufficient_ for a low cognitive load. 
   - The animation adds no value, it only makes the UI feel sluggish.

- ## CSS animation and Web Animation API won't be stalled by CPU intensive JavaScript, whereas other libs will start getting janky.

- Web Animations API Super Powers
  - you can easily sequence animations with WAAPI. 
    - Chaining animations is simple and robust (something you can't currently do in CSS).
    - No plugins needed, no library code to learn. It's part of the spec!
    - WAAPI is a W3C standard, no plugins needed — in browsers now!
  - you can easily fire a function when an animation ends

- ## Although Web Animations API superior for many use cases.
  - There's situations where HTML5 requestAnimationFrame() needs full Hz access & self-detect single framedrop stutter.
  - 120Hz TestUFO still unsupported on 120 Hz iPads. 

- ## Ionic uses the Web Animations API where it's available and automatically falls back to CSS where it's not. 
  - It's not something I've really looked into, but I don't there is enough support to use WAAPI alone yet. 
  - The good news: the API will be available to use without Ionic soon.
  - We dropped support for IE11 and Edge Legacy recently. That means that Web Animations are supported everywhere:

- ## Ionic animation is a high level abstraction of web animations api. 
  - You can see it in action on every ionic component.. 
  - I love their approach and syntax, pretty straight (but simpler) when compared with another libs, like greensock.. go for it!
  - https://github.com/ionic-team/ionic-framework/tree/master/core/src/utils/animation

- ## We are adopting Framer Motion as the standard for @godaddy but still need to figure out bundling (its quite large w/out tree shaking)
  - I believe Framer Motion 2 already supports tree-shaking or will support it soon with Popmotion 9

- For shoelace, Here’s an early prototype of declarative animations using the Web Animation API. 
  - Over 500 are already built in.

- ## CSS Keyframes are underrated
  - Coupled with CSS custom properties and web animation API, not sure we really need those fancy JS libraries. 
    - Tried quite a few and keep having to ditch them due to performance issues. 
    - Just wish there was a good tool for spring/physics with CSS.
  - Yup! (although interrupt-able animations probably need JS, as well as springs)
  - Would be great for there to be a performant browser primitive for spring animations

- ## We'd like to see the Web Animations API do all that GSAP can do
  - True, WAAPI can't do much without a lot of code, but in most of the apps, GSAP is way overkill. CPU and memory consumption-wise
  - Just saying from a performance standpoint. Still, Greensock rocks. And don't let anyone deny the fact that GSAP SVG Animations are super

 
