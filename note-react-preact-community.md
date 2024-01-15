---
title: note-react-preact-community
tags: [community, preact, react]
created: 2021-04-24T15:07:05.237Z
modified: 2021-05-13T03:46:35.666Z
---

# note-react-preact-community

# guide

# preact web components
- ## Why I Chose Preact for my Latest Project
- https://dev.to/muhimasri/why-i-chose-preact-for-my-latest-projectsharing-my-experience-working-with-preact-on-my-latest-javascript-project-48h
- Unlike React, Preact uses the browser’s native `addEventListener` for handling events internally so it can listen to native DOM events dispatched from Custom Elements. 
  - Also, it has a special approach to know when to pass data to Custom Elements as either properties or attributes.
- you can use preact-custom-element to turn any Preact component into a Web Component!

- ## Preact works with both React and Web Component toolkits.
- https://twitter.com/munawwarfiroz/status/1378223550226653185
- We've been working on the second half of the rewrite of Preact's renderer. 
  - It adds support for pluggable component models (+better compat), improves average & worst-case performance, and provides a foundation for first-class asynchrony (+suspense) and new diffing modes.
  - Time is already being split between this large effort and WMR, which is a larger project than it seems at first glance (it includes what is essentially a light implementation of babel+JSX+rollup).
- I didn't check WC toolkits (duh, didn't think of that). Then the only way is to try them out. 
  - They don't explicitly write preact compatibility. 
  - Some toolkits like react-spectrum has documented the bugs with preact.
- afaiu spectrum is pretty new, so that may change. Though its size makes it a bit of an odd choice for preact apps (each spectrum component is larger than preact itself).
  - Seriously though, I think that’s how it should be. Preact is really just a thin layer on top of the DOM. Building actual components takes a lot of code, no matter the framework.
  - But also that’s not entirely true. Our components have a lot of overlapping pieces. One component may look large on bundlephobia, but most of the big pieces are shared between many different components, so it evens out in real apps.
# discuss-architecture
- ## 💡 [react-three-fiber on Preact? (discussion)](https://github.com/preactjs/preact/issues/2538)
- 202209: Preact always had a reconciler internally, but we don't expose it as it's closely married to the DOM. There are no current plans to change that, which means react-three-fiber is not supported.

- https://twitter.com/Cody_J_Bennett/status/1632674026408558592
  - Got custom renderers working in @preactjs by implementing react-reconciler via option hooks.

- [Add demos for performance comparisons](https://github.com/preactjs/preact/issues/1136)
  - Crucially the point of the triangle demo isn't to demo "performance", it's to show that there's separate scheduling for high priority and low priority updates, and that we can "rebase" the low priority reconciliation on top of a high priority update. 
  - It's nothing Preact would be able to do anyway without implementing a double buffer like in Fiber (and then resuming — which we are still missing).

- ## [async rendering 一直未合并pr· Pull Request_202112](https://github.com/preactjs/preact/pull/3386)
- https://github.com/matrix-marketing/preact
  - [Preact Async Rendering: Solution to Initial Render Blocking - DEV Community](https://dev.to/cagdas_ucar/preact-async-rendering-51p2)
- The only problem I have is that Google page speed insights keep telling me that our sites have too much blocking time. 
  - The solution is of course async rendering. It's not a new concept. 
  - It's similar to React Fiber but the implementation is quite different. 
- preact async rendering is exactly what's supposed to help with that. I've been using it in production with great success.

- [Asynchronous rendering pipeline based on microtask](https://github.com/preactjs/preact/issues/3127)

- ## I have been working on an experimental ground-up rewrite of Preact's renderer. It now renders TodoMVC faster than hand-written vanilla JS.
- https://twitter.com/_developit/status/1412451442946981890
  - It's somewhere between 1.5x and 3x faster than Preact 10 (depending on VM optimization state).
- A lot of the performance improvement comes from two key things: 
  - **moving to linked lists for tree structure**, 
  - and **replacing (nested) function calls with a primitive stack machine**. 
  - The latter has been super fun to work with, and it feels easier to mentally model than nested function calls.
- I think I mentioned a couple things higher up in this thread, but it basically comes down to:
  - replace functions with a stack machine
  - remove all intermediary(中间的) objects (arrays -> linked lists)
  - only allocate where absolutely required
  - don't make hot branches conditional

- It would be interesting to have a look. I'm making a preact inspired framework with as much running in a worker as possible.
  - I'm starting with a worker, will do the wasm(Rust) in the worker later if this works out. 
  - I went with a binary encoded vdom in a typed array. So will see how well it will handle tag attributes, but children and strings are quite compact. 
  - But so far only the tree diff lends itself to running in the worker. 
  - And at the end it will return a list of actions to be run against the Dom from the main thread. 
  - Will see if this approach works at all. But so far it's fun.
  - By binary encoded i meant an array of numbers(which is not very accurate), with a node being [type, length, text_index, ...children]. Still no props yet, will see how that fits in.
- heh yeah props are always the pain point, since they're completely arbitrary. FWIW I've seen a bit more success with moving the entire component tree (including the app code) into a Worker, since it means rendering can be done in 1 hop (apply patch) instead of 2 (diff -> patch).
  - it also has a pretty awesome advantage of isolating any longer-running app code (gnarly sort functions anyone?) and memory bloat (JSX is not great for this) in the Worker, so the main thread isn't affected.
  - **IMO one of the next big things for UI frameworks is serializable event responders**.
  - Your app runs somewhere isolated (a Worker, a server, WASM, etc), but it sends self-contained event handlers to the main thread. Most event responses can be done instantly on the main thread.
  - compiler-oriented frameworks with their own template/format are in the best position to do this, since they've already done the work of providing an authoring format that doesn't assume its on the main thread (and makes those assumptions ergonomic).
- Speaking of tree structures backed by linked lists,  `linkedom` by @WebReflection does really great proving the performance difference. I like these sorts of improvements. Keep 'em coming
  - [LinkeDOM – A triple-linked lists based DOM](https://www.youtube.com/watch?v=PEESaD7Qkxs)
- tbh I am actually fairly surprised! property access in JavaScript is easy to deopt, whereas array index access is relatively easy to keep from deopting. Even with a 100% homogeneous list, it's still possible for next/prev traversal to deopt within seldom-taken branches.
  - Linked Lists in JS are primarily beneficial when the values themselves are the links. Using dedicated link objects has allocation cost that outweighs(超过) traversal costs for an array.

- How could an abstraction be faster than bare metal JS? I'm assuming the comparable vanilla JS is sub-optimally written?
  - I wrote the vanilla version to be fast. My theory is that this implementation is faster because it is specifically written to trigger JS engine optimizations eagerly - the vanilla version ends up triggering deopts + reoptimizations as it stores state and applies DOM mutations.
  - Also the vanilla version uses functions to represent hierarchy and encapsulate state for list items. Those function calls aren't expensive ones, but they're still infinitely slower than something that has no function calls at all.
  - it's actually not that strange when you think about how JS engines optimize code. JIT optimizes for consistency, and abstractions are able to capitalize on that in a way direct imperative code generally can't.
- all framework should be faster than bare metal js, bc they schedule. base op perf plays a small role in how fast an app is. first thing that makes apps slow is read/write order → layout thrashing, diffing updates → too many changes, virtualisation → breaching 15ms/frame.
  - that brings us to the high probability that all bare metal js apps are sub-optimal bc if they weren't they'd have a framework wrapped or written around it. there's nothing in js that helps w/ scheduling, and the complexity, if not well abstracted, creeps into the entire codebase.
# discuss-🆚️-preact-react
- ## 

- ## 

- ## 

- ## [Anyone using Preact in prod? : reactjs_202301](https://www.reddit.com/r/reactjs/comments/10o661t/anyone_using_preact_in_prod/)
- TLDR: Steer clear of preact. Try Next or Remix.
  - Almost all issues we encounter upgrading dependencies are related to Preact, because even if the thing runs first time, good chance half of your unit tests will fail.
  - I can’t count the number of times my tests have been flaky because I have preact and react in the same project (because react is listed as a peer dependency of something), and webpack has got its panties in a bunch because it’s not sure how to render something.
  - React Testing Library is at version what, 12? The preact counterpart is v2. Using preact you miss out on features like Suspense that you now have to implement manually.

- Exactly the same experience, I ended up spending a couple of days and moved everything into React.

- do not use a library/framework similar react just because it has better performance. React is fast enough, just focus on architecture/detail design instead

- Fullcalendar uses preact by default, and I use it in a project in prod. But that's about it.

- ## [Preact vs. React: A Quick Comparison | HackerNoon_202202](https://hackernoon.com/major-differences-between-preact-and-react-which-one-should-you-use)
- Preact is a JavaScript library, considered the lightweight 3kb alternative of React with the same modern API and ECMA Script support.

- Preact-pros
  - Lightweight
  - Compatible: preact/compat to offer 100% compatibility
- Preact-cons
  - Hooks are stored separately in Preact and need to be imported differently
  - No Synthetic Event Handling: Preact is based on browser API and doesn’t support synthetic event handling
  - Use of additional library: With Preact, it is necessary to use additional libraries like preact/compat, preact/test-utils, etc., to bring connectivity between Preact and React-based npm packages. This makes the project large and slow.

- React-pros
  - One-way Data flow
  - Large Community
  - Reusable Components
- React-cons
  - View-centric Library

- ## [Will Preact stay API compatible with React 16?_201911](https://github.com/preactjs/preact-compat/issues/432)
- we added all of those in Preact X. We even ship with a rough implementation for `Suspense`

# discuss
- ## 

- ## 

- ## 
