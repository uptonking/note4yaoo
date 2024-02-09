---
title: toc-repos-lang-js
tags: [js, repos, toc]
created: 2020-09-28T05:27:32.927Z
modified: 2021-05-14T15:04:42.225Z
---

# toc-repos-lang-js

# guide

- [most depended upon packages](https://www.npmjs.com/browse/depended)
  - lodash, core-js, moment, debug, uuid
  - fs-extra, glob, chalk, commander, yargs, inquirer, minimist, colors, chokidar
  - axios, express, request, node-fetch, async, bluebird, body-parser, isomorphic-fetch
  - react, vue, classnames, rxjs, jquery, redux
  - typescript, webpack, dotenv, @babel/runtime, jest, socket.io, redis
  - styled-components, 
  - ramda, deepmerge, date-fns
  - marked
# js-utils
- https://github.com/pull-stream/pull-stream /js
  - https://pull-stream.github.io/
  - pull streams work great for "object" streams as well as streams of raw text or binary data.
  - pull-streams are not directly compatible with node streams, but pull-streams can be converted into node streams

- https://github.com/gvergnaud/ts-pattern /ts
  - The exhaustive Pattern Matching library for TypeScript with smart type inference.
  - Pattern-match on any data structure: nested Objects, Arrays, Tuples, Sets, Maps and all primitive types.
  - Supports predicates, unions, intersections and exclusion patterns for non-trivial cases.
  - Pattern Matching is a code-branching technique coming from functional programming languages that's more powerful and often less verbose than imperative alternatives (if/else/switch statements), especially for complex conditions.

- https://github.com/swan-io/boxed /ts
  - https://swan-io.github.io/boxed/
  - https://swan-io.github.io/boxed/core-concepts
  - Utility types for functional TypeScript
  - Provide utility types that make data-manipulation and storage easier
  - Immutable (all provided types are)
  - Compatibility with ts-pattern (using patterns we provide).
  - The way we like to think of the data-structures we expose are that they're boxes (or containers) that may or may not contain a value.

- https://github.com/fluture-js/Fluture /202005/js/inactive
  - Fantasy Land compliant (monadic) alternative to Promises
  - Much like Promises, Futures represent the value arising from the success or failure of an asynchronous operation (I/O). 
  - Though unlike Promises, Futures are lazy and adhere to the monadic(单元的，单体的) interface.

- https://github.com/mitranim/posterus /js/NoDeps/inactive
  - Composable async primitives with cancelation, control over scheduling, and coroutines. 
  - Superior replacement for JS Promises.
  - Supports cancelation.
  - Mostly synchronous.
  - Exposes its scheduler, allowing to opt into asynchrony, and opt out by flushing pending tasks on demand.
# js-data-structure
- https://github.com/Conaclos/cow-list /ts
  - Cow List provides a Copy-On-Write iterable list that supports logarithmic searches. 
  - It provides also a mutable iterable List with versioning capabilities.
  - Cow List naively supports lengthy values (objects with a length property). 
  - This makes Cow List a perfect fit to implement a `rope`.

- https://github.com/immutable-js/immutable-js /js/NoDeps
  - https://immutable-js.com/
  - Immutable persistent data collections for Javascript which increase efficiency and simplicity.
  - Immutable data cannot be changed once created, leading to much simpler application development, no defensive copying, and enabling advanced memoization and change detection techniques with simple logic. 
  - Persistent data presents a mutative API which does not update the data in-place, but instead always yields new updated data.
  - Immutable.js provides many Persistent Immutable data structures including: List, Stack, Map, OrderedMap, Set, OrderedSet and Record.
  - These data structures are highly efficient on modern JavaScript VMs by using structural sharing via hash maps tries and vector tries as popularized by Clojure and Scala, minimizing the need to copy or cache data.
  - While Immutable.js is inspired by Clojure, Scala, Haskell..., it's designed to bring these powerful concepts to JavaScript, and therefore has an Object-Oriented API that closely mirrors that of ES2015 Array, Map, and Set.

- https://github.com/skeate/lambdata /ts
  - https://skeate.github.io/lambdata/
  - lambdata is a library of persistent, purely functional data structures, written in Typescript using fp-ts, based on the work of Chris Okasaki.

- https://github.com/swannodette/mori /ClojureScript/inactive
  - A simple bridge to ClojureScript's persistent data structures and supporting APIs for vanilla JavaScript.

- https://github.com/liljenzin/confluent /cpp
  - Confluent sets and maps are sorted associative containers written in C++11.
  - [[1301.3388] Confluently Persistent Sets and Maps](https://arxiv.org/abs/1301.3388)

- https://github.com/pgte/js-sparse-array /201812/js
  - Sparse array implementation in JS with no dependencies
# repos
- https://github.com/tannerlinsley/react-table
- https://github.com/bvaughn/react-window
  - /9kStar/MIT/202001
  - React components for efficiently rendering large lists and tabular data
- https://github.com/bvaughn/react-virtualized
  - /20kStar/MIT/202008
  - React components for efficiently rendering large lists and tabular data.
- https://github.com/olifolkerd/tabulator
  - /3.5kStar/MIT/202009
  - interactive table generation JavaScript library
  - 无依赖，基于div实现
- https://github.com/frappe/datatable
  - /502Star/MIT/202009/js
  - A simple, modern and interactive datatable for the web
  - 基于div实现，每行对应的dom元素存在
  - 依赖hyperlist、sortablejs、lodash
  - https://github.com/tbranyen/hyperlist
    - /MIT/291Star/202006/js/NoDeps
    - A performant virtual scrolling list utility capable of rendering millions of rows
    - a fork of the existing (unmaintained) project: sergi/virtual-list
- https://github.com/joshwcomeau/react-flip-move /inactive
  - https://github.com/aholachek/react-flip-toolkit /ts
  - https://github.com/davidkpiano/flipping
- https://github.com/plotly/react-chart-editor
  - /325Star/MIT/202009
  - React component for creating & editing D3 charts
- https://github.com/apache/incubator-superset
  - /30.2kStar/Apache2/202009/python/js
  - a Data Visualization and Data Exploration Platform
  - 依赖python、flask、react
- https://github.com/SheetJS/sheetjs
  - /22.9kStar/Apache2/202009
  - Community Edition -- Spreadsheet Data Toolkit
  - 无依赖，自己实现了办公类文档的各种解析器 js-word、js-ppt、ssf、js-cfb
- https://github.com/popperjs/popper-core
  - /15.8kStar/MIT/202009
  - Positioning tooltips and popovers is difficult. Popper is here to help
- https://github.com/nhn/tui.editor
  - /11.8kStar/MIT/202009/js
  - Plain JavaScript component
  - provides Markdown/WYSIWYG mode, GFM Standard + Chart & UML Extensible.
  - 依赖codemirror5
- https://github.com/nhn/tui.calendar
  - /8.5kStar/MIT/202009/js
  - A JavaScript calendar that has everything you need.
- https://github.com/mdx-js/mdx
  - /9.7kStar/MIT/202009
  - let you seamlessly use JSX in your markdown documents
- https://github.com/jxnblk/mdx-deck
  - /9.5kStar/MIT/202009
  - React MDX-based presentation decks
  - 基于gatsby实现的文档展示工具有: docz, mdx-deck
- https://github.com/codemirror/CodeMirror
  - /21.3kStar/MIT/202010/js
  - In-browser code editor
  - CodeMirror 6 is a rewrite of the CodeMirror code editor. 
  - The new system provides solid accessibility, touchscreen support, better content analysis
  - It is not API-compatible with the old code.

## viz

- https://github.com/chartjs/Chart.js
  - /50.4kStar/MIT/202009/js
  - Simple HTML5 Charts using the canvas tag
- https://github.com/apache/incubator-echarts
  - /43kStar/Apache2/202009/js
  - interactive charting and data visualization library for browser
- https://github.com/processing/p5.js
  - /13.9kStar/LGPL/202009
  - p5.js has a full set of drawing functionality using the HTML5 canvas element
- https://github.com/frappe/charts
  - /13.5kStar/MIT/202009
  - modern, intuitive and responsive charts with zero dependencies
  - https://github.com/frappe/gantt
- https://github.com/plotly/plotly.js
  - /12.3kStar/MIT/202009
  - Open-source JavaScript charting library behind Plotly and Dash
- https://github.com/FormidableLabs/victory
  - /8.3kStar/MIT/202009
  - composable React components for building interactive data visualizations
  - 依赖d3
- https://github.com/uber/react-vis
  - /7.4kStar/MIT/202007
  - react components to render common data visualization charts

- https://github.com/markmarkoh/datamaps
  - Customizable SVG map visualizations for the web in a single Javascript file using D3.js
- https://github.com/nteract/semiotic
  - data visualization framework combining React & D3
- https://github.com/TargetProcess/tauCharts
  - /1.9kStar/Apache2/202007
  - a data-focused JavaScript charting library based on D3 
- https://github.com/visgl/luma.gl
  - High-performance Toolkit for WebGL-based Data Visualization
- https://github.com/syt123450/giojs
  - A Declarative 3D Globe Data Visualization Library built with Three.js
- https://github.com/apexcharts/apexcharts.js
  - Interactive JavaScript Charts built on SVG
- https://github.com/NUKnightLab/TimelineJS
  - A Storytelling Timeline built in JavaScript.

- https://github.com/mermaid-js/mermaid
  - /32.1kStar/MIT/202009/js
  - Generation of diagram and flowchart from text in a similar manner as markdown
- https://github.com/jgraph/drawio
  - Source to app.diagrams.net
- https://github.com/alyssaxuu/flowy
  - minimal javascript library to create flowcharts
- https://github.com/adrai/flowchart.js
  - Draws simple SVG flow chart diagrams from textual representation of the diagram

## apps

- https://github.com/getredash/redash
  - /17.3kStar/BSD/202009/python
  - Connect to any data source, easily visualize, dashboard and share your data.
  - 依赖flask
  - since 9.0.0-beta(2020-06-11)
    - backend code was updated to support Python 3
    - replaced Celery with RQ for background jobs processing
    - frontend code is now 100% React and we removed all the Angular dependencies.
- https://github.com/yyhsong/iDataV
  - 大屏数据可视化案例
- https://github.com/ricklamers/gridstudio
  - a cloud based data science tool that combines a spreadsheet view with a Python scripting environment
  - 依赖flask

- https://github.com/YMFE/yapi
  - /18kStar/Apache2/202009
  - 轻松创建、发布、维护 API
  - https://hellosean1025.github.io/yapi
- https://github.com/star7th/showdoc
  - 一个非常适合IT团队的在线API文档、技术文档工具
  - 依赖php

## ui-components-design

- https://github.com/pure-css/pure
  - /21.1kStar/BSD/202008
  - A set of small, responsive CSS modules
- https://github.com/jgthms/bulma
  - /41.3kStar/MIT/202009/css
  - Modern CSS framework based on Flexbox
- https://github.com/animate-css/animate.css
  - /68kStar/MIT/202009/css
  - A cross-browser library of CSS animations.

- https://github.com/mui-org/material-ui
  - /61.2kStar/MIT/202009/js
  - React components for faster web development
- https://github.com/ElemeFE/element
  - /47.4kStar/MIT/202009/vue
  - A Vue.js 2.0 UI Toolkit for Web
- https://github.com/Semantic-Org/Semantic-UI /inactive
  - a UI framework designed for theming.
- https://github.com/reactstrap/reactstrap
  - React Bootstrap 4 components
- https://github.com/vitmalina/w2ui
  - /1.8kStar/MIT/202009
  - JavaScript UI library for building rich data-driven web applications.  
  - requires only jQuery (1.9+) as a dependency
- https://github.com/dcloudio/mui
  - 最接近原生APP体验的高性能框架

- https://github.com/javve/list.js 
  - /9.8kStar/MIT/201912/inactive
  - adding search, sort, filters and flexibility to tables, lists and various HTML elements. 
  - Built to be invisible and work on existing HTML.

- https://github.com/artf/grapesjs
  - /11.8kStar/BSD/202009
  - Free and Open source Web Builder Framework
  - 依赖backbone、cash-dom、codemirror、underscore
- https://github.com/givanz/VvvebJs
  - /3.4kStar/Apache2/202007
  - Drag and drop website builder
  - 依赖jquery3，bootstrap4，codemirror
- https://github.com/pandao/editor.md 
  - /10.2kStar/MIT/201905
  - embeddable online markdown editor(component), based on CodeMirror & jQuery & Marked.

## most-stars js-ts

- https://github.com/vuejs/vue
  - /173kStar/MIT/202009/ts
  - https://github.com/vuejs/vue-next
  - a progressive, incrementally-adoptable JS framework for building UI on the web
- https://github.com/facebook/react
  - /156kStar/MIT/202009/js
  - A declarative, component-based JS library for building user interfaces.
- https://github.com/twbs/bootstrap
  - /144kStar/MIT/202009/js
  - HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.
- https://github.com/microsoft/vscode
  - /104kStar/MIT/202009/ts
  - Visual Studio Code IDE
- https://github.com/d3/d3
  - /93.8kStar/BSD/202009/js
  - bring data to life using SVG, Canvas and HTML.
- https://github.com/mrdoob/three.js
  - /63.7kStar/MIT/202009/js
  - JavaScript 3D library.
- https://github.com/storybookjs/storybook
  - /53.7kStar/MIT/202009/ts
  - The UI component explorer
- https://github.com/gatsbyjs/gatsby
  - /47.1kStar/MIT/202009/js
  - Build blazing fast, modern apps and websites with React
- https://github.com/juliangarnier/anime
  - /36.8kStar/MIT/202004/js
  - works with CSS properties, SVG, DOM attributes and JS Objects.
- https://github.com/ColorlibHQ/AdminLTE
  - /36.2kStar/MIT/202009/js
  - Free admin dashboard template based on Bootstrap 4

- https://github.com/pixijs/pixi.js
  - /30.7kStar/MIT/202009/ts
  - Create digital content with the fastest 2D WebGL renderer.
- https://github.com/Leaflet/Leaflet
  - /29kStar/BSD/202009/js
  - JavaScript library for mobile-friendly interactive maps
# ast/compiler
- https://github.com/jquery/esprima /BSD/ts
  - a high performance, standard-compliant ECMAScript parser written in ECMAScript
# js-repos
- https://github.com/axios/axios
  - Promise based HTTP client for the browser and node.js
- https://github.com/PanJiaChen/vue-element-admin
  - vue admin
- https://github.com/moby/moby
  - for the container ecosystem to assemble container-based systems
- https://github.com/webpack/webpack
  - A bundler for javascript and friends. 
- https://github.com/jquery/jquery
  - js library
- https://github.com/vercel/next.js
  - React Framework: hybrid static & server rendering, smart bundling, route pre-fetching... No config needed.
- https://github.com/hakimel/reveal.js
  - The HTML Presentation Framework
- https://github.com/atom/atom
  - hackable text editor
- https://github.com/socketio/socket.io
  - Realtime application framework (Node. JS server)
- https://github.com/expressjs/express
  - Fast, unopinionated, minimalist web framework for node.
- https://github.com/RocketChat/Rocket.Chat
  - Solution for team communications
- https://github.com/Marak/faker.js
  - generate massive amounts of realistic fake data in Node.js and the browser
- https://github.com/date-fns/date-fns
  - Modern JavaScript date utility library
- https://github.com/markedjs/marked
  - A markdown parser and compiler. Built for speed.
- https://github.com/sequelize/sequelize
  - An easy-to-use multi SQL dialect ORM for Node.js
- https://github.com/airbnb/lottie-web
  - Render After Effects animations natively on Web, Android and iOS, and React Native
- https://github.com/Popmotion/popmotion
  - Simple animation libraries for delightful user interfaces
- https://github.com/fabricjs/fabric.js
  - Javascript Canvas Library, SVG-to-Canvas (& canvas-to-SVG) Parser
- https://github.com/adobe-webplatform/Snap.svg
- https://github.com/Flipboard/react-canvas
- https://github.com/wekan/wekan
  - open-source kanban (built with Meteor).
- https://github.com/mojs/mojs
  - motion graphics toolbelt for the web
- https://github.com/nuysoft/Mock
  - a simulation data generator
  - High performance canvas rendering for React components
- https://github.com/STRML/react-grid-layout
  - A draggable and resizable grid layout with responsive breakpoints, for React.
- https://github.com/kamranahmedse/driver.js
  - /11.7kStar/MIT/202003
  - vanilla JavaScript engine to drive the user's focus across the page
- https://github.com/greensock/GSAP
  - /11.4kStar/NoChargeLic/202008
  - Animate CSS, SVG, canvas, React, Vue, WebGL, colors, strings, motion paths, generic objects
- https://github.com/krisk/Fuse
  - a lightweight fuzzy-search, in JS, with zero dependencies.
- https://github.com/markdown-it/markdown-it
  - Markdown parser, done right. 100% CommonMark support, extensions, syntax plugins 
- https://github.com/mdx-js/mdx
  - JSX in Markdown for ambitious projects
- https://github.com/sghall/react-move
- https://github.com/frontend-collective/react-sortable-tree
- https://github.com/boo1ean/casual
  - Fake data generator for javascript
- https://github.com/CartoDB/cartodb
  - Location Intelligence & Data Visualization tool
- https://github.com/PatMartin/Dex
  - A data visualization tool written in Java/JavaFX
- https://github.com/humangeo/leaflet-dvf
  - Leaflet Data Visualization Framework
- https://github.com/react-csv/react-csv
  - React components to build CSV files on the fly 
- https://github.com/TerriaJS/terriajs
  - A library for building rich, web-based geospatial data explorers.
- https://github.com/Shopify/draggable
  - JavaScript Drag & Drop library your grandparents warned you about
- https://github.com/airbnb/react-dates
  - An easily internationalizable, mobile-friendly datepicker library for the web
- https://github.com/PrismJS/prism
  - Lightweight, robust, elegant syntax highlighting.
- https://github.com/mobz/elasticsearch-head
  - A web front end for an elasticsearch cluster
# nodejs
- https://github.com/OptimalBits/node_acl /201805/js/inactive
  - This module provides a minimalistic ACL implementation inspired by Zend_ACL.
  - When you develop a web site or application you will soon notice that sessions are not enough to protect all the available resources. Avoiding that malicious users access other users content proves a much more complicated task than anticipated. ACL can solve this problem in a flexible and elegant way.
  - Create roles and assign roles to users.

- https://gitee.com/weolar_admin/mininodejs20 /GPL/202312/cpp
  - 基于quickjs、nodejs14实现的山寨版nodejs
  - 使用quickjs替换v8后的精简nodejs。编译出的二进制文件相比原版，体积大幅减少，冷启动速度大幅提升。
# js-runtime
- https://github.com/awslabs/llrt /MIT/202402/rust
  - lightweight JavaScript runtime designed to address the growing demand for fast and efficient Serverless applications.
  - It's built in Rust, utilizing QuickJS as JavaScript engine, ensuring efficient memory usage and swift startup.
  - Extremely surprised it uses QuickJS and they specifically chose no JIT. It does make good sense for their situation though.
# pref
- https://github.com/narutosstudent/load-balancer /202401/ts
  - Built a load balancer from scratch. 
  - Includes Round Robin algorithm and health check
  - Health check happens every 10th second. They're done in the background.
  - `http-proxy` is a Node.js library that allows you to create HTTP proxy servers. A proxy server simply forwards client HTTP requests to other servers and returns the response back to the client.
# benchmarking
- https://github.com/tinylibs/tinybench /MIT/202401/ts
  - tiny and lightweight benchmarking library
  - You can run your benchmarks in multiple JavaScript runtimes, Tinybench is completely based on the Web APIs with proper timing using `process.hrtime` or `performance.now`.
# more
- https://github.com/liljenzin/confluent /cpp
  - Confluent sets and maps are sorted associative containers written in C++11.
  - [[1301.3388] Confluently Persistent Sets and Maps](https://arxiv.org/abs/1301.3388)
