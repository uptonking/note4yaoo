---
title: pattern-arch-flux-examples
tags: [elm, examples, flux, redux]
created: 2023-11-17T10:27:56.649Z
modified: 2023-11-17T10:28:14.247Z
---

# pattern-arch-flux-examples

# guide

- tips
  - flux的参考案例比elm多, event-sourcing架构更经典
  - 支持undo/history/snapshot: flux, elm
  - 考虑将redux-devtools的协议和交互作为time-travel的通用方案，在api/ui/数据结构
  - 支持多store
  - 应用层级的store不适合保存变化频率很高的状态，如input输入框、scroll、animation

- component vs app
  - 跨框架的component常使用adapter模式，跨框架的app应用使用flux/elm
  - component层的数据流常是内存+sync，app层的数据流尝试client-server+async

- resources
  - [Fluxxor - What is Flux?](http://fluxxor.com/what-is-flux.html)
  - [Redux without the sanity checks in a single file](https://gist.github.com/gaearon/ffd88b0e4f00b22c3159)
# popular
- https://github.com/voronianski/flux-comparison /2.8kStar/MIT/202006/js
  - Practical comparison of different Flux solutions
  - Similar app implemented with different Flux solutions including Facebook's, Yahoo's and others.
  - 还提供了 Non React.js examples: riot, vuex
  - [Flux Comparison by Example | Hacker News_201502](https://news.ycombinator.com/item?id=8989495)

- nanostores /2.5kStar/MIT/202301/js/多multi-stores/多bindings
  - https://github.com/nanostores/nanostores
  - state manager for React/RN/Vue/Svelte with many atomic tree-shakable stores
  - With small atomic and derived stores, you do not need to call the selector function
  - 提供了扩展，persist to localStorage, router, i18n, logux-client-crdt，使用最佳实践
  - 支持ssr

- https://github.com/facebookarchive/flux /17.4kStar/BSD/202303/js/函数式风格/archived
  - https://facebookarchive.github.io/flux/docs/in-depth-overview
  - Application Architecture for Building User Interfaces
  - We recommend using more sophisticated alternatives like Redux, MobX, Recoil, Zustand, or Jotai
  - Flux is more of a pattern than a framework
  - However, we often use `EventEmitter` as a basis for `Store`s and React for our `View`s
  - The one piece of Flux not readily available elsewhere is the `Dispatcher`.
  - https://github.com/huanghaiyang/fluxory /201608/js
    - flux history; back([actionType]); forward([actionType])

- https://github.com/yahoo/fluxible /1.8kStar/BSD/202311/js/函数式风格
  - https://fluxible.io/faq.html
  - A pluggable container for universal flux applications
  - 👉🏻 Singleton-free for server rendering 
    - Stores are classes that are instantiated per request or client session. 
    - This ensures that the stores are isolated and do not bleed information between requests.
  - Facebook’s Flux only works on the client, but it may be easier to figure out since it doesn’t have to deal with concurrency issues.
  - [Action History Plugin_201604](https://github.com/yahoo/fluxible/pull/418)
  - [Time travel devtooling](https://github.com/yahoo/fluxible/issues/215)
    - The architecture of Fluxible is very suitable for implementing alt-devtool or redux-devtools style devtooling.
  - [Enable debug](https://github.com/yahoo/fluxible/issues/382)
    - You can do this on any app compiled with debug intact 
    - Expand Local Storage, Add a key debug, add value *
  - [Routing + Fetch Data architecture](https://github.com/yahoo/fluxible/issues/18)
  - https://github.com/fleur-js/fleur /202204/ts
    - An Fully-typed Flux framework inspired by Fluxible
    - Runs on Node/Web. No dependence to React
    - immer.js builtin Store
    - 👉🏻 Default async operations (side effector) support
    - Server-side rendering support
    - Support React Hooks in @fleur/react
    - Fleur recommends Re-ducks like directory structure.
    - Support Redux DevTools，支持时间旅行
    - https://github.com/fleur-js/froute
      - Framework independent Router for React. redux/Fleur

- https://github.com/goatslacker/alt /3.5kStar/MIT/201609/js/class风格/支持undo
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
  - [Add a time travel decorator_201504](https://github.com/goatslacker/alt/pull/208)
  - https://github.com/goatslacker/alt-tutorial /201506/js
    - simple flux tutorial built with alt and react
  - https://github.com/goatslacker/alt-devtool
  - [From Alt to Redux ecosystem (redux-actions, redux-thunk, react-redux, redux-saga)](https://gist.github.com/chodorowicz/c4916dbe1c81ccb14caf)
  - forks
  - https://github.com/bitshares/alt
  - https://github.com/SpaceKnow/alt /decorator
  - https://github.com/koliseoapi/alt-ng /202001/js
    - https://alt-ng.koliseo.com/
    - A flux implementation without the boilerplate

- https://github.com/zalmoxisus/remotedev /MIT/201812/js
  - Remote debugging for any flux architecture.
  - Monitoring flux app's actions along with states to a remote monitor. 
  - Meant to be used even in production with any flux architecture for web, universal, React Native, hybrid, desktop and server side apps.

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
  - https://github.com/acdlite/flummox-immutable-store /201504/js
    - Flummox store with Immutable.js support for serialization and undo/redo

- https://github.com/HubSpot/general-store /202110/ts
  - http://github.hubspot.com/general-store
  - Simple, flexible store implementation for Flux
  - aims to provide all the features of a Flux store without prescribing the implementation of that store's data or mutations.
  - All other features, like Immutability, data fetching, undo, etc. are implementation details.
  - Using Redux devtools extension you can inspect the state of a store
  - [Keeping Flux Flexible with general-store_201502](https://product.hubspot.com/blog/keeping-flux-flexible-with-general-store)

- https://github.com/Kuasr/flux /202212/ts
  - a library that implements flux architecture designed by Meta with some modifications used in Kuasr's projects.

- https://github.com/threepointone/disto /201507/js/支持undo和snapshot
  - mildly opinionated flux
  - deprecated, consider using redux instead
  - follows the original flux architecture, with no new concepts
  - leans heavily on regular functions
  - timetravel helper: r.record(); r.stop(); r.play(); r.snapshot(); 
- https://github.com/NoMoreDeps/shadow-flux /202009/ts
  - https://nomoredeps.github.io/shadowjs
  - Flux implementation in typescript
  - S-Flux V3 comes with an integrated State Visualizer
  - roadmap: Improve Debug visualizer to allow time travel

- https://github.com/ohager/nanoflux /201702/js/functional
  - lightweight and dependency-free Flux implementation
  - uses a pure functional approach as a performant solution.
  - The idea of this implementation is to support a very small, but full Flux implementation (separated Action, Dispatcher, and Store), and also a "fluxy" version, with Action and Dispatcher merged in one unit.
- https://github.com/ChiuMungZitAlexander/vanilux /202311/ts
  - 一个使用原生JS实现Flux架构的库
- https://github.com/victorpotasso/fluxo /202205/ts
  - A Vanilla FLUX library

- https://github.com/youwol/flux-view /202311/ts/rxjs
  - Tiny library to render HTML documents using reactive programming primitives.
  - It leverage reactive programming primitives provided by RxJS to enable HTML elements being defined not only using plain values but also in terms of stream.

- https://github.com/geotrev/core-flux /202307/js
  - functional flux utility. Control the flow of state data between subscribers
  - You can create as few or as many stores as your heart desires! They will all be independent from one another.

- https://github.com/redux-loop/redux-loop /2kStar/202111/js/elm/inactive
  - https://redux-loop.js.org/
  - A library that ports Elm's effect system to Redux
  - Many other methods for handling effects in Redux, especially those implemented with action-creators, incorrectly teach the user that asynchronous effects are fundamentally different from synchronous state transitions
    - With redux-loop, the reducer doesn't just decide what happens now due to a particular action, it decides what happens next.
    - All of the behavior of your application can be traced through one place, and that behavior can be easily broken apart and composed back together
    - This is one of the most powerful features of the Elm architecture, and with redux-loop it is a feature of Redux as well.
  - https://github.com/jarvisaoieong/redux-architecture /201603/js
    - https://github.com/jarvisaoieong/redux-architecture
    - elm architecture in redux with redux-loop
    - This repo is port of the elm architecture examples in redux with redux-loop to show the benefits of hierarchical composition everywhere. 
    - Use redux-loop as side effect solution
    - I used my fork of redux-loop and redux-logger to demonstrate how to log the high order action and async action

- https://github.com/Yomguithereal/baobab /js/inactive
  - JavaScript & TypeScript persistent and optionally immutable data tree with cursors.
  - It is mainly inspired by functional zippers (such as Clojure's ones) and by Om's cursors.
  - It aims at providing a centralized model holding an application's state and can be paired with React easily through mixins, higher order components, wrapper components or decorators
  - you can create cursors to easily access nested data in your tree and listen to changes concerning the part of the tree you selected.
  - Note that the tree, being a persistent data structure, will shift the references of the objects it stores in order to enable immutable comparisons between one version of the state and another
  - Baobab lets you record the successive states of any cursor so you can seamlessly implement undo/redo features.
  - https://github.com/Yomguithereal/baobab-react
    - React integration for Baobab.
# examples
- https://github.com/jorinvo/miniflux-todomvc /201612/js/immutable-js
  - https://jorinvo.github.io/miniflux-todomvc
  - I rebuilt TodoMVC to learn how to use the ideas behind the Flux architecture
  - you can try out time traveling and you can access the global helpers render, actions, state and states.
  - Immutable.js for awesome data structures
  - [Miniflux_201507](https://jorin.me/miniflux/)
- https://github.com/MandarinConLaBarba/flux-immutable-todomvc /201502/js
  - http://mandarinconlabarba.github.io/flux-immutable-todomvc/
  - A TodoMVC Implementation with Flux and ImmutableJS
  - instead of undoing you load a previous state as the new state

- https://github.com/NickStefan/rixif /201602/js
  - In early 2015, I had wanted to implement an entire excel experience in javascript.
  - With React, Immutable.js, and old school vanilla flux, I got pretty far
  - [How to implement a spreadsheet | Hacker News_201507](https://news.ycombinator.com/item?id=9940126)
    - I implemented a spreadsheet in react, flux, immutable, and used a command pattern
    - I did not take the approach of cells actually observing each other. Instead I had a recursive function that worked from the entered cell 
    - The hardest part was updating the string representations of the formulas when you insert a new column or row, and then re-updating each cell's dependencies arrays.
    - One 🛑 mistake I made was trying to implement the undo/redo to be totally reversable at every step. So every command stores the way to go both back and forward. In hindsight, I should have just stored forward commands and rebaked from the beginning when someone wanted to go back in time.
    - Handsontable.js. That library has some major design flaws. Handsontable only takes simple 'number' or 'string' value for each cell

- https://github.com/stonarini/bike-web-b2b /202304/js
  - front-end in vanilla.js for bike-service-hub. 
  - Using new concepts, such as classes, web-components, generators... and the flux pattern.
  - https://github.com/stonarini/bike-service-hub

- https://github.com/AlexEntrepreneur/SimpleFlux /MIT/202305/ts/class风格
  - A way to organise simple vanilla javascript components inspired by the Flux architecture
  - organise a simple vanilla JS project into class components with local and global states
  - It does not use a virtual DOM and is still mutative, using inbuilt DOM manipulation methods.
  - https://github.com/AlexEntrepreneur/Notes-Board-Demo /202304/js
    - a single-page notes app demonstrating SimpleFlux

- https://github.com/Akashh1996/Tour-of-hero /202102/js
  - Application created in vanilla javascript adapting the React-flux style with store and component seperated
  - The data displayed is by fetching the mocked API.

- https://github.com/design-with-js/flux-plain-js /201909/js/单文件
  - Flux pattern in vanilla js single page application
- https://github.com/srobertson421/vanilla-state /201711/js/单文件
  - Reactive App built using vanilla JS. Utilizes principles found in React and in Flux architectures like Redux.

- https://github.com/auth0-blog/react-flux-jwt-authentication-sample /201509/js
  - Sample for implementing Authentication with a React Flux app and JWTs
  - [Adding authentication to your React Flux app](https://auth0.com/blog/adding-authentication-to-your-react-flux-app/)

- https://github.com/swarajlaha/product-inventory /202005/js
  - A product inventory application made using React JS and JSON server, with features like - user authentication, managing products, with a responsive UI and good UX.

- https://github.com/davezuko/flux-wizard-demo /201509/js
  - A lightweight, flux-based wizard system for React
  - Free "undo changes" ability to revert all changes made in a step session

- https://github.com/SJern/slamk /201609/js
  - a full-stack web application inspired by the popular team-collaboration application Slack
  - using the Flux architecture and React.js on the front-end and Ruby on Rails on the back-end
# utils
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

- https://github.com/ajpocus/adventure-kit /201708/js
  - A toolkit for making adventure and RPG games in the browser.
  - I used the Flux architecture here, but it was before I heard about Redux, so I used alt.js instead

## undo/history

- https://github.com/isocroft/Radixx /201810/js/代码是ng风格
  - This is a simple library that implements the Facebook Flux Architecture with a twist to how the entire application state is managed and changed/updated.
  - It resembles Redux in a lot of ways. The key deferentiator in both is that Radixx utilizes an actions stack and Redux utilizes an immutable state tree.
    - 偏向event-sourcing
    - Redux is basically event-sourcing where there is a single projection to consume the application state.
    - A single state tree can grow big really fast for a single store but an actions stack grows subtlely for a number of stores when dealing with complex single-page applications(SPAs)
  - Infinite/Finite Undo/Redo + Time Travel
  - 😁 Gains of Redux single store, Same applies to Radixx
    - Infinite Undo/Redo + Live-Editing Time Travel (As application state is immutable).
    - Predictable Atomic Operation on Application state object (As actions are run in a specific predictable order).
    - Single source of truth (No Guesswork!!) for applicaton state
  - 😩 Troubles with Redux single store
    - Dynamically structured state is impossible. (mature, complex apps need this the most).
    - Increased probability of state key(s) collisions between reducers (very likely in a big complex web app)
    - Global variables are most times a bad thing (This applies to the composition of the Redux application state itself) as you could clobber(痛打；猛揍) them unknowingly. 类似数据库的单点故障问题
    - Performance suffers as your state tree gets larger
    - Each time the connect() decorator is called, it pulls in the entire application state (when using react-redux project library).
  - Use of Traits (as Mixins) for ReactJS and VueJS (even though most people think mixins are dead and composition should be the only thing in used, i still think mixins have a place)
  - Use with Single Page App Frameworks/Libraries e.g. VueJS 1.x/2.x, AngularJS 1.x, Angular 2.x, Ractive, ReactJS, jQuery
  - don't store this in Radixx stores (e.g. Text Input - being entered, Animation Tween Properties/Values, Scroll Position Values, Text Box Caret Position, Mouse Position Values, Unserializable State - like functions)

- https://github.com/conatus/flame /MIT/201601/js
  - Opinionated single-state-tree immutable Flux
  - 依赖flux、immutable.v3、immutable-diff
  - The key difference between Flux and Flame, is that the stores themselves do not hold onto any state whatsoever, instead they are provided access to a subtree of a single, immutable global tree which they are able to modify. Components are not able to access the raw state tree, instead they request access to a store(s) subtree within that tree.
  - Flame keeps it like Flux. Anyone with an existing Flux implementation will be able to use and understand Flame with very little modifications
  - Flame's state tree is immutable - every action handler inside a store is expected to provide a new ImmutableJS instance for every action it handles, with a history of changes recorded.
  - What's unique about Flame however is how that history is stored - each of those changes described by a store's handler is recorded as a diff between two immutable states, instead of another instance of the entire state tree

- https://github.com/mj1618/reckon-js /201609/js
  - an event-based, immutable state container for javascript apps.
  - Reckon manages state as Facebook Immutable objects. 
  - Reckon provides cursors, views and scoped events so that a single Reckon instance can be used for all state in an application.

- https://github.com/yoshuawuyts/state-atom /201508/js
  - Create an immutable state atom. Forms the basis for hot reloading, infinite undo/redo (time-travel) and more.
  - Backend applications have both persistant state (database) and application state (memory). state-atom takes this analogy and applies it to the frontend. Changes saved to the atom are immutable, returning mutable copies when read. Only when actively persisting the state back to the atom will listeners fire and changes propagate throughout the application.
# flux-like
- [A Redux-like Flux implementation in <75 lines of code](https://gist.github.com/acdlite/9f1b5883d132ad242323)

- https://github.com/luisvinicius167/dutier /201806/js/NoDeps
  - The immutable, async and hybrid state management solution for Javascript applications.
  - async by default
  - Works well with any Javascript Framework
  - inspired by Redux
  - The application state is stored in an object tree inside a single store.

- https://github.com/nitrogenlabs/arkhamjs /202212/ts
  - http://arkhamjs.io/
  - Javascript Flux framework
  - Consisting of a singular state tree with a unidirectional data flow.
  - All data is stored within a single store.
  - [ArkhamJS React Framework. Next generation javascript framework… | by Giraldo Rosales | Medium_201701](https://medium.com/@nitrog7/arkhamjs-react-framework-8f0ecd28cfbc)

- https://github.com/f/delorean /201704/js
  - a tiny Flux pattern implementation.
  - Unidirectional data flow, it makes your app logic simpler than MVC
  - framework agnostic. There's no view framework dependency.
  - Built-in React.js integration, easy to use with Flight.js and Ractive.js 

- https://github.com/kenwheeler/mcfly /201703/js
  - a library that provides all 3 components of Flux architecture, using Facebook's Dispatcher, and providing factories for Actions & Stores.

- https://github.com/jmreidy/fluxy /201506/js/支持undo
  - An implementation of Facebook's Flux architecture.
  - Fluxy is an implementation that includes some differentiating features:
    - View components should be completely separated from Flux. They can intereact with Flux Stores and Actions via direct API calls, without coupling them to the Flux implementation
    - Promises (via Bluebird) drive the Dispatcher/Action system, along for the easy registration of async action handlers
    - Stores embrace immutable data, going so far as to be powered by Mori, which provides a light convenience API around ClojureScript's data structures.
  - [Redo support](https://github.com/jmreidy/fluxy/issues/41)
    - One should be able to redo(). The store shouldn't pop states on undo(), but only when doing set().
    - Another option is how http://mandarinconlabarba.github.io/flux-immutable-todomvc does it, instead of undoing you load a previous state as the new state.

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
  - https://microsoft.github.io/satcheljs/book/core-concepts.html
  - Satchel is a data store based on the Flux architecture. 
  - we found reducers and immutable state cumbersome to deal with
  - Satchel is an opinionated implementation of Flux.
    - Orchestrators are Satchel's mechanism for dealing with side effects. For instance, an orchestrator might make a service call and dispatch more actions once it returns.
    - The root store (and therefore the entire store underneath it) is a MobX observable
  - It is characterized by exposing an observable state that makes view updates painless and efficient.
  - Satchel uses MobX under the covers to allow React components to observe the data they depend on.
  - 依赖mobx.v4、mobx-react.v5

## flux-non-js

- https://github.com/redux-rs/redux-rs /MIT/202212/rust
  - A Rust implementation of Redux.

- https://github.com/brunocodutra/reducer /MIT/202212/rust
  - A predictable reactive framework for Rust apps inspired by Redux

- https://github.com/wordpress-mobile/WordPress-FluxC-Android /202311/kotlin
  - WordPress-FluxC-Android is a networking and persistence library that helps to connect and sync data from a WordPress site (self hosted, or wordpress.com site).
  - Based on the Flux pattern, we're using: Dagger2 for dependency injection, WellSql for persistence.
  - https://github.com/wordpress-mobile/WordPress-Android /kotlin

- https://github.com/Yarikx/reductor /201711/java
  - Redux inspired predictable state container library for Java/Android.
  - It leverages annotation processing to validate correctness and generate boilerplate code at compile time

- https://github.com/lgvalle/android-flux-todo-app /201610/java
  - Example of how to implement an Android TODO App using Facebook Flux Architecture

- https://github.com/satorufujiwara/android-flux-architecture /201712/kotlin
  - A showcase of Flux architecture patterns for Android apps
- https://github.com/masmovil/masmini-kotlin /202105/kotlin
  - Minimal Flux architecture written in Kotlin.
# more
- https://github.com/nadimtuhin/redux-vue /201710/js
  - Vue Redux is tested to work on vue v2 and should be used with vue-jsx

- https://github.com/redux-zero/redux-zero /1.9kStar/MIT/202008/ts/inactive
  - lightweight state container based on Redux
  - 不依赖redux
  - [Introducing Redux Zero. Redux Zero is a lightweight state… | by Matheus Lima | Medium_201710](https://medium.com/@matheusml/introducing-redux-zero-bea42214c7ee)
