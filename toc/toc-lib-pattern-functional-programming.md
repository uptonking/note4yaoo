---
title: toc-lib-pattern-functional-programming
tags: [functional, pattern, toc]
created: 2020-11-02T19:13:11.667Z
modified: 2023-07-26T11:23:38.282Z
---

# toc-lib-pattern-functional-programming

# guide

- functional-examples
  - guardian-editor
  - britecharts
# popular
- https://github.com/staltz/callbag-basics /1.5kStar/MIT/201711/js
  - allbag is just a spec, but callbag-basics is a real library you can use.
  - [callbag和rxjs有什么区别](https://www.zhihu.com/question/270126057/answer/352363505)
    - 从终端用户角度没有区别，operator库实现者要换个写法。从思维模式上没有本质区别。
    - 从使用思维上仍然是把业务逻辑包装成流，然后把流通过operator合起来运算。没有本质差别。
    - 编程模型上几乎是等价的，只是API设计的口味不一样
  - https://github.com/callbag/callbag
    - A standard for JS callbacks that enables lightweight observables and iterables
    - Callbag中的source可以转换成RxJS的Observable
  - https://github.com/0no-co/wonka
    - https://wonka.kitten.sh/
    - A tiny but capable push & pull stream library for TypeScript and Flow, loosely following the callbag spec
    - a lightweight iterable and observable library loosely based on the callbag spec. 

- https://github.com/reactivex/rxjs
  - /23.3kStar/Apache2/202011/ts
  - https://rxjs.dev/
  - A reactive programming library for JavaScript
  - 替代: bacon, most
- https://github.com/cyclejs/cyclejs /9.8kStar/MIT/202009/ts
  - [Cycle.js - Streams](https://cycle.js.org/streams.html)
  - A functional and reactive JavaScript framework for predictable code
  - reactive: it is fully responsible for managing its own state by reacting to external events. 
    - The selling point for widespread Reactive programming is to build self-responsible modules which focus on their own functionality rather than changing external state. 
    - This leads to Separation of Concerns.
  - Reactive programming can be implemented with: event listeners, RxJS, Bacon.js, Kefir, most.js, EventEmitter, Actors, and more
    - Even spreadsheets utilize the same idea of the cell formula defined at the arrow head. 
    - The above definition of Reactive programming is not limited to streams
  - Cycle.js supports multiple stream libraries, such as RxJS, xstream, and most.js, 
    - by default we choose `xstream` because it was custom built for Cycle.js.
    - a Stream in xstream is an event stream which can emit zero or more events, and may or may not finish. 
    - If it finishes, then it does so by either emitting an error or a special “complete” event.
- https://github.com/staltz/xstream /2.2kStar/MIT/202010/ts
  - An extremely intuitive, small, and fast functional reactive stream library for JavaScript
  - Only 26 core operators and factories
  - Tailored for Cycle.js, or applications with limited use of subscribe
- https://github.com/baconjs/bacon.js /ts
  - https://baconjs.github.io/
  - Functional reactive programming library for TypeScript and JavaScript
  - Bacon.js is quite similar to RxJs
    - The major difference is that in bacon, there are two distinct kinds of Observables: the EventStream and the Property. 
    - The former is for discrete events while the latter is for observable properties that have the concept of "current value".
    - there are no "cold observables", which means also that all EventStreams and Properties are consistent among subscribers
- https://github.com/kefirjs/kefir /js/inactive
  - A Reactive Programming library for JavaScript
  - inspired by Bacon.js and RxJS with focus on high performance and low memory usage.
- https://github.com/cujojs/most /js/inactive
  - Monadic streams for reactive programming

- https://github.com/ramda/ramda
  - /19.7kStar/MIT/202010/js
  - Practical functional Javascript
- https://github.com/getify/Functional-Light-JS
  - Pragmatic, balanced FP in JavaScript.
- https://github.com/gcanti/fp-ts
  - /5kStar/MIT/202010/ts
  - Functional programming in TypeScript
- https://github.com/fluture-js/Fluture /202005/js/inactive
  - Fantasy Land compliant (monadic) alternative to Promises
  - Much like Promises, Futures represent the value arising from the success or failure of an asynchronous operation (I/O). 
  - Though unlike Promises, Futures are lazy and adhere to the monadic(单元的，单体的) interface.
- https://github.com/SodiumFRP/sodium-typescript
  - Typescript/Javascript implementation of Sodium FRP (Functional Reactive Programming) library
- https://github.com/marblejs/marble
  - functional reactive Node.js framework for building server-side applications, based on TS and RxJS.
- https://github.com/hufeng/iflux
  - immer.js + react.js
# reactive
- tips
  - 具体的业务如ospreadsheet会禁用框架内部的reactivity，自己管理数据和状态，以便实现undo、协作等功能
  - reactive编程模式大多会引入operator的复杂度

- https://github.com/modderme123/js-reactivity-benchmark
  - Current reactivity benchmarks (S.js, CellX) are focused on creation time, and update time for a static graph.
  - We've created a new benchmark that allows library authors to compare their frameworks against each other, and against the existing benchmarks, as well as against a new configurable benchmark with dynamically changing sources.

- https://github.com/justin-schroeder/arrow-js /ts/NoDeps/在benchmark非常靠后
  - https://www.arrow-js.com/docs/
  - A tiny ~2kb library for building reactive interfaces in native JavaScript
  - Static by default, reactive by choice
  - No Virtual DOM
  - Arrow relies heavily on modern features of JavaScript such as template literals, modules (think import and export), and Proxies.
  - Reactive Data => reactive
    - Reactive data objects have an $on and $off methods that allow us to observe mutations to their properties. 
  - Templates => html
    - Reactive expressions are callable functions, everything else is a static expression.
  - Watching data => watch
    - tracks any reactive data dependencies of that function, and then re-calls that function if any of the dependencies change

- https://github.com/adamhaile/S /ts/inactive
  - S.js is a small reactive programming library. 
  - It combines an automatic dependency graph with a synchronous execution engine.
  - https://github.com/adamhaile/surplus
    - Surplus is a compiler and runtime to allow S.js applications to create high-performance web views using JSX. 
    - Surplus treats JSX like a macro language for native DOM instructions.
    - These DOM instructions create real DOM nodes that match your JSX. There's no virtual DOM middle layer standing between your JSX and the DOM.
    - DOM updates are handled by S computations.

- https://github.com/modderme123/reactively /ts/实现未使用proxy
  - a library for fine grained reactive programming. 
  - Use Reactively to add smart recalculation and caching almost anywhere. 
  - shipped with no effects or autorun. It was just a pull based system
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

- https://github.com/alibaba/formily /ts/多框架
  - https://formilyjs.org/
  - High Performance Normal Form/Dynamic(JSON Schema) Form/Form Builder 
  - Support React/React Native/Vue 2/Vue 3
  - 阿里巴巴统一前端表单解决方案
  - 代码量大，功能全
  - Formily2.x 在实现的过程中发现 Mobx 还是存在一些不兼容 Formily 核心思想的问题，最终，只能重新造了一个轮子，延续 Mobx 的核心思想的 @formily/reactive

- https://github.com/ryansolid/mobx-jsx /ts
  - Raw MobX performance without being restrained by a Virtual DOM
  - a demonstration of how MobX fine grain control can be leveraged directly in JSX for considerably better performance than pairing it with a Virtual DOM library
  - It compiles JSX to DOM statements and wraps expressions in functions that can be called by the library of choice.
  - MobX JSX works both with function and Class components
  - MobX JSX also supports a Context API.
  - Alternatively supports Tagged Template Literals or HyperScript
  - Tagged Template solution is much more performant that the HyperScript version, but HyperScript opens up compatibility with some companion tooling

- https://github.com/Riim/cellx /ts
  - fast implementation of reactivity for javascript

- https://github.com/emberjs/data /ts
  - a lightweight reactive data library for JavaScript applications that provides composable primitives for ordering query/mutation/peek flows, managing network and cache, and reducing data for presentation.
  - The core of Ember‍Data is the Store, which coordinates interaction between your application, the Cache, and sources of data (such as your API or a local persistence layer). Optionally, the Store can be configured to hydrate the response data into rich presentation classes.

- https://github.com/vanjs-org/van /js
  - https://vanjs.org/
  - lightweight, zero-dependency and unopinionated Reactive UI framework based on pure vanilla JavaScript and DOM. 
  - You can convert any HTML snippet into VanJS code with our online converter.
  - VanJS helps you manage states and UI bindings as well, with a more natural API
# functional dom ui
- choo /6.5kStar/MIT/202001/js/在benchmark非常靠后
  - https://github.com/choojs/choo
  - A 4kb framework for creating sturdy frontend applications
  - At the core of Choo is an event emitter, which is used for both application logic but also to interface with the framework itself. The package we use for this is nanobus.
  - Choo uses nanomorph, which diffs real DOM nodes instead of virtual nodes
  - https://github.com/choojs/nanocomponent
    - Isolate native DOM libraries from DOM diffing algorithms
    - Class based components offering a familiar component structure
  - https://github.com/tornqvist/fun-component
    - Syntactic sugar on top of nanocomponent.
- https://github.com/kbrsh/moon
  - /6kStar/MIT/202003/js
  - https://moonjs.org/
  - The minimal & fast library for functional user interfaces
- https://github.com/hybridsjs/hybrids
  - The simplest way to create web components from plain objects and pure functions! 
- https://github.com/wtnbass/fuco
  - Functional Component like React, but for Web Components.

- https://github.com/CONNECT-platform/connective
  - https://github.com/CONNECT-platform/connective-html
  - agent-based reactive programming library for typescript
  - CONNECTIVE is a thin layer on top of RxJS, so it provides all the toolset of rxjs by proxy. 
  - However, while RxJS's API is better suited for short-lived and small flows, CONNECTIVE adds tools better suiting long-living and large/complex flows.

- https://github.com/funkia/list
  - An immutable list with unmatched performance and a comprehensive functional API.
- https://github.com/energydrink9/functional-data-grid
  - Data grids in functional style with ReactJS
- https://github.com/jongold/further
  - algebraic style composition for functional UIs
- https://github.com/mozilla/reflex
  - Functional reactive UI library

- https://github.com/nickslevine/zebras
  - Data analysis library for JavaScript built with Ramda
# hooks
- https://github.com/clebert/batis
  - A JS library for reactive programming using React-like Hooks
  - Even though Hooks are actually a constrained solution for modeling states in actually stateless functional components, they have proven to be very elegant in their design. 
  - In my opinion, they are particularly suitable for modeling finite-state automata.
  - I wanted to use this kind of reactive programming in other areas as well, such as programming web workers or even JS-controlled robots. 
    - Therefore I wrote Batis
- https://github.com/michael-klein/hookuspocus
  - allow you to add hooks to any function.
  - Internally, hookuspocus uses WeakMaps if possible to keep states between runs (and falls back to simple Maps).
# games/ecs
- https://github.com/LastOliveGames/becsy /ts/NoDeps
  - https://lastolivegames.github.io/becsy/
  - A multithreaded Entity Component System (ECS) for TypeScript and JavaScript, inspired by ECSY and bitecs.
  - Becsy is currently in 0.x status. What's there is reasonably well tested but many features are still missing and you can expect frequent API changes. Most importantly, multi-threading is not yet implemented.
  - bidirectional entity references with strong referential integrity
  - declarative system ordering based on data dependencies
  - built-in support for representing state machines (per Sander Mertens)
  - From ECSY we take:
    - a friendly object-oriented API for both JS and TS clients
    - reactive queries (rather than event callbacks)
    - references to native JS objects in components
  - From bitecs we take:
    - extensive use of ArrayBuffer for performance
    - a sparse array architecture

- https://gitlab.inria.fr/Loki/PolyphonyECS /js
  - Polyphony is an experimental toolkit demonstrating the use of Entity-Component-System (ECS) to design Graphical User Interfaces (GUI). 
  - It also extends the original ECS model to support advanced interfaces.
  - Systems are entities → we can model their dependencies and ordering with components
  - Devices are also entities → it makes it easy to access their data, and allows the support for multiple devices (mice, keyboards, ...)
  - Events are signaled using temporary components (deleted at the end of the systems chain) → systems can react to events without callbacks and observer patterns
  - [Polyphony ECS GUI and future](https://github.com/traffaillac/traffaillac.github.io/issues/1)

- https://github.com/NateTheGreatt/bitECS /js/NoDeps
  - Functional, minimal, data-oriented, ultra-high performance ECS library written using JavaScript TypedArrays.

- https://github.com/ecsyjs/ecsy /js/archived
  - https://ecsyjs.github.io/ecsy/
  - ECSY (pronounced as "eck-see") is an highly experimental Entity Component System framework implemented in javascript, aiming to be lightweight, easy to use and with good performance.
  - Framework agnostic
  - Designed to avoid garbage collection as possible
  - Support for reactive behaviour on systems (React to changes on entities and components)
  - ECSY will not ship with features that bind it to a rendering engine or framework. Instead, we encourage the community to build framework specific projects like ecsy-three, ecsy-babylon, and ecsy-two.
  - ECSY does not adhere strictly to "pure ECS design". We focus on APIs that push users towards good ECS design like putting their logic in systems and data in components. 

- inspired by ecsy
  - https://github.com/DavidPeicho/ecstra /ts
    - Fast & Flexible EntityComponentSystem (ECS) for JavaScript and Typescript, available in browser and Node.js.
  - https://github.com/mreinstein/ecs /js
    - data oriented, functional entity component system.

- https://github.com/fritzy/ape-ecs /js
  - performant, featureful, and flexible Entity-Component-System library for JavaScript, intended for use in games and simulations.
  - Persisted Queries (indexes) are updated as Entity composition changes.
  - Not all systems need to run every frame.
  - The Entity-Component-System paradigm is great for managing dynamic objects in games and simulations.
# more-fp
- https://github.com/paldepind/flyd
  - /1.5kStar/MIT/201809/js
  - The minimalistic but powerful, modular, functional reactive programming library in JavaScript.
- https://github.com/nullobject/fkit
  - A functional programming toolkit for JavaScript.
- https://github.com/sebastienfilion/functional
  - Common Functional Programming Algebraic data types for JavaScript that is compatible with most modern browsers and Deno.
- https://github.com/osteele/functional-javascript
  - It defines the standard higher-order functions such as map, reduce (aka foldl), and select (aka filter)
  - It also defines functions such as curry, rcurry, and partial for partial function application; and compose, guard

- https://github.com/frouriojs/velona
  - Velona is TypeScript DI helper for functional programming.

- https://github.com/mreinstein/ecs
  - data oriented, functional entity component system.

- https://github.com/TomerAberbach/contextus
  - The context you know and love, but framework agnostic!
