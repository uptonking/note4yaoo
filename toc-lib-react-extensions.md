---
title: toc-lib-react-extensions
tags: [extensions]
created: '2020-11-19T12:42:31.906Z'
modified: '2020-11-19T12:43:25.788Z'
---

# toc-lib-react-extensions

## experimental-react

- https://github.com/sokra/rawact
  - /2.6kStar/MIT/201812/js
  - [如何评价webpack作者开发的rawact babel插件？](https://www.zhihu.com/question/301791037/answers/updated)
  - A babel plugin which compiles React.js components into native DOM instructions to eliminate the need for the react library at runtime.
  - What if we could transpile React.js components to native DOM operations at build-time?
  - Svelte has proven that this type of framework-eliminating transpilation can work very well.
  - rawact主要的价值在于减少最终发布的代码量，然而生成的代码比同等价值的React.createElement要臃肿，也就是说应用越大，最终能省下的代码尺寸越少。
    - 一旦生成的代码量差异超过React本身runtime size，就完全没有意义了。
  - 比较有实际意义的用例是把React编译到不依赖React本身的 web components，或者是针对内存要求比较极端的低端设备。但总的来说不可能替代React。
  - React未来的核心竞争力在于Fiber/Concurrent带来的一系列新能力，比如Time slicing, Suspense等。用Svelte的思路去编译React是舍本取末
  - 这一类项目（rawact, Svelte, Angular Ivy）的根本意义在于探究view层runtime vs. AOT 的平衡点在哪里，
    - 是依赖一个比较全能的runtime + declarative的view instruction（比如 vdom），还是依赖一个轻量的runtime（号称没有runtime其实最终还是要抽取出复用的函数，等于是一个轻量的 runtime）+ 比较imperative的view instruction。
    - 纯模版类的更适合后者，因为编译的输入限制多了反而容易做分析和优化，代价是要牺牲 render function 的灵活性
    - React由于JSX太过灵活，从view层面做AOT就比较难做，但可能对prepack这样的基于运行分析的亲和性更好（比如可以做 component folding）
    - Vue在这一块的路线则是尽可能通过分析模版给vdom runtime留下hint，可以减少大量vdom的运行时判断开销，绕过一些基于JSX难以手动优化的地方
    - Inferno已经证明了优化到极致的vdom是可以逼近手写的vanilla代码的，也就是说两个方向的理论极限差的并不多，所以光看理论很难说哪个最好，还是要看实际benchmark。
  - JSX确实太灵活了，又没有表达式类型信息，只好先运行一遍render，然后进行diff。
    - 但是明明大部分组件都很简单，当state变化后，本组件dom变化，开发者一眼就能看出来，编译器却无法通过静态分析看出来
  - 在特定场景下，比如首页渲染的时候，能用babel把runtime消灭掉，也是一种解法。首屏的逻辑能有多复杂。
    - 可以复用组件做轻量页面比如login, 然后再后台悄悄下载runtime
    - 但是对vue的意义不大因为vue的runtime本身就很小。
  - 赞同两种方式往后发展最后的性能瓶颈会达到一致，但是对于render函数比较灵活不好处理不太能理解。
    - 目前 jsx 的静态处理只是替换 h function，对 jsx 本身的内容不做静态分析（只做转换），
    - 而 template 在静态处理时如文中所说则加入了 hint 来降低 vdom 的 runtime 开销。
    - 所以如果下一步在做 jsx 转换的时候也加入更多的处理，比如 eliminate，hint 等等，那和 template 差距也不大了。
    - 两种表现形式包含的静态信息是一致的才应该是「优化性能殊途同归」的本质，而现有的两种处理形式只不过是对这些信息的利用率有高低区分而已。
- https://github.com/mohebifar/vidact
  - /672Star/MIT/202004/ts
  - https://mohebifar.github.io/vidact/
  - A compiler that converts React-compatible codes to VanillaJS with no Virtual DOM
  - It is similar to Svelte, but unlike Svelte, Vidact does not introduce a new syntax. 
    - It takes in pure React-compatible JavaScript (JSX) and outputs plain JavaScript.
  - known limitations. 
    - It does not fully comply with React's behaviour in some edge cases, and probably never will, 
      - but the goal is to get as close behaviour to React as possible. 
    - Also, it currently only supports functional components and does not support class components.
  - Vidact is a babel-plugin that scans your source code to find what parts of the UI need to be updated in response to a prop or state change 
    - and generates a plain JavaScript code that should have the same DOM result as the equivalent React code. 
    - Note that all of this is done in build time

## build-babel-webpack

## react-fwk-conversion

- https://github.com/bitovi/react-to-webcomponent
  - converts React components to custom elements
  - The custom element acts as a wrapper for the underlying react component.

## more-react