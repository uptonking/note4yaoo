---
title: thread-fwk-web-components-lit-html
tags: [lit-element, lit-html, thread, web-components]
created: '2021-01-07T19:36:55.221Z'
modified: '2021-01-19T17:09:26.629Z'
---

# thread-fwk-web-components-lit-html

# pieces

- ## 

- ## 

- ## 

- ## 

- ## The more I play with Web Components, the more I wonder what shadow dom is good for other than adding third party ads to a web site.
- https://twitter.com/dam/status/1416190642573778945
- please outline the value of the Shadow DOM
  - It is supposed to be good for style encapsulation, but if a website implements a CSS design system correctly then Shadow DOM seems to be more of a burden than a benefit.
- Web components are primarily designed for highly reusable things. If they exist only within a single website then their value is much less. Shadow DOM is more valuable for something like a Stripe embed
  - Exactly. Shadow DOM seems to be perfect for the embedded use case.
  - I feel like the reuse statement should be challenged though. 
  - You can definitely reuse Web Components without Shadow DOM. In some ways it seems easier to do so without it.

- ## Core API for turning any Vue 3 component into a custom element.
- https://twitter.com/justinfagnani/status/1414615879866720270
  - Works with most Vue APIs including props, emits, and even provide/inject between nested Vue custom elements. Slots will render as native slot elements.
  - There are different trade-offs here, the CE version lacks certain features like scoped slots, more efficient SSR (no need for simulated DOM / serialization) and introduces a bit more overhead. So shipping CE by default would be a pure loss for Vue users.
- You could ship both and the web components consumers wouldn't have to know about using Vue at all.
  - On SSR, we(lit)'re working on an open server-side interface for SSR without DOM. Lit works this way and renders elements through this interface so we can plug in different impls.
- We're still working up a standalone description of the protocol(SSR Interface), but here's the interface in Lit SSR
  - The reason for this ElementRenderer interface is that Lit basically has a separate streaming DOM-free server-side implementation, and we want to be able to render CEs via  an intermediary to enable that for other libraries.
  - [Server-Side Rendering (SSR) API](https://github.com/webcomponents/community-protocols/issues/7)

- ## Merged the first draft of the Context Protocol into the web components community protocols!
- https://twitter.com/justinfagnani/status/1411126244368740353
  - This proposes a context API that's interoperable across web component implementations, 
  - and because it's event-based, even framework components.
- This is part of a broader effort to layer cross-component coordination and framework-like features on top of the base component model
  - We're also working on SSR, hot-module replacement, things similar to Suspense, and more.
- Especially love the event-based approach. Intuitive and simple enough to be successful and potentially very powerful.

- ## Counter argument; there is an even bigger ecosystem of vanilla JS libraries that often integrate nicely with Svelte more than React, since Svelte has regular events/bindings. 
- https://twitter.com/DanaWoodman/status/1390030682789859329
  - Using actions to integrate to vanilla JS can be effective. 
  - Doesn't work with all of them of course.

- ## How @buildWithLit templates work in 4 steps:
- https://twitter.com/justinfagnani/status/1385659190153121795
  - html tag gets template strings and data 
  - Lit creates HTML from template strings 
  - Browser parses HTML into a `<template>` , Lit records marker locations
  - Lit clones `<template>` and inserts data at marker locations
- The first three steps are the "template preparation" steps and only happen once per template.
  - That work is reused across every rendered instance and every re-render of the template. 
- I think you mentioned somewhere you were working in making this preparation AOT?
  - Yep! We have compiled template support in core, with tests

- ## What if it were incredibly easy to create reusable web components with Preact too?
- https://twitter.com/justinfagnani/status/1385017231101231107
  - With new @lit/reactive-element package, you can easily use any rendering layer and still get all the reactive property, scoped style, and update lifecycle goodness that drives Lit.
- What's really great is how very simple the implementation is
  - We pushed more of Lit's styling and decorators into ReactiveElement and published it as a separate package so that more people could use this as a base with their preferred template system, or no template system at all.
- Still React event and prop issues?
  - Preact doesn't use delegated events and uses introspection to detect and use custom properties. It has always worked with Custom Elements.
  - @lit-labs/react: React integration for Web Components and Reactive Controllers.

- ## People often ask how lit-html works because it looks like it's just doing string building, and it's a bit unintuitive that it could be so fast.
- https://twitter.com/justinfagnani/status/1247652729922531328
- Separating out the static from the dynamic pieces of a template has traditionally been a hard problem, but using string template literals makes it so easy!
  - And now it makes our SSR code really fast too
- `strings` and `values` are both arrays. The vm calls the tag function something like this: `tag(['hello '], 1)` .

- ## What makes a lit-html or stencil based component suite more "future proof" than a collection of framework-x components wrapped as native custom elements? 
- https://twitter.com/youyuxi/status/1380181910631112708
  - I see the "future proof" slogan being used as major selling points for these WC-based solutions (lion, fast-element etc.) but by using them you are still running hundreds of kilobytes of JavaScript written and maintained by others.
  - If all you care is for components to be distributed and used as native custom elements, most major frameworks have the capability to do that already (maybe except for React?...)
  - In other words, if a framework provides the capability of compiling and distributing its components as native Custom Elements, it's also "future proof"?
- Nothing, and that's sort of the point; once you commit to publishing as custom elements, you get all the compat (so long as you respect API stability) and can change internals (as AMP did). Win/win!
  - A goal of WC has been to help promote component re-use across these sorts of boundaries, letting things built in one tool interop more-or-less-seamlessly over time.
  - E.g., folks who like Vue should be able to use Vue to build their components, but still be able to consume things built another way. Similarly, folks who want to build in Vue should have a bigger market than Vue-centric apps. That future is enabled by interop + low runtime cost.
- Future-proof cannot really apply to lit-html or lit-element the way you are referring to!
  - However, compiler-built web components (Svelte, Stencil.js) are almost self-enclosed. The notion of run-time abstracted "enough" away for the consumer to bother about it.
  - Also, web components are good as long as you do not need patterns like Render Prop or Vue.js style slots or even React Children. It ends up being a super nightmare.
  - Almost nothing works well. Simple a11y focus-trapping is nearly impossible.
- For me the key point to consider here is: "How easy would it be for me to migrate my collection of components to not use any dependency in the future"
  - Ideally, we could all create vanilla WC and they will live forever without any real maintenance. But since the APIs are low level, the ergonomics can become a big hurdle on productivity as you mentioned
  - So, any collection of a certain scope will need to embrace a library
  - This is why I personally prefer class-based libraries for creating web components like lit or FAST rather than compiler or functional-based approaches
  - The standard requires you to extend a class, embracing that fact makes it easier if you ever need to go back

- ## Introducing Esri's new design system - Calcite
- https://twitter.com/mapdex/status/1379846669320085505
  - Esri is another company all in on Web Components.  
- https://github.com/Esri/calcite-components
  - Web Components for the Calcite Design System. 
  - Built with Stencil JS.

- ## web components lock you in to the web - use React primitives like View, Text, Image and be free
- https://twitter.com/notbrent/status/1135103126724325377
- Are you referencing RNW?
  - that’s one possible implementation, yeah. react-primitives was another. maybe at some point this will all just be part of React itself

- ## preact-custom-element: Convert any Preact component to a web component!
- https://twitter.com/marvinhagemeist/status/1300822560804872192
  - Propagate context through Custom Element boundaries
  - Reflect DOM property changes to Preact props
  - Sync DOM attributes with props 
- How does that work without using a class for the custom element?
  - Oh, I see the Reflect.construct().
  - That's only supported in browsers that have classes, and it's much slower than a real class. Why not use classes directly?
  - Need to check the git history. It was already there when I came on board. I'll get back to ya
- I have a question. I recently gained experience with stencil and found that web components props only consume strings. The Preact approach also allows me to use complex prop binding.
  - In my opinion all renderers should set properties only. Attributes can be reflected by the elements themselves if needed. One of few useful use cases for attributes is for CSS selectors where it makes sense. Otherwise you only need ever properties.
  - This is an interesting idea. However, there are still a number of native element attributes that don’t map back and forth to properties, e.g. aria attributes. What do we do about those?
  - Fall through when there is no corresponding property

- ## If you have `class SubEl extends HTMLElement {}` .
- https://twitter.com/justinfagnani/status/1359213920272044034 
  - is there any way to dynamically add something like `SubEl.prototype.disconnectedCallback = function() { }`

- Custom element reaction callbacks are torn off at definition time so that they don't require a lookup for every invocation.
  - So you need to do the patching before `define()` .

- ## Looking for some publicly available/open source web components to test the custom elements manifest analyzer on
- https://twitter.com/passle_/status/1357676192413999105
  - Do you have some components written with either lit or vanilla, JS or TS, that are available on github? 
- dile-tabs
  - Hadnt considered window.customElements.define, only customElements.define. Very helpful, thanks for sharing!

- ## The web is definitely not a great application platform currently, but there’s no reason why it can’t be! 
- https://twitter.com/devongovett/status/1355557264631988229
  - The fundamentals are there. 
  - The DOM is a UI tree just like any native UI framework. 
  - We just need better built in UI controls. 
  - Instant delivery is the web’s killer feature.
- I believe it’s the best app delivery platform. It not the best UI platform though.
- And no gate keeper

- ## CE v1 is not a spec without a way to extend existing HTML elements
- https://twitter.com/Rich_Harris/status/1352327436512485377
- To be fair it's really only a more specific version of an issue Seb Markbåge identified long ago
  - because of WCs we're no longer able to change HTMLElement without risking breaking the web
- With is=, the issue extends to every subclass of HTMLElement. We need to worry about what scripts with is= might be defining or responding on each element.
- looking forward to have *any* way to extend builtins via the platform, meanwhile I've done that for years and never, *ever*, had an issue in doing so.
  - if a new attribute lands on the root prototype, in case it collides with *my* prototype, it'd be *my duty* to fix *my class*
  - what bugs me, is that HTMLElement is exactly on the same boat: if *anything* new lands on its prototype, or any of its ancestors prototypes, non builtin Custom Elements are *as broken*, and hazardous, as anything else.
  - Events, Node accessors, and so on + HTML5 changes rarely.
  - meanwhile, the Web is extensible (hence broken?) by default, and all frameworks to date trashed here and there attributes without data- prefixes; Custom Elements v1 is 75% fully supported, and WebKit needs a polyfill (luckily small enough), and no progress is happening => FWs win

- ## Element Worklet is my proposal for threaded DOM: Custom Elements in threads for performance isolation.
- https://twitter.com/_developit/status/1351953283447984131
  - I built a prototype using worker-dom
  - https://glitch.com/edit/#!/element-worklet
- Very interesting. What would be the resource cost of spinning up an Element Worklet? Unlike iframes, devs might be tempted to make very liberal use of such a feature
  - This is actually something that is already nicely accounted for by the Worklets spec: 
  - addModule() doesn't instantiate a thread, it only creates one or more Realms in which the given worklet will be executed. 
  - An implementation can choose to pool or share a single thread, etc.

- ## Web Components people know that you can use semantic HTML5 with JS frameworks right? 
- https://twitter.com/swyx/status/1351432826751651849
  - I hear a lot of disingenuous strawman arguments against "div-itis".
- Not to mention that WCs have a11y drawbacks that aren't shared by built-in elements that *can't* just be solved with education
  - break a11y
  - break progressive enhancement (no SSR, broken without JS)
  - don't work with SVG
  - share a global namespace instead of being modular
  - Imagine how much tedious moralising we'd see if JS frameworks shipped with similar limitations
- custom elements have to be JS. 
  - But the fact that there's no renderToString or equivalent has been a blocker for me.
  - This is because they're designed for progressive enhancement. 
  - Once you treat them this way objections around accessibility and server render go away. 
  - It's not what they're good at.
- I think we collectively need to clarify our definition of progressive enhancement. 
  - For me, it means things like `<form>` works without JS, but progressively enhances to an AJAX-enabled form with JS. 
  - That's straight-up impossible with `<fancy-form>` .
  - It's also perfectly possible for your fancy-element to surface a hidden regular input field in its light-dom to participate in any regular form container. 
  - I agree this is a hack while we wait for AOM and form participation to land 
  - but it is possible to solve a11y and form issues.
- For me the conclusion is inescapable 
  - if we care about building robust, resilient applications that meet a11y requirements, we should avoid using web components. 
  - The energy currently devoted to them should be spent on standardising CSS scoping and adding new built-in elements

- ## the last time I tried to use web components I found it difficult to scale communication between components. 
- https://twitter.com/nickemccurdy/status/1351111354397159427
  - Probably not an issue for prerendered websites, 
  - but if my content was totally static I would just use Jekyll personally.
- Communication between components is pretty easy with events, passing data down, and the other usual state management solutions.
- This is made a lot easier with the event handler binding syntax in `lit-html` . 
  - In raw webcomponents setting up all the handlers is such pain.

- ## lit-html vs handlebars
- lit-html approach is very similar to what handlebars template do. Perhaps with nicer syntax and dev experience
  - Much more than that. 
  - Using platform caching mechanism for speed.
  - No transpilation needed and the list goes on

- Some template languages have built-ins for ifs and loops. like `{{#if }}` in Handlebars. 
  - lit-html is more like JSX in that templates themselves have no control-flow, and control-flow is done by composing templates with JS.
  - `when()` is JavaScript, and a directive. 
    - It's not part of the core functionality, and not part of any template syntax. 
    - It's just a JavaScript expression that interacts with the Parts API.

- Polymer 3 and lit-html have very different template syntaxes. 
  - lit-html is pure JavaScript, not handlebars-like. 
  - lit-html is easier to debug than JSX because it's plain, standard, JavaScript and doesn't get transformed by a build step. 
  - You debug the actual source.

 
