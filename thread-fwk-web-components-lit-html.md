---
title: thread-fwk-web-components-lit-html
tags: [lit-element, lit-html, thread, web-components]
created: '2021-01-07T19:36:55.221Z'
modified: '2021-01-19T17:09:26.629Z'
---

# thread-fwk-web-components-lit-html

# pieces

- ## 

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

 
