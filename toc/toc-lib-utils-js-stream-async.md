---
title: toc-lib-utils-js-stream-async
tags: [async, lang-js, stream, toc, utils]
created: 2023-04-04T22:36:09.902Z
modified: 2023-04-04T22:36:31.529Z
---

# toc-lib-utils-js-stream-async

# guide

- async-sync (push/pull)
  - event/stream/observable/iterator 可作为统一async/sync的思路
  - 模式的选型会影响整个codebase的代码风格
  - 主流库的实现大多基于Promise/async/await，而不是generator

- queue vs setInterval/loop
  - queue内置更多功能，如pause/resume, FIFO顺序
  - 是否需要传输数据，event更容易传输数据
  - queue需要task的fn提前定义，动态add-task的复杂度高，但动态add-task的场景本身就复杂相关业务也复杂
  - 执行的优先级不同
    - setInterval作为macroTask执行fn的时机是下一个event-loop
    - queue如果使用同步方式实现，执行fn的时机是当前event-loop

- queue-features
  - pause/resume
  - concurrency
  - priority
  - persistence
  - dependence
  - dynamic-add-task
# popular
- https://github.com/vercel/resumable-stream /438Star/MIT/202510/ts
  - https://ai-sdk.dev/docs/ai-sdk-ui/chatbot-resume-streams
  - Library for wrapping streams of strings (Like for example SSE web responses) in a way that a client can resume them after they lost a connection, or to allow a second client to follow along.
  - Designed for use in serverless environments without sticky load balancing.
  - The library relies on a pubsub mechanism and is designed to be used with Redis. It was designed to minimize latency impact and Redis usage for the common case that stream recovery is not needed. In that common case the library performs a single `INCR` and `SUBSCRIBE` per stream.
  - How it works
    - The first time a resumable stream is invoked for a given streamId, a standard stream is created. This is now the producer.
    - The producer will always complete the stream, even if the reader of the original stream goes away.
    - the producer starts listening on the pubsub for additional consumers.
    - When a second resumable stream is invoked for a given streamId, it publishes a messages to alert the producer that it would like to receive the stream.
    - The second consumer now expects messages of stream content via the pubsub.
    - The producer receives the request, and starts publishing the buffered messages and then publishes additional chunks of the stream.

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

- https://github.com/TomerAberbach/lfi /apache2/202308/ts
  - A lazy functional iteration library supporting sync, async, and concurrent iteration
  - Lazy: delays applying operations until their results are needed
  - Functional: provides highly composable functions
  - Iteration: supports sync iterables, async iterables, and unique concurrent iterables
  - https://github.com/loganfsmyth/gensync /202010/js
    - This module allows for developers to write common code that can share implementation details, hiding whether an underlying request happens synchronously or asynchronously. 
    - This is in contrast with many current Node APIs which explicitly implement the same API twice, once with calls to synchronous functions, and once with asynchronous functions.

- https://github.com/graphicore/obtainJS /201604/js
  - Framework to unify synchronous and asynchronous JavaScript.

- https://github.com/web-infra-dev/unport /MIT/202407/ts/还可参考openrpc
  - A Universal Port with strict type inference capability for cross-JSContext communication.
  - Unport emerges as a well-architected solution, meticulously designed to simplify the complexity revolving around various JSContext environments.
    - Node.js, ChildProcess, Webview, Web Worker, worker_threads, WebSocket, iframe, MessageChannel, ServiceWorker, and much more.
  - Each of these JSContext environments exhibits distinct methods of communicating with the external world
    - the lack of defined types can make handling the code for complex projects an arduous task.
  - You only need to define the message types (MessageDefinition) and Intermediate communication channel (Channel) that different JSContexts need to pass, and you will get a unified type of Port
    - a MessageDefinition is a crucial concept that defines the structure of the messages that can be sent and received through a Channel.
    - a Channel is a fundamental concept that represents a Intermediate communication pathway between different JavaScript contexts
  - unrpc: Starting with the 0.6.0 release, we are experimentally introducing support for Typed RPC
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
# queue-persistence
- https://github.com/taskforcesh/bullmq /4.8kStar/MIT/202401/ts
  - https://bullmq.io/
  - reliable, Redis-based distributed queue for Node.
  - It is backed by Redis, which makes it easy to scale horizontally and process jobs across multiple servers.
  - BullMQ is a rewrite of the popular Bull library by the same authors, but with a new API and a more modern codebase written in Typescript and with a bunch of new features and performance improvements.
- https://github.com/felixmosh/bull-board /MIT/202402/ts
  - Bull Dashboard is a UI built on top of Bull or BullMQ to help you visualize your queues and their jobs. 
  - With this library you get a beautiful UI for visualizing what's happening with each job in your queues, their status and some actions that will enable you to get the job done.
  - As this library provides only the visualization for your queues, Aside the options to retry and clean jobs, this library is not responsible for processing the jobs, reporting progress or any other thing. This must be done in your application with your own logic; 
  - This library doesn't hijack Bull's way of working.
- https://github.com/OptimalBits/bull /14.8kStar/MIT/202401/js
  - reliable, Redis-based queue for Node.
  - Carefully written for rock solid stability and atomicity.
  - Bull is currently in maintenance mode, we are only fixing bugs. For new features check BullMQ

- https://github.com/agenda/agenda /9.2kStar/MIT/202208/ts/inactive
  - http://agendajs.com/
  - Lightweight job scheduling for Node.js
  - Scheduling with configurable priority, concurrency, repeating and persistence of job results.
  - Event backed job queue that you can hook into.
  - Mongo backed persistence layer.
  - Agenda-rest: optional standalone REST API.
  - originally a fork of agenda.js
  - https://github.com/agenda/agendash /MIT/202304/js/inactive
    - A Dashboard for Agenda.
    - Job status auto-refreshes: 60-second polling by default.

- https://github.com/jhuckaby/Cronicle /MIT/202406/js
  - https://cronicle.net/
  - Cronicle is a multi-server task scheduler and runner, with a web based front-end UI.
  - It handles both scheduled, repeating and on-demand jobs, targeting any number of 🧐 slave servers, with real-time stats and live log viewer.
  - https://github.com/jhuckaby/Cronicle/pull/621
    - Cronicle v0.x is in maintenance-only mode. We are no longer adding any new features, because we are hard at work on the next major version of Cronicle (called Orchestra)
    - It is a complete ground-up rewrite from scratch, and will have MANY of the requested features 
  - https://github.com/jhuckaby/performa
    - a multi-server monitoring system with a web based front-end UI

- https://github.com/breejs/bree /MIT/202405/js
  - https://jobscheduler.net/
  - Bree is a Node.js and JavaScript job task scheduler with worker threads, cron, Date, and human syntax
  - uses worker threads (Node.js) to spawn sandboxed processes, and supports async/await, retries, throttling, concurrency, and cancelable jobs with graceful shutdown. 
  - Made for Forward Email and Lad.
  - Built for @ladjs, @forwardemail, @spamscanner, @cabinjs.

- https://github.com/wakatime/wakaq-ts /BSD/202403/ts/inactive
  - Background task queue for TypeScript backed by Redis, a super minimal Celery
  - For the original Python version, see WakaQ for Python.

- https://github.com/scality/backbeat /apache2/202410/js
  - https://www.zenko.io/
  - the core engine for asynchronous replication, optimized for queuing metadata updates and dispatching work to long-running tasks in the background.
  - Backbeat is an engine with a messaging system at its heart. It's part of Zenko, Scality’s Open Source Multi-Cloud Data Controller

- https://github.com/coleifer/huey /5.7kStar/MIT/202510/python
  - https://huey.readthedocs.io/
  - a little task queue for python
  - examples: mini, falsk, django
  - Although Huey was designed with Redis in mind, the storage system implements a simple API and many other tools could be used instead of Redis if that's your preference.
    - redis, sqlite, file-system, or in-memory storage
  - multi-process, multi-thread or greenlet task execution models
  - schedule tasks to execute at a given time, or after a given delay
  - 实现使用装饰器: `@huey.task(retries=2, retry_delay=60)`.
# concurrency/async
- https://github.com/sindresorhus/p-queue
  - Promise queue with concurrency control
  - For servers, you probably want a Redis-backed job queue instead.
  - 支持pause/concurrency/priority
  - Returns a new queue instance, which is an `EventEmitter3` subclass.
  - 依赖eventemitter3、p-timeout
- https://github.com/sindresorhus/p-limit /MIT/202410/js
  - Run multiple promise-returning & async functions with limited concurrency
  - Works in Node.js and browsers.
  - 🆚 How is this different from the p-queue package?
    - This package is only about limiting the number of concurrent executions, while `p-queue` is a fully featured queue implementation with lots of different options, introspection, and ability to pause the queue.

- https://github.com/poppinss/defer /MIT/202409/ts/adonis
  - A managed deferred queue to run async operations in the background
  - @poppinss/defer package allows you to run async operations in the background using an in-memory queue.
  - Think of it as setImmediate but with support for monitoring, error handling, and the ability to gracefully shutdown process by flushing the queue.
  - You may pause the queue from processing tasks using the `queue.pause` method and resume it using the `queue.resume` method.
  - By default, 10 tasks are processed concurrently
  - 依赖fastq
  - https://github.com/mcollina/fastq /ISC/ISC/202402/js
    - Fast, in memory work queue
    - If you need zero-overhead series function call, check out fastseries. 
    - For zero-overhead parallel function call, check out fastparallel.

- https://github.com/Jcanno/best-queue /MIT/202203/ts/NoDeps/inactive
  - Queue in runtime based promise
  - 支持pause/concurrency

- https://github.com/hajnalben/embedded-queue /MIT/202311/ts/inactive
  - embedded-queue is job/message queue for any platform. 
  - It does not required any other repository for storing data, like Redis, MySQL, and so on.
  - 支持in-memory/nedb/custom
  - [about delay queue · hajipy/embedded-queue](https://github.com/hajipy/embedded-queue/issues/43)
    - 不支持pause
    - how should I suspend the queue
    - In the current implementation, the queue can only process the added jobs immediately. We have found that there is a demand for the new feature, but it cannot be implemented immediately.
  - https://www.npmjs.com/package/@abtnode/queue
    - A simple job queue built on top of nedb and fastq

- https://github.com/BalassaMarton/sequential-task-queue /MIT/201812/ts/inactive
  - FIFO task queue for node and the browser. 
  - Supports promises, timeouts and task cancellation.
  - The primary goal of this component is to allow asynchronous tasks to be executed in a strict, predictable order. 
  - 不支持pause

- https://github.com/XadillaX/scarlet-task /MIT/202409/ts
  - an advanced task queue module for Node.js, featuring the ability to configure multiple child queues for a single task queue.

- https://github.com/andywer/threads.js /MIT/202404/ts/inactive
  - Make web workers & worker threads as simple as a function call.
  - Offload CPU-intensive tasks to worker threads in node.js, web browsers and electron using one uniform API.
  - Uses web workers in the browser, worker_threads in node 12+ and tiny-worker in node 8 to 11.

- https://github.com/austinksmith/Hamsters.js /564Star/Artistic/202310/js
  - https://www.hamsters.io/
  - 100% Vanilla Javascript Multithreading & Parallel Execution Library
  - Node.js, ReactNative
  - Inside existing worker threads (Threading inside Threads)

## scheduler/DAG/topo-sort

- https://github.com/pmndrs/directed /MIT/202506/ts
  - A flexible, minimal scheduler written in TypeScript. 
  - Directed is powered by a directed acyclic graph (DAG) allowing for dependency-based scheduling.
  - Directed supports a functional and class API depending on what is comfy for you.

- https://github.com/nicolas-van/modern-async /MIT/202410/js
  - https://nicolas-van.github.io/modern-async/
  - A modern JavaScript tooling library for asynchronous operations using async/await, promises and async generators
  - This library is a modernized alternative to a lot of libraries like Async.js that were created using the legacy callback style to handle asynchronous operations.
    - Its goal is to be as complete as any of those libraries while being built from the very beginning with async/await and promises in mind.
  - Typescript support

- https://github.com/caolan/async /MIT/202410/js
  - Async utilities for node and the browser
  - https://github.com/suguru03/neo-async /202012/js/inactive
    - drop-in replacement for Async, it almost fully covers its functionality and runs faster

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

## task-flow/multi-engine

- https://github.com/meirwah/awesome-workflow-engines /md
  - A curated list of awesome open source workflow engines
  - saas, bpm, embedded

- https://github.com/danielduarte/flowed /MIT/202309/ts/inactive/依赖少/示例多
  - https://danielduarte.github.io/flowed
  - [flowed/doc/tutorial.md](https://github.com/danielduarte/flowed/blob/main/doc/tutorial.md)
  - https://github.com/danielduarte/flowed/tree/main/test/examples
  - A fast and reliable flow engine for orchestration and more uses in Node.js, Deno and the browser
  - The flow specifications are written in JSON format
  - Flow executions can be paused and resumed with task granularity. The same for stopping and resetting
  - 依赖[flowed-st JSON Selector + Transformer](https://github.com/danielduarte/flowed-st)
  - Asynchronous and synchronous tasks. The flow will take care of promises, waiting for results according to dependencies.
  - Using the Flowed plugin system, any developer can add their own resolver library and easily integrate it into the flow engine.
  - In order to run tasks in parallel, they don't have dependence on each other.
  - you can specify dependence between tasks arbitrarily, not only when one of them needs results from the other.
  - Flows can have cyclic dependencies forming loops. In order to run these flows, external parameters must raise the first execution.
  - https://github.com/danielduarte/flowed-server /依赖loopback
    - Execute Flowed flows as a service.
  - https://github.com/danielduarte/flowed-ui /202003/js/inactive
    - easy to use UI to work with flows made in Flowed
  - https://github.com/danielduarte/flowed-sdk
    - used in browser

- https://github.com/rudderlabs/rudder-workflow-engine /MIT/202410/ts
  - https://transformers-workflow-engine.rudderstack.com/#/workflow-engine
  - A generic embeddable workflow execution engine library
  - To bring standardization, we are building a workflow engine that is config driven to provide improved readability, testability, reusability, and speed of development.
  - Since we want to express the transformation of the logic using easy to read and write template based language. We support following template languages: JSONata, JsonTemplate
  - Users should be able to express the destination transformation logic as a series of steps in a YAML file as a workflow. Steps can be written as template base languages.
  - ❓ 是否与rudder绑定
  - https://github.com/rudderlabs/rudder-transformer /ElasticLic
    - a service which transforms the RudderStack events to destination-specific singular events. 

- https://github.com/iauroSystems/io-flow-core /apache2/202312/ts/inactive
  - designed to automate and manage the flow of tasks, activities, and information within an organization or system. 
  - It serves as a central platform that orchestrates and coordinates the execution of business processes or workflows. 
  - At its core, a IO Flow provides a framework for defining, modeling, and executing workflows
  - 支持mongodb
  - IO Flow can integrate with various external systems, databases, or applications to gather inputs, retrieve or update data, and trigger actions.
  - IO Flow provide real-time monitoring and reporting capabilities, allowing stakeholders to track the progress, performance, and key metrics of workflows.

- https://github.com/cloudb2/processus /MPLv2/201512/js/inactive
  - http://cloudb2.github.io/processus
  - A simple lightweight nodejs workflow engine designed to help orchestrate multiple tasks.

- https://github.com/nodeca/idoit /MIT/202102/js/inactive
  - Redis-backed task queue engine with advanced task control and eventual consistency
  - Task grouping, chaining, iterators for huge ranges.
  - Load distribution + worker pools.

- https://github.com/reverb-app/reverb /MIT/MIT/202404/ts/inactive
  - https://reverb-app.github.io/
  - Reverb is an event-driven, asynchronous workflow engine that orchestrates the logic and infrastructure developers need to build complex background tasks. 
  - Users define tasks as multi-step functions in their repository, and Reverb handles triggering and executing them step-by-step. 
    - The service is self-hosted on Amazon Web Services (AWS) and is deployable with one command using our CLI tool
  - 🏘️ Reverb’s functionality is organized in a three-node pattern. 
    - The three nodes are the Ingress Server, the Graphile Workers Server and the Functions Server.
    - Ingress Server provides API endpoints for enqueueing your application's Reverb triggers, including events and webhooks. It also provides an endpoint for retrieving logs related to your events and workflows
    - Graphile Workers Server hosts Graphile Worker runners that are responsible for managing your Postgres job queue and processing your application's Reverb workflows. These include jobs triggered by events, cron, or steps within the Reverb step functions you've defined
    - Functions Server hosts your application's Reverb workflow definitions and contains all the code needed to create these jobs from the provided template.
    - A function can be a single function invocation or can consist of multiple steps**._ Each step will need to be awaited._**
    - Steps can run code, delay execution, invoke another workflow, or emit an event.

- https://github.com/tabkram/execution-engine /MIT/202312/ts
  - https://tabkram.github.io/execution-engine/
  - a TypeScript library that enables tracing and visualization of code execution workflows in your project. 
  - Gain insights into the dynamic sequence of code execution by capturing detailed traces in JSON format, easily parseable into graphs.
  - [Easily parseable into graphs using tools like json-to-graph online demo.](https://tabkram.github.io/json-to-graph/?data=https%3A%2F%2Fraw.githubusercontent.com%2Ftabkram%2Fjson-to-graph%2Fmain%2Fdata%2Ftrace.json)

- https://github.com/runabol/tork /592Star/MIT/202410/go
  - https://tork.run/
  - Tork is a highly-scalable, general-purpose workflow engine.
  - https://github.com/runabol/tork-web

## dataflow/reactive/functional-programming

- https://github.com/hoplon/javelin /202310/clojure
  - Spreadsheet-like dataflow programming in ClojureScript

- https://github.com/Day8/re-frame /202311/clojure
  - a ClojureScript framework for building user interfaces. It has a data-oriented, functional design.

- https://github.com/observablehq/runtime /ISC/js
  - The Observable runtime lets you run Observable notebooks as true reactive programs in any JavaScript environment

- https://github.com/receptron/graphai /MIT/202410/ts
  - GraphAI is an asynchronous data flow execution engine, which allows developers to build agentic applications by describing agent workflows as declarative data flow graphs in YAML or JSON.
  - agentic applications require making multiple asynchronous API calls (e.g., OpenAI's chat-completion API, database queries, web searches) and managing data dependencies among them
  - GraphAI allows developers to describe dependencies among those agents (asynchronous API calls) in a data flow graph in YAML or JSON, which is called declarative data flow programming

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

## async-sync-converter

- https://github.com/thefrontside/effection /MIT/202409/ts
  - https://frontside.com/effection
  - Structured concurrency and effects for JavaScript
  - Effection leverages the idea of structured concurrency to ensure that you don't leak any resources, effects, and that cancellation is always properly handled. 
  - It helps you build concurrent code that feels rock solid at scale, and it does all of this while feeling like normal JavaScript.
  - Effection runs on all major JavaScript platforms including NodeJs, Browser, and Deno.
  - Unlike Promises and async/await, Effection is fundamentally synchronous in nature, which means you have full control over the event loop and operations requiring synchronous setup remain race condition free.
  - 👉 For every Async/Await/Promise API we provide Structured Concurrency compliant Effection alternative.
  - [Announcing Effection 3.0 -- Structured Concurrency and Effects for JavaScript _202311](https://frontside.com/blog/2023-12-18-announcing-effection-v3/)
    - This new version refines and simplifies the abstractions we first created in version 2.0 while introducing some new ones of exceptional power.
    - the new Context API and an even better TypeScript experience
    - Rebuilt with Delimited Continuations

- https://github.com/dmaevsky/conclure /MIT/202211/js/NoDeps/inactive
  - Brings cancellation and testability to your async flows.
  - It is a tiny (core is < 200 lines of code), zero dependencies generator runner. 
  - Using generators instead of promises allows for a LOT more flexibility, including cancellation, sync resolution, and better testing. The API is strictly the same as `async/await`.
  - 🤼 You should avoid Promises for two major reasons:
    - Promises are greedy: once created, cannot be cancelled
    - `await promise` always inserts a tick into your async flow, even if the promise is already resolved or can be resolved synchronously.
  - You can see a Promise as a particular type of an iterator for which the JS VM provides a built-in runner, a quite poorly designed one nonetheless.
  - Conclure JS is a custom generator runner that
    - allows you to cancel your async flows
    - ensures that sync flows always resolve synchronously
    - delivers better testability through the use of effects as popularized by redux-saga.

- https://github.com/Kaciras/deasync /MIT/202403/cpp/ts
  - Turns async function into sync via JavaScript wrapper of Node event loop
  - DeAsync turns async code into sync, implemented with a blocking mechanism by calling Node.js event loop at JavaScript layer. 
  - The core of deasync is written in C++.

- https://github.com/TomerAberbach/betterator /apache2/202204/ts/inactive
  - A better sync and async iterator API.
  - Familiar: lots of other programming languages use the same API

- https://github.com/un-ts/synckit /MIT/202401/ts
  - Perform async work synchronously in Node.js using `worker_threads` with first-class TypeScript and Yarn P'n'P support.

- https://github.com/thelinuxlich/go-go-try /2020401/ts
  - Tries to execute a sync/async function, returns a Golang style result
  - https://github.com/astoilkov/good-try

- https://github.com/grimmer0125/d4c-queue /202111/ts
  - Wrap an async/promise-returning/sync function as a queue-ready async function, which is enqueued while being called. 
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
- https://github.com/tokio-js/tokio /MIT/202301/ts
  - JavaScript's asynchronous runtime
