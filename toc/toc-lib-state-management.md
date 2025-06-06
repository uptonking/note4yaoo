---
title: toc-lib-state-management
tags: [lib, state, toc]
created: 2024-05-28T12:38:00.092Z
modified: 2020-07-14T11:03:53.196Z
---

# toc-lib-state-management

# guide
- 实现状态管理的思路
  - flux/event
    - redux/logux
    - zustand
    - storeon
    - unistore
  - atoms
    - jotai
    - nanostores
    - recoil
    - effector
  - proxy
    - mobx
    - valtio
  - state-machine
    - xstate
    - zag.js
  - server-state-cache
    - swr
    - tanstack-query
  - signals
    - preact/signal

- 状态管理选型参考
  - react
    - constate
    - unstated-next
    - react-redux
  - 状态管理中的异步逻辑，近几年swr/react-query非常流行

- url as state-management

- 基于hooks模仿redux的api
  - [State Management with React Hooks and Context API](https://devsmitra.medium.com/state-management-with-react-hooks-and-context-api-2968a5cf5c83)
  - [React doesn't need state management tool, I said](https://dev.to/tolgee_i18n/react-doesnt-need-state-management-tool-i-said-31l4)
    - https://github.com/tolgee/tolgee-platform/blob/main/webapp/src/fixtures/createProvider.tsx
# agnostic
- redux /53.7kStar/MIT/202005/ts/单向数据流
  - https://github.com/reduxjs/redux
  - https://redux.js.org/
  - Predictable state container for JavaScript apps.
  - 源码简单，中间件丰富
  - 全局唯一的store可能导致过多的subscriber执行

- mobx /22.1kStar/MIT/202007/ts/响应式数据流/NoDeps
  - https://github.com/mobxjs/mobx
  - https://mobx.js.org/README.html
  - a battle tested library that makes state management simple and scalable by transparently applying functional reactive programming (TFRP).
  - Mobx implements TFRP in a glitch-free, synchronous, predictable and efficient manner.
  - mobx isn't pubsub. It doesn't do change detection
  - 基于隐式的自动依赖搜集和执行，支持细粒度的修改与通知，但可能代理对象过多，分析排查不便

- nanostores /2.5kStar/MIT/202301/js
  - https://github.com/nanostores/nanostores
  - state manager for React/RN/Vue/Svelte with many atomic tree-shakable stores
  - With small atomic and derived stores, you do not need to call the selector function
  - 提供了扩展，persist to localStorage, router, i18n, logux-client-crdt，使用最佳实践
  - 支持ssr
  - [Astro: Sharing state using nanostores](https://docs.astro.build/en/core-concepts/sharing-state/#why-nano-stores)
  - We released Nano Stores 0.5, a new version of tiny (200-900 bytes) state manager for React/Vue/Svelte, designed to:
    - Move logic from components to stores and separate application logic and UI
    - Support tree-shaking
    - [Nano Stores 0.5 · Issue_202109](https://github.com/nanostores/nanostores/issues/57)
  - [Nano Stores in Angular: how to make the state management simpler - DEV Community](https://dev.to/evilmartians/nano-stores-in-angular-how-to-make-the-state-management-simpler-38a1)

- effector /4.3kStar/MIT/202309/ts/event-driven
  - https://github.com/effector/effector
  - https://effector.dev/
  - effective multi-store state manager for Javascript apps (React/Vue/Node.js)
  - Effector offers the possibility to describe the business logic in the same language as the product development team communicates, using basic primitives: Event, Store, Effect respectively. 
  - stores should be freely combined - data that the application needs can be statically distributed, showing how it will be converted in runtime.
  - no decorators, no need to use classes or proxies; the api library uses only functions and plain js objects
  - [Article "Why did I choose Effector instead of Redux or MobX?"](https://gist.github.com/Chudesnov/03a9338db1826eb1019ea712bedd3e3b)
    - built to work with lots of different stores simultaneously.
    - Effector uses immutable state, explicitly combines stores' state and only allows changing it through events.
  - [The best part of Effector - DEV Community](https://dev.to/effector/the-best-part-of-effector-4c27)
  - [jotai New APIs: isAtom, watch/unwatch, atom((get) ](https://github.com/pmndrs/jotai/issues/1217)
    - jotai atoms are just configs and they don't hold values. So, you can't directly read/write atoms. 
    - It's very different from module state libs such as zustand and effector.
    - There has been a huge demand on it, so we implemented an experimental feature (merged).

- tanstack-store /164Star/MIT/202401/ts
  - https://github.com/TanStack/store
  - https://tanstack.com/store
  - a framework agnostic data store that ships with framework specific adapters for major frameworks like React, Solid, Vue and Svelte.
  - primarily used for state management internally for most framework agnostic TanStack libraries. 
  - It can also be used as a standalone library for any framework or application.

- storeon /1.5kStar/MIT/202009/js
  - https://github.com/storeon/storeon
  - A tiny event-based Redux-like state manager for React, Vue, Angular, and Svelte.
  - [Using async data fetching does not return the latest state after calling state.get()](https://github.com/storeon/storeon/issues/152)
    - We recommend moving to nanostores

- reatom /504Star/MIT/202006/ts
  - https://github.com/artalar/reatom
  - Reatom is a blend of the one-way data flow (by flux and global store) and decentralized atoms for deterministic and flexible description of state and its changes
  - Inspired by redux, kefir, effector
  - framework-agnostic: independent and self-sufficient
  - debugging: immutable data, devtools (redux ecosystem support by adapter)
  - synchronous glitch free: resolve diamond problem
  - Why is API so strange, can't it be simpler? to support type check
  - Reatom is built on top of SSoT(single source of truth) idea and attempts to strictly follow it to ensure reliability. 
  - Therefore it prefers immutable global state and other limitations
    - impossible to create cyclic dependencies
- Kel /12Star/MIT/202005/js
  - https://github.com/vijitail/Kel
  - A dead simple, event driven state management library for Vanilla JS apps.
- picostate /10Star/MIT/202001/ts
  - https://github.com/estrattonbailey/picostate
  - Event-based immutable state management. 源码非常简单
  - integrates seamlessly with React
- substate /11Star/MIT/202009/ts
  - https://github.com/tamb/substate
  - pub/sub state management with optional deep cloning
  - To manage state with a simple pub/sub pattern and unidirectional data flow
  - [SubState: I abandoned Redux for a Flux/Pub-Sub hybrid](https://medium.com/@t.saporito/substate-why-i-abandoned-redux-26d01419d74b)

- xstate /MIT/12.2kStar/202007/状态机
  - https://github.com/davidkpiano/xstate
  - https://xstate.js.org/docs/
  - JS and TS finite state machines and statecharts for the modern web.
  - It uses event-driven programming, state machines, statecharts, and the actor model to handle complex logic in predictable, robust, and visual ways.
- state-designer /472Star/MIT/202107/ts
  - https://github.com/steveruizok/state-designer
  - https://state-designer.com/
  - 主要用于自研的tldraw、perfect-freehand、globs.design
  - library for managing the state of a user interface. 
  - It prioritizes the design experience, making it easy to experiment with ideas, iterate on solutions, and communicate the final result.
  - State Designer is heavily inspired by xstate. 
    - Note that, unlike xstate, State Designer does not adhere to the scxml spec.
  - Write state-charts in a simple declarative syntax.
    - Create both global and local component states.
  - Put simply, a statechart is a beefed up state machine.  
    - The beefing up solves a lot of the problems that state machines have, especially state explosion that happens as state machines grow.

- akita /Apache2/2.3kStar/202007/ts
  - https://github.com/datorama/akita
  - https://datorama.github.io/akita/
  - Akita is a state management pattern, built on top of RxJS, 
    - which takes the idea of multiple data stores from Flux and the immutable updates from Redux, 
    - along with the concept of streaming data, to create the Observable Data Stores model.
- cerebral /MIT/1.9kStar/202005/js
  - https://github.com/cerebral/cerebral
  - https://cerebraljs.com/
  - Declarative state and side effects management for popular JavaScript frameworks
  - To handle everything(updating state) from a simple toggle to very complex operations, Cerebral has the concept of sequences. 
    - Sequences allows you to compose functions together into a flow. 
    - sequences are based on function-tree, a project that came out of the initial experimentations in the first version of Cerebral.

- store /187Star/MIT/202010
  - https://github.com/fabiospampinato/store
  - simple framework-agnostic modern state management library.
  - Thanks to usage of `Proxy` s you just have to wrap your state with store, 
  - mutate it and retrieve values from it just like if it was a regular object, 
  - and listen to changes via onChange or useStore.
- event-reduce /3Star/MIT/202010/ts/NoDeps
  - https://github.com/soxtoby/event-reduce
  - A small, opinionated, state management library based on reducing observable events into state
  - 吸收了redux和mobx的优点
  - event-reduce also has support for time-travelling debugging with the Redux DevTools.
  - What if my application is more complicated than a single counter?
    - I'd recommend putting your events in their own class
  - Chances are, your application is going to be even more complicated than even a list of counters grin. 
    - You're going to need more model classes, and you're going to want to scope events to particular child models. 
- pulse /225Star/MIT/202010/ts
  - https://github.com/pulse-framework/pulse
  - Global state and logic for reactive JavaScript applications. 
  - Supports frameworks like React, Vue, and React Native.
  - Replaces Redux, Vuex, and MobX for state; and for API requests, replaces Axios and fetch.
- suber /22Star/MIT/201703/js/NoDeps
  - https://github.com/oskarhane/suber
  - An eventbus/pubsub compatible with Redux middlewares
  - Works with popular side effects handling middlewares like redux-saga and redux-observable
- https://github.com/ForsakenHarmony/parket
  - A library to manage application state, heavily inspired by mobx-state-tree
  - This library uses Proxies and Symbols

- https://github.com/oslabs-beta/ZusTime
  - With ZusTime you can inspect your Zustand store and application by stepping both forward and backwards in your code, allowing you to visualize snapshots of state at various points in time. 
  - This type of debugging tool limits the need for countless console logs and prevents you from having to run your application over and over again

- https://github.com/facebookarchive/flux /js/archived
  - https://facebookarchive.github.io/flux/
  - Application Architecture for Building User Interfaces
  - An application architecture for React utilizing a unidirectional data flow.
  - Flux is more of a pattern than a framework, and does not have any hard dependencies. However, we often use EventEmitter as a basis for Stores and React for our Views.
  - The Flux project has been archived and no further changes will be made. We recommend using more sophisticated alternatives like Redux, MobX, Recoil, Zustand, or Jotai.
# event pub/sub
- EventEmitter /3kStar/Unlicense/202001/js/NoDeps
  - https://github.com/Olical/EventEmitter
  - brings the power of events from platforms such as node.js to your browser
  - 对应npm包 https://www.npmjs.com/package/wolfy87-eventemitter

- https://github.com/felladrin/create-pubsub /ts
  - A tiny Event Emitter and Observable Store for JavaScript apps.
  - a Vanilla JavaScript library, so it's framework-agnostic.

- PubSubJS /3.3kStar/MIT/202008/js
  - https://github.com/mroderick/PubSubJS
  - Dependency free topic-based publish/subscribe library written in JavaScript
  - PubSubJS has synchronisation decoupling, so topics are published asynchronously.
  - PubSubJS is designed to be used within a single process, and is not a good candidate for multi-process applications (like Node.js – Cluster with many sub-processes).
  - Use "constants" for topics and not string literals. PubSubJS uses strings as topics
- https://github.com/choojs/nanobus
  - We had the requirement for a * event to catch all calls, and figured we could improve the file size at the same time. 
  - This library is about 1/3rd the size of Node's version.
  - Are these emitters asynchronous? No.
- https://github.com/faye/faye /4.4kStar/apache2/202008/js/inactive
  - Faye is a publish-subscribe messaging system based on the Bayeux protocol. 
    - Bayeux协议目的是使用ajax实现客户端和服务器的双向通信
  - It provides message servers for Node.js and Ruby, and clients for use on the server and in all major web browsers.

- https://github.com/ganapativs/pure-cache
  - tiny in-memory JavaScript cache with near realtime cache expiry feature
- https://github.com/bpmn-io/scroll-tabs
  - ScrollTabs adds scroll buttons on the left and right side of the tabs container if not all tabs are visible. 
  - It also adds a mouse wheel listener on the container.
- https://github.com/garronej/evt
  - EventEmitter's typesafe replacement
  - Why would someone pick EVT over RxJS:
    - RxJS introduces a lot of abstractions. It's a big jump from EventEmitter.
    - RxJS tends to be quite verbose.
    - With RxJS It is often needed to resort to custom type guards, the filter operator breaks the type inference.
    - It could be months before RxJS it eventually supports Deno.
    - No official guideline on how to integrate RxJS with React.
  - EVT is an attempt to address all these points while trying to remain as accessible as EventEmitter.
# comparison
- https://github.com/dai-shi/will-this-react-global-state-work-in-concurrent-rendering
  - Test tearing and branching in React concurrent rendering

- https://github.com/turtleflyer/compare-react-state-management-solutions
  - The objective of this project is to compare the performance of the use-interstate library with the popular state management libraries for React, namely Redux and Recoil.
  - use-interstate is an unopinionated state management solution for React that leans to be as simple as the standard hook useState

- https://github.com/Odonno/react-state-management-comparison
  - Comparison of different React state management libraries (hooks, mobx, recoiljs)
# state-orm
- https://github.com/redux-orm/redux-orm /202104/js/inactive
  - https://redux-orm.github.io/redux-orm/
  - simple and immutable ORM to manage relational data in your Redux store.
  - Redux-ORM deals with related data, structured similar to a relational database. The database in this case is a simple JavaScript object database.
  - For simple apps, writing reducers by hand is alright, but when the number of object types you have increases and you need to maintain relations between them, things get hairy. 
    - ImmutableJS goes a long way to reduce complexity in your reducers, but Redux-ORM is specialized for relational data.
  - [Call for Maintainer and Contributors](https://github.com/redux-orm/redux-orm/issues/123)
    - I've been moving away from redux to things like react-query and lost traction on redux-orm

- tinybase /1.4kStar/MIT/202212/ts/NoDeps
  - https://github.com/tinyplex/tinybase
  - https://tinybase.org/
  - TinyBase is a smart new way to structure your local app data
  - 基于自定义TinyQL(类似SQL)实现查询
  - 基于checkpoint实现undo
  - 基于hlc crdt实现冲突处理

- https://github.com/dmaevsky/tinyx /202211/js/NoDeps/inactive
  - A tiny state manager for big applications
  - Redux inspired
  - Middleware: logging, time travel, etc. out of the box
  - Expressive syntax for describing transactions, ImmerJS inspired, but using plain JS objects.
  - Automatic individual patches recording, again ImmerJS inspired, and without Proxy voodoo magic
  - Directly usable in SvelteJS applications: follows Svelte's store API
  - Plugin available for VueJS (so you can use it instead of, say, VueX)
  - You can put anything into your store: functions, promises, whatever you please, it is your store ! It is never augmented with proxies or tampered with in any way.

- orbit /2.3kStar/MIT/202209/ts/概念特别多
  - https://github.com/orbitjs/orbit
  - Orbit is a composable data framework for managing the complex needs of today's web applications.
  - Although Orbit is primarily used as a flexible client-side ORM, it can also be used server-side in Node.js.

- https://github.com/arnelenero/react-entities /js
  - provides simplified state management for React apps. 
  - Uses plain functions to implement state changes
  - Made specifically for React, and built on React Hooks
  - An entity is a single-concern data object whose state can be bound to any number of components in the app as a "shared" state. Once bound to a component, an entity's state acts like local state, i.e. it causes the component to update on every change.

- https://github.com/arnelenero/simpler-state /js
  - provides the simplest state management for React.
  - Use plain functions to update state (including async)
  - Highly extensible with plug-ins (e.g. persistence, dev tools)
  - Multiple times faster than context/reducer solution
  - This library is an evolution of the already production-proven react-entities that I also wrote. It shares the same stable core, but with a very different API.

- https://github.com/Yomguithereal/baobab /js/inactive
  - JavaScript & TypeScript persistent and optionally immutable data tree with cursors.
  - It is mainly inspired by functional zippers (such as Clojure's ones) and by Om's cursors.
  - It aims at providing a centralized model holding an application's state and can be paired with React easily through mixins, higher order components, wrapper components or decorators
  - you can create cursors to easily access nested data in your tree and listen to changes concerning the part of the tree you selected.
  - Note that the tree, being a persistent data structure, will shift the references of the objects it stores in order to enable immutable comparisons between one version of the state and another
  - Baobab lets you record the successive states of any cursor so you can seamlessly implement undo/redo features.
  - https://github.com/Yomguithereal/baobab-react
    - React integration for Baobab.

- https://github.com/malerba118/xorma /202501/ts
  - A synchronous, reactive, in-memory database powered by mobx.
  - https://x.com/austin_malerba/status/1883887696042488189
    - A reactive in-memory database for building complex frontend apps like video editors, design tools, and games.
    - I first conceived of it in 2022 while setting out to build diode and I’ve used it in basically every project since.
  - Why would one use xorma instead of SqlLite in the browser? Because of the reactivity?
    - They’re nothing alike tbh. It’s not a database like you’d traditionally think of a database. It’s a state management library that feels like an orm.
# signals
- https://github.com/preactjs/signals /ts/实现不依赖proxy
  - Signals is a performant state management library with two primary goals
    - Make it as easy as possible to write business logic for small up to complex app
    - Integrate into frameworks as if they were native built-in primitives
  - Signals can be accessed directly and your component will automatically re-render when the signal's value changes.
  - [Reactive/Store-like primitive](https://github.com/preactjs/signals/issues/4)
  - [Proposal: Multi-value Signal using bitmaps (bit arrays)](https://github.com/preactjs/signals/pull/217)
  - 🤔 [Reasoning for using prototype over classes](https://github.com/preactjs/signals/issues/216)
    - It performed better in benchmarks, and avoided cruft resulting from transpiled TypeScript classes
  - https://gitlab.com/kevindoughty/undo-manager /MIT/202404/js
    - Undo and redo management for Preact Signals
- https://github.com/luisherranz/deepsignal
  - Preact signals, but using regular JavaScript objects
  - DeepSignal works by wrapping the object with a `Proxy` that intercepts all property accesses and returns the signal value by default.
  - This allows you to easily create a deep object that can be observed for changes, while still being able to mutate the object normally.
  - Nested objects and arrays are also converted to deep signal objects/arrays, allowing you to create fully reactive data structures.
  - https://github.com/EthanStandel/deepsignal
    - wrap Preact's Signal model to make it a full state management solution
  - https://github.com/melnikov-s/preact-observables
    - enables the use of deep observable objects for `@preact/signals` supporting objects, arrays, Map, Set, WeakMap and WeakSet
- https://github.com/KusStar/signals-persist
  - A library for persisting state of a signal.
- https://github.com/Suv4o/signals-in-vanilla-js
  - [Signals in Vanilla JS](https://www.trpkovski.com/2023/04/25/signals-in-vanilla-js/)
- https://github.com/ic3Dragon/such-a-fancy-shopping-list
  - A shopping list app using typescript and preact signals

- https://github.com/stackblitz/alien-signals /MIT/202410/ts
  - The lightest signal library
  - The goal of alien-signals is to create a Signal library with the lowest overhead.
  - We have set the following scheduling logic constraints:
    - Based on Push-Pull
    - No dynamic objects
    - No use of Array/Set/Map
    - No recursion calls
    - Class properties must be fewer than 10 (https://v8.dev/blog/fast-properties)
  - The overall performance of alien-signals is approximately 400% that of Vue 3.4's reactivity system.
  - To achieve high-performance code generation in https://github.com/vuejs/language-tools, I needed to write some on-demand computed logic using Signals, but I couldn't find a low-cost Signal library that satisfied me.

- https://github.com/tldraw/signia /ts
  - Reactive signals that scale, by tldraw.
  - It uses a new clock-based lazy reactivity system that allows signals to scale with complex data-intensive applications.
  - Signia has a global logical clock. This is an integer that gets incremented every time any atom is updated.
  - signia-react实现基于proxy
    - With the native Proxy, all other calls such as access/setting to/of properties will be forwarded to the target Component
  - https://twitter.com/djsheldrick/status/1631572755777830912
    - Signia is like MobX and computed, but with the diffing thing mentioned above, and always-on caching for computeds. 
    - (MobX throws cached values away when there are no active observers). 
    - Signia doesn't use proxies to wrap data.

- https://github.com/WebReflection/usignal
  - A blend(混合，融合) of @preact/signals-core and solid-js basic reactivity API, with API and DX mostly identical to @preact/signals-core but extra goodness inspired by solid-js
  - this library has lazy, non side-effecting, computed values, something @preact/signals-core recently introduced and Solid 2.0 is planning to improve.

- https://github.com/jotaijs/jotai-signal
  - 支持jotai v1和v2

- https://github.com/starbeamjs/starbeam /MIT/202310/ts
  - Starbeam is a new kind of reactive library. 
  - It interoperates natively with React state management patterns, Svelte stores, the Vue composition API, and Ember's auto-tracking system.
  - Use normal JavaScript APIs and access patterns.

- https://github.com/maverick-js/signals /ts
  - a tiny (~1kB minzipped) library for creating reactive observables via functions called signals. 
  - You can use signals to store state, create computed properties (y = mx + b), and subscribe to updates as its value changes

- https://github.com/oslabs-beta/solid-dev-tool
  - A SolidJS signal tracking dependency & structural visualizer developer tool

- more-signal
  - https://github.com/dai-shi/valtio-signal
  - https://github.com/react-gx/gx
# multi-stores/atoms
- https://github.com/Omnistac/zedux /413Star/MIT/202502/ts
  - A Molecular State Engine for React.
  - Zedux is a multi-paradigm state management tool that features a powerful composable store model wrapped in a DI-driven atomic architecture.
  - Zedux borrows ideas from Redux, Recoil, and React Query. 
  - Zedux takes the unique approach of separating the state layer (stores) from the architecture layer (atoms). This allows for a powerful Dependency Injection model, conceptually similar to Angular's but simpler and more dynamic.

- https://github.com/acacode/reffect /202006/ts/archived
  - a declarative and reactive multi-store state manager for JavaScript/TypeScript applications inspired by Reatom and Effector
# state-machine
- https://github.com/beekai-oss/little-state-machine /1.4kStar/202212/ts
  - React custom hook for persist state management
  - Tiny with 0 dependency and simple
  - Persist state by default (sessionStorage or localStorage)
  - 依赖react
  - 似乎采用flux架构

- https://github.com/jakesgordon/javascript-state-machine
  - /7.4kStar/MIT/201807/js
  - A library for finite state machines. xstate也是
  - [web前端为什么很少用有限状态机设计框架？](https://www.zhihu.com/question/278938893)
    - 我觉得区别还是前端树状结构比较明显，所以整个问题可以用决策树（路由）或组件树（vDOM tree）+很简单的局部状态来建模，所以不会有游戏里那种 很大的有限状态机，局部状态用几个变量来存就行了
- https://github.com/davestewart/javascript-state-machine
  - An expressive, feature-rich, event-driven JavaScript finite-state machine
- https://github.com/ifandelse/machina.js
  - js ex machina - finite state machines in JavaScript
- https://github.com/matthewp/robot
  - A functional, immutable Finite State Machine library

- https://github.com/Jblew/xstatedb
  - State database using xstate
- https://github.com/steelbreeze/state
  - Hierarchical/Executable finite state machine for TypeScript and JavaScript
  - v8 does not yet contain any support for serialization due to the challanges brought by the introduction of deferred events

- https://github.com/thefrontside/microstates
  - Microstates makes working with pure functions over immutable data feel like working with the classic, mutable models we all know
  - A Microstate is just an object that is created from a value and a type. 
  - The value is just data, and the type is what defines how you can transition that data from one form into the next. 
  - Unlike normal JavaScript objects, microstates are 100% immutable and cannot be changed. 
- https://github.com/ralusek/statorade
  - JavaScript event-driven state machine.
- https://github.com/alexmdodge/ts-state-machine
  - A package with a simple state machine for the purpose of learning
# react
- https://github.com/developit/unistore /2.9kStar/MIT/202006/js/inactive
  - A tiny 350b centralized state container with component bindings for Preact & React.
  - names and ideas from Redux-like libraries
  - https://github.com/developit/stockroom
    - Offload your store management to a worker.
    - Stockroom seamlessly runs a Unistore store (and its actions) in a Web Worker, setting up optimized bidirectional sync so you can also use & subscribe to it on the main thread.
    - same API as unistore - a simple add-on
    - centralized actions with the option of running on the main thread

- react-redux-useMutableSource(api已升级为useSyncExternalStore)
  - https://codesandbox.io/s/react-redux-usemutablesource-eyxoe
- mut /7Star/MIT/202008/ts
  - https://github.com/snakeUni/mut
  - state management library based on Immer and useMutableSource
  - if useMutableSource is available then use useMutableSource otherwise use useSubscribe

- constate /3.7kStar/MIT/202204/ts
  - https://github.com/diegohaz/constate
  - https://codesandbox.io/s/github/diegohaz/constate/tree/master/examples/counter
  - 根据selector自动拆分成多个context，需要比较 创建多个context的消耗 和 使用useMemo的消耗
  - 使用selector自动创建的context是嵌套的，注意嵌套地狱
  - Write local state using React Hooks and lift it up to React Context only when needed with minimum effort.
  - 优点：相比于unstated-next，不需要自己创建Provider
  - 缺点：需要自己实现状态隔离
  - [constate 原理解析](https://zhuanlan.zhihu.com/p/86630237)
  - https://github.com/gouflv/constate-crud-example
    - [基于 constate 的状态管理 - 实践](https://github.com/gouflv/blog/issues/2)
    - [基于 constate 的状态管理](https://github.com/gouflv/blog/issues/5)

- unstated-next /3.5kStar/MIT/202005/ts
  - https://github.com/jamiebuilds/unstated-next
  - 封装很少，无selector
  - 200 bytes to never think about React state management libraries ever again

- react-hooks-global-state /MIT/473Star/202007
  - https://github.com/dai-shi/react-hooks-global-state
  - Simple global state for React with Hooks API
  - [Steps to Develop Global State for React With Hooks Without Context](https://blog.axlight.com/posts/steps-to-develop-global-state-for-react/)
  - [v2] new implementIation with useMutableSource
- recoil /MIT/7.9kStar/202007/js
  - https://github.com/facebookexperimental/Recoil
  - https://recoiljs.org/
  - Recoil is an experimental set of utilities for state management with React
  - Promote an Actor model event-based architecture
- zustand /4.9kStar/MIT/202010/ts/redux-like
  - https://github.com/pmndrs/zustand
  - a comfy api based on react hooks, isn't boilerplatey or opinionated, 
  - but still just enough to be explicit and flux-like.
  - https://github.com/charkour/zundo
    - undo/redo middleware for zustand
- jotai /1.8kStar/MIT/202010/ts/like-atoms
  - https://github.com/pmndrs/jotai
  - state resides with React, getting full benefits from suspense and concurrent mode
  - How does Jotai differ from Recoil?
    - No string keys. TypeScript oriented. Minimalistic API
- react-tracked /MIT/645Star/202006
  - https://github.com/dai-shi/react-tracked
  - https://react-tracked.js.org/docs/comparison
  - Simple and fast global state with React Context. Eliminate unnecessary re-renders without hassle.
  - Technically, it uses Proxy underneath, and it tracks state usage in render so that if only used part of the state is changed, it will re-render.
  - React context by nature triggers propagation of component re-rendering if a value is changed.
    - To avoid this, this libraries use undocumented feature of `calculateChangedBits` . 
    - It then uses a subscription model to force update when a component needs to re-render.
  - [v2] new implementation with useMutableSource
    - https://github.com/dai-shi/react-tracked/pull/43
- react-sweet-state /MIT/387Star/202007
  - https://github.com/atlassian/react-sweet-state
  - https://atlassian.github.io/react-sweet-state/
  - Taking the good parts of Redux and React Context to build a flexible, scalable and easy to use state management solution.
  - This library merges ideas from redux, react-redux, redux-thunk, react-copy-write, unstated, bey, react-apollo just to name a few. 
  - Moreover it has been the result of months of discussions with devs at Atlassian
- react-easy-state /MIT/2.1kStar/202004
  - https://github.com/RisingStack/react-easy-state
  - Simple React state management with ES6 Proxies
- https://github.com/eserozvataf/react-eventmanager
  - /16Star/Apache2/201908/ts/deprecated
  - Event-based simple React state management with decorators

- https://github.com/aweary/react-copy-write /js/inactive
  - An immutable React state management library with a simple mutable API, memoized selectors, and structural sharing. 
  - Powered by Immer.

- https://github.com/lostpebble/pullstate /ts
  - https://lostpebble.github.io/pullstate
  - Simple state stores using immer and React hooks
  - Uses immer for state updates - easily and safely mutate your state directly
  - Originally inspired by the now seemingly abandoned library - bey. Although substantially different now- with Server-side rendering and Async Actions built in

- https://github.com/vigetlabs/microcosm /MIT/201909/js/inactive
  - a state management tool for React
  - Other Flux implementations treat actions as static events; the result of calling a dispatch method or resolving some sort of data structure like a Promise.
  - Microcosm actions are first-class citizens.

- https://github.com/nanxiaobei/flooks /202310/ts
  - State Manager for React Hooks, Auto Optimized
  - flooks realizes a gorgeous auto optimization, only actually used data will be injected into the component, re-render completely on demand
  - zustand, need a selector; flooks, no selector needed
- https://github.com/jaredpalmer/mutik
  - A tiny (495B) immutable state management library based on Immer
  - Mutik uses the recently-merged useMutableSource hook internally.
- https://github.com/keajs/kea
  - Production Ready State Management for React
- pure-store /132Star/MIT/202006/ts
  - https://github.com/gunn/pure-store
  - a simple immutable store that lets you update state directly (i.e. imperatively)
  - 更新状态无需actions，但可自己实现
- https://github.com/immerjs/use-immer
  - /1.6kStar/MIT/202007/ts
  - Use immer to drive state with a React hooks
- https://github.com/pedronauck/reworm
  - Forget about actions, connections, reducers and a lot of boilerplate to create and manage states. 
- https://github.com/bcherny/undux
  - Dead simple state for React. Now with Hooks support.
  - 依赖rxjs
- https://github.com/dobjs/dob
  - state management tool using proxy.
- https://github.com/developit/linkstate
  - Bind events to state. Works with Preact and React.
- https://github.com/fabien-h/acta
  - simple state manager and event dispatcher for react.
- https://github.com/yamalight/outstated
  - Simple hooks-based state management for React
  - Like unstated but with hooks
- https://github.com/jamesknelson/govern
  - Component-based state management for JavaScript.
# redux-like
- https://github.com/davezuko/re-frame /13Star/MIT/201912/js/inactive
  - Vanilla JavaScript port of the popular ClojureScript library for pragmatic, flux-like state management
  - Re-frame helps make state management predictable, testable, and pragmatic. It achieves this via message passing, which decouples action from intent. 
  - On top of this, it provides first-class semantics for dealing with side-effects
  - From a high-level, re-frame is flux-like with events and event handlers, which are similar to redux's actions and reducers. 
  - Compared to redux, re-frame is more feature complete out of the box, with built-in interceptors, effects, subscriptions, and test utilities. 

- https://github.com/redux-zero/redux-zero /1.9kStar/MIT/202008/ts/inactive
  - lightweight state container based on Redux
  - 不依赖redux
  - [Introducing Redux Zero. Redux Zero is a lightweight state… | by Matheus Lima | Medium_201710](https://medium.com/@matheusml/introducing-redux-zero-bea42214c7ee)

- easy-peasy /MIT/3.6kStar/202006
  - https://github.com/ctrlplusb/easy-peasy
  - https://easy-peasy.now.sh/
  - 依赖redux、redux-thunk、immer
  - Vegetarian friendly state for React
- https://github.com/nanxiaobei/retalk
  - The Simplest Redux. 依赖redux、react-redux
# reactive
- https://github.com/axiijs/axii /MIT/202503/ts
  - https://axii.dev/
  - An Incremental Reactive Frontend Framework
  - a brand-new frontend framework that relies on an "incremental update" reactive data structure to truly build a high-performance data logic layer.
  - Uses React-style JSX, but functions execute only once, creating real DOM elements instead of Virtual DOM.
  - Binds updates to elements by recognizing reactive data structures. No special syntax, no framework-specific hooks, no compiler magic.
  - Rich reactive structures like RxList / RxMap / RxSet / RxTime suitable for various scenarios.
  - https://github.com/axiijs/boilerplate
  - https://github.com/axiijs/statemachine
    - data0 based statemachine
  - https://github.com/axiijs/action0
    - data0 based action management library.
# observable
- https://github.com/xolvio/pojo-observer
  - A minimalist object observer with React hooks support. 
  - Allows you to separate concerns between presentation and interaction logic
  - This library is a minimal observer pattern implementation that takes in a POJO as a subject, instruments it, and performs callbacks when the subject has changed. 
  - It's not opinionated at all and allows you to use it however you see fit, like choosing the event library to add (or not).
# url-params-as-state
- https://github.com/47ng/nuqs /MIT/202412/ts
  - https://nuqs.47ng.com/
  - Type-safe search params state manager for React frameworks - Like useState, but stored in the URL query string.
  - Simple: the URL is the source of truth
  - Supports Next.js (app and pages routers), plain React (SPA), Remix, React Router, and custom routers via adapters
  - useSearchParams 得过一次服务器，nuqs 会立即更新
  - tanstack router 自带这个功能
  - 之前准备用ahooks的use-state-url但是只支持react-router
# games
- https://github.com/fritzy/ape-ecs /js
  - performant, featureful, and flexible Entity-Component-System library for JavaScript, intended for use in games and simulations.
  - Persisted Queries (indexes) are updated as Entity composition changes.
  - Not all systems need to run every frame.
  - The Entity-Component-System paradigm is great for managing dynamic objects in games and simulations.

- https://github.com/pmndrs/racing-game /ts/r3f
  - https://racing.pmnd.rs/
  - This project is a showcase for the feasibility of React in gaming. 
  - Every thing is a self contained component using react-three-fiber to express threejs with React semantics. 
  - [before this gets too complex, let's discuss some directions](https://github.com/pmndrs/racing-game/issues/117)
    - Following ECS means the project won't be as easy as it is today to understand, copy/paste, and so on. 
  - https://github.com/coldi/r3f-game-demo
    - A demo on how to do a simple tile-based game with React and react-three-fiber
# more-state
- https://github.com/GantMan/ReactStateMuseum /js
  - A whirlwind tour of React state management systems by example
  - Examples to help portray the how, why, which, pros, and cons of various state management systems in the React ecosystem.

- https://github.com/josephg/statecraft /ISC/201911/ts/inactive
  - Statecraft is a protocol and set of tools for interacting with data that changes over time. 
  - It is the spiritual successor to Sharedb.
  - The store guarantees that the data is immutable with respect to time. (So if the data changes, the version number goes up).
    - Stores can choose how much historical data to store and return.
  - Stores provide a standard set of methods to interact with the data: fetch/mutate/subscribe
  - A Statecraft store is more than just a database abstraction
    - Unlike traditional transactional databases, Statecraft stores compose together like LEGO. Stores wrap one another
  - The philosophy of Statecraft is to "ship the architecture diagram". 
    - The API is designed to make it easy to re-expose a statecraft store over the network. 

- https://github.com/regionjs/region-core
  - region-core is a progressive View Model Management Framework. 
  - You can use it while using react state, redux, and benefit from it.
- Valoo: just the bare necessities of state management.
  - https://gist.github.com/developit/a0430c500f5559b715c2dddf9c40948d
- bloc /MIT/4.9kStar/202007/dart
  - https://github.com/felangel/bloc
  - https://bloclibrary.dev/
  - A predictable state management library that helps implement the BLoC design pattern
  - for flutter and dart
- https://github.com/vuejs/vuex
- https://github.com/Tencent/westore
  - 微信小程序解决方案 - 1KB js 覆盖状态管理、跨页通讯、插件开发和云数据库开发

- concent/helux /MIT/626Star/202007
  - https://github.com/heluxjs/helux
  - https://github.com/concentjs/concent
  - https://concentjs.github.io/concent-doc/
  - 内置依赖收集，可预测、零入侵、渐进式、高性能的react开发框架
  - [redux、mobx、concent特性大比拼, 看后生如何对局前辈 - 掘金](https://juejin.cn/post/6844904116284555271)
- https://github.com/EOSIO/demux-js
  - Deterministic event-sourced state and side effect handling for blockchain applications
  - Taking inspiration from the Flux Architecture pattern and Redux
- https://github.com/yottaawesome/brainlet
  - A simple state and event engine for JS web apps.
- https://github.com/troch/reinspect
  - Use redux devtools to inspect useState and useReducer 
  - API: StateInspector, useState(initialState, id?), useReducer(reducer, initialState, initializer?, id?)
