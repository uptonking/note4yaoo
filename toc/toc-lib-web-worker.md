---
title: toc-lib-web-worker
tags: [lib, toc, web-worker]
created: 2020-12-19T18:21:50.241Z
modified: 2020-12-19T18:22:27.577Z
---

# toc-lib-web-worker

# guide

- worker-usecase
  - Use web worker for Excel export 

- resources
  - https://github.com/deebloo/things-you-can-do-in-a-web-worker
# worker-web
- https://github.com/albertodeago/cloc-web
  - https://cloc-web.netlify.app/
  - The objective of this project is to implement a simple CLOC application using WebWorkers to keep the UI interactive and the new WebFileSystemAPI to let the user select the project from the local file-system.

- https://github.com/StudentOfJS/query-plus
  - fetch and process data in web worker, store in indexedDB.
  - We created Query+ as a React hook library, to make fetching, processing and caching data as easy as possible.

- https://github.com/ampproject/worker-dom
  - /2.6kStar/Apache2/202012/ts
  - The same DOM API and Frameworks you know, but in a Web Worker.
  - An in-progress implementation of the DOM API intended to run within a Web Worker.
  - Purpose: Move complexity of intermediate work related to DOM mutations to a background thread, 
    - sending only the necessary manipulations to a foreground thread.
  - usecase
    - Embedded content from a third party living side by side with first party code.
    - Mitigation of expensive rendering for content not requiring synchronous updates to user actions.
    - Retaining main thread availability for high priority updates by async updating elsewhere in a document.

- https://github.com/johnny-quesada-developer/easy-web-worker
  - This library extends the capabilities of the Worker by integrating a pattern of cancelable promises from the library cancelable-promise-jq.
  - https://github.com/johnny-quesada-developer/easy-web-workers-example

- https://github.com/worker-tools/parsed-html-rewriter
  - A DOM-based implementation of Cloudflare Worker's HTMLRewriter.
  - this implementation parses the entire DOM (provided by linkedom), and runs selectors against this representation.
  - As a result, it is slower, more memory intensive, and can't process streaming data.
- https://github.com/worker-tools/html-rewriter
  - WASM-based implementation of Cloudflare's HTML Rewriter for use in Deno, browsers, etc.

- https://github.com/cloudflare/lol-html /rust
  - Low Output Latency streaming HTML rewriter/parser with CSS-selector based API.
  - It is designed to modify HTML on the fly with minimal buffering. 
  - It can quickly handle very large documents, and operate in environments with limited memory resources. 

- https://github.com/bvaughn/js-worker-search
  - Full text client-side search based on js-search but with added web-worker support for better performance.
# worker-examples
- [Excel export web worker script](https://gist.github.com/damoresa/77b40cd393d1606ea10c92a4d802d32c)

- https://github.com/dai-shi/react-worker-components
  - React Worker Components simplify using Web Workers

- https://github.com/dai-shi/react-hooks-worker
  - React custom hooks for web workers.

- https://github.com/alewin/useWorker
  - Use web workers with react hook

- https://github.com/sws2apps/react-sw-helper
  - A pure react component for managing service worker life cycle. 

- https://github.com/gustavodomenico/web-worker-sorting /js
  - Application to show the usage of web workers and how to have responsive UIs while doing some heavy computation in the background.

- https://github.com/cranx/profiles-search /vue/js
  - A simple application that demonstrates responsive real-time filtering of a large list using a virtual list and a web worker

- https://github.com/bloomberg/ipydatagrid
  - Fast Datagrid widget for the Jupyter Notebook and JupyterLab
  - [I see some cons using Web Workers like it is done in ipysheet](https://github.com/bloomberg/ipydatagrid/issues/3)
# worker-utils
- https://github.com/BuilderIO/partytown
  - Relocate resource intensive third-party scripts off of the main thread and into a web worker

- https://github.com/worker-tools/workers.js.org
  - Worker Runtimes are an adaptation of the Service Workers API, which is a browser standard for offline web applications. 
  - To give web developers more freedom over offline experiences, the specification includes a (minimal) HTTP server. 
  - Typically, they also implement other browser APIs such as Fetch, Streams, and Web Cryptography, making their global scope similar to that of a Service Worker. We call them Worker Runtimes or Worker Contexts.

- https://github.com/alberto-f/workerpubsub
  - Main and Web Worker thread communication through a pubsub implementation.

- https://github.com/stateful/tangle
  - tangle allows to sync states between various components that live in different sandbox environments, e.g. iframes, webworkers, worker threads or VSCode webviews. 
  - It simplifies the communication between these sandboxes drastically. 
  - The package was mainly developed to help share data between various of webviews within a VSCode extension.

- https://github.com/Mng12345/webworker-test
  - performance of every worker under different threads number

- https://github.com/tbela99/workerize
  - Export a class or function into a web worker

- https://github.com/dumbmatter/promise-worker-bi
  - Promise-based messaging for Web Workers and Shared Workers
  - performant library for communicating with web workers and shared workers, using promises. 
  - This is based on promise-worker which only allows you to send messages from the browser to the worker, not in reverse. This library allows both

- https://github.com/web-perf/react-worker-dom
  - Experiments to see the advantages of using Web Workers to Render React Virtual DOM
  - Only node updates are sent over to the UI thread, result in a much more responsive UI.
  - I am not actively working on this. 
    - With React Fiber, this may not be relevant. 
    - Also note that there is react-native-dom, which does something similar.

- https://github.com/MattiasBuelens/remote-web-streams
  - Web streams that work across web workers and iframes.
  - With this libray, you can create pairs of readable and writable streams where you can write chunks to a writable stream inside one context, and read those chunks from a readable stream inside a different context. 

- https://github.com/AlloyTeam/alloy-worker
  - 面向事务的高可用 Web Worker 通信框架
# worker-node
- [Support Web Workers · nodejs/node](https://github.com/nodejs/node/issues/43583)
  - Node.js does have `worker_threads`, but the API differs in many ways and it's really difficult to properly bridge them. 
  - There are attempts at bridging these APIs in user-land, but the most popular one is incomplete and not actively maintained.

- https://github.com/developit/web-worker /js
  - Native cross-platform Web Workers. 
  - In the browser, it's simply an alias of Worker.
  - In Node, it's a web-compatible Worker implementation atop Node's worker_threads.
# service-worker
- https://github.com/mswjs/msw
  - a seamless REST/GraphQL API mocking library for browser and Node.js.
  - Use Express-like routing syntax to capture requests. 
  - Utilizing the Service Worker API, which can intercept requests for the purpose of caching, Mock Service Worker responds to captured requests with your mock definition on the network level. 

- https://github.com/GoogleChrome/workbox /ts/inactive
  - JavaScript libraries for Progressive Web Apps
  - Introducing Workbox, a set of modules that simplify common service worker routing and caching.
  - [Workbox - Chrome Developers](https://developer.chrome.com/docs/workbox/)

- https://github.com/gauntface/simple-push-demo /js
  - A simple example of use push notifications on the web using Service Workers

- https://github.com/hanford/next-offline
  - make your Next.js application work offline using service workers via Google's workbox

- https://github.com/jcubic/wayne /js
  - Service Worker Routing library for in browser HTTP requests
  - It's like Express inside Service Worker.
  - Most of the time Service Worker is used for caching of HTTP requests and making the app work when there is no internet (mostly for PWA), 
    - but in fact you can create completely new responses to requests that never leave the browser. 
    - This library make that easier by adding simple API similar to Express.
# sandbox
- https://github.com/slashd-analytics/run
  - Run is a tiny library that runs user-provided code into a Web Worker.

- https://github.com/markwylde/workerbox
  - A secure sandbox to execute untrusted user JavaScript, in a web browser, without any risk to your own domain/site/page.
# more
