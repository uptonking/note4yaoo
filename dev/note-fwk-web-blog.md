---
title: note-fwk-web-blog
tags: [blog, framework, web]
created: 2020-11-08T10:01:14.339Z
modified: 2020-12-08T13:29:35.248Z
---

# note-fwk-web-blog

# web-framework-comparison

## [Why I Finally Chose React over Vue.js](https://javascript.plainenglish.io/why-i-finally-chose-react-over-vue-f090cb0e097a)

- After some years building apps with both libraries, I’ve found that I prefer React. 
- It’s not because React is more popular
- Vue.js is easier — but not enough that it makes a difference
- So, if both libraries are so similar, and each has its pros and cons, why do I prefer React?
- The answer ultimately lies in JSX, React’s templating system. 
  - Whereas Vue uses XML with embedded Javascript, JSX is truly Javascript, only formatted like XML.
  - React, therefore, is JavaScript all the way down — and this has two important benefits.

### Better compatibility with TypeScript

- To understand the value of Typescript compatibility, we need to review the benefits of having a type system in the first place.
- For one, it makes code more readable. 
  - it’s beneficial to future you as you scale the application.
- Second, a type system helps you design more robust abstractions. 
- A final benefit of TypeScript is its help in quickly catching subtle bugs.
- All these benefits mean faster development and fewer bugs, improvements that see increasing returns as the complexity of the application grows.
- JSX = more types
- Every part of a JSX element can (and should) be typed: components, props, children, and so on.
- for a library to integrate well with Typescript, all of its features must be easily typed. Thanks to JSX, React easily meets this criteria.
- Indeed, it is possible to type many of these elements in Vue as well, but the effort required is often greater
- React’s larger ecosystem does make a difference
- React libraries and add-ons are more likely to support TypeScript.

### A more functional paradigm

- In math and computer science, a function is an operation that consumes some inputs and returns some output. 
- The best functions are pure and deterministic.
- Pure functions have no side effects; they ignore state and care only about the inputs to the function.
- Deterministic functions always return the same output given the same inputs.
- These functions are easier to test, simpler to think about, and improve code readability.
- Since JSX is JavaScript, we can treat JSX elements as first-class variables. 
- The difference may appear insignificant, but there are two distinct disadvantages to Vue’s organization. 
  - First, it spreads code for one part of the component across the entire file. 
  - Second, it’s unclear just from looking at the formatAsMoney method where the method is used or what will happen if it’s changed or removed.
- Another important difference between React and Vue is how child components pass data up to parents. 
  - In React, the parent component passes a function to the child that the child calls; 
  - this pattern demands an advanced understanding of functional JavaScript, but is far more powerful and flexible than Vue’s `emit` pattern. 
  - And because React’s functional pattern is truer to Javascript, it also offers superior TypeScript compatibility.

- I’ll close with some final advice: don’t make an important tech decision without fully understanding your options.
  - Take the time to become proficient at Vue/React to understand its strong and weak points. 
  - Whatever you pick, your choice shouldn’t determine the quality of your end product, and it certainly shouldn’t determine the quality of your code
- Sort out your wants and needs as a team, discuss the pros and cons of your options, and reach an agreement that satisfies as much of your team as possible.

## [lit-html vs hyperHTML vs lighterhtml_201902](https://webreflection.medium.com/lit-html-vs-hyperhtml-vs-lighterhtml-c084abfe1285)

- When `lit-html` released at the end of July 2017 as an experimental, not production ready, library, 
  - I’ve created few days after a huge gist comparing it with what was, at that time, the already production ready `hyperHTML`.
- `lighterhtml` was also recently born as hyperHTML drop-in simplified alternative, making the comparison actually fair
- To start with, hyperHTML has a viperHTML node server side alter ego, with API features parity, asynchronous streamed renders, and components.
  - viperHTML is isomorphic hyperHTML , but deprecated
  - This is also true for most modern alternatives of mine, such as ucontent, but if that's the only deal breaker, have a look at heresy-ssr, which is 1:1 based on lighterhtml, hence likely always 100% in features parity with it, 
- Removing all these features, plus simplifying the API, was the goal of lighterhtml, 
  - which in its 0.9 version is as fast as lit-html, but also always smaller, in size, than hyperHTML

- **lit-html VS lighterhtml**
- It is true that lit-html might be slightly richer in features, if you use its directives, 
  - but what I consider important here, is what we can do with just their core, summarized as such:
    - be as standard based as possible
    - create, and use, arbitrary DOM content
    - be able to quickly change content on the page (aka: DOM diffing)
  - These points are what lit-html core offers as a whole, while lighterhtml includes some extra feature we’ll see, and compare, later on.

- How much standard ?
  - Both lighterhtml and lit-html are based on “just standards”, meaning you can use JS without the need to transpile it, and you declare HTML, or SVG, through template literals.
- As developer, you don’t need to do anything different than writing HTML as you know, the library will figure out at runtime, 
  - accordingly with the kind of node it’s dealing with, what should result as input.value, as input.disabled, and as input.addEventListener("click", handler) .
- The only real non standard syntax available in lighterhtml, but already widely accepted by the community, is the self closing tag.

- What does `html` return ?
  - In the case of lit-html, the html function tag returns some instance of some internal class used by the library to understand its own content.
  - In lighterhtml though, you can use right away html or svg to create content

- What about performance ?
  - There are two sides to this metric: 
    - one is the bundled size, where smaller would mean faster time to be interpreted, 
    - and one is the raw rendering performance of the library itself.
  - Currently, lighterhtml wins in the keyed benchmark 
    - while lit-html wins in the non keyed one
    - if you’d like to know why lighterhtml is heavier, 
      - it’s mostly because it inherits the same compatibility granted by hyperHTML, 
      - and it patches internally, at runtime, a lot of little gotchas found in various browsers or JavaScript transpilers.
    - lit-html also fixes through little global runtime shims some browser, but it’s not as backward compatible as lighterhtml is.
- What does keyed VS non-keyed mean?
  - In few words, keyed results are the one you’d expect the most, while non keyed results mean that any created node could represent any sort of data.
  - If it makes any sense, you can think of non-keyed as the result of any server side rendered page, 
    - where nodes that relate to specific articles, items, database results, or user preferences, are just on the layout with some info exposed through some attribute.
  - With keyed results, html.for(entity) will always return the node associated to entity object, 
    - giving us the ability to eventually retrieve, or update, directly, 
    - any node associated to a single entity without even knowing if such node has been already rendered or not.
    - Instead, only what needs to get updated will actually get updated, as you can see in the console.

- In both hyper and lighterhtml case, updates are performed through the domdiff helper 
  - which uses just a node and any sort of algorithm to quickly compute the amount of changes needed between one DOM state, and another.
- Beside constant faster time in the initial creation, I wouldn’t say lighterhtml is any significantly faster than lit-html in these Code Pens.

- I think both lighterhtml and lit-html win on the Web, cause both provide a relatively straight forward and simple mechanism to create, and update, any sort of content.

- lit-html pros
- built-in directives to simplified common tasks and easily extends the lib
- smallest core when directives, repeat, style-map, and guard functionalities are not needed
- blazing fast compared to any bigger framework

- lighterhtml pros
  - React like hooks out of the box through its `lighterhtml.hook(useRef)`feature 
    - and any hooks oriented project such as augmentor, dom-augmentor, or TNG-Hooks, 
    - so that hooks can provide a way to extend renders as you need, just like directives would do
  - simple to start, simpler to use when it comes to keyed items, 
    - with no need of a repeater and style maps out of the box
  - widely backward compatible and transpilers resistant
  - blazing fast compared to any bigger framework
  - it always wins in terms of memory consumption

## [Web Component Solutions: A Comparison](https://levelup.gitconnected.com/web-component-solutions-a-comparison-e2fa25c34730)

- LitElement seems like an excellent choice, unless you are concerned about the BSD-3-Clause license
- Stencil seems on par with LitElement, but without the license concerns, and would be a great choice, especially if you’re already using Stencil for design or enjoy working with TypeScript
- if you are using, or might use, Salesforce in the future, LWC is the obvious choice because of its easy integration with other Salesforce workflows
  - You might also consider LWC if you enjoy being an early adopter of new web component technology trends, don’t like JSX syntax, or have a preference for keeping your HTML, CSS, and JavaScript code in separate files.

## [discussion: I think rewriting UI systems every few years and reimplementing in various JS frameworks that come and go is a serious waste of manpower.](https://news.ycombinator.com/item?id=18237757)

- I'd so wish people would embrace web components properly once and for all, with LitElement, Svelte or Stencil. 
- If I had to guess, I would guess that React will still be around in 5 years, but I'm not sure web components will. 
  - Sure, they may still be a part of the standard, 
  - but they might be so obscure(无名的；鲜为人知的) that there isn't enough of a community around them to be a feasible option. 
- I agree, and this is why I use React (or rather Preact) for both apps and interactive elements on the page. 
  - The big caveat is that in practice it's really easy to end up with a React project that is much more difficult to maintain compared to a monolithic(统一整体的) framework (Ember, Angular, Vue, even), 
  - because of all the other crap(质量差的东西；蹩脚货) that might be used to take care of all the stuff React doesn't do.
  - For example, I recently took on a React project that used a whole bunch of other packages for state management, routing, etc., 
    - and a number of those packages were no longer supported (or outright compromised). 
    - While it's nice that React is still React, a lot of these other packages are tightly woven into the whole 'fabric' (react-swipeable-redux-router type stuff).
  - For my part, when I start a React project I try to minimize these problems by generally avoiding react-specific packages. 
    - So instead of react-router, I'll just use page.js for routing. 
    - In some cases I might use the reactified version (Redux comes to mind, but I avoid that most of the time for smaller stuff).
  - This still isn't a panacea(万灵药；万能之计), 
    - and as a result I've been moving more and more stuff to a more 'vanilla' Railsy backend (Elixir/Phoenix, specifically). 
    - While the ecosystem does seem to be stabilizing a bit, it's still insane, 
    - and thankfully there are or will be ways to still add a bunch of 'dynamic' shit to the front-end without drowning in this insanity
- I think UI framework switches happen for two reasons:
  - They've accumulated so much technical debt with their existing solution that progress has slowed to a crawl, developer morale is really low, etc. 
    - A migration strategy can be found that doesn't have such an upfront cost, and will dramatically improve velocity as features are converted.
  - The design is totally changing, or the product is being rethought, and so it's not an invisible code rewrite, it's essentially building a new product.
- You named Web Components, I've been embracing them for a while, 
  - but if you tried to switch from Google's Polymer to LitElement, it wouldn't go smooth as you could have imagined. 
  - Both Polymer and LitElement are based on Shadow Dom and WC features curated by Google, but are not 100% backward compatible. 
  - That is to say, Web Components have been divided from within the same tech. 
  - No need to mention the rival concepts of "everything HTML" of Polymer 2.0 and fixing it to be "all JS and webpack-ready" in 3.0, and consequential deprecation of Bower.
- Svelte and Stencil compile your code into web components 
  - different approach than polymer that is a suite of quite a few higher-level abstractions that you might not want to pay for (20kb of js).
- 不同ui库的性能不好比较，库会更新，js-frameworks-benchmark也会更新
- React and similar frameworks optimise performance by batching DOM updates in one big read-compute-write cycle. 
  - With web components that don't share centralised DOM manipulation code its hard to see how that would work, and this can be a big performance problem.

# more-web-framework

- lit-html is not a new framework, but simply a template library
  - lit-html has no component model, so by using it to implement WCs, you get a component model.
  - A template library is not in direct competition with Web Component base classes/frameworks(polymer, svelte, stencil, skate), but can be used by them. 
    - It's already integrated with Skate, will be integrated with Polymer soon, and Stencil is looking into using it too.
- some folks will avoid lit-HTML in favor of Stencil's JSX approach, 
  - or in favor of Svelte's Vue-alike HTML components, 
  - or more generally to decide whether to observe changes and respond to them or whether to regenerate the UI as a function of state.
- I think you mis/underestimate the extent to which you have a component model already. 
  - What you already have is the equivalent of React's "functional components", where the component is nothing but its render method.
  - When we (Polymer folks) think of a component model, we think of a lifecycle. 
    - Being notified when you boot up, when you're activated, when you're deactivated, and when the state you care about changes. 
    - React has that, Web Components have that, lit doesn't.

# ref

- [Vanilla JS Plugins](https://vanillajstoolkit.com/plugins/)
  - These are hand-selected plugins that I would actually use or have used on a project.
  - 大多数framework agnostic，质量高
- [Building State management system like react from scratch with VanillaJS.](https://dev.to/logeekal/building-state-management-system-like-react-from-scratch-with-vanillajs-3eon)
  - I want to build a state Management system similar to React but very bare-bones. 
  - But it should follow one-way data flow. 
- [React vs Lit implementations of the React homepage demos.](https://pinkhominid.github.io/react-v-lit/)
- [Comparing reactivity models - React vs Vue vs Svelte vs MobX vs Solid vs Redux](https://dev.to/lloyds-digital/comparing-reactivity-models-react-vs-vue-vs-svelte-vs-mobx-vs-solid-29m8)
- [What's the deal with SvelteKit?](https://svelte.dev/blog/whats-the-deal-with-sveltekit)
  - Sapper is an app framework (or 'metaframework') built on top of Svelte (which is a component framework). 
    - Its job is to make it easy to build Svelte apps with all the modern best practices like server-side rendering (SSR) and code-splitting, and to provide a project structure that makes development productive
    - It uses filesystem-based routing (as popularised by  Nextjs)
    - your project's file structure mirrors the structure of the app itself.
  - The first of those foundational assumptions is that you need to use a module bundler like  or  to build apps. 
    - SvelteKit uses Rollup to make your apps fast
  - The other foundational assumption is that a server-rendered app needs, well, a server. 
    - Sapper effectively has two modes 
      - `sapper build`, which creates a standalone app that has to run on a Node server, 
      - and `sapper export` which bakes your app out as a collection of static files suitable for hosting on services like GitHub Pages.
    - Static files can go pretty much anywhere, but running a Node server (and monitoring/scaling it etc) is less straightforward. 
    - Nowadays we're witnessing a shift towards serverless platforms, in which you as the app author don't need to think about the server your code is running on, with all the attendant(伴随的；在场的) complexity. 
    - SvelteKit fully embraces the serverless paradigm, and will launch with support for all the major serverless providers, 
      - with an 'adapter' API for targeting any platforms that we don't officially cater to. 
      - In addition, we'll be able to do partial pre-rendering, which means that static pages can be generated at build time but dynamic ones get rendered on-demand.
