---
tags: [state]
title: toc-lib-state-management
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-05T04:39:00.406Z'
---

# toc-lib-state-management

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
  - JavaScript and TypeScript finite state machines and statecharts for the modern web.
- recoil /MIT/7.9kStar/202007
  - https://github.com/facebookexperimental/Recoil
  - https://recoiljs.org/
  - Recoil is an experimental set of utilities for state management with React
  - Promote an Actor model event-based architecture
- bloc /MIT/4.9kStar/202007
  - https://github.com/felangel/bloc
  - https://bloclibrary.dev/
  - A predictable state management library that helps implement the BLoC design pattern
  - for flutter and dart
- easy-peasy /MIT/3.6kStar/202006
  - https://github.com/ctrlplusb/easy-peasy
  - https://easy-peasy.now.sh/
  - Vegetarian friendly state for React
- unstated-next /MIT/2.6kStar/202005
  - https://github.com/jamiebuilds/unstated-next
  - 200 bytes to never think about React state management libraries ever again
- constate /MIT/2.6kStar/202002
  - https://github.com/diegohaz/constate
  - Write local state using React Hooks and lift it up to React Context only when needed with minimum effort.
- akita /Apache2.0/2.3kStar/202007
  - https://github.com/datorama/akita
  - https://datorama.github.io/akita/
  - Akita is a state management pattern, built on top of RxJS, which takes the idea of multiple data stores from Flux and the immutable updates from Redux, along with the concept of streaming data, to create the Observable Data Stores model.
- react-easy-state /MIT/2.1kStar/202004
  - https://github.com/RisingStack/react-easy-state
  - Simple React state management with ES6 Proxies
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
    - To avoid this, this libraries use undocumented feature of `calculateChangedBits` . It then uses a subscription model to force update when a component needs to re-render.
  - [v2] new implementation with useMutableSource
    - https://github.com/dai-shi/react-tracked/pull/43
- cerebral /MIT/1.9kStar/202005
  - https://github.com/cerebral/cerebral
  - https://cerebraljs.com/
  - Declarative state and side effects management for popular JavaScript frameworks
- misc
  - https://github.com/vuejs/vuex
