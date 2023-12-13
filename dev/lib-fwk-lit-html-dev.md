---
title: lib-fwk-lit-html-dev
tags: [lib, lit-html, tagged-template-literals]
created: 2020-11-08T10:39:49.902Z
modified: 2021-05-13T02:48:27.497Z
---

# lib-fwk-lit-html-dev

# guide

- lit-html特点
  - standard js, no compiler needed
  - no vdom
- lit-element特点

- [lit/dev-docs/design/how-lit-html-works.md](https://github.com/lit/lit/blob/main/dev-docs/design/how-lit-html-works.md)

- ## [How it Works](https://github.com/Polymer/lit-html/wiki/How-it-Works)
- This is a deep-dive into how lit-html works, what makes it fast, how the code is organized, and what could be improved. 
- lit-html is an HTML templating library. 
  - Templates are written in JavaScript by mixing static HTML strings and dynamic JavaScript values using template literals. 
  - lit-html enables a functional/UI-as-data programming model, fast initial rendering, and fast updates that minimally update DOM when state changes.
  - The key that enables this is separating static parts of templates from the dynamic parts with template literals, and never traversing or updating the static parts after the initial render.
- Phases of Template Rendering
  1. Define
  2. Prepare
  3. Create
  4. Update

- ## Since lit-html uses web components, how is it different from React components ?
- https://twitter.com/h4rishabh/status/1280178522062012417
- To clarify, lit-html doesn't require web components
  - it just renders standard HTML which includes web components. 
  - But since lit-html doesn't have its own component model, web components are a natural fit. 
  - We have users who don't use WCs though, they'll use only render functions.
  - Yeah, the separation of template system from component model can be confusing for some, especially as basically every framework unnecessarily ties the two together.
- lit-html is different from React in a lot of ways. Conceptually it enables the same `UI=f(state)` pattern as React, but:
  * it's standard JS syntax
  * doesn't need a compiler
  * doesn't use vdom
  * is smaller
  * separates static & dynamic content, and so
  * is a lot faster
- lit-html also has more features for creating DOM:
  - it can set attributes & properties, 
  - add event handlers vis addEventListener (rather than needing event props), 
  - create any DOM parsable by innerHTML (like templates and comments), 
  - can handle more data types like Nodes.
- It's also very robust against 3rd party DOM operations. 
  - Since it only updates DOM where expressions are, 3rd party code can modify other DOM from templates and lit-html doesn't care - it just skips over it.
- Finally, directives are a powerful API for customizing rendering. 
  - 1st party directives handle things like 
    - rendering strings as raw HTML, 
    - caching DOM chunks between switching renders (think tabs), 
    - removing attributes if data is missing 
    - and diffing against live property values.

- ## [How is lit-html efficient without template compilation?](https://github.com/Polymer/lit-html/issues/944)
- Really enjoying this lib and it's simplicity and use of JS for logic.
  - Handlebars has `compile()`, JSX has build time compilation to functions, many others have build compilation. 
  - I'm wondering how, since we don't pre-compile lit templates, are they still efficient? 
- lit-html prepares templates the first time they're rendered, not every execution. 
  - The preparation step records where the expressions are in the DOM so that on the changing expressions are ever updated.
# roadmap
- [Reactive controller adapters for other frameworks](https://github.com/Polymer/lit-html/issues/1682)
  - We would like to enable a framework-agnostic subset of reactive controller to work across frameworks.
# pieces
- The primary drawback of lit-html to me is that it doesn't seem to work with Typescript as well as JSX does (specifically for custom component props)
  - This is the territory of linting/IDE plugins, as popularity picks up these things will come as well. But you're right today there is more for JSX.
  - I usually only create a web component for the view and then create functions that return a template for the components
# discuss-vdom
- ## 

- ## 

- ## 📝 [[design-doc] How lit-html works_202306](https://github.com/lit/lit/pull/3931/commits/7f4aad3b3cb03eb334536441c4a2957639fe0b3c)
- Comparison to Virtual DOM
- lit-html is comparable in many ways to virtual-DOM (VDOM) approaches, but it works without storing a separate representation of the DOM in memory, or computing DOM diffs like virtual-DOM libraries must do.
- Where VDOMs work at the level of the DOM representation of a UI, lit-html works at the _value_ level.
- lit-html UIs are values, like VDOM, but instead of each DOM node being represented as a single value, the DOM structure is represented by a reference to a template.
- lit-html only tracks the tree of dynamic values (called `Parts` ) that is more sparse than the associated DOM tree, so traversing dynamic values when necessary is faster.

# discuss

 

- ## [怎么评价 lit-html ?](https://www.zhihu.com/question/269188214/answers/updated)
- 先说结论：不考虑在工程中使用
  - 快速渲染DOM
  - 很容易接入状态管理工具
  - 不需要构建工具（评：意味着不高的浏览器兼容性）
  - 很小的体积（评：更适合C端）
  - 支持promise注入（评：鸡肋，直接在view层调promise，只适合小应用。api复用怎么办？状态管理怎么办？）

- ## I was bit confused about using lit-html over React 
- https://twitter.com/h4rishabh/status/1280185672632958977
- I would kind of think of `lit-html` like everything that happens when React renders. 
  - Or put another way: lit-html isn't a complete replacement for React. 
  - If that's what you want, I'd look into lit-element (which uses lit-html under the hood for rendering).
- A huge benefit of lit-html over React is lit-html does not use a Virtual DOM. 
  - VDOM is super inefficient (checks every live node against every new virtual node), so the middle ground of lit-html (checks only dynamic nodes) gives you huge performance improvements
- Another huge benefit of lit-html is you'll be writing extremely standard JavaScript and HTML.
  - The only parts of the library that aren't standard are 3 declarative sigils: ".", "@", and "?" which allow you to programmatically bind to properties, events, and boolean attributes
  - Everything else you write will be normal JavaScript and tagged template literals, which means the skills and patterns you use will be reusable anywhere.
- If what you're looking for *is* a complete React replacement, look into lit-element. All of the same statements apply with these added things:
  - The component model you'll be working in is built into the browser
  - You get CSS isolation by default (if you can use shadowDOM)
- You'll never be locked into a framework because what you're using is basically just a base Class on top of the platform-native component model.
  - I sometimes recommend (if you have time) building your own component base class to see how you might solve the same problems
- I found that after about a day of work, I had a base class similar to lit-element, but it was much less efficient and much less flexible.
  - I switched to lit-element because I know if it ever becomes a problem, I can replace it with something else that depends on the platform
- Aside from the natural interoperability of web components, low-lock-in is one of our goals with LitElement. 
  - It shouldn't do so much that you can't easily migrate away from it.

- ## use lit-html with polymer components?
- https://twitter.com/aboodman/status/1306299867757641728
- Material Web Components are made with LitElement and lit-html 
- Inputs are a special case because they maintain their own state. There are two ways to handle that:
  1. Listen for an `input` event and update your state to match
  2. Use the live() directive to always defer to the input's state
- It seems like the issue is that I can't really find many libraries designed to work with lit-html in a "controlled" mode. 
  - As we discussed before all the Google-provided widgets seem to be uncontrolled. 
  - But also, most 3p libs for polymer (or the web generally) mutate dom directly.
- So the result is that though technically you can use lit-html controlled (one-way dataflow) like React, 
  - in practice this is difficult today because you're on your own for all widgets.
- I'm not sure I understand the issue.
  - Just like stateful built-in elements, a stateful web component can be used in a "controlled" way with some fairly simple event handling and state management.

- ## What's the purpose of lit-html and hyperhtml?
- https://www.reddit.com/r/javascript/comments/8iydo2/whats_the_purpose_of_lithtml_and_hyperhtml/
- lit-html is a replacement for vdom, and is a little lower level than what something like react does. 
  - It may someday be the basis for a framework like react though.
- It's a different take on solving the same problem that VDOM solves; declarative DOM construction.
  - You write your DOM how you'd like it to look, 
  - and you pass values directly to the elements (either as properties or as attributes) in the DOM (like with React etc.). 
  - This way, your mental model of the DOM is simpler, since you don't have to juggle `document.createElement` and `document.querySelector` etc.
- It's a solution that doesn't use JSX, template strings serve the same purpose, 
  - so you don't have to spend half your time on the boilerplate Webpack/build setup before you actually code. 
  - It's just plain JS. 

# ref
- [The history of hyperHTML followed by lit-html](https://gist.github.com/WebReflection/ab43649d9e4a53ac900b5924c77a310e)
- [Easy apps with hyperHTML — 1, wire/bind_201809](https://dev.to/pinguxx/easy-apps-with-hyperhtml-1-31cc)
