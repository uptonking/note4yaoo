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
# docs
- Logux uses the peer-to-peer model. 
  - There is no big difference between client and server. 
  - This is why we call both client and server “nodes”.
- Logux Core provides BaseNode class, which will synchronize actions between two nodes. 
  - ClientNode and ServerNode classes extend this class with small behaviour changes.
- If a user opens a website with Logux in multiple browser tabs, tabs will elect one leader, and only this leader will keep the connection. If the user closes the leader tab, tabs will re-elect a new leader.

- subscriptions and channels are the main way to get data from the server. 
  - It asks the server to send current data state and re-send all actions with these data changes.
- Channel is just a string like exchange-rate or users/14.
- The client remembers all the subscriptions. If the client loses connection, it will re-subscribe to channels again.
# examples
- https://github.com/logux/examples
  - 仅支持单用户多窗口同步

- https://github.com/zumkorn/logux-simple-app
  - front+back
# more
