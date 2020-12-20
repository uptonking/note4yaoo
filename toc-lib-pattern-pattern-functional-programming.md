---
title: toc-lib-pattern-pattern-functional-programming
tags: [functional, pattern, toc]
created: '2020-11-02T19:13:11.667Z'
modified: '2020-12-20T15:47:26.038Z'
---

# toc-lib-pattern-pattern-functional-programming

## popular

- https://github.com/reactivex/rxjs
  - /23.3kStar/Apache2/202011/ts
  - https://rxjs.dev/
  - A reactive programming library for JavaScript
  - [callbag和rxjs有什么区别](https://www.zhihu.com/question/270126057/answer/352363505)
- https://github.com/staltz/callbag-basics
  - /1.5kStar/MIT/201711/js
  - allbag is just a spec, but callbag-basics is a real library you can use.
  - https://github.com/callbag/callbag
    - A standard for JS callbacks that enables lightweight observables and iterables
    - Callbag中的source是可以转换成RxJS的Observable的
- https://github.com/cyclejs/cyclejs
  - /9.8kStar/MIT/202009/ts
  - A functional and reactive JavaScript framework for predictable code
  - @cycle/state依赖rxjs
- https://github.com/staltz/xstream
  - /2.2kStar/MIT/202010/ts
  - An extremely intuitive, small, and fast functional reactive stream library for JavaScript
  - Only 26 core operators and factories
  - Tailored for Cycle.js, or applications with limited use of subscribe
- https://github.com/baconjs/bacon.js
  - Functional reactive programming library for TypeScript and JavaScript
- https://github.com/kefirjs/kefir
  - A Reactive Programming library for JavaScript
  - inspired by Bacon.js and RxJS with focus on high performance and low memory usage.

- https://github.com/ramda/ramda
  - /19.7kStar/MIT/202010/js
  - Practical functional Javascript
- https://github.com/getify/Functional-Light-JS
  - Pragmatic, balanced FP in JavaScript.
- https://github.com/gcanti/fp-ts
  - /5kStar/MIT/202010/ts
  - Functional programming in TypeScript
- https://github.com/fluture-js/Fluture
  - Fantasy Land compliant (monadic) alternative to Promises
  - Much like Promises, Futures represent the value arising from the success or failure of an asynchronous operation (I/O). 
  - Though unlike Promises, Futures are lazy and adhere to the monadic(单元的，单体的) interface.
- https://github.com/SodiumFRP/sodium-typescript
  - Typescript/Javascript implementation of Sodium FRP (Functional Reactive Programming) library
- https://github.com/cyclejs/cyclejs
  - A functional and reactive JavaScript framework for predictable code
- https://github.com/marblejs/marble
  - functional reactive Node.js framework for building server-side applications, based on TS and RxJS.
- https://github.com/hufeng/iflux
  - iflux = immer.js + react.js

- https://github.com/choojs/choo
  - /6.5kStar/MIT/202001/js
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

## hooks

- https://github.com/clebert/batis
  - A JS library for reactive programming using React-like Hooks
  - Even though Hooks are actually a constrained solution for modeling states in actually stateless functional components, they have proven to be very elegant in their design. 
  - In my opinion, they are particularly suitable for modeling finite-state automata.
  - I wanted to use this kind of reactive programming in other areas as well, such as programming web workers or even JS-controlled robots. 
    - Therefore I wrote Batis
- https://github.com/michael-klein/hookuspocus
  - allow you to add hooks to any function.
  - Internally, hookuspocus uses WeakMaps if possible to keep states between runs (and falls back to simple Maps).

## more-fp

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
