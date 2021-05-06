---
title: web-animations-api-blog
tags: [animation, waapi, web]
created: '2020-08-03T06:38:58.197Z'
modified: '2020-12-21T07:44:33.306Z'
---

# web-animations-api-blog

# Web Animations API Tutorial Series

- ## [Let’s talk about the Web Animations API_Dan Wilson](http://danielcwilson.com/blog/2015/07/animations-intro/)
  - This is an introduction to a tutorial series on the Web Animations API coming to browsers. 
  - That wasn’t implemented yet (you’ll find out what happened in Part 5), but its goal of providing a way to unite the CSS, JS, and SVG ways to animate kept me interested. 
  - CSS has hardware acceleration for smooth transitions and support is built into the browser, 
    - but rules are declared in CSS and require jumping through JavaScript hoops to get values dynamically changed.
  - `requestAnimationFrame` has good support and lets the browser optimize when to animate, 
    - but it can still hang up if there is a lot of other JavaScript running. 
    - It also often requires more math to get timing down.
  - `setInterval` introduced many developers to animations, 
    - but it is imprecise and can lead to stuttering animations.
  - `jQuery.animate()` introduced several other developers to animations, but often has performance issues.
  - Libraries such as Velocity and GreenSock (GSAP) improve JavaScript performance and have been tested in many situations to be the best they can be. 
    - They still, however, require maintaining and loading external libraries.
  - In general, we like it when browsers support as much as they can, and they take over the optimizations. 
    - Browsers now have `document.querySelector` because we saw the value jQuery provided to select DOM elements. 
    - So utilities in libraries moved into the browser natively. 
    - Ideally, we could pack as much animation control at the browser level. 
    - These libraries can then focus on providing newer features, and the cycle can continue.
  - The Web Animations API tries to do this. 
    - It aims to bring the power of CSS performance, add the benefits and flexibility of JavaScript (and SVG animation, which we will talk about in a future post), and leave it to the browsers to make it work well.
    - The syntax is similar to CSS but adds the options of variables, controls, and finish callbacks.

- ## [Web Animations API Tutorial Part 1: Creating a Basic Animation](http://danielcwilson.com/blog/2015/07/animations-part-1/)
- ## [Web Animations API Tutorial Part 2: The Animation & Timeline Controls](http://danielcwilson.com/blog/2015/07/animations-part-2/)
- ## [Web Animations API Tutorial Part 3: Multiple Animations](http://danielcwilson.com/blog/2015/08/animations-part-3/)
- ## [Web Animations API Tutorial Part 4: GroupEffects & SequenceEffects](http://danielcwilson.com/blog/2015/09/animations-part-4/)
- ## [Web Animations API Tutorial Part 5: The Loveable Motion Path](http://danielcwilson.com/blog/2015/09/animations-part-5/)

- ## [Web Animations API Tutorial Conclusion](http://danielcwilson.com/blog/2015/09/animations-conclusion/)
  - The spec, browser implementations, and polyfill have been going on for a while, and they are ready to examine closely.

- ## [When to Use the Web Animations API_201608](http://danielcwilson.com/blog/2016/08/why-waapi/)
  - I still typically prefer CSS for animating. 
    - You state an animation once, and all matching selectors will pick up on it without you having to iterate through them all. 
    - There’s a reason over time we’ve seen things move from JS to CSS, and for me it’s hard to beat declaring some rules in CSS and calling it a day.
  - So Why Go with the API?
    - Dynamic/Random/New Values
    - A Plethora of Class Toggles
    - Playback Control
    - Chaining Multiple Animations
  - The Web Animations spec that underlies the Web Animations API is all about uniting JS and CSS methods.

- ## [3 Ways to Use Independent Transform Properties](http://danielcwilson.com/blog/2017/10/all-the-transform-ways/)
- ## [Additive Animation with the Web Animations API](http://danielcwilson.com/blog/2018/01/additive-animation/)

- ## [CSS + the Web Animations API_202004](http://danielcwilson.com/blog/2020/04/css-in-the-waapi/)
  - While the Web Animations API initially brought a similar mechanism as CSS animations to JavaScript, it also added a few additional features like modifying playback rate and jumping to different points in an animation’s timeline. 
  - As the final pieces of the Web Animations Level 1 specification roll out to browsers, it’s not just JavaScript that gets extra features.
  - Getting all Web Animations with the API
    - One of the newer pieces now available is the ability to get references to all the animations for a specific element or even a full document. 
    - `document.getAnimations();`
    - The best part is that this new Web Animations API method does not just return animations that were created with the Web Animations API, but also CSS Animations and CSS Transitions. 
    - Any API method can then be called on the CSS animations and transitions as though it had been created by the API.
  - How do I know where an animation was created?
    - Each animation that appears in the `getAnimations()` array today will be of type `Animation` , `CSSAnimation` , or `CSSTransition` .
    - This means each type will have the normal Web Animations API methods, but the two CSS ones will have an extra property that are specific to those needs.
      - animationName, transitionProperty
    - If you need to know which WAAPI animation is which, you can look at the keyframes or timing options, or specify an `id` at creation which is returned back.
  - Extending CSS Animations with the Web Animations API
    - Since all these animations share a common interface and have the same underlying engine behind them (one of the main goals of the Web Animations specification), we can now use the API to interact with our CSS animations.
  - CSS animations and transitions have long had solid JavaScript event listeners for `animationend` , `transitionstart` , and others, so the Web Animations API does not bring much new here. That said, the WAAPI offers comparable callbacks and Promises if those are preferred.

# Web Animations in Safari 13.1

- [webkit: Web Animations in Safari 13.1_202004](https://webkit.org/blog/10266/web-animations-in-safari-13-1/)

- With the release of iOS 13.4, iPadOS 13.4, and Safari 13.1 in macOS Catalina 10.15.4, web developers have a new API at their disposal: Web Animations. 
- As a web developer, I’ve enjoyed the simplicity and great performance of CSS Animations and CSS Transitions.
- However, in my day-to-day work, I also found a few areas where these technologies were frustrating: dynamic creation, playback control, and monitoring an animation’s lifecycle.
- The great news is that these issues are all taken care of by the new Web Animations API

- Animation Creation
  - While CSS allows you to very easily animate a state change (the appearance of a button, for instance), it will be a lot trickier if the start and end values of a given animation are not known ahead of time.
  - Forcing a style invalidation will not let the browser perform that task at the time it will judge most appropriate.
  - And if you consider using CSS Animations instead, you would have to first generate a dedicated `@keyframes` rule and insert it inside a `<style>` element, failing to encapsulate what is really a targeted style change for a single element and causing a costly style invalidation.

``` JS
// Set the transition properties and start value.
element.style.transitionProperty = "transform";
element.style.transitionDuration = "1s";
element.style.transform = "translateX(0)";

// Force a style invalidation such that the start value is recorded.
window.getComputedStyle(element);

// Now, set the end value.
element.style.transform = "translateX(100px)";
```

- The value of the Web Animations API lies in having a JavaScript API that preserves the ability to let the browser engine do the heavy lifting of running animations efficiently while enabling more advanced control of your animations.
- Now the browser will be able to process all new animations at the next most opportune moment with no need to force a style invalidation. 
  - This means that animations you author yourself as well as animations that may originate from a third-party JavaScript library – or even in a different document (for instance, via an `<iframe>` ) – will all be started and progress in sync.

- Playback Control
  - While the `animation-play-state` property allows control of whether a CSS Animation is paused or playing, there is no equivalent for CSS Transitions and it only controls one aspect of playback control. 
  - If you want to set the current time of an animation, you can only resort to roundabout techniques such as clever manipulations of negative animation-delay values, and if you want to change the speed at which an animation plays, the only option is to manipulate the timing values.
  - WAAPI gives developers control over the behavior of animations after they have been created. 

- Animation Lifecycle
  - While the `transition*` and `animation*` family of DOM events provide information about when CSS-originated animations start and end, it is difficult to use them correctly.
  - Using the Web Animations API, writing this kind of code is not just easier but safer because you have a direct reference to an `Animation` object rather than working through animation events scoped to an element’s hierarchy. 

- Web Animations are not designed to replace existing technologies but rather to tightly integrate with them. 
  - You are free to use whichever technology you feel fits your use case and preferences best.
- The Web Animations specification does not just define an API but also aims to provide a shared model for animations on the web; 
  - other specifications dealing with animations are defined with the same model and terminology. 
  - As such, it’s best to understand Web Animations as the foundation for animations on the web, and think of its API as well as CSS Transitions and CSS Animations as layers above that shared foundation.

- To make a great implementation of the Web Animations API, we had to start off fresh with a brand new and shared animation engine for CSS Animations, CSS Transitions, and the new Web Animations API.
  - Even if you don’t use the Web Animations API, the CSS Animations and CSS Transitions you’ve authored are now running in the new Web Animations engine.
  - No matter which technology you choose, the animations will all run and update in sync, events dispatched by CSS-originated animation and the Web Animations API will be delivered together, etc.
  - But what may matter even more to authors is that the entire Web Animations API is available to query and control CSS-originated animations! 
  - You can specify animations in pure CSS but also control them with the Web Animations APIs using `Document.getAnimations()` and `Element.getAnimations()` .

- At this stage, SVG Animations remain distinct from the Web Animations model, and there is no integration between the Web Animations API and SVG. 
  - This remains an area of improvement for the Web platform.

- Shipping support for Web Animations is an important milestone for animations in WebKit. 
  - Our new animation engine provides a more spec-compliant and forward-looking codebase to improve on. 

# Web Animations in WebKit

- [Web Animations in WebKit_201806](https://webkit.org/blog/8343/web-animations-in-webkit/)

- Browser engines have supported various animation features for many years, CSS Transitions and CSS Animations being two widely-supported approaches to authoring efficient animations on the Web. 
- While these features have proven popular, they become limited when developers try to integrate browser-implemented animations via JavaScript:
  - Creating a CSS Transition dynamically requires forcing or waiting for a style invalidation(失效) so start and end values can be specified
  - Creating CSS Animations dynamically requires `@keyframe` rules to be generated and inserted in a global stylesheet
  - Animations created via CSS are not represented via JavaScript and cannot be queried or controlled
- The value of Web Animations lies in having a JavaScript API that preserves the ability to let the browser engine do the heavy lifting of running animations efficiently while enabling more advanced control of your animations. 
- The Web Animations specification goes further than specifying a JavaScript API. 
  - It provides a timing and animation model for web browsers to implement features such as CSS Transitions and CSS Animations. 
  - In fact, in WebKit, we’ve updated our implementation of these existing CSS technologies so that the same CSS Transitions and Animations you’ve been authoring for years are now represented as Web Animations objects in the browser. 
  - Using the `getAnimations()` method, you can obtain a reference to a `CSSTransition` or `CSSAnimation` object which are `Animation` subclasses. 
  - Then you can seek or pause a CSS transition running on an element just like we did above with an animation created using `element.animate()` . 
  - As a developer, you can think of CSS Transitions and Animations as a declarative layer above Web Animations.

# Web Animations API improvements in Chromium 84

- [Web Animations API improvements in Chromium 84_202005](https://web.dev/web-animations/)

- Orchestrating animations with promises, performance improvements with replaceable animations, smoother animations with composite modes, and more.

- The Web Animations API is a tool that enables developers to write imperative animations with JavaScript. 
- It was written to underpin(巩固，构成sth的基础) both CSS animation and transition implementations and enable future effects to be developed, as well as existing effects to be composed and timed.

！[The long history of the Web Animations API](https://webdev.imgix.net/web-animations/waapi-timeline.png)

- Creating an animation via the Web Animations API should feel very familiar if you've used `@keyframe` rules
- The amount of code is about the same, but with JavaScript, you get a couple of superpowers that you don't have with CSS alone. This includes the ability to sequence effects, and an increased control of their play states.
- Example: Dynamic interactions with partial keyframes 
- When creating animations based on events, such as on `mousemove` , a new animation is created each time, which can quickly consume memory and degrade performance. 
  - To address this problem, **replaceable animations** were introduced in Chromium 83, enabling automated cleanup, where finished animations are flagged as replaceable and automatically removed if replaced by another finished animation. 

# Web Animations API Now Supported in All Evergreen Browsers

- [Web Animations API Now Supported in All Evergreen Browsers](https://www.infoq.com/news/2020/06/web-animations-evergreen-browser/)

- With the release of Safari 13.1, the Web Animations API now ships with all evergreen browsers.
- Early animations in web browsers were typically created with JavaScript APIs.
  - This approach was flexible but could not easily allow browsers to optimize animations with hardware acceleration or hooks into the layout and rendering pipeline.
- CSS Animations and CSS Transitions were first introduced by the WebKit team in 2007 and eventually became web standards. 
  - These APIs are easy to use and overcome the challenges of early JavaScript animation implementations.
- However, CSS animations and transitions have known limitations, particularly around the dynamic creation of animations, controlling the playback of animations, and monitoring the lifecycle of an animation.
- The Web Animations API introduces a solution that gives the optimization power of CSS animations and transitions, but the flexibility of earlier JavaScript-based APIs. 
- The Web Animations specification provides a shared model for animations on the web. CSS Transitions and CSS Animations exist as layers above that shared foundational model.

# ref

- [Exploring the Web Animations API_202001](https://www.javascriptjanuary.com/blog/exploring-web-animations-api)
  - In terms of performance, I haven't been able to see much difference between using CSS animations and the Web Animations API but that could be because my example is pretty small.
  - From what I understand, one big advantage is that, compared to other ways of animating using JavaScript, the WAAPI runs on the compositor, so we're letting the main thread forget about animations and deal with the rest of our code.
- [Animating like you just don’t care with Element.animate](https://hacks.mozilla.org/2016/08/animating-like-you-just-dont-care-with-element-animate/)
  - With the release of Firefox 48, `Element.animate()` is implemented in release versions of both Firefox and Chrome. 
    - Furthermore, there’s a polyfill( `web-animations.min.js` ) that will fall back to using `requestAnimationFrame` for browsers that don’t yet support Element.animate(). 
    - In fact, if you’re using a framework like Polymer, you might already be using it!
  - Of course, you can get the same effect by using CSS Animations and CSS Transitions — in fact, in browsers that support Web Animations, the same engine is also used to drive CSS Animations and Transitions — but for some applications, script is a better fit.
