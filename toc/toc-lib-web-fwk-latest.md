---
title: toc-lib-web-fwk-latest
tags: [framework, latest, toc, web]
created: 2020-12-31T15:13:15.052Z
modified: 2020-12-31T15:18:33.994Z
---

# toc-lib-web-fwk-latest

# fwk-latstest

- https://github.com/finos/perspective
  - Streaming pivot visualization via WebAssembly
# reactive
- https://github.com/justin-schroeder/arrow-js /ts
  - https://www.arrow-js.com/docs/
  - A tiny ~2kb library for building reactive interfaces in native JavaScript
  - Reactive Data => reactive
    - Reactive data objects have an $on and $off methods that allow us to observe mutations to their properties. 
  - Templates => html
    - Reactive expressions are callable functions, everything else is a static expression.
  - Watching data => watch
    - tracks any reactive data dependencies of that function, and then re-calls that function if any of the dependencies change

- https://github.com/modderme123/reactively /ts
  - a library for fine grained reactive programming. 
  - Use Reactively to add smart recalculation and caching almost anywhere. 
  - [Native Signals can be done completely absent of scheduling and effects.](https://twitter.com/RyanCarniato/status/1691473859202146304)
    - @modderme123 released Reactively last year that shipped with no effects or autorun. 
    - It was just a pull based system
  - [Super Charging Fine-Grained Reactive Performance - DEV Community](https://dev.to/modderme123/super-charging-fine-grained-reactive-performance-47ph)
    - I've been working on a new fine grained reactivity libary called Reactively inspired by my work on the SolidJS team.
  - Reactively caches the results of the render() function automatically and Reactively won't run render() again unless its inputs have changed. So the second call to render() is optimized into a no-op.
  - Reactively is useful to avoid unnecessarily repeating expensive operations 
    - (memory allocation, network operations, storage, long computations, DOM manipulation, etc.) 
    - While you can manually write your own caching and dependency checking, a declarative approach is easier, and the result is more maintainable.
  - Traditionally, if you want to memoize a function in JavaScript, you have to manually specify all the dependencies as parameters, even if sometimes you don't use all the parameters.
    - Reactively eschews(避开, 回避) that in favor of automatically detecting what variables you use in a reactive expression.
    - Additionally, Reactively allows you to dynamically change which variables you depend on at runtime
  - Reactively is a hybrid push-pull system. 
    - It pushes dirty notifications down the graph, and then executes reactive elements lazily on demand as they are pulled from leaves. 
    - This costs the framework some bookkeeping and an extra traversal of its internal graph. But the developer wins by getting the simplicity of a pull system and the most of the execution efficiency of a push system.
  - Push systems emphasize pushing changes from the roots down to the leaves. 
    - Push algorithms are fast for the framework to manage but can push changes even through unused parts of the graph, which wastes time on unused user computations and may surprise the user. 
    - For efficiency, push systems typically expect the user to specify a 'batch' of changes to push at once.
  - Pull systems emphasize traversing the graph in reverse order, from user consumed reactive elements up towards roots. 
    - Pull systems have a simple developer experience and don’t require explicit batching. 
    - But pull systems are are apt to traverse the tree too often. 
    - Each leaf element needs to traverse all the way up the tree to detect changes, potentially resulting in many extra traversals.
- https://github.com/bubblegroup/bubble-reactivity /ts
  - He continued his work at @bubble and generalized approach to async propagation, but again effects aren't needed. The lib provides an effect.ts but it isn't necessary. It could be done implemented completely in userland by extending the Computation class.

- https://github.com/adamhaile/S /ts
  - S.js is a small reactive programming library. 
  - It combines an automatic dependency graph with a synchronous execution engine.
  - https://github.com/adamhaile/surplus
    - Surplus is a compiler and runtime to allow S.js applications to create high-performance web views using JSX. 
    - Surplus treats JSX like a macro language for native DOM instructions.
    - These DOM instructions create real DOM nodes that match your JSX. There's no virtual DOM middle layer standing between your JSX and the DOM.
    - DOM updates are handled by S computations.

- https://github.com/emberjs/data /ts
  - a lightweight reactive data library for JavaScript applications that provides composable primitives for ordering query/mutation/peek flows, managing network and cache, and reducing data for presentation.
  - The core of Ember‍Data is the Store, which coordinates interaction between your application, the Cache, and sources of data (such as your API or a local persistence layer). Optionally, the Store can be configured to hydrate the response data into rich presentation classes.
# more
