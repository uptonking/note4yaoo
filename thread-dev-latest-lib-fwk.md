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

- ## 

- ## Introducing Partytown: Run Third-Party Scripts From a Web Worker
- https://twitter.com/adamdbradley/status/1441069845559140355
  - Relocate third-party scripts into a web worker 
  - Synchronous main thread DOM ops from the worker
  - Sandbox and isolate scripts, control DOM access
  - React/Next.js or no framework at all
  - Lazy loaded 6kb library
  - [Partytown: Run Third-Party Scripts From a Web Worker](https://dev.to/adamdbradley/introducing-partytown-run-third-party-scripts-from-a-web-worker-2cnp)
- partytown uses sync XHR under the hood via a proxy to facilitate DOM access from a worker. 
