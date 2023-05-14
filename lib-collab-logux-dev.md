---
title: lib-collab-logux-dev
tags: [collaboration, logux]
created: 2023-05-14T04:29:05.202Z
modified: 2023-05-14T04:30:34.915Z
---

# lib-collab-logux-dev

# guide

# dev
- tips
  - logux client/server
  - nanostores提供persistent/router/query-fetch/logux-sync
# [Why I created Logux_202003](https://slides.com/ai/why-logux/)
- https://slides.com/ai/logux2#/94
  - logux is not a crdt, not a db
  - it's a framework to implement both

- autoprefixer is stable
  - time for a new adventure

- Simple AJAX works only on localhost
  - A lot of code even for simple edge cases, like loading/error/data

- Let’s forget about AJAX and dream about the perfect state sync for SPA
  - We have stores in our apps
- With extra code to sync state with server
- Feature 1: sync state without extra code
- Feature 2: sync state between tabs by default
- Feature 3: built-in authorization
  - Feature 3a: built-in client version
- Feature 4: Optimistic UI
  - Feature 4a: global UI for network errors
  - Feature 4b: Offline
- Feature 5: Collaborative First Apps
  - Feature 5a: Real-Time Updates
  - Feature 5b: The same changes order

- My own solution for client-server sync
- Proxy server for Web Sockets
- Logux Proxy re-send changes to clients
- Changes have time mark to keep order
# more
