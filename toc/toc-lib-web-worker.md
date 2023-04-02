---
title: toc-lib-web-worker
tags: [lib, toc, web-worker]
created: 2020-12-19T18:21:50.241Z
modified: 2020-12-19T18:22:27.577Z
---

# toc-lib-web-worker

# worker-web

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
# worker-react
- https://github.com/dai-shi/react-hooks-worker
  - React custom hooks for web workers.
# worker-utils
- https://github.com/Mng12345/webworker-test
  - performance of every worker under different threads number
# worker-node

# more
