---
title: web-components-blog
tags: [blog, web-components]
created: '2020-11-10T03:16:27.687Z'
modified: '2020-12-21T08:04:19.490Z'
---

# web-components-blog

# [Declarative Shadow DOM_202009](https://web.dev/declarative-shadow-dom/)

- Shadow DOM is one of the three Web Components standards, rounded out by HTML templates and Custom Elements. 
  - These features combined enable a system for building self-contained, reusable components that integrate seamlessly into existing applications just like a built-in HTML element.
  - Shadow DOM provides a way to scope CSS styles to a specific DOM subtree and isolate that subtree from the rest of the document
- Until now, the only way to use Shadow DOM was to construct a shadow root using JavaScript
  - An imperative API like this works fine for client-side rendering
  - However, many web applications need to render content server-side or to static HTML at build time. 
  - This can be an important part of delivering a reasonable experience to visitors who may not be capable of running JavaScript.
- The justifications(解释；正当理由) for Server-Side Rendering (SSR) vary from project to project. 
  - Some websites must provide fully functional server-rendered HTML in order to meet accessibility guidelines, 
  - others choose to deliver a baseline no-JavaScript experience as a way to guarantee good performance on slow connections or devices.
- Historically, it has been difficult to use Shadow DOM in combination with Server-Side Rendering because there was no built-in way to express Shadow Roots in the server-generated HTML. 
  - There are also performance implications when attaching Shadow Roots to DOM elements that have already been rendered without them. 
  - This can cause layout shifting after the page has loaded, or temporarily show a flash of unstyled content ("FOUC") while loading the Shadow Root's stylesheets.
- Declarative Shadow DOM (DSD) removes this limitation, bringing Shadow DOM to the server.
- A Declarative Shadow Root is a `<template>` element with a `shadowroot` attribute
  - A template element with the `shadowroot` attribute is detected by the HTML parser and immediately applied as the shadow root of its parent element. 
  - This gives us the benefits of Shadow DOM's encapsulation and slot projection in static HTML. 
  - No JavaScript is needed to produce the entire tree, including the Shadow Root.
- Declarative Shadow Dom also includes a new API for getting the HTML contents of an element. 
  - The new `getInnerHTML()` method works like `.innerHTML`, but provides an option to control whether shadow roots should be included in the returned HTML
- Components built using Custom Elements get automatically upgraded from static HTML. 
  - With the introduction of Declarative Shadow DOM, it's now possible for a Custom Element to have a shadow root before it gets upgraded.

# [Why I don't use web components_201906](https://dev.to/richharris/why-i-don-t-use-web-components-2cia)

- 仅供参考，标准及实现都已更新，文章中提到的部分问题已解决了

- I'm mostly writing this for my future self, so that I have something to point to next time someone asks why I'm a web component skeptic(怀疑论者), and why Svelte doesn't compile to custom elements by default. 
  - (It can compile to CEs, and it can consume CEs as evidenced by its perfect score on Custom Elements Everywhere.)
- Progressive enhancement
  - This may be an increasingly old-fashioned view, but I think that websites should work without JavaScript wherever possible. Web components don't.
  - With JavaScript enabled, it（example) progressively enhances — rather than opening a new tab, it opens a small popup window instead. But without, it still works fine.
  - By contrast, the web component HTML would look something like this.
  - which is useless and inaccessible, if JS is disabled or somehow broken, or the user is on an older browser.
- CSS in, err... JS
  - If you want to use Shadow DOM for style encapsulation, you have to include your CSS in a `<style>` element. 
  - The CSS-in-JS community in particular has been criticised for not putting CSS in .css files, and yet here we are.
- Platform fatigue(疲劳、厌倦)
  - more bugs on Chromium
  - It also creates complexity for developers, who are encouraged to learn these new features
- Polyfills
  - a Chrome-only feature
  - The three spec editors are all Googlers.
- Composition
  - slotted content renders eagerly in custom elements. 
  - It turns out that most of the time you want slotted content to render lazily.
- Confusion between props and attributes
- Leaky design
- The DOM is bad
- Global namespace
- These are all solved problems
  - The biggest frustration of all is that we already have really good component models. 
  - We're still learning, but the basic problem — keep the view in sync with some state by manipulating the DOM in a component-oriented fashion — has been solved for years.
  - Yet we're adding new features to the platform just to bring web components to parity with what we can already do in userland.

- discussion

- Web components are not React, Vue or Svelte components, they are not logical containers, 
  - they are true html elements that live in the document and they should be used like any other html element. 
  - Taking a web component and comparing it to an abstracted svelte component is totally misleading. 
  - They do different things.

# ref

- [google-dev: Building Web Components](https://developers.google.com/web/fundamentals/web-components)
- [How searching for a bundle-free React led me to web components_202008](https://www.bryanbraun.com/2020/08/31/how-searching-for-a-bundle-free-react-led-me-to-web-components/)
  - I couldn’t really use React in the bundle-free dev workflows
  - The problem is JSX—you gotta run it through Babel. There’s no way around it!
  - a few options:
    - Skip JSX and use React.createElement instead.
    - Replace JSX with a bundle-free alternative like hyperscript or htm.
    - Use a React-alternative written in Vanilla JS. 🏗
