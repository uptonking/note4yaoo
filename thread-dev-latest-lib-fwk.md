---
title: thread-dev-latest-lib-fwk
tags: [dev, framework, latest, lib, thread, toc]
created: 2021-09-24T06:49:35.028Z
modified: 2021-09-24T06:50:06.230Z
---

# thread-dev-latest-lib-fwk

# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Introducing Sandpack 2.0 and Nodebox, a Node.js runtime for any browser.
- https://twitter.com/codesandbox/status/1626304039251062785
  - Run Node.js in any browser, any device
  - Nodebox is the first runtime that allows you to run Node.js in any browser, any context, and any application 
  - One of the biggest challenges of enabling this was performance. So, we took the time to redesign the Sandpack transpiler using Rust, refined our caching and made many other optimizations.

- ## Introducing Partytown: Run Third-Party Scripts From a Web Worker
- https://twitter.com/adamdbradley/status/1441069845559140355
  - Relocate third-party scripts into a web worker 
  - Synchronous main thread DOM ops from the worker
  - Sandbox and isolate scripts, control DOM access
  - React/Next.js or no framework at all
  - Lazy loaded 6kb library
  - [Partytown: Run Third-Party Scripts From a Web Worker](https://dev.to/adamdbradley/introducing-partytown-run-third-party-scripts-from-a-web-worker-2cnp)
- partytown uses sync XHR under the hood via a proxy to facilitate DOM access from a worker. 
