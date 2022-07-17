---
title: web-animations-api-waapi-docs
tags: [animation, docs, waapi, web]
created: 2020-08-02T13:35:01.695Z
modified: 2021-09-22T04:13:57.615Z
---

# web-animations-api-waapi-docs

# pieces

- https://caniuse.com/web-animation
  - usage: 93.66% (202103), 除IE外都支持

# Web Animations API (WAAPI)

- The Web Animations API allows for synchronizing and timing changes to the presentation of a Web page, i.e. animation of DOM elements. 
  - It does so by combining two models: the Timing Model and the Animation Model.
- The Web Animations API opens the browser’s animation engine to developers and manipulation by JavaScript. 
  - This API was designed to underlie(构成sth的基础) implementations of both CSS Animations and CSS Transitions, and leaves the door open to future animation effects. 
  - It is one of the most performant ways to animate on the Web, letting the browser make its own internal optimizations without hacks, coercion, or `window.requestAnimationFrame()` .
- With the Web Animations API, we can move interactive animations from stylesheets to JavaScript, separating presentation from behavior. 
  - We no longer need to rely on DOM-heavy techniques such as writing CSS properties and scoping classes onto elements to control playback direction. 
  - And unlike pure, declarative CSS, JavaScript also lets us dynamically set values from properties to durations.
- For building custom animation libraries and creating interactive animations, the Web Animations API might be the perfect tool for the job.
- Over a decade ago, SMIL brought animation to SVG. 
  - Back then it was the only animation engine browsers had to worry about. 
  - While four out of five browsers supported SMIL, it only animated SVG elements, could not be used from CSS, and was very complex — often leading to inconsistent implementations. 
- Ten years later, the Safari team introduced the CSS Animations and CSS Transitions specs.
- The Internet Explorer team requested an animations API to consolidate and normalize animation functionality across all browsers, and thus efforts began in earnest among Mozilla Firefox and Google Chrome developers to create the one animation spec to rule them all: the Web Animations API.
- The Web Animations API runs on top of two models, one that handles time—Timing—and one that handles visual change over time—Animation.
- The Timing Model keeps track of how far along a set timeline we've come. 
- The Animation Model determines what the animated object should look like at any given time.
- Web animations consist of Timeline Objects, Animation Objects, and Animation Effect Objects working together. By assembling these disparate objects, we can create animations of our own.

# ref

- [Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API)
- [Using the Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Using_the_Web_Animations_API)
- [Web Animations API Concepts](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Web_Animations_API_Concepts)
- https://caniuse.com/#feat=web-animation
  - some browsers may support only level 1
