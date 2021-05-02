---
title: note-react-alternatives
tags: [alternatives, react]
created: '2020-12-12T09:10:55.449Z'
modified: '2020-12-12T09:11:07.197Z'
---

# note-react-alternatives

# react-alternatives

## preact

- https://github.com/preactjs/preact
  - /27.8kStar/MIT/202011/js
  - Fast 3kB React alternative with the same modern API. Components & Virtual DOM.

- API
  - Not all the React features are present in Preact; 
  - it contains only a small part of the React Application Interface functionality. 
- Size
  - As I mentioned in the beginning, Preact is much lighter than React. 
  - React is 5.3 KB, whereas Preact is only 3 KB. 
- Performance
  - Because of being lightweight, Preact is faster as compared to React applications.

- Preact Pros
  - It is much compact, precise, and lightweight in size (3KB) so your application can perform faster.
  - Preact uses ES6 API, which enables you to uplift your application from React to Preact very easily. 
    - You can even adapt it as a library to create fantastic user-interfaces for your project. 
  - Entrepreneurs can create new projects easily by using the official CLI without the trouble of getting into Babel and Webpack configuration. 
  - You can get all the help from the official website examples and Preact documentation to kick-start your application development. 
  - Along with all the inspiring features of React, the Preact library also consists of some special features like the LinkedState.

- Preact Cons
  - You do not get the context support. 
  - For the stateful functionalities of your application, the createClass function is missing. 
    - Preact only allows you to use ES6 class and stateless components. 
  - Preact doesn’t care about the React propTypes. 
  - The community size is yet to reach the competition with React. 
  - Preact lacks innovation and mostly mimics React.

### [The Zen of Preact's source code_202105](https://puruvj.dev/blog/deep-dive-into-preact-source-code)

- Preact's source code is written in TypeScript, but the main files themselves aren't. 
  - The main files with the functionality are written in plain JavaScript, 
  - but they use JSDoc to pull in Types from TypeScript Definition files (.d.ts).
- There's a whole article about Using TypeScript without TypeScript, 
  - but the TLDR; here would be: Avoid development time tooling. 
  - If its just plain JS, you don't need to run a file watcher to transpile files as you change them. Just run what you got.
  - This is a very interesting approach and I see more and more libraries take it up, especially non-UI libraries
  - For UI libraries, you already got a web server running, so adding in TypeScript in the tooling won't change much, go ahead and add TypeScript

- Preact's source code is very very well written and commented, as you'd expect from such a paramount framework.
  - One of the reasons Preact is so small is that it reuses it's own exported function in its other exported functions. A LOT
- Preact is quite a big library to cover in a blog post, so I'll just cover the interesting parts.

- Notable points: `h`, which is Preact's JSX factory, is actually named `createElement`. Just like `React.createElement`. 
  - But is exported as `h` because it allows you to write raw Preact(Without JSX), also because it was initially inspired from HyperScript 
- `ref`s in P/React are basically used to encapsulate values that shouldn't trigger re-renders and are not re-created on every re-render.
  - A `ref` is just an object with `current` property set to `null`.
- Consumer expects its children to be a function, and it's simply calling it with the context data. 
  - As for Provider, what it's doing mostly is modifying its parent component's lifecycle hooks to watch for context state changes.

- Hooks are located in a separate directory. 
  - Unlike React, everything is opt-in in Preact
- `useState` is basically calling `useReducer`.
  - `const useState = (initialState) => useReducer(invokeOrReturn, initialState); `.
- `useCallback` is just useMemo under the hood
  - `const useCallback = (callback, args) => useMemo(() => callback, args); `.

## Inferno

- https://github.com/infernojs/inferno
  - /14.6kStar/MIT/202011/ts
  - An extremely fast, React-like JavaScript library for building modern user interfaces

- React has a fully synthetic event system, whereas Inferno only supports partial synthetic events, including certain functions such as onClick. 
- You can not use React Native with Inferno as you can in React. Inferno surrounds the DOM structure for browser/server edits. 
- It lacks support for React legacy strings like ref, callback, or createRef, etc. 
- Using Inferno, you can get lifecycle events based on functional components instead of the ES2015 classes. 
- You can debug your Inferno apps using React dev tool extensions by using “inferno-devtools” command. 
- You can set up your styles in Inferno using the CSS property name method.

- Inferno JS Pros 
  - Inferno is a lightweight React alternative 
  - It is super-fast as it uses internal objects for optimizations. 
  - Instead of copying React, Inferno has some unique lifestyle methods. 
  - Inferno uses the classic old CSS properties. 
  - You get add-ons like routing, server-side rendering, and more
- Inferno JS Cons 
  - Inferno is not yet backed up by adequate community size. Because of the smaller ecosystem, you do not get timely help and support. 
  - Unlike React, Inferno does not support Hooks, Memo, suspense, or lazy to keep the library compact. However, you can keep considering these features while writing in Inferno. 
  - The setState works synchronously. 
  - To use any of the React components, you first need to write and use a React component.

# react-like-repos

- https://github.com/NervJS/nerv
  - /5.3kStar/MIT/202006/ts
  - Nerv is a virtual-dom based TypeScript library with identical React 16 API
    - higher performance, tinier package size and better browser compatibility.
    - Support React 16 features, Error Boundaries, Portals, custom DOM attributes, etc.
    - Battle tested, serve in JD.com home page and TOPLIFE.com
    - hooks 已经支持了
  - [What's the tradeoff?](https://github.com/NervJS/nerv/issues/10)
    - for Nerv, compatible with React is our main goal, by doing that, we can sacrifice performance and size.

- https://github.com/yisar/fre
  - /1.5kStar/MIT/202010/ts
  - Tiny React-like framework with Time slicing and Algebraic effects.
  - currently no support for the class-based Component API
  - preact准确来说是 react15-like，你可以用它代替react来用，但是不存在【通过preact源码看react源码】
    - preact的hooks实现，是借助数组实现的，而 react 是链表
    - diff算法，preact 是 vdom 树，react 是 fiber 链，遍历不同，比对思路不同，effects 和 cleanups 都是不一样的
    - concurrent 和 suspense这俩在 preact 里完全没有，他们通过 ric 和自己实现的 suspense，完全不是一个层面哈
  - fre在源码层面，是可以和react对等的，包括我上面说的几个方面（链表，算法，concurrent，suspense），更适合作为【从fre源码看react源码】的样本

- https://github.com/RubyLouvre/anu
  - /3.1kStar/MIT/202002/js
  - the React16-compat library with hooks
- https://github.com/djalbat/reaction
  - An alternative implementation of React.
  - 不支持hooks
- https://github.com/neact/neact
  - Neact is a fast alternative to React, support ie8
- https://github.com/Foveluy/Luy
  - a React-like framework
- https://github.com/ahonn/tiny-react
  - a tiny react-like library, just for fun, in 2017
- https://github.com/z81/kekjs
  - React like UI library

## react-api-like

- Crank
  - Crank uses the same JSX syntax and diffing algorithm popularized by React, allowing you to write HTML-like code directly in JavaScript.
- solid
  - a declarative JavaScript library for creating user interfaces without Virtual DOM

- https://github.com/tvler/experimental-react-like-framework
  - A new, experimental frontend for React inspired by SwiftUI.
    - Zero distinction between functions and components
    - No return statement
  - Bet: JSX is bad
    - JSX immediately requires a complex build environment. 
    - Differences between HTML is small but painful for beginners.
  - Bet: React.createElement is bad
    - Building a complex template with React.createElement ends up as a deeply-nested function call with no breakpoints at the very bottom of your component code. 
    - JSX is an attempt to make this format more presentable, 
    - but it doesn't solve the underlying issue that your template is inside of a function call, with no access to if-statements, for-loops, etc.
  - Bet: Code based off of execution-order is good
    - Facebook built hooks around execution-order and received major backlash by the engineering community, but resulted in few actual real-world problems.

- https://github.com/cancerberoSgx/jsx-alone
  - Render JSX without libraries like React with 0 overhead

- https://github.com/recksjs/recks
  - React-like RxJS-based framework
- https://github.com/jussi-kalliokoski/react-no-jsx
  - react-no-jsx is a pure JS DSL to be used instead of JSX
  - It allows you to define your virtual DOM trees using a square bracket based syntax

- https://github.com/alephjs/aleph.js
  - The React Framework in Deno.

# ref

- [Best React-like JSX UI libraries in 2020_202007](https://areknawo.com/best-react-like-jsx-ui-libraries-in-2020/)
- [6 Best Alternatives to ReactJS_202007](https://www.bacancytechnology.com/blog/best-react-js-alternatives)
