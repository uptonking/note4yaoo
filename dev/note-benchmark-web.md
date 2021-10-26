---
title: note-benchmark-web
tags: [benchmark, web]
created: '2019-12-22T12:19:22.028Z'
modified: '2020-07-14T09:28:43.976Z'
---

# note-benchmark-web

# guide

- tips
  - 不必执着于选择最正确的测试api和库，分析业务场景，选择最重要的性能指标，有针对性地进行优化
  - it matters far more what you measure than the timer API you pick
  - 很多测试api甚至自身都不是一致的，时快时慢

- [7GUIs: A GUI Programming Benchmark](https://eugenkiss.github.io/7guis/)
  - 7GUIs defines seven tasks that represent typical challenges in GUI programming. 
  - In addition, 7GUIs provides a recommended set of evaluation dimensions.
  1. Counter
  2. Temperature Converter
  3. Flight Booker
  4. Timer
  5. CRUD
  6. Circle Drawer
  7. Spreadsheet Cells
  - ref
    - https://github.com/andrewgreenh/7guis (react实现，多使用class组件)
# data-grid-table
- https://github.com/handsontable/performance-lab
  - JavaScript performance tests for Handsontable
- https://github.com/bryntum/grid-performance
  - A performance comparison of popular JavaScript data grid components. 
  - Measures the initial rendering time and scroll performance for the following data grids
  - ag-grid, bryntum, devextreme, dhtmlx, extjs

- https://github.com/zsimo/render-table-benchmark
  - https://zsimo.github.io/render-table-benchmark/public/
  - different ways to render the same table with the same data. 
  - The purpose is to experiment different Javascript template engines and benchmark them with Vanilla implementation.
  - tested: hyperhtml lighterhtml lit-html nanomorph pug pug + nanomorph + nanohtml svelte
# react
- https://github.com/paularmstrong/react-component-benchmark
  - This project aims to provide a method for gathering benchmarks of component tree mount, update, and unmount timings.
  - Since this project does not hook into the React renderer directly, the values gathered are not 100% accurate and may vary slightly because they're taken from a wrapping component.

- https://github.com/reduxjs/react-redux-benchmarks
  - Performance benchmark harness for React-Redux
# web-ui
- https://github.com/mikolaj6r/web-benchmark /202011
  - Node benchmark that uses Lighthouse and generates charts, tables, markdown and big json with results.

- https://github.com/Polymer/tachometer
  - tachometer is a tool for running benchmarks in web browsers. 
  - It uses repeated sampling and statistics to reliably identify even the smallest differences in timing.
# js
- https://github.com/bryntum/siesta
  - Siesta is a stress-free, ubiquitous, open-source JavaScript/TypeScript testing tool

- [JS: Benchmarking Lazy Getters](https://webreflection.medium.com/js-benchmarking-lazy-getters-9b132f45c15e)
  - Lazily evaluating properties is not just handy, but mandatory in some case.
- [Compare markdown implementations.](https://johnmacfarlane.net/babelmark2/)
  - 只提供了操作示例，没有提供结论

- https://github.com/yesvods/jsperf
  - 基于主流benchmark库测试部分js api的性能
  - 条件判断，使用字符串等非Boolean，性能会比直接用true/false差
  - 使用Map或{}来查找key，比IndexOf有 21, 600x 性能提升，不论是Array还是Object
  - 通过substring获取字符串子集比遍历接着加号连接有 97x 性能提升
  - typeof属于原生基本操作，速度炒鸡快，基本无视性能使用
  - for-in, for-of ing

- https://github.com/caderek/benny
  - simple benchmarking framework for JS/TS libs
  - 依赖benchmark
- https://github.com/kupriyanenko/astrobench
  - library for running in the browser performance benchmarks, based on Benchmark.js

- https://github.com/speedracer/speedracer
  - a performance runner, like a test runner, but for performance
  - It runs scripts (races) in Chrome (headlessly if possible) and produces detailed traces and reports on scripting, rendering and painting.
# frontend-framework
- [前端框架基准测试最新结果：18个框架当中有13个达到顶级](https://www.infoq.cn/article/UHsl0gogHtL2BM*vJIOs)
  - https://www.infoq.com/news/2019/04/real-world-framework-benchmark
  - runtime对性能的影响不算很大，浏览器层执行dom操作的影响最大

- https://github.com/krausest/js-framework-benchmark
  - https://krausest.github.io/js-framework-benchmark/index.html
  - [Chrome 79 - 93 results](https://github.com/krausest/js-framework-benchmark/issues/683)
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

- https://github.com/matteofigus/api-benchmark
  - A node.js tool that measures and compares performances of single and multiple apis inspired by BenchmarkJs
- https://github.com/jeffbski/bench-rest
  - benchmark REST (HTTP/HTTPS) API's. 
  - node.js client module for easy load testing / benchmarking REST API's…

- [radEventListener: a Tale of Client-side Framework Performance_202008](https://css-tricks.com/radeventlistener-a-tale-of-client-side-framework-performance/)
  - To be fair to React, these pitfalls likely exist in many VDOM frameworks, because the nature of them adds necessary overhead to manage all sorts of things 
  - if you use React or any VDOM library, you should spend some time investigating its impact on an array of devices
# engineering
- https://github.com/seancdavis/ssg-build-performance-tests
  - A comparison on build performance of popular SSGs, as they are tasked with processing local markdown files as the data source
- https://github.com/GoogleChromeLabs/tooling.report/
  - https://tooling.report/
  - tooling.report a quick way to determine the best build tool for your next web project

- https://github.com/webpack/benchmark
  - https://webpack.github.io/benchmark/
  - 比较了几个常用库的build时间：atlaskit-editor、rome、esbuild-three
- https://github.com/parcel-bundler/parcel-benchmark-action
  - This is an experimental GitHub Action for testing Parcel's performance and bundle size on a couple demo applications to automatically measure and report performance impact of PRs on these examples.
- https://github.com/atlassian/parcel-stress-test
  - Apache2
# more-benchmarks
- [Today I looked into the performance of different layout modes in CSS.](https://twitter.com/JoshWComeau/status/1356377422925541377)

- [textJust how much faster is vanilla JS than frameworks?_202008](https://gomakethings.com/just-how-much-faster-is-vanilla-js-than-frameworks/)

- https://github.com/Polymer/benchmarks
  - A collection of benchmarks related to Polymer Project libraries.
  - For the runner used by these benchmarks, see tachometer
  - Shack is a simplified subset of the Polymer Shop demo app, implemented for benchmarking purposes using lit-html, LitElement, and Polymer 3. 
  - To compare the first-contentful-paint time for each of these implementations, 
