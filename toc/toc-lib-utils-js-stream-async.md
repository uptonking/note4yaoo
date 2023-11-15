---
title: toc-lib-utils-js-stream-async
tags: [async, lang-js, stream, toc, utils]
created: 2023-04-04T22:36:09.902Z
modified: 2023-04-04T22:36:31.529Z
---

# toc-lib-utils-js-stream-async

# guide

- blogs
  - [kappa architecture vs event sourcing](https://github.com/tschudin/ssb-icn2019-paper/issues/6)
# popular
- https://github.com/EloquentStudio/StreamTable.js /201604/js
  - streams data for tables in the background, updates and renders them using templating frameworks like Mustache.js, HandleBars.js
  - The idea behind StreamTable.js is to initially populate minimum rows (maybe 10 or 20) and after that it streams data silently in the background and update the table.
- https://github.com/EloquentStudio/filter.js /201802/js
  - http://eloquentstudio.github.io/filter.js/
  - Complete solution for client side filtering and rendering using JSON data
  - client-side JSON objects filter which can render html elements. 
  - Multiple filter criteria can be specified and used in conjunction with each other.
  - Add data using ajax streaming

- https://github.com/jimmywarting/StreamSaver.js /js
  - the solution to saving streams in the web browser. 
  - It is perfect for web apps where there's a need to save large amounts of data on devices with e.g. limited RAM.
  - there is this new native way to save files to the HD:
    - https://github.com/whatwg/fs
  - I also built native-file-system-adapter so you can have it in all Browsers, Deno, and NodeJS with different storages
    - https://github.com/jimmywarting/native-file-system-adapter

- https://github.com/Kanaries/web-data-loader /ts
  - allows you to load large data files in browser. 
  - It supports stream data and runs in webworker which will not block the main thread while loading the data. 
  - web-data-loader also support stream data sampling, it now support Reservoir Sampling methods.

- https://github.com/jahewson/node-byline
  - Line-by-line Stream reader for node.js

- https://github.com/Claviz/bellboy /202305/ts
  - Highly performant JavaScript data stream ETL engine.
  - Bellboy streams input data row by row. Every row, in turn, goes through user-defined function where it can be transformed.
  - When enough data is collected in batch, it is being loaded to destination.
  - A job in bellboy is a relationship link between processor and destinations
  - Each processor in bellboy is a class which has a single responsibility of processing data of specific type
  - Every job can have as many destinations (outputs) as needed. For example, one job can load processed data into a database, log this data to stdout and post it by HTTP simultaneously.
  - New processors and destinations can be made by extending existing ones.

- https://github.com/vweevers/detect-tabular /js
  - A stream that detects tabular data (spreadsheets, dsv or json) and yields objects.
  - npm i detect-tabular map-tabular-keys snake-case jsonstream
  - support
    - text: csv,tsv,json,ndjson
    - binary: xlsx,xls,ods
  - https://github.com/vweevers/tabular-stream

- https://github.com/finos/regular-table /js/NoDeps
  - A Javascript library for the browser, regular-table exports a custom element named `<regular-table>`, which renders a regular HTML `<table>` to a sticky position within a scrollable viewport. 
  - Only visible cells are rendered and queried from a natively async virtual data model, making regular-table ideal for enormous or remote data sets
  - Use it to build Data Grids, Spreadsheets, Pivot Tables, File Trees
  - Virtual Data Model
    - a simple data model, a two dimensional Array
    - even for very small data sets, regular-table won't read your entire dataset at once. 
    - Instead, we'll need to write a simple virtual data model to access DATA and COLUMN_NAMES indirectly
    - With an async data model, it's easy to serve getDataSlice() remotely from node.js or re-implement the JSON response protocol in any language. 
  - Because of the structure of the HTML `<table>` element,  `<td>` elements must be aligned with their respective row/column, which causes default `<regular-table>` to only be able to scroll in increments of a cell, which can be irregular when column data is of different lengths. 
  - regular-table is natively compatible with `perspective`, a WebAssembly streaming visualization engine. 
    - https://github.com/finos/perspective

- https://github.com/holepunchto/hypercore /js
  - Hypercore is a secure, distributed append-only log.
  - Built for sharing large datasets and streams of real time data
# stream
- https://github.com/zoubin/streamify-your-node-program
  - 对Node.js中stream模块的学习积累和理解
  - https://github.com/jeresig/node-stream-playground
    - created to help Node.js developers better understand how streams work by showing a number of use cases that are easily plug-and-play-able. 

- https://github.com/pull-stream/pull-stream /js
  - In classic-streams(node-v0.8x), streams push data to the next stream in the pipeline. 
  - In new-streams(node-v0.10x), data is pulled out of the source stream, into the destination. 
  - pull-stream is a minimal take on streams, pull streams work great for "object" streams as well as streams of raw text or binary data.

- https://github.com/pillarjs/send
  - Streaming static file server with Range and conditional-GET support

- https://github.com/caolan/highland
  - The high-level streams library for Node.js and the browser. 

- https://github.com/maxogden/mississippi
  - the goal of the modules included in mississippi is to make working with streams easy without sacrificing speed, error handling or composability.

- https://github.com/archiverjs/node-archiver
  - A streaming interface for archive generation
  - Archiver supports the following formats 
    - json, zip, tar

- https://github.com/nodejs/readable-stream
  - Node-core streams for userland
  - supports Node, as well as evergreen browsers.

- https://github.com/jimhigson/oboe.js
  - Oboe.js is an open source Javascript library for loading JSON using streaming, combining the convenience of DOM with the speed and fluidity of SAX.

- https://github.com/node-formidable/formidable
  - A Node.js module for parsing form data, especially file uploads.

- https://github.com/staltz/xstream /ts
  - An extremely intuitive, small, and fast functional reactive stream library for JavaScript
  - Only 26 core operators and factories
  - Tailored for Cycle.js, or applications with limited use of subscribe

- https://github.com/joewalnes/smoothie
  - http://smoothiecharts.org/
  - a really small charting library designed for live streaming data. 
  - I built it to reduce the headaches I was getting from watching charts jerkily updating every second.

## json

- https://github.com/jgranstrom/zipson /ts
  - a drop-in alternative to `JSON.parse/stringify` with added compression and streaming support.

- https://github.com/ibmruntimes/yieldable-json /js
  - Asynchronous JSON parser and stringify APIs that make use of generator patterns
  - This library provides asynchronous version of standard `JSON.parse` and `JSON.stringify` APIs.

- https://gitlab.com/philbooth/bfj /js
  - Big-Friendly JSON. Asynchronous streaming functions for large JSON data sets.
  - If you need to parse huge JSON strings or stringify huge JavaScript data sets, it monopolises the event loop and can lead to out-of-memory exceptions.
  - BFJ implements asynchronous functions and uses pre-allocated fixed-length arrays to try and alleviate those issues.
  - Is it fast?
    - No. BFJ yields frequently to avoid monopolising the event loop, interrupting its own execution to let other event handlers run. The frequency of those yields can be controlled with the yieldRate option, but fundamentally it is not designed for speed.

- https://github.com/uhop/stream-json /js
  - It can parse JSON files far exceeding available memory streaming individual primitives using a SAX-inspired API.
  - `jsonl/Parser` parses a JSONL file producing objects similar to StrIt can parse JSON files far exceeding available memory.
  - a micro-library of node.js stream components with minimal dependencies for creating custom data processors oriented on processing huge JSON files while requiring a minimal memory footprint. 
  - Streaming SAX-inspired event-based API is included as well.

- https://github.com/jimhigson/oboe.js /js
  - Oboe.js is an open source Javascript library for loading JSON using streaming, combining the convenience of DOM with the speed and fluidity of SAX.

- https://github.com/plantain-00/stringify2stream
  - A js library to stringify json to stream to avoid out-of-memory of JSON.stringify.

## generator

- https://github.com/TomerAberbach/lfi
  - A lazy functional iteration library supporting sync, async, and concurrent iteration.

- https://github.com/0no-co/wonka
  - A tiny but capable push & pull stream library for TypeScript and Flow, loosely following the callbag spec

- https://github.com/staltz/callbag-basics
  - /1.5kStar/MIT/201711/js
  - allbag is just a spec, but callbag-basics is a real library you can use.
  - https://github.com/callbag/callbag
    - A standard for JS callbacks that enables lightweight observables and iterables
    - Callbag中的source可以转换成RxJS的Observable

- https://github.com/mafintosh/tar-stream
  - a streaming tar parser and generator.

## buffer

- https://github.com/sindresorhus/into-stream
  - Convert a string/promise/array/iterable/asynciterable/buffer/typedarray/arraybuffer/object into a stream

- https://github.com/sindresorhus/to-readable-stream
  - Convert a string/Buffer/Uint8Array to a readable stream

- https://github.com/rvagg/bl
  - bl is a storage object for collections of Node Buffers, exposing them with the main Buffer readable API. 
  - Also works as a duplex stream so you can collect buffers from a stream that emits them and emit buffers to a stream that consumes them!

- https://github.com/sindresorhus/get-stream
  - Get a stream as a string, buffer, or array
  - This module accepts a stream instead of being one and returns a promise instead of using a callback. 
  - it doesn't depend on the huge readable-stream package.

- https://github.com/jferrl/stream-to-buffer
  - converts a Node.js Readable to buffer

- https://github.com/mike-marcacci/fs-capacitor
  - FS Capacitor is a filesystem buffer for finite node streams. 
  - It supports simultaneous read/write

- https://github.com/aldipermanaetikaputra/simple-line-reader
  - Simple, buffered, line-by-line file reader with customizable buffer size.

- https://github.com/aldipermanaetikaputra/linereader2
  - Asynchronous, buffered, line-by-line file reader with customizable buffer size and separator.

- https://github.com/aldipermanaetikaputra/simple-chunk-reader
  - Simple, buffered, chunk-by-chunk file reader with customizable buffer size.

## html

- https://github.com/snappyjs/node-xml-stream /js
  - A tiny simple and fast XML/HTML stream parser with an easy-to-use interface (using NodeJS streams)
  - It is a perfect match for use in feed parsers (e.g. ATOM/RSS/RDF)
  - If you need a parser that is more heavy-weight with more functionality I recommend node-sax-js

- https://github.com/marko-js/writable-dom
  - write a stream of raw HTML chunks into an existing element in the DOM. 
  - Each chunk of HTML is handled in a way that is similar to how browsers process and display it.

- https://github.com/justinwilaby/sax-wasm /rust/ts
  - The first streamable, low memory XML, HTML, JSX and Angular Template parser for WebAssembly.
  - Inspired by sax js and rebuilt with Rust for WebAssembly, sax-wasm brings optimizations for speed and support for JSX syntax.

- https://github.com/mscdex/busboy /js
  - A streaming parser for HTML form data for node.js
  - A node.js module

- https://github.com/popeindustries/lit /js
  - Fast server-rendering and client-hydration of lit-html templates and web components
# concurrency/async
- https://github.com/sindresorhus/p-queue
  - Promise queue with concurrency control
  - For servers, you probably want a Redis-backed job queue instead.

- https://github.com/sindresorhus/p-limit
  - Run multiple promise-returning & async functions with limited concurrency

- https://github.com/andywer/threads.js /ts
  - Make web workers & worker threads as simple as a function call.
  - Offload CPU-intensive tasks to worker threads in node.js, web browsers and electron using one uniform API.
  - Uses web workers in the browser, worker_threads in node 12+ and tiny-worker in node 8 to 11.

- https://github.com/austinksmith/Hamsters.js /564Star/Artistic/202310/js
  - https://www.hamsters.io/
  - 100% Vanilla Javascript Multithreading & Parallel Execution Library
  - Node.js, ReactNative
  - Inside existing worker threads (Threading inside Threads)

## task-scheduler/dag

- https://github.com/caolan/async
  - Async utilities for node and the browser

- https://github.com/observablehq/runtime
  - The Observable dataflow runtime.

- https://github.com/ThomWright/balamb
  - Concurrently run a set of dependent, asynchronous tasks with type-safe dependencies

- https://github.com/alephnan/viae.ts
  - a library to define a directed-acyclic-graph of async functions. 
  - The library efficiently visits the graph, performing dependency injection and unwrapping of promises along the way.

- https://github.com/fibo/dflow
  - a minimal Dataflow programming engine
    - A node represents a block of code: it can have inputs and outputs.
    - An edge connects an input to an output.
    - A graph represents a program. It can contain nodes and edges. Nodes are executed, sorted by their connections.
  - A graph can be saved as a JSON file. It can be then loaded and executed.
  - it is supposed that you implement your own nodes
- https://github.com/fibo/flow-view
  - a visual editor for Dataflow programming
  - Nodes and edges can be created via API

- https://github.com/lukehutch/tiny-reactive-dataflow /202210/js
  - A tiny reactive dataflow library for asynchronously scheduling a Directed Acyclic Graph (DAG) of functions in Javascript.
  - works similarly to React's state change propagation algorithm; 
  - All computation is fundamentally DAG-structured, consisting of **edges**, which are data dependencies between values, and **nodes**, representing both a function and the result of computing that function on specific inputs to produce the value at the node.
  - Dependencies are specified using a "pull model" (a function depends upon, or pulls from, its parameters), but computation is driven using a "push model", with changes propagating from upstream nodes to downstream nodes.
  - Create all dataflow nodes as (optionally async) functions, or as "named lambdas", and register them
    - Function names are used as node names. 
    - Function parameter names refer to the node names of upstream dependencies. 

- https://github.com/wangqiangplus/dagrunner
  - dag task runner based puppeteer
  - api request
  - element selector

- jerosoler/Drawflow /3.2kStar/MIT/202206/js/inactive
  - https://github.com/jerosoler/Drawflow
  - https://jerosoler.github.io/Drawflow/
  - Drawflow allows you to create data flows easily and quickly.
  - Data sync on Nodes
  - Vanilla javascript (No dependencies)
  - [A simple example showing execution of the flow created using drawflow](https://github.com/jerosoler/Drawflow/issues/543)

- https://github.com/glebec/batching-toposort /201903/js/NoDeps
  - Efficiently sort interdependent tasks into a sequence of concurrently-executable batches.
  - Errors on cyclic graphs
    - Batching-Toposort expects a directed acyclic graph (DAG) implemented via **adjacency list**. 
    - In other words, construct an object whose keys are dependency IDs, and whose values are lists of dependent IDs.
  - Motivation
    - Often one needs to schedule interdependent tasks. 
    - In order to determine task order, the classic solution is to use topological sort. 
    - However, toposort typically outputs a list of individual tasks, without grouping those that can be executed concurrently. 
    - Batching-Toposort takes this additional consideration into account, producing a list of lists of tasks. 
    - The outer list is ordered; each inner list is unordered.

- https://github.com/datavis-tech/topologica /201811/js
  - Minimal library for reactive dataflow programming. 
  - Based on topological sort.
  - Topologica is primarily intended for use in optimizing interactive data visualizations created using D3.js and a unidirectional data flow approach. 
    - The problem with using unidirectional data flow with interactive data visualizations is that it leads to unnecessary execution of heavyweight computations over data on every render. 
    - Topologica.js lets you improve performance by only executing heavy computation and rendering operations when they are actually required.
    - It also allows you to simplify your code by splitting it into logical chunks based on reactive functions, and makes it so you don't need to think about order of execution at all.
  - Why use topological sorting? To avoid inconsistent state.
    - propagation using breadth-first search would cause e to be set twice, and the first time it would be set with an inconsistent state 

- https://github.com/mtomran/dep-resolver
  - A modified version of Kahn's algorithm for topological sorting to resolve dependencies of asynchronous tasks.

- https://github.com/daanmichiels/promiseDAG /201710/js
  - Generalization of JavaScript's Promise.all() to directed acyclic graphs
  - https://github.com/vvvvalvalval/promise-dag
  - https://github.com/SidBala/dagmise

- https://github.com/qualiancy/breeze-dag /201211/js
  - Async flow control for directed-acyclic-graph iteration.

## dataflow/reactive/functional-programming

- https://github.com/hoplon/javelin /202310/clojure
  - Spreadsheet-like dataflow programming in ClojureScript

- https://github.com/Day8/re-frame /202311/clojure
  - a ClojureScript framework for building user interfaces. It has a data-oriented, functional design.

- https://github.com/observablehq/runtime /ISC/js
  - The Observable runtime lets you run Observable notebooks as true reactive programs in any JavaScript environment

## excel/sheet-formula

- https://github.com/snapview/sunrise /MIT/202206/ts
  - Spreadsheet-like dataflow programming in TypeScript
  - Sunrise provides a spreadsheet-like computing environment consisting of source cells and formula cells and introduces the Cell interface to represent both

- https://github.com/taggon/tiny-formula /ts/NoDeps
  - A toolset for parsing excel-like formula and calculating with custom functions.

- https://github.com/elis/djit /202005/js/inactive
  - Javascript Spreadsheet Engine
  - Create an Excel-like object in Javascript that automagically computes itself whenever updated.
  - [I made a Spreadsheet engine in Javascript](https://www.reddit.com/r/javascript/comments/g4o075/i_made_a_spreadsheet_engine_in_javascript/)
# stream-examples
- https://github.com/nagix/chartjs-plugin-streaming
  - Chart.js plugin for live streaming data

- https://github.com/Ziv-Barber/officegen
  - Standalone Office Open XML files (Microsoft Office 2007 and later) generator for Word (docx), PowerPoint (pptx) and Excell (xlsx) in javascript. 
  - The output is a stream.
  - officegen should work on any environment that supports Node.js including Linux, OSX and Windows. 
  - officegen also supporting PowerPoint native charts objects with embedded data.

- https://github.com/eclipse/streamsheets /js
  - An open-source tool for processing stream data using a spreadsheet-like interface.

- https://github.com/paulmillr/readdirp
  - Recursive version of `fs.readdir`. Exposes a stream API and a promise API.

- https://github.com/davidgatti/How-to-Stream-Movies-using-NodeJS
  - a very quick and easy article explaining how to stream movies to an HTML 5 video tag using NodeJS
# storage
- https://github.com/maxogden/abstract-blob-store /js/inactive
  - A test suite and interface you can use to implement streaming file (blob) storage modules for various storage backends and platforms.
  - The goal of this module is to define a de-facto standard streaming file storage/retrieval API. Inspired by the abstract-leveldown module

- https://github.com/hackergrrl/append-only-log /js/inactive
  - Abstract interface for an append-only log.
  - Like abstract-blob-store, but for append-only logs.

- https://github.com/debezium/debezium /java
  - https://debezium.io/
  - provides a low latency data streaming platform for change data capture (CDC). 
  - You set up and configure Debezium to monitor your databases, and then your applications consume events for each row-level change made to the database. 
  - Only committed changes are visible
  - since Debezium records the history of data changes in durable, replicated logs, your application can be stopped and restarted at any time, and it will be able to consume all of the events it missed while it was not running
  - Monitoring databases and being notified when data changes has always been complicated. 
    - Relational database triggers can be useful, but are specific to each database
    - Debezium provides modules that do this work for you. 
    - Some modules are generic and work with multiple database management systems
    - Other modules are tailored for specific database management systems
# more
