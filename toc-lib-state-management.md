---
title: toc-lib-state-management
tags: [lib, state, toc]
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-14T11:03:53.196Z'
---

# toc-lib-state-management

## agnostic

- redux /MIT/53.7kStar/202005/ts/单向数据流
  - https://github.com/reduxjs/redux
  - https://redux.js.org/
  - Predictable state container for JavaScript apps.
  - 源码简单，插件丰富，插件有时会导致状态管理变得复杂
- mobx /MIT/22.1kStar/202007/ts/响应式数据流
  - https://github.com/mobxjs/mobx
  - https://mobx.js.org/README.html
  - MobX is a battle tested library that makes state management simple and scalable by transparently applying functional reactive programming (TFRP).
  - Mobx implements TFRP in a glitch-free, synchronous, predictable and efficient manner.
  - mobx isn't pubsub. It doesn't do change detection
- xstate /MIT/12.2kStar/202007/状态机
  - https://github.com/davidkpiano/xstate
  - https://xstate.js.org/docs/
  - JS and TS finite state machines and statecharts for the modern web.
- storeon /1.5kStar/MIT/202009/js
  - https://github.com/storeon/storeon
  - A tiny event-based Redux-like state manager for React, Vue, Angular, and Svelte.
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
- effector /2.8kStar/MIT/202010/ts
  - https://github.com/effector/effector
  - Effector is an effective multi-store state manager for Javascript apps (React/Vue/Node.js)
- https://github.com/artalar/reatom
  - Reatom is a blend of the one-way data flow (by flux and global store) and decentralized atoms for deterministic and flexible description of state and its changes
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

## event pub/sub

- EventEmitter /3kStar/Unlicense/202001/js/NoDeps
  - https://github.com/Olical/EventEmitter
  - brings the power of events from platforms such as node.js to your browser
  - 对应npm包 https://www.npmjs.com/package/wolfy87-eventemitter
- PubSubJS /3.3kStar/MIT/202008/js
  - https://github.com/mroderick/PubSubJS
  - Dependency free topic-based publish/subscribe library written in JavaScript
  - PubSubJS has synchronisation decoupling, so topics are published asynchronously.
  - PubSubJS is designed to be used within a single process, and is not a good candidate for multi-process applications (like Node.js – Cluster with many sub-processes).
  - Use "constants" for topics and not string literals. PubSubJS uses strings as topics

## react

- recoil /MIT/7.9kStar/202007
  - https://github.com/facebookexperimental/Recoil
  - https://recoiljs.org/
  - Recoil is an experimental set of utilities for state management with React
  - Promote an Actor model event-based architecture
- zustand /4.9kStar/MIT/202010/ts
  - https://github.com/pmndrs/zustand
  - a comfy api based on react hooks, isn't boilerplatey or opinionated, 
  - but still just enough to be explicit and flux-like.
- jotai /1.8kStar/MIT/202010/ts
  - https://github.com/pmndrs/jotai
  - state resides with React, getting full benefits from suspense and concurrent mode
  - How does Jotai differ from Recoil?
    - No string keys. TypeScript oriented. Minimalistic API
- react-hooks-global-state /MIT/473Star/202007
  - https://github.com/dai-shi/react-hooks-global-state
  - https://blog.axlight.com/posts/steps-to-develop-global-state-for-react/
  - Simple global state for React with Hooks API
  - [v2] new implementation with useMutableSource
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
- unstated-next /MIT/2.6kStar/202005
  - https://github.com/jamiebuilds/unstated-next
  - 200 bytes to never think about React state management libraries ever again
- constate /MIT/2.6kStar/202002
  - https://github.com/diegohaz/constate
  - Write local state using React Hooks and lift it up to React Context only when needed with minimum effort.
- react-easy-state /MIT/2.1kStar/202004
  - https://github.com/RisingStack/react-easy-state
  - Simple React state management with ES6 Proxies
- https://github.com/eserozvataf/react-eventmanager
  - /16Star/Apache2/201908/ts/deprecated
  - Event-based simple React state management with decorators
- https://github.com/aweary/react-copy-write
  - An immutable React state management library with a simple mutable API, memoized selectors, and structural sharing. 
  - Powered by Immer.
- https://github.com/developit/unistore
  - state container with component actions for Preact & React
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

## redux-like

- easy-peasy /MIT/3.6kStar/202006
  - https://github.com/ctrlplusb/easy-peasy
  - https://easy-peasy.now.sh/
  - 依赖redux、redux-thunk、immer
  - Vegetarian friendly state for React
- https://github.com/nanxiaobei/retalk
  - The Simplest Redux. 依赖redux、react-redux
- https://github.com/redux-zero/redux-zero
  - /1.9kStar/MIT/202008/ts
  - lightweight state container based on Redux

## state-machine

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
- https://github.com/thefrontside/microstates
  - Microstates makes working with pure functions over immutable data feel like working with the classic, mutable models we all know
  - A Microstate is just an object that is created from a value and a type. 
  - The value is just data, and the type is what defines how you can transition that data from one form into the next. 
  - Unlike normal JavaScript objects, microstates are 100% immutable and cannot be changed. 
- https://github.com/ralusek/statorade
  - JavaScript event-driven state machine.
- https://github.com/alexmdodge/ts-state-machine
  - A package with a simple state machine for the purpose of learning

## more-state

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
- https://github.com/GantMan/ReactStateMuseum
  - A whirlwind tour of React state management systems by example
- concent /MIT/626Star/202007
  - https://github.com/concentjs/concent
  - https://concentjs.github.io/concent-doc/
  - 内置依赖收集，可预测、零入侵、渐进式、高性能的react开发框架
- https://github.com/EOSIO/demux-js
  - Deterministic event-sourced state and side effect handling for blockchain applications
  - Taking inspiration from the Flux Architecture pattern and Redux
- https://github.com/yottaawesome/brainlet
  - A simple state and event engine for JS web apps.
- https://github.com/troch/reinspect
  - Use redux devtools to inspect useState and useReducer 
  - API: StateInspector, useState(initialState, id?), useReducer(reducer, initialState, initializer?, id?)
