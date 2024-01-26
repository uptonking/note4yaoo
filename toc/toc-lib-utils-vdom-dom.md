---
title: toc-lib-utils-vdom-dom
tags: [dom, toc, utils, vdom]
created: 2023-11-23T09:53:51.673Z
modified: 2023-11-23T09:56:33.507Z
---

# toc-lib-utils-vdom-dom

# guide
- vdom
  - 标准定义，可参考dom、jsdom、ast
# vdom
- https://github.com/snabbdom/snabbdom /ts
  - A virtual DOM library with focus on simplicity, modularity, powerful features and performance.
  - 每个VNode的属性
    - selector: tag#id.className
    - data: any
    - children: VNode[]
    - text: string
    - elm: 每个VNode对应的真实dom节点
  - who is using #snabbdom 用例
    - vue, owl1
  - Snabbdom consists of an extremely simple, performant and extensible core that is only ≈ 200 SLOC. 
  - It offers a modular architecture with rich functionality for extensions through custom modules. 
  - To keep the core simple, all non-essential functionality is delegated to modules.
  - [snabbdom的源码以及 仿写一个自己的vDOM库](https://lastnigtic.cn/posts/virtual-dom/)
  - 未使用event-delegation或synthetic
    - `elm.addEventListener(name, listener, false)` 直接操作dom
    - Snabbdom allows swapping event handlers between renders. This happens without actually touching the event handlers attached to the DOM
  - [Support custom elements 已支持](https://github.com/snabbdom/snabbdom/issues/141)
  - [Isomorphic snabbdom](https://github.com/snabbdom/snabbdom/issues/86)
    - I have put together a little starter kit that does SSR with snabbdom-to-html
- https://github.com/ged-odoo/blockdom
  - Owl framework 1.x is based on a fork of snabbdom
  - version 2 is not ready yet, but will be based on blockdom.
  - It features blocks, supports fragments, manage synthetic event handlers and more.

- https://github.com/livoras/simple-virtual-dom /MIT/202003/js
  - Simple virtual-dom algorithm. It has only ~500 lines of code
  - [如何理解虚拟DOM](https://www.zhihu.com/question/29504639/answer/73607810)
  - [深度剖析：如何实现一个 Virtual DOM 算法](https://github.com/livoras/blog/issues/13)

- https://github.com/fantasticit/vdom /js
  - A simple basic implement of virtual-dom algorithm
  - [vdom 原理解析与简单实现](https://github.com/fantasticit/coding/issues/23)
  - 实际应用：https://github.com/spritejs/q-charts

- https://github.com/patrick-steele-idem/morphdom /js
  - lightweight DOM diffing/patching (no virtual DOM needed)
  - Lightweight module for morphing an existing DOM node tree to match a target DOM node tree. 
  - Instead of replacing the existing DOM tree with a new DOM tree we want to transform the existing DOM tree to match the new DOM tree while minimizing the number of changes to the existing DOM tree. 
  - morphdom does not rely on any virtual DOM abstractions. Because morphdom is using the real DOM, the DOM that the web browser is maintaining will always be the source of truth. 
  - morphdom can be used with any templating language that produces an HTML string.
  - The transformation is done in a single pass of both the original DOM tree and the target DOM tree and is designed to minimize changes to the DOM 
  - the algorithm used by this module will automatically match up elements that have corresponding IDs and that are found in both the original and target DOM tree
  - Support for diffing the real DOM with a virtual DOM was introduced in v2.1.0
  - Both morphdom and virtual DOM based solutions update the real DOM with the minimum number of changes. The only difference is in how the differences are determined. **morphdom compares real DOM nodes while virtual-dom and others only compare virtual DOM nodes**.

- https://github.com/bigskysoftware/idiomorph /js
  - a javascript library for morphing one DOM tree to another
  - Both morphdom and nanomorph use the `id` property of a node to match up elements within a given set of sibling nodes. When an id match is found, the existing element is not removed from the DOM, but is instead morphed in place to the new content.
  - However, in both these algorithms, the structure of the children of sibling nodes is not considered when morphing two nodes: only the ids of the nodes are considered. This is due to performance: it is not feasible to recurse through all the children of siblings when matching things up.
  - Idiomorph takes a different approach: before node-matching occurs, both the new content and the old content are processed to create id sets, a mapping of elements to a set of all ids found within that element. Id sets can be computed relatively efficiently via a query selector + a bottom up algorithm.
  - idiomorph 来自于框架 htmx。
  - https://twitter.com/chloerei/status/1712027755259560298
    - React 成名于 shadow dom，它让开发者尽管 render，库来计算差异然后更新到页面上，提高了开发效率。
    - Turbo 8 有点类似这个机制，服务端尽管 render，浏览器拿到 html body 之后对比之间的差异，然后更新变化的部分。Turbo 8 用到库是 idiomorph
    - Phoenix 的 LiveView 也是类似机制，用的库是 morphdom

- https://github.com/natemoo-re/micromorph /ts
  - A very tiny library for diffing live DOM nodes.
  - With the /nav entrypoint, Micromorph automatically converts your MPA into a SPA while only re-rendering content that has changed.

- https://github.com/google/incremental-dom /ts
  - Incremental DOM is a library for building up DOM trees and updating them in-place when data changes. 
  - 👉🏻 It differs from the established virtual DOM approach in that no intermediate tree is created (the existing tree is mutated in-place). 
  - This approach significantly reduces memory allocation and GC thrashing
  - Incremental DOM is primarily intended as a compilation target for templating languages.
  - Think of it as ASM.dom

  - https://github.com/aidenybai/hundred /ts/NoDeps
    - Hundred is intended to be a toy block virtual DOM based off of Million.js, and is a proof-of-concept and a learning resource
    - This implementation is similarly based off of [blockdom](https://github.com/ged-odoo/blockdom).

- https://github.com/AFASSoftware/maquette /ts
  - simple virtual DOM library

- https://github.com/Matt-Esch/virtual-dom /10.8kStar/MIT/201604/js
  - A JavaScript DOM model supporting element creation, diff computation and patch operations for efficient re-rendering
  - 用例: reflex
  - forks
  - https://github.com/MilanConrad/virtual-dom-diff-printing /202307/js
    - Included pretty diff printing
  - https://github.com/Sota-Watanabe/virtual-dom /202111/js
    - Add comment
  - https://github.com/imtaotao/virtual-dom /201808/js
    - feat: add createElement and vnode
  - https://github.com/pupperjs/virtual-dom /202206/js
    - virtual DOM now accepts attributes for comments (for using hooks)
  - https://github.com/CrazyEggInc/virtual-dom /202109/js
    - Refactor apply-properties.js to synchronize it with vdom-serialized
  - https://github.com/QuisPic/virtual-dom-ae /202010/js
    - Added Thunk.
  - https://github.com/Raynos/vdom-thunk /201506/js
    - A thunk optimization for virtual-dom
    - Use Thunk when you want to avoid re-rendering subtrees.
    - Thunk will only re-evaluate the subtree if the arguments you pass to it change. This means you should use an immutable data structure (like observ-struct)

- superfine /1.6kStar/MIT/202104/js/hyperapp作者
  - https://github.com/jorgebucaran/superfine
  - a minimal view layer for building web interfaces. 
  - we use the `h()` and `text()` functions to create a lightweight representation of the DOM (or virtual DOM for short), and `patch()` to actually render the DOM.
  - Superfine won't re-create the entire DOM every time we use patch(). By comparing the old and new virtual DOM we are able to change only the parts of the DOM that need to change instead of rendering everything from scratch.
  - who is using #superfine-vdom
    - typewriter
  - forks
  - https://github.com/whaaaley/superfine /202208/js
    - Add shadowRoot nodes, Treat `shadow-root` prop similar to `key`.

- https://github.com/trueadm/t7 /js
  - lightweight JavaScript template library that compiles ES2015 template strings into virtual DOM objects.

- https://github.com/elm/virtual-dom /202205/elm
  - A virtual DOM implementation that backs Elm's core libraries for HTML and SVG.
# dom
- https://github.com/retentioneering/retentioneering-dom-observer
  - The package contains tools for parsing DOM data, observing DOM and tracking changes.
  - This class is a wrapper over `MutationObserver`, allowing you to observe changes even of those nodes that are not already in the DOM
  - Observation will automatically start as soon as the target node appends in the DOM.

- https://github.com/wilsonpage/fastdom /202206/js
  - Eliminates layout thrashing by batching DOM measurement and mutation tasks
  - Eliminates layout thrashing by batching DOM read/write operations 
  - Each measure/mutate job is added to a corresponding measure/mutate queue. The queues are emptied (reads, then writes) at the turn of the next frame using `window.requestAnimationFrame`.

- https://github.com/CoCreate-app/CoCreate-clone /js
  - https://cocreate.app/docs/clone
  - Clone an html element by #id, identify targeted elements using clone_id="" attribute. 
  - Capable of creating nested & complex cloning logic for kanbans, tasklists etc.
# utils
- https://github.com/dumijay/CalDom /MIT/202107/js
  - https://caldom.org/
  - An agnostic, reactive & minimalist (3kb) JavaScript UI library with direct access to native DOM.
  - A 2-in-1 virtual-DOM & no-virtual-DOM approach if you will.
# more
