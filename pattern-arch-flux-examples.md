---
title: pattern-arch-flux-examples
tags: [examples, flux, redux]
created: 2023-11-17T10:27:56.649Z
modified: 2023-11-17T10:28:14.247Z
---

# pattern-arch-flux-examples

# guide

# popular
- https://github.com/voronianski/flux-comparison /2.8kStar/MIT/202006/js
  - Practical comparison of different Flux solutions
  - Similar app implemented with different Flux solutions including Facebook's, Yahoo's and others.
  - 还提供了 Non React.js examples: riot, vuex
  - [Flux Comparison by Example | Hacker News_201502](https://news.ycombinator.com/item?id=8989495)

- https://github.com/facebookarchive/flux /17.4kStar/BSD/202303/js/函数式风格/archived
  - https://facebookarchive.github.io/flux/docs/in-depth-overview
  - Application Architecture for Building User Interfaces
  - We recommend using more sophisticated alternatives like Redux, MobX, Recoil, Zustand, or Jotai.
  - Flux is more of a pattern than a framework
  - However, we often use `EventEmitter` as a basis for `Store`s and React for our `View`s
  - The one piece of Flux not readily available elsewhere is the `Dispatcher`.

- https://github.com/yahoo/fluxible /1.8kStar/BSD/202311/js
  - https://fluxible.io/faq.html
  - A pluggable container for universal flux applications.
  - 👉🏻 Singleton-free for server rendering 
    - Stores are classes that are instantiated per request or client session. 
    - This ensures that the stores are isolated and do not bleed information between requests.
  - Facebook’s Flux only works on the client, but it may be easier to figure out since it doesn’t have to deal with concurrency issues.

- https://github.com/fleur-js/fleur /202204/ts
  - An Fully-typed Flux framework inspired by Fluxible.
  - Runs on Node / Web.
  - Server-side rendering support
  - Support React Hooks in @fleur/react
  - Fleur recommends Re-ducks like directory structure.
  - https://github.com/fleur-js/froute
    - Framework independent Router for React. redux/Fleur

- https://github.com/almin/almin /503Star/MIT/202108/ts/class风格/inactive
  - https://almin.js.org/
  - Client-side DDD/CQRS for JavaScript.
  - Almin is an implementation of Read/Write Stack Architecture that is well-known as Flux/CQRS.
  - I often hear a story that "Control flow of Flux/Redux is cool, but where to implement domain logic."
    - Almin aim to fill the Missing things between MV* and Flux/Redux.
  - Responsibility Layers patten - well-known as DDD(Domain-Driven Design)/CQRS

- https://github.com/davezuko/re-frame /13Star/MIT/201912/js/inactive
  - Vanilla JavaScript port of the popular ClojureScript library for pragmatic, flux-like state management
  - Re-frame helps make state management predictable, testable, and pragmatic. It achieves this via message passing, which decouples action from intent. 
  - On top of this, it provides first-class semantics for dealing with side-effects
  - From a high-level, re-frame is flux-like with events and event handlers, which are similar to redux's actions and reducers. 
  - Compared to redux, re-frame is more feature complete out of the box, with built-in interceptors, effects, subscriptions, and test utilities. 

- https://github.com/goatslacker/alt /3.5kStar/MIT/201609/js/class风格
  - https://alt.js.org/
  - Isomorphic flux implementation
  - 100% Flux: Unidirectional data flow
    - stores have no setters, 
    - Actions are fire and forget
    - you get constants, and Flux's single central dispatcher. All Stores receive the dispatch
  - Isomorphic and works with react-native. Server Side Rendering
  - At any point in time you can take a snapshot of the entire application state and then reload it later
  - Extremely flexible and unopinionated in how you use flux. 
    - Create traditional singletons or use dependency injection.
    - your asynchronous data fetching can live in the actions, or they can live in the stores. 
    - Stores may also be traditional singletons as in flux, or you can create an instance and have multiple store copies. This leads us into server side rendering.
  - Creating separate instances of flux rather than relying on singletons can help when building isomorphic applications.
    - Singletons only become a problem if you wish to share data fetching with client and server
    - Taking this approach means you're making the trade-off of injecting the flux instance into your application in order to retrieve the stores and use the actions. 
    - This approach is similar to how fluxible solves isomorphic applications.
  - 服务端无法使用action
  - https://github.com/goatslacker/alt-tutorial /201506/js
    - simple flux tutorial built with alt and react

- https://github.com/acdlite/flummox /1.7kStar/MIT/201708/js
  - https://acdlite.github.io/flummox
  - modular, testable, isomorphic Flux. No singletons required.
  - No singletons = isomorphism for free
  - What makes Flummox special? 
    - Flummox allows you to encapsulate your entire Flux set-up — stores, actions, constants, and the dispatcher — into a single class, with zero singletons or global references.
    - `const flux = new Flux();` 初始化
    - There are many benefits to this approach, but the biggest one is that it makes isomorphism (running the same code on both the server and the client) incredibly straightforward.
  - The primary goal of Flummox is reduce the boilerplate involved in setting up Flux for your application, so the API has been kept as minimal and predictable as possible. It uses Facebook’s dispatcher under the hood.
  - isomorphic is one of the biggest motivating factors for creating this library. 
    - Isomorphism is tricky or impossible in many other Flux libraries because they rely on singleton objects, spread out across multiple modules.
    - because Flummox does not rely on singletons, you get isomorphism for free: just create a new Flux instance on each request
    - Flummox also gives you the ability to serialize the initial state of your application on the server, send it down to the client as a string
  - The dispatcher and constants are implementation details — no need to interact with them unless you want to

- https://github.com/HubSpot/general-store /202110/ts
  - http://github.hubspot.com/general-store
  - Simple, flexible store implementation for Flux
  - aims to provide all the features of a Flux store without prescribing the implementation of that store's data or mutations.
  - All other features, like Immutability, data fetching, undo, etc. are implementation details.
  - Using Redux devtools extension you can inspect the state of a store
  - [Keeping Flux Flexible with general-store_201502](https://product.hubspot.com/blog/keeping-flux-flexible-with-general-store)

- https://github.com/Kuasr/flux /202212/ts
  - a library that implements flux architecture designed by Meta with some modifications used in Kuasr's projects.

- https://github.com/ohager/nanoflux /201702/js
  - lightweight and dependency-free Flux implementation
  - uses a pure functional approach as a performant solution.
  - The idea of this implementation is to support a very small, but full Flux implementation (separated Action, Dispatcher, and Store), and also a "fluxy" version, with Action and Dispatcher merged in one unit.
- https://github.com/ChiuMungZitAlexander/vanilux /202311/ts
  - 一个使用原生JS实现Flux架构的库
- https://github.com/victorpotasso/fluxo /202205/ts
  - A Vanilla FLUX library

- https://github.com/geotrev/core-flux /202307/js
  - functional flux utility. Control the flow of state data between subscribers
  - You can create as few or as many stores as your heart desires! They will all be independent from one another.
# flux-like
- https://github.com/nitrogenlabs/arkhamjs /202212/ts
  - http://arkhamjs.io/
  - Javascript Flux framework
  - Consisting of a singular state tree with a unidirectional data flow.
  - All data is stored within a single store.
  - [ArkhamJS React Framework. Next generation javascript framework… | by Giraldo Rosales | Medium_201701](https://medium.com/@nitrog7/arkhamjs-react-framework-8f0ecd28cfbc)

- https://github.com/luisvinicius167/dutier /201806/js/NoDeps
  - The immutable, async and hybrid state management solution for Javascript applications.
  - async by default
  - Works well with any Javascript Framework
  - inspired by Redux
  - The application state is stored in an object tree inside a single store.

- https://github.com/f/delorean /201704/js
  - a tiny Flux pattern implementation.
  - Unidirectional data flow, it makes your app logic simpler than MVC
  - framework agnostic. There's no view framework dependency.
  - Built-in React.js integration, easy to use with Flight.js and Ractive.js 

- https://github.com/kenwheeler/mcfly /201703/js
  - a library that provides all 3 components of Flux architecture, using Facebook's Dispatcher, and providing factories for Actions & Stores.

- https://github.com/reflux/refluxjs /5.4kStar/BSD/201804/js
  - A simple library for uni-directional dataflow application architecture with React extensions inspired by Flux
  - The main function of Reflux is to introduce a more functional programming style architecture by eschewing(避免使用, 避开) MVC like pattern and adopting a single data flow pattern.

- https://github.com/karelsteinmetz/bobflux /201911/ts
  - pure functional implementation of FLUX architecture
  - inspired by Flux, Reflux and Redux
  - depends on Bobril
  - https://github.com/Bobris/Bobril /202310/ts
    - Component oriented framework inspired by ReactJs (Virtual DOM, components with state) and Mithril (small size, more complete framework). 
    - Compared to ReactJS Added speeeed, autoprefixer, CSS in JS, router, additional livecycle methods, only rAF based repaint. 
    - Bobril ignores Isomorphic JavaScript

- https://github.com/addthis/fluxthis /201902/js
  - super-opinionated, yell-at-you-for-everything, immutable Flux framework

- https://github.com/tkh44/smitty /201704/js
  - Tiny flux implementation built on mitt
  - Usage with Preact and React

- https://github.com/microsoft/satcheljs /395Star/MIT/202203/ts
  - https://microsoft.github.io/satcheljs
  - Satchel is a data store based on the Flux architecture. 
  - It is characterized by exposing an observable state that makes view updates painless and efficient.
  - we found reducers and immutable state cumbersome to deal with
  - Satchel uses MobX under the covers to allow React components to observe the data they depend on.
  - 依赖mobx.v4、mobx-react.v5
# examples
- https://github.com/stonarini/bike-web-b2b /202304/js
  - ront-end in vanilla.js for bike-service-hub. 
  - Using new concepts, such as classes, web-components, generators... and the flux pattern.
  - https://github.com/stonarini/bike-service-hub

- https://github.com/design-with-js/flux-plain-js /201909/js
  - Flux pattern in vanilla js single page application
  - https://github.com/AlexEntrepreneur/SimpleFlux

- https://github.com/auth0-blog/react-flux-jwt-authentication-sample /201509/js
  - Sample for implementing Authentication with a React Flux app and JWTs
  - [Adding authentication to your React Flux app](https://auth0.com/blog/adding-authentication-to-your-react-flux-app/)
# utils
- https://github.com/zalmoxisus/remotedev /201812/js
  - Remote debugging for any flux architecture.

- https://github.com/lmiller1990/flux-entities /202007/ts
  - The flux entity pattern, or simply the entity pattern, is a common pattern I identified and extracted over the last few years of working on various single page apps
  - This pattern, however is applicable to any flux library
  - This is the official library and reference implementation for the pattern.

- https://github.com/elyor-sh/mobx-flux /202310/ts
  - fast package for comfortable work with flux architecture in mobx. 
  - It's easy to replace the redux-toolkit with this package. 

- https://github.com/the-dr-lazy/deox /202103/ts
  - https://deox.js.org/
  - Functional Type-safe Flux Standard Utilities
  - The most common complaint about Flux is how it makes you write a lot of boilerplate. 
    - this is where Deox takes place to make maintenance of Flux architecture simpler and more readable by sticking to functional programming paradigm.

- https://github.com/piotrwitek/typesafe-actions /202207/ts
  - Typesafe utilities for "action-creators" in Redux / Flux Architecture
  - https://github.com/aikoven/typescript-fsa

- https://github.com/optimizely/nuclear-js /201809/js
  - https://optimizely.github.io/nuclear-js/
  - Traditional Flux architecture built with ImmutableJS data structures.
  - All app state is in a singular immutable map, like Om
# more
- https://github.com/redux-zero/redux-zero /1.9kStar/MIT/202008/ts/inactive
  - lightweight state container based on Redux
  - 不依赖redux
  - [Introducing Redux Zero. Redux Zero is a lightweight state… | by Matheus Lima | Medium_201710](https://medium.com/@matheusml/introducing-redux-zero-bea42214c7ee)
