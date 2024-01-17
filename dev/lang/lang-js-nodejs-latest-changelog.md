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

## v22.0.0_202404

- ### v21.0.0_20231017
  - [Node.js 21 is now available! | Node.js](https://nodejs.org/en/blog/announcements/v21-release-announce)

- ESM: `--experimental-default-type` flag to flip module defaults
  - Input that is already explicitly defined as ES modules or CommonJS, such as by a package.json "type" field or `.mjs/.cjs` file extension or the --input-type flag, is unaffected. 
  - extensionless files are interpreted as WebAssembly if `--experimental-wasm-modules` is passed
- Module customization hook `globalPreload` removed; use `register` and `initialize` instead
  - use `register` to send data from the application thread to the customization hooks, and the `initialize` hook to establish a communications channel between the threads.
- Stable `fetch/WebStreams`.
  - Both modules were marked as stable
  - This impacts WebStreams, FormData, Headers, Request, Response, and fetch.
- A experimental browser-compatible WebSocket implementation arises with this release
  - `--experimental-websocket`.
- Add `flush` option to `fs.writeFile` function
  - When writing to files, it is possible that data is not immediately flushed to permanent storage. This allows subsequent read operations to see stale data.
  - forces the data to be flushed at the end of a successful write operation.
- introduced the global `navigator` object, enhancing web interoperability. 
  - Now, developers can access hardware concurrency information through `navigator.hardwareConcurrency`
- Support for globs in the Node.js test runner
- updates of the V8 JavaScript engine to 11.8, which is part of Chromium 118

## v20.0.0_20230418

- [v20.11.0_2024-01-09](https://nodejs.org/en/blog/release/v20.11.0)
  - esm: add `import.meta.dirname` and `import.meta.filename`.
    - https://twitter.com/meijer_s/status/1745727753964462431
    - IMO `import.meta.url` is sufficient, but might as well use `filename` and `dirname` if they exist.
    - `import.meta.url` is sufficient, `import.meta.filename` is convenient. Not all abstractions are bad
    - No more `path.dirname(fileURLToPath(import.meta.url))`;
  - fs: add c++ fast path for writeFileSync utf8
  - stream: use Array for Readable buffer

- v20.0.0_2023-04-18
  - [Node.js 20 is now available! | Node.js](https://nodejs.org/en/blog/announcements/v20-release-announce)
  - Experimental Permission Model
    - Restrict access to the filesystem/child_process/worker_threads/native-addons
  - Custom ESM loader hooks nearing stable
    - Custom ES module lifecycle hooks supplied via loaders (`--experimental-loader=./foo.mjs`) now run in a dedicated thread, isolated from the main thread
    - In alignment with browser behavior, `import.meta.resolve()` now returns synchronously
  - Stable Test Runner
  - Experimental SEA/Single Executable Apps
  - V8 JavaScript engine updated to 11.3
  - Ada to 2.0

- v19.7.0_2023-02-21
  - Node.js supports the creation of single executable applications by allowing the injection of a JavaScript file into the node binary. 
    - doesn't require node to be installed locally.
    - The single executable application feature only supports running a single embedded CommonJS file.

- v19.6.0_2023-02-03
  - ✨ Includes `npm@9.4.0` adding a new option for installations similar to pnpm/yarn

- v19.0.0_2022-10-18
  - [Node.js 19 is now available! | Node.js](https://nodejs.org/en/blog/announcements/v19-release-announce)
  - `node --watch` support for running in ‘watch’ mode
  - Node.js has removed the `--experimental-specifier-resolution` flag. Its functionality can now be achieved via custom loaders.
  - The WebCrypto API is now stable 
  - The `node:test` module supports mocking during testing via a top-level `mock` object.
  - Starting with this release, Node.js sets `keepAlive` to true by default
    - The default keep-alive duration is 5 seconds.
    - Node.js HTTP server will now automatically disconnect idle clients (which are using HTTP Keep-Alive to reuse the connection) when close() is invoked.
  - V8 engine is updated to version 10.7, which is part of Chromium 107. This version includes a new feature to the JavaScript API: `Intl.NumberFormat`.
  - Node.js 19 ships with npm@8.19.2

## v18.0.0_20220418

- ✨ Global `fetch` enable by default, inspired by node-fetch
- Core `test` runner module to write the unit tests and report results in Test Anything Protocol (TAP) format. 
- experimental JSON Import Assertions
- experimental Web Streams API
- global Blob, BroadcastChannel
- server.headersTimeout/requestTimeout

- v17.5.0
  - importing a JSON file is possible using Import Assertions
    - `node --experimental-json-modules ./your-file.json`.
    - [Import Assertions - Chrome Platform Status, from v91](https://chromestatus.com/feature/5765269513306112)

## v16.0.0_20210420

- v16.5.0_2021-07-14
  - Web Streams API: An implementation of the WHATWG Streams Standard.
    - ReadableStream
    - WritableStream
    - TransformStream
  - [v16.15.1 removing the --experimental-json-modules flag](https://stackoverflow.com/questions/73824694/node-16-is-the-experimental-json-modules-cli-flag-still-required)

- v16.0.0_2021-04-20
  - Stable `AbortController` implementation based on the AbortController Web API
  - Stable Timers Promises API, removing the need to use util.promisify()
  - Experimental Web Crypto API
  - ✨ npm v7 support workspaces
  - Node.js will run natively on the Apple M1

## v14.0.0_20200421

- v14.17.0
  - `crypto.randomUUID` added

- v14.0.0_2020-04-21
  - Experimental `AsyncLocalStorage` API
    - In other languages, it is the same as thread-local storage.
    - used to share data between asynchronous calls.
    - This can be considered as a global variable related to a particular asynchronous execution context.
  - Experimental Web Assembly System Interface (WASI)
  - Changes to Stream APIs for maintaining streamline behaviors and vagueness over the various pieces of Node.js core.
  - GitHub (owned by Microsoft) acquired npm

## v12.0.0_20190423

- Faster async/await implementation
- Async stack traces came
- Default HTTP parser switched to llhttp
- Node 11.0.0 adds `queueMicrotask` as experimental
- Deno, a new way to JavaScript

## v10.0.0_20180424

- es module `.mjs` experimental support
- Node.js can HTTP/2 push
- npm v6

## v8.0.0_20170530

- the year of mainstream adoption
- N-API: Next generation Node.js APIs for native modules
- HTTP2 Arrives into the Node.js Core
- V8 introduces Node.js in its testing suite, officially making Node.js a target for the JS engine, in addition to Chrome
- npm focuses more on security

- v7.6.0_2017-02-21
  - ✨ async/await support

## v6.0.0_20160426

- The leftpad incident
- yarn released

## v4.0.0_20150908

- Node v4.2.0, first Long Term Support release
- IO.js is merged back into Node.js
- npm introduces private modules

## v0.x_20090303

- v0.10.0_20130311
  - koa released
  - ghost blogging
  - MEAN stack
  - in-2014: major fork io.js, with the motive of introducing ES6 support and moving faster

- v0.x.x_20090303
  - first presentation on Node.js from Ryan Dahl at JSConf
  - First very early preview of npm
  - in-2010: express, socket.io
  - in-2011: npm v1, used by linkedin/uber
  - in-2012: hapi
# more-nodejs-changelog
- [History of Node.js on a Timeline, from 2009 until now (June, 2019)](https://blog.risingstack.com/history-of-node-js/)

- [The History of Node.js_202008](https://www.section.io/engineering-education/history-of-nodejs/)
