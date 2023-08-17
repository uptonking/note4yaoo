---
title: note-react-alternatives-rewrite-toc
tags: [alternatives, lib, react, rewrite, toc]
created: 2020-12-12T09:10:55.449Z
modified: 2021-09-20T20:12:38.499Z
---

# note-react-alternatives-rewrite-toc

# guide

- 难点
  - ❓ setState只触发子组件的渲染

- react alternative/like/mini/clone
  - js: preact, didact, fre.v1, luy, mini-react
  - ts: inferno, nerv
# react-rewrite
- https://github.com/leontrolski/leontrolski.github.io/blob/master/33-line-react-with-comments.js
  - [33 line React](https://leontrolski.github.io/33-line-react.html)

- https://github.com/pomber/didact
  - /3.8kStar/MIT/202010/js
  - [A DIY guide to build your own React](https://pomb.us/build-your-own-react/)
- https://github.com/davidbarone/didact
  - The original Didact source code has been slightly modified 
  - Inclusion of addition hooks
- https://github.com/manasb-uoe/didact
  - Typed version of didact
  - this repository refactors the code into separate files of TypeScript code and adds more features: useEffect, userMemo, useRef
# react-alternatives
- https://github.com/LuSuguru/fake-react /75Star/202007/ts
  - 基于React 16.8.6 的源码并使用 TypeScript 仿写的 React, 实现了90%的功能
  - 还提供了源码解析系列文档，有28个文档

- https://github.com/JokerLHF/mini-react-web
  - 基于react 17 使用 ts 实现了一个 mini-react
  - 抛弃了 ClassComponent，只支持 FunctionComponent

- https://github.com/BetaSu/just-react
  - https://react.iamkasong.com/
  - 卡颂 《React技术揭秘》 一本自顶向下的React源码分析书(不是又一个手撸react)
  - 本书的宗旨是打造一本严谨、易懂的React源码分析教程，分为理念篇、架构篇、实现篇
  - 本书在React版本更新后会及时补充，当前版本v17.0.0-alpha
- https://github.com/BetaSu/big-react /文章丰富但功能少，useState触发全量render
  - https://github.com/BetaSu/react-on-the-way
  - /364Star/202007/js
  - 基于V16.13.1，从0实现React
  - v1 Render-Commit整体架构体系, HostComponent的首屏渲染
  - v2 FunctionComponent类型组件的首屏渲染, hook架构体系
  - v3 useState hook对单一HostComponent的状态更新
  - v4 实现了React Diff算法，可以更新多个兄弟子节点了
  - v5 实现useEffect hook首屏及再次渲染的完整逻辑
  - v6 之前的版本中，我们都是同步执行render流程；为产生的update赋予一个优先级，高优先级的update会优先进入render流程。
  - https://github.com/BetaSu/simple-virtual-DOM

- million /5.4kStar/MIT/202211/ts
  - https://github.com/aidenybai/million
  - https://millionjs.org/
  - Million is a drop-in replacement for React with a lightweight (<1kb) Virtual DOM
  - By computing the user interface beforehand with a compiler, Million reduces the overhead of traditional Virtual DOM.
  - While alternative libraries like Preact reduce bundle sizes by efficient code design, Million takes it a step further by leveraging compilation to make a quantum leap in improving bundle size and render speed.
  - [How does Million.js ( @milliondotjs ) work?](https://twitter.com/aidenybai/status/1647005716350406656)
  - https://github.com/aidenybai/million-react
    - React Fiber is not supported by default, some features, particularly Suspense, are implemented only as passthrough components.
  - https://github.com/aidenybai/hundred /ts/NoDeps
    - Hundred is intended to be a toy block virtual DOM based off of Million.js, and is a proof-of-concept and a learning resource
    - This implementation is similarly based off of [blockdom](https://github.com/ged-odoo/blockdom).

## preact

- https://github.com/preactjs/preact
  - /27.8kStar/MIT/202108/js
  - Fast 3kB React alternative with the same modern API. Components & Virtual DOM.
- https://github.com/matrix-marketing/preact
  - [Preact Async Rendering: Solution to Initial Render Blocking - DEV Community](https://dev.to/cagdas_ucar/preact-async-rendering-51p2)

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

## inferno

- https://github.com/infernojs/inferno
  - /14.6kStar/MIT/202108/ts
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
# react-src-code
- https://github.com/AttackXiaoJinJin/reactExplain /js
  - React源码解析16.8.6，还发布了掘金系列文章  /js

- https://github.com/bubucuo/mini-react /ts
  - Mini React是我为了React课程而写的项目
  - https://github.com/bubucuo/DebugReact
    - 本项目用于调试源码，即修改配置使得项目中引用的 react 包来自 src/react

- react核心源码解析__全栈潇晨
  - [react源码解析19. 手写迷你版react](https://zhuanlan.zhihu.com/p/383433662)
    - 实现过于简单，没有提供单独的github仓库
  - [知乎专栏发布](https://www.zhihu.com/column/c_1345788302880878592)
  - [个人网站的视频课程 需注册](https://xiaochen1024.com/series/60b1b600712e370039088e24)

- https://github.com/baozouai/react-source-study
  - 本仓库在 react-source-code-debug的基础上保留了V17和Lanes模型，且删除掉了大量无关文件、代码（如其中的__DEV__相关判断)，只保留了核心的react、react-dom、react-reconciler、和scheduler
  - https://github.com/neroneroffy/react-source-code-debug
    - React 源码调试环境，源代码详细注释，跟随官方仓库进行更新

- https://github.com/Bogdan-Lyashenko/Under-the-hood-ReactJS
  - This repository contains an explanation of inner work of React. 
# react-like-repos
- https://github.com/NervJS/nerv
  - /5.3kStar/MIT/202006/ts/inactive
  - Nerv is a virtual-dom based TypeScript library with identical React 16 API
    - higher performance, tinier package size and better browser compatibility.
    - Support React 16 features, Error Boundaries, Portals, custom DOM attributes, etc.
    - Battle tested, serve in JD.com home page and TOPLIFE.com
    - hooks 已经支持了
  - [What's the tradeoff?](https://github.com/NervJS/nerv/issues/10)
    - for Nerv, compatible with React is our main goal, by doing that, we can sacrifice performance and size.
    - Is there any react's feature you don't and won't support definitely?
      - React Fiber and React Native. I afraid we will stick with stack reconciler instead of fiber. 

- https://github.com/Ajaxy/teact
  - super-performant web framework with zero dependencies implementing React paradigm.
  - originally developed as part of Telegram JavaScript contest and now powers the official Telegram Web client.

- https://github.com/yisar/fre
  - /1.5kStar/MIT/202004/js-v1/ts-v2
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

- https://github.com/MrWangJustToDo/MyReact  /js
  - 实现自己的react框架 了解fiber架构 函数组件 hook 异步更新 等react的基础功能
- https://github.com/MuYunyun/cpreact  /js
  - Build React from Scratch
  - [从0到1实现React](http://muyunyun.cn/blog/React/%E4%BB%8E0%E5%88%B01%E5%AE%9E%E7%8E%B0React/0.%E5%89%8D%E7%BD%AE%E5%87%86%E5%A4%87)

- ts实现

- https://github.com/zerrol/ts-react
  - 用typescript写的react
- https://github.com/SamChou19815/mini-react
  - Sam's Implementation of a simplified React for educational purpose
  - It should be simple enough so that I could teach it to an average developer in less than two hours.
  - 勉强能用，部分实现useState, useEffect
- https://github.com/vutran1710/WriteYourOwnReact
  - Fiber reconciliation - not perfect, but generally it works.
  - 勉强能用，未实现：hooks、class lifecycle methods
- https://github.com/huihao/fake
  - fake react
- https://github.com/djwxfdt/react-source-doc
  - 用typescript重写react源码，逐行写上阅读理解，支持直接调试。
  - 任务调度（scheduler）已完成
  - 协调（react-reconciler）进行中

- js实现

- https://github.com/alan-oliv/mini-react /js
  - a library built to basically study fiber algorithm and implementation
  - mini-react, mini-react-dom, mini-react-reconciler
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
- https://github.com/jackiewillen/build-your-own-react
  - 手把手带你用85行代码实现一个React.js
  - [Build Your Own React__201705](https://hackernoon.com/build-your-own-react-48edb8ed350d)
- https://github.com/djalbat/reaction  /js
  - 不支持hooks
  - The code base is tiny compared to React but React's core functionality is nonetheless implemented faithfully
  - https://github.com/djalbat/Inference
    - A dispatcher in a similar vein to Redux. To go hand in hand with Reaction. 

## react-api-like

- https://github.com/suchipi/concubine
  - concubine provides the framework necessary to create a "Hooks" system with full TypeScript typings, like the one React uses.

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

- https://github.com/hellopao/mpreact
  - react like framework for wechat mini program
# ref
- [Best React-like JSX UI libraries in 2020_202007](https://areknawo.com/best-react-like-jsx-ui-libraries-in-2020/)
- [6 Best Alternatives to ReactJS_202007](https://www.bacancytechnology.com/blog/best-react-js-alternatives)
