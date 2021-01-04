---
title: toc-lib-pattern-rxjs
tags: [pattern, rxjs, toc]
created: '2020-12-13T14:35:15.196Z'
modified: '2020-12-13T14:36:15.618Z'
---

# toc-lib-pattern-rxjs

# popular

- awesome-rxjs
  - 使用rxjs的代表：nestjs, angular, redux-observable, textbus
  - https://github.com/ichpuchtli/awesome-rxjs
  - https://github.com/RxJS-CN/rxjs-articles-translation
  - https://github.com/Widdershin/rxjs-ecosystem
  - https://github.com/oldratlee/reactive-practice-at-taobao

- https://github.com/redux-observable/redux-observable
  - redux-observable === redux + rxjs 是一个胶水库
  - 作用是将Redux中的朴素同步dispatch事件转化成RxJS事件流
  - RxJS middleware for action side effects in Redux using "Epics"
  - redux-observable (because of RxJS) truly shines the most for complex async/side effects. 
  - If you're not already comfortable with RxJS, you might consider using redux-thunk for simple side effects 
  - and then use redux-observable for the complex stuff. 
  - An Epic is a function which takes a stream of actions and returns a stream of actions. Actions in, actions out.
- https://github.com/LeetCode-OpenSource/rxjs-hooks
  - React hooks for RxJS
- https://github.com/re-rxjs/react-rxjs
  - offers React bindings for RxJS
- https://github.com/typeless-js/typeless
  - toolkit for building scalable React apps with Typescript.
  - TypeScript + React Hooks + RxJS
  - Event-driven architecture using RxJS.
- https://github.com/tbhuabi/textbus
  - 依赖prismjs、rxjs、reflect-metadata、@tanbo/di, @tanbo/css-themes, @tanbo/color
  - 基于数据驱动的富文本编辑器
- https://github.com/musicq/vist /2019
  - Virtual-list component build with react and rxjs
- https://github.com/cellbang/malagu
  - core依赖reflect-metadata、inversify、rxjs、jexl、traverse
  - 可以认为是一个nodejs版本的spring boot
- https://github.com/sigi-framework/sigi
  - Sigi is a high level Effect Manager with well designed API based on RxJS and Immer.
  - Sigi contains a tiny dependency injection implementation. 
    - Which allow you easier to compose your Modules and Services.
    - And it also provides benefit when you want to write some tests.
  - Sigi now support React/React Native and Vue@2.x, 
    - we will also provide support for Flutter soon
- https://github.com/marblejs/marble
  - functional reactive Node.js framework for building server-side applications, based on TypeScript and RxJS.
- https://github.com/pubkey/rxdb
  - A realtime Database for JavaScript Applications
  - a NoSQL-database for JavaScript Applications like Websites, hybrid Apps, Electron-Apps and NodeJs. 
  - Reactive means that you can not only query the current state, but subscribe to all state changes like the result of a query or even a single field of a document.
  - RxDB implements rxjs to make your data reactive. 
    - This makes it easy to always show the real-time database-state in the dom without manually re-submitting your queries.
- https://github.com/Nozbe/WatermelonDB
  - Reactive & asynchronous database for powerful React and React Native apps

- https://github.com/canalplus/rx-player
  - The RxPlayer is a library implementing a DASH and Microsoft Smooth Streaming video player directly on the browser, without plugins. 
  - It relies on HTML5 Media Source Extensions and Encrypted Media extensions and is written in TypeScript
  - The abstractions provided by rxjs and the inclusion of cancellation mechanisms (unlike say, ES6 Promises) were perfectly adapted to some of our IO-heavy code.
- https://github.com/ahomu/Talkie /201805
  - 依赖rxjs、markdown-it、lit-html
  - Simple slide presentation library. 
- https://github.com/microsoft/paris
  - Paris is a data management library for webapps, using TypeScript and RxJS to implement Domain-Driven Design.
  - 类似sql查询的场景，接口使用rxjs风格

- https://github.com/rxmqjs/rxmq.js
  - JavaScript pub/sub library based on RxJS
  - an in-memory message bus based on rxjs - inspired by postal.js
  - https://github.com/postaljs/postal.js
    - an in-memory message bus - very loosely inspired by AMQP
- https://github.com/hermanbanken/RxFiddle
  - Visualize your Observables
- https://github.com/janryWang/react-eva
  - Effects+View+Actions(React distributed state management solution with rxjs.)
  - Faster than one-way data stream, Because when we manage the state distribution, the entire React tree will not be fully redrawn due to a state change.
  - More elegant than react ref
- https://github.com/ui-model/ui-model
  - 依赖@angular/core和rxjs
  - ui-model is a set of the streamlined UI logics extracted from ui controls for frontend developers.
  - We will use RxJS to expose event interfaces, but we will limit ourselves from RxJS's advanced features.
- https://github.com/AveroLLC/types-first-ui
  - an opinionated framework for building long-lived, maintainable UI
  - Epics(backed by redux-observable) as mechanism for side effects/middleware (vs. thunks or sagas)

# rxjs-state

- https://github.com/TalkingData/rxloop /201910
  - 基于RxJS的可预测状态管理容器，redux + redux-observable架构(Inspired by dva)
  - redux自身的300行代码只处理简单的同步数据流，把脏活、累活比如异步数据流全扔给各种适配和插件处理了。
- https://github.com/reobservable/reobservable /201903
  - Redux + rxjs + redux-obersvable best practice. Inspired by dva, rematch.
- https://github.com/Dynalon/reactive-state /202010
  - Redux-clone build with strict typing and RxJS down to its core. 
  - A typed, wrist-friendly state container aimed as an alternative to Redux when using RxJS. 
- https://github.com/jas-chen/rx-redux /201508
  - A reimplementation of redux using RxJS.
- https://github.com/LeetCode-OpenSource/ayanami
  - A better way to react with state. Inspired by redux-epics-decorator
  - Use RxJS to create side effects and more

- https://github.com/datorama/akita
  - Akita is a state management pattern, built on top of RxJS, 
    - which takes the idea of multiple data stores from Flux and the immutable updates from Redux, 
    - along with the concept of streaming data, to create the Observable Data Stores model.
- https://github.com/bcherny/undux
  - Dead simple state for React. Now with Hooks support.
  - Familiar abstractions: just get and set
  - 依赖rxjs
- https://github.com/felangel/bloc.js
  - predictable state management library that helps implement the BLoC design pattern in JavaScript
  - The goal of this library is to make it easy to separate presentation from business logic, facilitating testability and reusability.
- https://github.com/thefrontside/microstates
  - makes working with pure functions over immutable data feel like working with the classic, mutable models
- https://github.com/lacolaco/reactive-store
  - Very simple store implementation for state management with RxJS.
- https://github.com/tanfonto/storx
  - Dead simple state management built with RxJS
- https://github.com/shayeLee/floway
  - 基于 RxJS v6 的前端应用状态管理解决方案

# examples

- https://github.com/baadal/starter-web
  - 依赖@motion/styled、express、react-router-dom、rxjs6
  - React Starter Kit for building API-driven Modern Web Apps.
  - Server-side rendering (SSR)
  - CSS Modules, CSS-in-JS
  - Server-driven UI
- https://github.com/oh-my-c0de/oh-my-fullstack
  - Full stack web application skeleton 
  - 依赖Next9, Redux4, RxJS6, redux-observable, Immutable4, Express, antd3
- https://github.com/fdecampredon/react-rxjs-todomvc /2017
  - TodoMVC implementation with React and RxJS

- https://github.com/atfzl/ReactUI
  - an interactive React component builder which modifies your original code for you

- https://github.com/nelsW70/rxjs-autocomplete
  - rxjs autocomplete search using github api, debounceTime, distinctUntilChanged, switchMap, map, filter (from Rachel Poulos presentation)
- https://github.com/Troy96/IMDbify-front /angular
  - A custom autocomplete created using RxJS operators to search for movies off IMDb.
- https://github.com/eliseumds/react-autocomplete /2014
  - Playing around with ReactJS and RxJS
- https://github.com/spadin/autocomplete
  - Learning how to do autocomplete using RxJS and redux-observable
- https://github.com/nem035/rxjs-autocomplete-example
  - demonstration of an autocomplete box for Wikipedia using RxJS.

# extensions

- https://github.com/cartant/rxjs-spy
  - A debugging library for RxJS
  - The engineers at Slack have adopted rxjs-spy
  - rxjs-spy introduces a tag operator that can be used to identify observables. It attaches a string tag to an observable
  - it performs no additional processing and does not alter the observable's behaviour or value in any way.
  - The API's methods are tag-based and tags can be matched using explicit literals, regular expressions or function predicates. 
  - rxjs-spy exposes a module API intended to be called from code and a console API - via the spy global 
- https://github.com/tomyitav/redis-messaging-manager
  - Pubsub messaging library, using redis and rxjs
- https://github.com/kosich/rxjs-autorun
  - Re-evaluate an expression whenever Observable in it emits

- https://github.com/staltz/toy-rx
  - A tiny implementation of RxJS that actually works, for learning.
  - I made this so people can look into the implementation of a simple RxJS and feel like they can actually understand it.
  - It's missing a ton of stuff that the official RxJS covers, such as:
    - Subscribe supports partial Observer objects
- https://github.com/WangYuLue/simple-rxjs
  - 200行代码理解rxjs的核心概念
- https://github.com/akanass/rx-http-request
  - The world-famous HTTP client Request now RxJS compliant, wrote in full Typescript|ES6 for client and server side.
- https://github.com/ReactiveX/IxJS
  - The Interactive Extensions for JavaScript (IxJS) brings the Array#extras combinators to iterables, generators, async iterables and async generators. 

- https://github.com/curran/model
  - Model.js manages the execution flow of the data flow graphs you define. 
  - Kind of like Backbone and React, but simpler and designed specifically for making D3 easier to use. 
- https://github.com/CONNECT-platform/connective
  - https://github.com/CONNECT-platform/connective-html
  - agent-based reactive programming library for typescript
  - CONNECTIVE is a thin layer on top of RxJS, so it provides all the toolset of rxjs by proxy. 
  - However, while RxJS's API is better suited for short-lived and small flows, CONNECTIVE adds tools better suiting long-living and large/complex flows.
- https://github.com/kitten/rxjs-diagrams /2017
  - React Components for visualising RxJS observables and operators
- https://github.com/cartant/rxjs-marbles
  - An RxJS marble testing library for any test framework
- https://github.com/kwonoj/rx-sandbox
  - Marble diagram DSL based test suite for RxJS 6
  - No dependencies to specific test framework
  - Near-zero configuration, works out of box
- https://github.com/insidewhy/rxjs-websockets
  - A very flexible and simple websocket library for rxjs
- https://github.com/kondi/rxjs-grpc
  - Typesafe gRPC with RxJS in TypeScript

# more-repos

- https://github.com/recksjs/recks
  - React-like RxJS-based framework
- https://github.com/grammarly/focal
  - Program user interfaces the FRP way.
  - Use lenses to decompose the application state into smaller parts
- https://github.com/fanduel-oss/refract
  - Handle your component effects and side-effects in a clear and declarative fashion by using asynchronous data streams (reactive programming).
- https://github.com/frintjs/frint
  - deprecated
  - Modular JavaScript framework for building scalable and reactive applications
