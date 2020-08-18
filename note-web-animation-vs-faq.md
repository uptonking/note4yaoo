---
title: note-web-animation-vs-faq
tags: [animation, comparison, faq, web]
created: '2020-08-02T13:31:18.116Z'
modified: '2020-08-02T13:39:43.308Z'
---

# note-web-animation-vs-faq

## faq

- ### 对于list或grid中的项目，拖动A到B的位置，实现的效果可以有2种
  1. A到B的位置，B到A的位置，其他不变
  2. A到B的位置，然后A之后B之前的所有元素前移一位，最后B挨着A
  - 从性能角度考虑，选第一种

## translate3d vs translateZ vs rotateZ

- The `translate3d()` CSS function repositions an element in 3D space. 
  - Its result is a `<transform-function>` data type.
- The `translateZ()` CSS function repositions an element along the z-axis in 3D space, i.e., closer to or farther away from the viewer. 
  - Its result is a `<transform-function>` data type.
  - `translateZ(tz)` is equivalent to `translate3d(0, 0, tz)` .
- The ` rotateZ()` CSS function defines a transformation that rotates an element around the z-axis without deforming(v, 使变形) it. 
  - Its result is a `<transform-function` > data type.
  - `rotateZ(a)` is equivalent to `rotate(a)` or `rotate3d(0, 0, 1, a)` .
- ref
  - [CSS performance relative to translateZ(0)](https://stackoverflow.com/questions/10814178/css-performance-relative-to-translatez0)
    - CSS transformations create a new stacking context and containing block, as described in the spec
    - It forces the browser to use hardware acceleration to access the device’s graphical processing unit (GPU) to make pixels fly. 
      - Web applications, on the other hand, run in the context of the browser, which lets the software do most (if not all) of the rendering, resulting in less horsepower for transitions. 
      - But the Web has been catching up, and most browser vendors now provide graphical hardware acceleration by means of particular CSS rules.
    - `translate3d(0,0,0)` does nothing in terms of what you see. It moves the object by 0px in x,y and z axis. It's only a technique to force the hardware acceleration.
  - [translate3d vs translate performance](https://stackoverflow.com/questions/22111256/translate3d-vs-translate-performancek)
    - The use of translate3d pushes CSS animations into hardware acceleration. Even if you're looking to do a basic 2d translation, use translate3d for more power

## css transition vs animation

- 用法上最大的区别：animation可设置多个中间状态
- 性能上几乎无差别，都基于web animations api的engine

## css vs js animation

- 考虑现有库已用的动画或周边库的选择
- 用法上最大的区别：js可控制动画更多细节
  - 动态创建动画的时机、播放流程控制、添加动画生命周期监听器
- css animation使用更简单
- 性能上不必提前考虑
  - 因为layout和repaint的开销比css和js执行的开销大得多
- 考虑流行度：web animations api 在github上不受欢迎
- 考虑对svg、canvas的支持
  - svg支持使用css transition和css animation

## requestAnimationFrame vs waapi

## 聊一聊CSS动画

- [聊一聊CSS动画](https://juejin.im/post/6844903909710888967)

- css transition的优点在于简单易用，但是它有几个很大的局限
  - transition只能定义开始状态和结束状态，不能定义中间状态，也就是说只有两个状态。
  - transition需要事件触发，所以没法在网页加载时自动发生。
  - transition是一次性的，不能重复发生，除非一再触发。
  - 一条transition规则，只能定义一个属性的变化，不能涉及多个属性。

- css animation不足
  - 如果需要多个动画需要随时的暂停，播放，反向播放，动态改变播放速率，监听到动画的完成和取消，需要用js来为css animation增加不同的样式从而改变动画，会让css文件和js文件太过于“笨重”

## CSS3 animation vs CSS3 transition

- [CSS3 animation vs CSS3 transition_201506](https://www.pixelstech.net/article/1434375977-CSS3-animation-vs-CSS3-transition)

- animation会竞争CPU资源，可能有延迟，transition使用GPU
  - CSS3 animation will not lift the animation rendering process to the GPU like what CSS3 transition does. 
  - This will cause lagging effect when many JS tasks are executing at the same time. Because all tasks are competing for the CPU. 
  - While CSS3 transition may lift the animation to GPU so that it will not compete with CPU and can be renderrred separately
  - animation使用GPU的方式是加上 `transform: translateZ(0)` 或 `translate3d(0, 0, 0)` 或 `rotateZ(360deg)` . 
    - This will composite the elements into their own layers (by tricking the browser into thinking it will be doing 3D transforms) 
    - and the browser should, in most cases, take advantage of GPU acceleration, lessening the burden on the CPU.
- 动画完成时，是否会保存状态，animation会回到初始状态
  - After each animation, the CSS3 animation will move back to its original state where before the animation starts While CSS3 transition will keep the animation state after each transition.
- 执行次数的区别，animation可设置循环次数
  - CSS3 animation can have iteration count set(animation-iteration-count) which means how many times the animation will be repeated. 
  - But CSS3 transition will only perform the animation once. 
  - To repeat the animation with CSS3 transition, JavaScript may need to be used.
- 动画中间状态的控制，animation可设置多个中间态
  - CSS3 animation gives more control to the developer on how the animation is performed. You can define what the state should be at different stages of the animation, e.g, 0%, 10%, 30%, 50%....
  - CSS3 transition can only define the start and end state and the rest will be handled by the browser.
- animation的易用性不如transition简单
  - CSS3 transition is more simpler to use, it doesn't require you to create your own keyframes. There are a predefined set of animations which can be used. And there are a set of effects you can use to transition an element.
  - Animation takes a lot more code

## CSS and JavaScript animation performance

- [mdn: CSS and JavaScript animation performance](https://developer.mozilla.org/en-US/docs/Web/Performance/CSS_JavaScript_animation_performance)

- There are many ways to implement web animations, such as CSS transitions/animations or JavaScript-based animations (using `requestAnimationFrame()` ). 

- CSS `transition` s provide an easy way to make animations occur between the current style and an end CSS state, e.g., a resting button state and a hover state. 
  - Even if an element is in the middle of a transition, the new transition starts from the current style immediately instead of jumping to the end CSS state.  
- CSS `animation` s, on the other hand, allow developers to make animations between a set of starting property values and a final set rather than between two states. 
  - CSS animations consist of two components: a style describing the CSS animation, and a set of key frames that indicate the start and end states of the animation's style, as well as possible intermediate points.  
- **In terms of performance, there is no difference between implementing an animation with CSS transitions or animations**. 
- Both of them are classified under the same CSS-based umbrella in this article.

- Compared to `setTimeout()` / `setInterval()` , which need a specific delay parameter, `requestAnimationFrame()` is much more efficient. 
- Developers can create an animation by simply changing an element's style each time the loop is called (or updating the Canvas draw, or whatever.)
- Like CSS transitions and animations, `requestAnimationFrame()` pauses when the current tab is pushed into the background.

- The fact is that, in most cases, the performance of CSS-based animations is almost the same as JavaScripted animations — in Firefox at least. 
- Some JavaScript-based animation libraries, like GSAP and Velocity, even claim that they are able to achieve better performance than native CSS transitions/animations. 
  - This can occur because CSS transitions/animations are simply resampling element styles in the main UI thread before each repaint event happens, which is almost the same as resampling element styles via a `requestAnimationFrame()` callback, also triggered before the next repaint. 
  - If both animations are made in the main UI thread, there is no difference performance-wise.

- we'd argue that CSS animations are the better choice. But how? 
- The key is that as long as the properties we want to animate do not trigger reflow/repaint, we can move those sampling operations out of the main thread. 
- The most common property is the CSS `transform` . 
  - If an element is promoted as a layer, animating `transform` properties can be done in the GPU, meaning better performance/efficiency, especially on mobile. 
- In summary, we should always try to create our animations using CSS transitions/animations where possible. 
  - If your animations are really complex, you may have to rely on JavaScript-based animations instead.

##　WAAPI-Powered GSAP? Unlikely.

－[WAAPI-Powered GSAP? Unlikely._201710](https://greensock.com/waapi/)

- WAAPI is a native browser technology that's similar to CSS animations, but for JavaScript. It's much more flexible than CSS animations and it taps into the same mechanisms under the hood so that the browser can maximize performance.
- these are things that make it architecturally impossible (or very cumbersome) to build GSAP on WAAPI
  - Custom easing
  - Independent transform components
    - For example, try moving (translate) something and then halfway through start rotating it and stagger a scale toward the end
    - Additive animations (composite:"add") probably aren't an adequate solution either. 
  - Custom logic on each tick
  - Non-DOM targets
    - WAAPI doesn't let you animate arbitrary properties of generic objects, like `{myProperty:0}` . 
    - GSAP can use animate any sort of objects including canvas library objects, generic objects, WebGL values, whatever.
  - Global timing controls
  - WAAPI still isn't implemented in several major browsers today. 
    - And then there are the browser inconsistencies (like the infamous SVG origin quirks)
- The main benefit I see in using WAAPI inside GSAP is to get the off-the-main-thread-transforms juice but even that only seems useful in relatively uncommon scenarios, and it comes at a very high price. 
  - I'm struggling to find another compelling reason to build on WAAPI; 
  - GSAP already does everything WAAPI does plus a lot more.

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
  - Solid performance, especially for transforms and opacity
  - always free

- EDIT: 
  - Brian Birtles, one of the primary authors of the WAAPI spec, reached out and offered to work through the issues and try to find solutions (some of which may involve editing the spec itself) which is great. 
  - Rachel Nabors has also worked to connect people and find solutions. 
  - Although it may take years before it's realistic to consider building on WAAPI, it's reassuring to have so much support from leaders in the industry who are working hard to move animation forward on the web. 
- EDIT 2020: 
  - Now Brian Birtles is the only one working on WAAPI and he does so on a volunteer basis, so further development of WAAPI has understandably slowed down in recent times.

## Myth Busting: CSS Animations vs. JavaScript

- [Myth Busting: CSS Animations vs. JavaScript_201704](https://css-tricks.com/myth-busting-css-animations-vs-javascript/)

- The following is a guest post by Jack Doyle, author of the GreenSock Animation Platform (GSAP).
- This article is meant to raise awareness about some of the more significant shortcomings of CSS-based animation
- Lack of independent scale/rotation/position control
  - In CSS, they’re all crammed into one `transform` property, making them impossible to animate in a truly distinct way on a single element
- performance
  - The newer GSAP is also JavaScript-based but it’s literally up to 20x faster than jQuery.
  - The GPU is highly optimized for tasks like moving pixels around and applying transform matrices and opacity, so modern browsers try to offload those tasks from the CPU to the GPU. 
  - The secret is to isolate the animated elements onto their own GPU layers because once a layer is created (as long as its native pixels don’t change), it’s trivial for the GPU to move those pixels around and composite them together. 
  - Instead of calculating every single pixel 60 times per second, it can save chunks of pixels (as layers) and just say “move that chunk 10 pixels over and 5 pixels down” (or whatever).
  - Declaring your animations in CSS allows the browser to determine which elements should get GPU layers, and divvy them up accordingly.
  - you can do that with JavaScript too. Setting a `transform` with a 3D characteristic (like `translate3d` or `matrix3d` ) triggers the browser to create a GPU layer for that element. 
  - Also note that not all CSS properties get the GPU boost in CSS animations. 
    - In fact, most don’t. 
    - Transforms (scale, rotation, translation, and skew) and opacity are the primary beneficiaries.
  - Offloading calculations to a different thread
  - using a different CPU thread for animation-related calculations doesn’t come without costs
  - First of all, only properties that don’t affect document flow can truly be relegated to a different thread. So again, transforms and opacity are the primary beneficiaries.
  - Since graphics rendering and document layout eat up the most processing resources (by FAR) in most animations (not calculating the intermediate values of property tweens), the benefit of using a separate thread for interpolation is minimal. 
    - For example, if 98% of the work during a particular animation is graphics rendering and document layout, and 2% is figuring out the new position/rotation/opacity/whatever values, 
    - even if you calculated them 10 times faster, you’d only see about a 1% speed boost overall.
  - The results confirm what is widely reported on the web – CSS animations are significantly faster than jQuery.
  - However, on most devices and browsers I tested, the JavaScript-based GSAP performed even better than CSS animations 
  - Although well-optimized JavaScript is often just as fast if not faster than CSS animations, 3D transforms do tend to be faster when animated with CSS, but that has a lot to do with the way browsers handle 16-element matrices today (forcing conversion from numbers to a concatenated string and back to numbers)
- Using css animations, You cannot seek to a particular spot in the animation, nor can you smoothly reverse part-way through or alter the time scale or add callbacks at certain spots or bind them to a rich set of playback events. JavaScript provides great control
- Modern animation is very much tied to interactivity, so it’s incredibly useful to be able to animate from variable starting values to variable ending ones (maybe based on where the user clicks, for example), or change things on-the-fly but declarative CSS-based animation can’t do that.
- It is becoming increasingly common to animate canvas-based objects and other 3rd-party library objects, but unfortunately CSS animations can only target DOM elements.
- There are a few more workflow-related conveniences that are missing in CSS Animations
  - Relative values
  - Nesting
  - Progress reporting
  - Targeted kills
  - Concise code

- You can’t really do any of the following with CSS animations
  - Animate along a curve (like a Bezier path).
  - Use interesting eases like elastic or bounce or a rough ease. 
    - There’s a cubic-bezier() option, but it only allows 2 control points, so it’s pretty limited.
  - Use different eases for different properties in a CSS keyframe animation; eases apply to the whole keyframe.
  - Physics-based motion. 
    - For example, the smooth momentum-based flicking and snap-back implemented in this Draggable demo.
  - Animate the scroll position
  - Directional rotation (like “animate to exactly 270 degrees in the shortest direction, clockwise or counter-clockwise”).
  - Animate attributes.

- CSS animations are great for simple transitions between states (like rollovers) when compatibility with older browsers isn’t required. 3D transforms usually perform very well
- However, JavaScript-based animation delivers far more flexibility, better workflow for complex animations and rich interactivity, and it often performs just as fast (or even faster) than CSS-based animation despite what you may have heard.
- The W3C is working on a new spec called Web Animations that aims to solve a lot of the deficiencies in CSS Animations and CSS Transitions, providing better runtime controls and extra features. 
  - It certainly seems like a step forward in many ways, but it still has shortcomings (some of which are probably impossible to overcome due to the need for legacy support of existing CSS specifications, so for example, independent transform component control is unlikely). 

## CSS VS JavaScript Animations

- [google: CSS Versus JavaScript Animations](https://developers.google.com/web/fundamentals/design-and-ux/animations/css-vs-javascript)

- There are two primary ways to create animations on the web: with CSS and with JavaScript. 
- Which one you choose **really depends on the other dependencies of your project**, and what kinds of effects you're trying to achieve.
  - Use CSS animations for simpler "one-shot" transitions, like toggling UI element states.
  - Use JavaScript animations when you want to have advanced effects like bouncing, stop, pause, rewind, or slow down.
  - If you choose to animate with JavaScript, use the Web Animations API or a modern framework that you're comfortable with.

- Most basic animations can be created with either CSS or JavaScript, but the amount of effort and time differs
- Use CSS when you have smaller, self-contained states for UI elements. 
  - CSS transitions and animations are ideal for bringing a navigation menu in from the side, or showing a tooltip. 
  - You may end up using JavaScript to control the states, but the animations themselves will be in your CSS.
- Use JavaScript when you need significant control over your animations. 
  - The Web Animations API is the standards-based approach, available today in most modern browsers. 
  - This provides real objects, ideal for complex object-oriented applications. 
  - JavaScript is also useful when you need to stop, pause, slow down, or reverse your animations.
- Use `requestAnimationFrame` directly when you want to orchestrate an entire scene by hand. 
  - This is an advanced JavaScript approach, but can be useful if you're building a game or drawing to an HTML canvas.
- Alternatively, if you're already using a JavaScript framework that includes animation functionality, such as via jQuery's `.animate()` method or GreenSock's `TweenMax` , then you may find it more convenient overall to stick with that for your animations.

- Animating with CSS is the simplest way to get something moving on screen. 
  - This approach is described as declarative, because you specify what you'd like to happen.
  - If you create separate CSS classes to manage your animations, you can then use JavaScript to toggle each animation on and off
  - `box.classList.add('move');`
  - Doing this provides a nice balance to your apps. 
  - You can focus on managing state with JavaScript, and simply set the appropriate classes on the target elements, leaving the browser to handle the animations. 
  - In addition to using CSS transitions, you can also use CSS animations, which allow you to have much more control over individual animation keyframes, durations, and iterations.
- If you’re new to animations, keyframes are an old term from hand-drawn animations. 
  - Animators would create specific frames for a piece of action, called key frames, which would capture things like the most extreme part of some motion, and then they would set about drawing all the individual frames in between the keyframes. 
  - We have a similar process today with CSS animations, where we instruct the browser what values CSS properties need to have at given points, and it fills in the gaps.
- With CSS animations you define the animation itself independently of the target element, and use the `animation-name` property to choose the required animation.
- If you want your CSS animations to work on older browsers, you will need to add vendor prefixes.

- JavaScript animations are imperative, as you write them inline as part of your code. 
  - You can also encapsulate them inside other objects.
  - You can use the Web Animations API to either animate specific CSS properties or build composable effect objects.
  - By default, Web Animations only modify the presentation of an element. 
  - If you'd like to have your object remain at the location it has moved to, then you should modify its underlying styles when the animation has finished.
- With JavaScript animations, you're in total control of an element's styles at every step. 
  - This means you can slow down animations, pause them, stop them, reverse them, and manipulate elements as you see fit. 
  - This is especially useful if you're building complex, object-oriented applications, because you can properly encapsulate your behavior.

## Animations and Performance

- [google: Animations and Performance](https://developers.google.com/web/fundamentals/design-and-ux/animations/animations-and-performance#css-vs-javascript-performance)

- Maintain 60fps whenever you are animating, because any less results in stutters or stalls that will be noticeable to your users
  - Take care that your animations don’t cause performance issues; ensure that you know the impact of animating a given CSS property.
  - Animating properties that change the geometry of the page (layout) or cause painting are particularly expensive.
  - Where you can, stick to changing `transform` and `opacity` .
  - Use `will-change` to ensure that the browser knows what you plan to animate.

- Animating properties is not free, and some properties are cheaper to animate than others. 
  - For example, animating the `width` and `height` of an element changes its geometry and may cause other elements on the page to move or change size. 
  - This process is called layout (or reflow in Gecko-based browsers like Firefox), and can be expensive if your page has a lot of elements. 
  - Whenever layout is triggered, the page or part of it will normally need to be painted, which is typically even more expensive than the layout operation itself.
- Where you can, you should avoid animating properties that trigger layout or paint. 
  - For most modern browsers, this means limiting animations to `opacity` or `transform` , both of which the browser can highly optimize; 
  - it doesn’t matter if the animation is handled by JavaScript or CSS.
- Use the `will-change` to ensure the browser knows that you intend to change an element’s property. 
  - This allows the browser to put the most appropriate optimizations in place ahead of when you make the change. 
  - Don't overuse `will-change` , however, because doing so can cause the browser to waste resources, which in turn causes even more performance issues.
- The general rule of thumb is that if the animation might be triggered in the next 200ms, either by a user’s interaction or because of your application’s state, then having `will-change` on animating elements is a good idea. 
  - For most cases, then, any element in your app’s current view that you intend to animate should have `will-change` enabled for whichever properties you plan to change

- relative merits of CSS and JavaScript animations from a performance perspective
  - CSS-based animations, and Web Animations where supported natively, are typically handled on a thread known as the "compositor thread". 
    - This is different from the browser's "main thread", where styling, layout, painting, and JavaScript are executed. 
    - This means that if the browser is running some expensive tasks on the main thread, these animations can keep going without being interrupted.
  - Other changes to transform and opacity, in many cases, can also be handled by the compositor thread.
  - If any animation triggers paint, layout, or both, the "main thread" will be required to do work. 
    - This is true for both CSS- and JavaScript-based animations, and the overhead of layout or paint will likely dwarf(使显得矮小) any work associated with CSS or JavaScript execution, rendering the question moot(悬而未决的事；有争议的问题).

## CSS Animations vs Web Animations API

- [CSS Animations vs Web Animations API_201808](https://css-tricks.com/css-animations-vs-web-animations-api/)
  - [CSS Animation 与 Web Animation API 之争](https://zhuanlan.zhihu.com/p/27867539)
  - [精读《CSS Animations vs Web Animations API》](https://zhuanlan.zhihu.com/p/27903404)

- difference between CSS animation and WAAPI: the default of CSS is ease, while the default of WAAPI is linear.
- WAAPI provides the same performance improvements as CSS animations, although that doesn’t mean a smooth animation is inevitable. 
- I had hoped that the performance optimizations of this API would mean we could escape the use of `will-change` and the totally hacky `translateZ ` —  and eventually, it might. 
- However, at least in the current browser implementations, these properties can still be helpful and necessary in dealing with jank issues.
- If you have a positive delay, you don’t need `will-change` since the browser will layerize at the start of the delay and when the animation starts it will be ready to go.
- WAAPI gives us a syntax to do in JavaScript what we could already achieve in a stylesheet. 
  - If we decide to stick to CSS for our animations and transitions, we can interact with those animations with WAAPI.
- The features mentioned in this article are just the beginning. 
  - The current spec and implementation look to be the start of something great.

## Compare the options for Animations on the Web

- [Compare the options for Animations on the Web](https://flaviocopes.com/animations/)

- CSS Transitions
  - It’s the simplest of the animations, and mostly used for subtle animations that integrate well with the rest of the page.
- CSS Animations
  - allow you to have more than just 2 states
- SVG Animations
  - SVG is a great vector-based format which allows to create animations using SMIL, the SVG animations “native” format.
  - SMIL was about to be deprecated in Chrome, but the team reversed this decision for the time being due to resistance, although SMIL has cross-browser inconsistencies (and IE/Edge do not support it).
  - They want to push CSS Animations and the Web Animations API instead of SMIL.
- Canvas API Animations
  - The Canvas API offers a way to paint on the screen, using rasters rather than vectors.
  - Animations are possible although not as performant
- Web Animations API
  - It’s currently only working in Chrome and Firefox. Safari, IE and Edge are still considering it, 
  - but a polyfill exists to make it work across all browsers.
- In addition to the native APIs, there are great libraries that abstract most of the details for you:
  - GreenSock
  - react-motion
  - velocity
  - three.js
