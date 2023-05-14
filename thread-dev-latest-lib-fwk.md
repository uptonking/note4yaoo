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

- ## nextgen web app framework wishlist:
- https://twitter.com/tmcw/status/1485379545276551173
  - webworkers as default for anything that might be cpu-bound
  - service workers, configured in a way that doesn't scare me, unclear
  - realtime data by default, websockets + crdt
  - actual patterns for managing focus & scroll state
- this is for an app, and by that I mean actually-a-complex-dynamic-web-application-not-a-website-or-shopping-cart-or-blog app that seriously, actually works in the client-side app paradigm. that 5-10% of apps that actually make sense with react today.

- As a fan of Rails-when-it-makes-sense, what *would* you use to build figma/linear?
  - react, svelte, webassembly, a crdt like replicache, logux, yjs, state management in jotai or mobx, something like comlink for webworkers.
  - partly the q is bc figma, linear, and vscode are so cutting-edge that their secret sauce(调味汁) is proprietary(专制)/custom, rather than in a framework

- ## Introducing Partytown: Run Third-Party Scripts From a Web Worker_202109
- https://twitter.com/adamdbradley/status/1441069845559140355
  - Relocate third-party scripts into a web worker 
  - Synchronous main thread DOM ops from the worker
  - Sandbox and isolate scripts, control DOM access
  - React/Next.js or no framework at all
  - Lazy loaded 6kb library
  - [Partytown: Run Third-Party Scripts From a Web Worker](https://dev.to/adamdbradley/introducing-partytown-run-third-party-scripts-from-a-web-worker-2cnp)
- partytown uses sync XHR under the hood via a proxy to facilitate DOM access from a worker. 
