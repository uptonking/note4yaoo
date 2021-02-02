---
title: note-benchmark-web
tags: [benchmark, web]
created: '2019-12-22T12:19:22.028Z'
modified: '2020-07-14T09:28:43.976Z'
---

# note-benchmark-web

# frontend-framework

- [前端框架基准测试最新结果：18个框架当中有13个达到顶级](https://www.infoq.cn/article/UHsl0gogHtL2BM*vJIOs)
  - https://www.infoq.com/news/2019/04/real-world-framework-benchmark
  - runtime对性能的影响不算很大，浏览器层执行dom操作的影响最大

- https://github.com/krausest/js-framework-benchmark
  - https://krausest.github.io/js-framework-benchmark/index.html
  - [JS web frameworks benchmark – Round 1_201601](https://www.stefankrause.net/wp/?p=191)
  - [JS web frameworks benchmark – Round 7_201711](https://www.stefankrause.net/wp/?p=454)
    - Surplus is fastest after vanillajs and it’s really impressively close(仅以些微之差获胜的). 
      - Petit-dom, Bobril and ivi follow right behind.
    - React 16 is really an improvement. It pushes react in front of preact and vue.js.
    - Angular and react are very close, especially with the no-zone variant.
  - [JS web frameworks benchmark – Round 8_201809](https://www.stefankrause.net/wp/?p=504)
    - The fastest frameworks are very fast. 
      - I can’t beat domc and stage0 and solid, surplus and ivy are very, very close.
    - Marionette made a significant jump. Version 4.0.0-beta.1 is only 24% slower than domc.
    - The (low level) webassembly framework stdweb is only 13% behind. Might be interesting to see how they continue.
  - A comparison of the performance of a few popular javascript frameworks
  - The following operations are benchmarked for each framework:
    - create rows,select row,partial update,remove row,append rows to large table
    - run memory,update memory,startup time,script bootup time,main thread work cost
  - A framework can implement an update for a list of data in two ways. 
    - Either keep an association between a list data element and a dom node (which is the keyed mode) 
      - or rearrange and reassign the DOM nodes as it wants to (non-keyed).
    - Keyed implementations create an association between the domain data and a dom element by assigning a `key`. 
      - If data changes the dom element with that key will be updated. 
    - Non-keyed implementations are free to reuse the existing dom nodes in whatever way they like and thus might be faster, 
      - but may cause issues if there’s a dependency on the particular dom nodes.
  - If you’re using CSS transitions or third-party frameworks non-keyed might cause problems, 
    - because e.g. removing an element might instead remove the last element from the dom node list and patch all others to display the correct values. 
    - This can cause problems when e.g. CSS transitions styles depend on removing the specific dom node.
    - Most (maybe all) keyed framework can behave non-keyed if one assigns the list’s array index as a key.
  - From the framework perspective handling only non-keyed updates makes dom reconciliation much easier. 
  - If you want my opinion: Choose a framework that supports keyed updates.

- Hadn't heard of domc and stage0. 
  - Took a peek but unfortunately it seems they use `Function()` to compile code on the fly, 
  - so they're not suitable for anything that might get deployed with a content security policy
  - Yes, it was acceptable as proof-of-concept. 

- [radEventListener: a Tale of Client-side Framework Performance_202008](https://css-tricks.com/radeventlistener-a-tale-of-client-side-framework-performance/)
  - To be fair to React, these pitfalls likely exist in many VDOM frameworks, because the nature of them adds necessary overhead to manage all sorts of things 
  - if you use React or any VDOM library, you should spend some time investigating its impact on an array of devices

# more-benchmarks

- [Today I looked into the performance of different layout modes in CSS.](https://twitter.com/JoshWComeau/status/1356377422925541377)

- [textJust how much faster is vanilla JS than frameworks?_202008](https://gomakethings.com/just-how-much-faster-is-vanilla-js-than-frameworks/)

- https://github.com/Polymer/benchmarks
  - A collection of benchmarks related to Polymer Project libraries.
  - For the runner used by these benchmarks, see tachometer
  - Shack is a simplified subset of the Polymer Shop demo app, implemented for benchmarking purposes using lit-html, LitElement, and Polymer 3. 
  - To compare the first-contentful-paint time for each of these implementations, 
