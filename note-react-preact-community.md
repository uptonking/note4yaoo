---
title: note-react-preact-community
tags: [community, preact, react]
created: '2021-04-24T15:07:05.237Z'
modified: '2021-05-13T03:46:35.666Z'
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
# discuss-stars
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
# discuss
- ## 

- ## 

- ## 
