---
title: lang-js-nodejs-latest-changelog
tags: [changelog, js, nodejs]
created: 2022-12-31T20:13:07.124Z
modified: 2022-12-31T20:13:33.307Z
---

# lang-js-nodejs-latest-changelog

# guide

- [Node.js ES2015/ES6, ES2016 and ES2017 support](https://node.green/)

- [Node.js Previous Releases with dates](https://nodejs.org/en/download/releases/)
# changelog
- v20.0.0_2023-04-18

- v19.7.0_2023-02-21
  - Node.js supports the creation of single executable applications by allowing the injection of a JavaScript file into the node binary. 
    - doesn't require node to be installed locally.
    - The single executable application feature only supports running a single embedded CommonJS file.

- v19.6.0_2023-02-03
  - ✨ Includes npm@9.4.0 adding a new option for installations similar to pnpm

- v19.0.0_2022-10-18
  - Highlights include the update of the V8 JavaScript engine to 10.7, HTTP(s)/1.1 KeepAlive enabled by default, and ESM Resolution adjusts.
  - The `node:test` module supports mocking during testing via a top-level `mock` object.

- v18.0.0_2022-04-18
  - ✨ Global `fetch` enable by default, inspired by node-fetch
  - experimental Web Streams API
  - global Blob, BroadcastChannel
  - Core `test` runner module to write the unit tests and report results in Test Anything Protocol (TAP) format. 
  - experimental JSON Import Assertions
  - server.headersTimeout/requestTimeout

- v17.5.0
  - importing a JSON file is possible using Import Assertions
    - node --experimental-json-modules ./your-file.js
    - [Import Assertions - Chrome Platform Status, from v91](https://chromestatus.com/feature/5765269513306112)

- v16.5.0_2021-07-14
  - Web Streams API: An implementation of the WHATWG Streams Standard.
    - ReadableStream
    - WritableStream
    - TransformStream

- v16.0.0_2021-04-20
  - Stable `AbortController` implementation based on the AbortController Web API
  - Stable Timers Promises API, removing the need to use util.promisify()
  - Experimental Web Crypto API
  - ✨ npm v7 support workspaces
  - Node.js will run natively on the Apple M1

- v14.17.0
  - crypto.randomUUID added

- v14.0.0_2020-04-21
  - Experimental `AsyncLocalStorage` API
    - In other languages, it is the same as thread-local storage.
    - used to share data between asynchronous calls.
    - This can be considered as a global variable related to a particular asynchronous execution context.
  - Experimental Web Assembly System Interface (WASI)
  - Changes to Stream APIs for maintaining streamline behaviors and vagueness over the various pieces of Node.js core.
  - GitHub (owned by Microsoft) acquired npm

- v12.0.0_2019-04-23
  - Deno, a new way to JavaScript
  - Faster async/await implementation
  - Async stack traces came
  - Default HTTP parser switched to llhttp
  - Node 11.0.0 adds `queueMicrotask` as experimental

- v10.0.0_2018-04-24
  - es module .mjs experimental support
  - Node.js can HTTP/2 push
  - npm v6

- v8.0.0_2017-05-30
  - the year of mainstream adoption
  - N-API: Next generation Node.js APIs for native modules
  - HTTP2 Arrives into the Node.js Core
  - V8 introduces Node.js in its testing suite, officially making Node.js a target for the JS engine, in addition to Chrome
  - npm focuses more on security

- v7.6.0_2017-02-21
  - ✨ async/await support

- v6.0.0_2016-04-26
  - The leftpad incident
  - yarn released

- v4.0.0_2015-09-08
  - Node v4.2.0, first Long Term Support release
  - IO.js is merged back into Node.js
  - npm introduces private modules

- v0.10.0_2013-03-11
  - koa released
  - ghost blogging
  - MEAN stack
  - in-2014: major fork io.js, with the motive of introducing ES6 support and moving faster

- v0.x.x_2009-03-03
  - first presentation on Node.js from Ryan Dahl at JSConf
  - First very early preview of npm
  - in-2010: express, socket.io
  - in-2011: npm v1, used by linkedin/uber
  - in-2012: hapi
# more-nodejs-changelog
- [History of Node.js on a Timeline, from 2009 until now (June, 2019)](https://blog.risingstack.com/history-of-node-js/)

- [The History of Node.js_202008](https://www.section.io/engineering-education/history-of-nodejs/)
