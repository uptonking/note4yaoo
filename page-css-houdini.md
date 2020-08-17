---
title: page-css-houdini
tags: [css, houdini, proposal, roadmap, spec]
created: '2020-08-08T11:28:48.214Z'
modified: '2020-08-08T11:30:01.467Z'
---

# page-css-houdini

## [CSS Houdini](https://developer.mozilla.org/en-US/docs/Web/Houdini)

- Houdini is a set of low-level APIs that exposes parts of the CSS engine, giving developers the power to extend CSS by hooking into the styling and layout process of a browser’s rendering engine.  
- Houdini is a group of APIs that give developers direct access to the CSS Object Model (CSSOM), enabling developers to write code the browser can parse as CSS, thereby creating new CSS features without waiting for them to be implemented natively in browsers.
- Advantages of Houdini
- Houdini enables faster parse times than using JavaScript `.style` for style changes.
  - Browsers parse the CSSOM — including layout, paint, and composite processes — before applying any style updates found in scripts. 
  - In addition, layout, paint, and composite processes are repeated for JavaScript style updates. 
  - Houdini code doesn't wait for that first rendering cycle to be complete. 
  - Rather, it is included in that first cycle — creating renderable, understandable styles. 
  - Houdini provides an object-based API for working with CSS values in JavaScript.
- With Houdini you could invent your own masonry, grid, or regions implementation, 
  - but doing so is not necessarily the best idea. 
  - The CSS Working group does a lot of work to ensure every feature is performant, handles all edge cases, and considers security, privacy, and accessibility. 
  - As you extend CSS with Houdini, make sure to keep these considerations in mind
- The Houdini APIs
  - **CSS Parser API**
    - An API exposing the CSS parser more directly, for parsing arbitrary CSS-like languages into a mildly typed representation.
  - **CSS Properties and Values API** 
    - Defines an API for registering new CSS properties. 
    - Properties registered using this API are provided with a parse syntax that defines a type, inheritance behaviour, and an initial value.
    - allows the registration of css custom properties, allowing for property type checking, default values, and properties that do or do not inherit their value.
  - **CSS Typed OM**
    - Converting CSSOM value strings into meaningfully typed JavaScript representations and back can incur a significant performance overhead. 
    - The CSS Typed OM exposes CSS values as typed JavaScript objects to allow their performant manipulation.
    - The CSS Typed OM makes CSS manipulation more logical and performant by providing object features (rather than CSSOM string manipulation), providing access to types, methods, and an object model for CSS values.
  - **CSS Layout API** 
    - Designed to improve the extensibility of CSS, this API enables developers to write their own layout algorithms, like masonry or line snapping. 
    - It is not yet natively available.
  - **CSS Painting API**
    - Developed to improve the extensibility of CSS — allows developers to write JavaScript functions that can draw directly into an element's background, border, or content via the `paint()` CSS function.
  - **Worklets**
    - An API for running scripts in various stages of the rendering pipeline independent of the main JavaScript execution environment. 
    - Worklets are conceptually similar to Web Workers, and are called by and extend the rendering engine.
    - With worklets, you can create modular CSS, requiring a single line of JavaScript to import configureable components: no pre-processors, post-processors or JavaScript frameworks needed.

## [Houdini: Demystifying CSS](https://developers.google.com/web/updates/2016/05/houdini)

- The Houdini task force consists of engineers from Mozilla, Apple, Opera, Microsoft, HP, Intel and Google working together to expose certain parts of the CSS engine to web developers. 
- The task force is working on a collection of drafts with the goal to get them accepted by the W3C to become actual web standards. 
- They set themselves a few high-level goals, turned them into specification drafts which in turn gave birth to a set of supporting, lower-level specification drafts. 
- The collection of these drafts is what is usually meant when someone talks about **Houdini**. 
- At the time of writing, the list of drafts is incomplete and some of the drafts are mere placeholders. That’s how early in development of Houdini we are.
