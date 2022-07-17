---
title: lib-fwk-lit-html-blog
tags: [blog, lit-html]
created: 2021-01-07T19:22:44.082Z
modified: 2021-05-13T02:48:04.397Z
---

# lib-fwk-lit-html-blog

# popular

## [Lit 2.0: New name, new site, new version: smaller, better, faster, and SSR-ready.](https://lit.dev/blog/2021-04-21-lit-2.0-meet-lit-all-over-again/)

- [Upgrade guide](https://lit.dev/docs/releases/upgrade/)

- Our major goals for Lit 2.0 were to reduce size, add powerful new features, improve performance and make some key changes under the hood to facilitate server-side rendering (SSR) — all while minimizing breaking changes.
-  Lit 2.0 is:
  - Smaller. 
    - Lit 2.0’s templating system weighs in at 2.8k (minified and compressed), 10% smaller than the previous version, 
    - and its complete component base class (including templating) is just 5.2k, 20% smaller than before.
  - Better. 
    - Meanwhile, we’ve added a raft of new features, including several templating enhancements; 
    - a clean, new, class-based API for directive authors; 
    - and reactive controllers, a powerful new primitive for sharing stateful logic between components.
  - Faster. 
    - Efficient rendering has always been one of our core values, and Lit 2.0 is speedier than ever before: 
    - up to 20% faster on initial render, and up to 15% faster on updates.
  - Server. 
    - Lit 2.0 includes the foundation for fast, streaming SSR and flexible client-side hydration, 
    - unlocking a full range of use cases — from integration with popular frameworks (e.g., Next.js) and static site generators (e.g., eleventy) to apps built entirely with Lit and other web components.

## [lit-html, JavaScript templating from the Polymer team at Google_201708](https://malloc.fi/lit-html-javascript-templating-from-polymer-team-google)

- Producing HTML output in JavaScript remains an unsettled area. 
- There are many schools of thought here. 
  - Some are still using traditional back end focused templating languages like Handlebars or Twig in JavaScript, 
  - while at the other extreme developers want to do templating in pure JS. 
  - While Vue.js and Angular have their own syntaxes, W3C Web Components have used the HTML Templates standard.
- So there is no shortage of options for doing templating in JavaScript. 
  - Currently the top of mind options are "Just JavaScript" templating approaches such as the JSX format from React, and custom templating syntaxes like the one from Vue.js or the one from Angular.
  - In addition there is the native HTML template specification used by Polymer, and the HTML Literals usable in *any* project using ES6+.
- The sheer number of options and the lack of a de-facto standard shows that there is room for improvement in the area
  - The Polymer team team at Google agrees and have developed an interesting alternative called lit-html
  - they have worked on a hybrid solution, where ES6+ templates literals are used together with concepts familiar to users of the JSX template format.
- lit-html has JSX like syntax based on Web Standards
- The lit-html project is somewhat aimed at this critique, and it has four major goals it aims to fulfill:
  - Efficient updates of previously rendered DOM
  - Easy access the JavaScript state that needs to be injected into DOM
  - Standard syntax without required build steps, understandable by standards-compliant tools
  - Very small size
- In browser implementations, dynamic DOM updates are often seen to be as inefficient. 
  - Lit-html does offer an improvement over raw DOM manipulation that the team claims is an improvement over virtual DOM based libraries like React. 

# more
