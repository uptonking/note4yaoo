---
title: toc-lib-state-management
tags: [lib, state, toc]
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-14T11:03:53.196Z'
---

# toc-lib-state-management

## agnostic

- redux /MIT/53.7kStar/202005/
  - https://github.com/reduxjs/redux
  - https://redux.js.org/
  - Predictable state container for JavaScript apps
- mobx /MIT/22.1kStar/202007
  - https://github.com/mobxjs/mobx
  - https://mobx.js.org/README.html
  - Simple, scalable state management
- xstate /MIT/12.2kStar/202007
  - https://github.com/davidkpiano/xstate
  - https://xstate.js.org/docs/
  - JS and TypeScript finite state machines and statecharts for the modern web.
- store /187Star/MIT/202010
  - https://github.com/fabiospampinato/store
  - simple framework-agnostic modern state management library.
  - Thanks to usage of `Proxy` s you just have to wrap your state with store, 
  - mutate it and retrieve values from it just like if it was a regular object, 
  - and listen to changes via onChange or useStore.
- cerebral /MIT/1.9kStar/202005
  - https://github.com/cerebral/cerebral
  - https://cerebraljs.com/
  - Declarative state and side effects management for popular JavaScript frameworks
- storeon /1.5kStar/MIT/202009
  - https://github.com/storeon/storeon
  - https://evilmartians.com/chronicles/storeon-redux-in-173-bytes
  - A tiny event-based Redux-like state manager for React, Preact, Angular, Vue and Svelte.
- https://github.com/vijitail/Kel
  - A dead simple, event driven state management library for Vanilla JS apps.
- https://github.com/estrattonbailey/picostate
  - Event-based immutable state management. 
  - integrates seamlessly with React

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
- easy-peasy /MIT/3.6kStar/202006
  - https://github.com/ctrlplusb/easy-peasy
  - https://easy-peasy.now.sh/
  - 依赖redux、redux-thunk、immer
  - Vegetarian friendly state for React
- unstated-next /MIT/2.6kStar/202005
  - https://github.com/jamiebuilds/unstated-next
  - 200 bytes to never think about React state management libraries ever again
- constate /MIT/2.6kStar/202002
  - https://github.com/diegohaz/constate
  - Write local state using React Hooks and lift it up to React Context only when needed with minimum effort.
- akita /Apache2/2.3kStar/202007
  - https://github.com/datorama/akita
  - https://datorama.github.io/akita/
  - Akita is a state management pattern, built on top of RxJS, 
    - which takes the idea of multiple data stores from Flux and the immutable updates from Redux, 
    - along with the concept of streaming data, to create the Observable Data Stores model.
- react-easy-state /MIT/2.1kStar/202004
  - https://github.com/RisingStack/react-easy-state
  - Simple React state management with ES6 Proxies
- concent /MIT/626Star/202007
  - https://github.com/concentjs/concent
  - https://concentjs.github.io/concent-doc/
  - 内置依赖收集，可预测、零入侵、渐进式、高性能的react开发框架
- https://github.com/eserozvataf/react-eventmanager
  - /16Star/Apache2/201908/ts/deprecated
  - Event-based simple React state management with decorators

## more-state

- bloc /MIT/4.9kStar/202007/dart
  - https://github.com/felangel/bloc
  - https://bloclibrary.dev/
  - A predictable state management library that helps implement the BLoC design pattern
  - for flutter and dart
- https://github.com/vuejs/vuex
- Valoo: just the bare necessities of state management.
  - https://gist.github.com/developit/a0430c500f5559b715c2dddf9c40948d
