---
title: lib-collab-yjs-hocuspocus-community
tags: [community, hocuspocus, yjs]
created: 2023-03-15T15:51:43.944Z
modified: 2023-03-15T15:52:29.437Z
---

# lib-collab-yjs-hocuspocus-community

# guide

# discuss-stars
- ## 

- ## 
# discuss-scaling
- ## 

- ## 

- ## 

- ## [Y-redis: An alternative backend to y-websocket - Show - Yjs Community _202403](https://discuss.yjs.dev/t/y-redis-an-alternative-backend-to-y-websocket/2509)
  - I just released y-redis - an alternative backend for y-websocket that is easy to scale and doesn’t keep data in-memory. 
  - It shows how you can implement auth, and it enables you to setup your own auth. 
  - I’ve made a lot of iterations on y-redis over the years. This is the first time I’m happy with my implementation.
  - Please note that there are other backends to y-websocket, that probably provide better support (e.g. y-sweet).

- Is it possible to combine hocuspocus and y-redis? I have Hocuspocus instance and I want to improve my performance with y-redis. Is it possible?
  - Nope, it’s either one. But hocuspocus has a redis-extension as well 

- ## [address horizontal scalability in documentation _202304](https://github.com/ueberdosis/hocuspocus/issues/575)

- ## [Need Single Websocket Connection to open different docs _202212](https://github.com/ueberdosis/hocuspocus/issues/460)
- Right now Hocuspocus is developed in a way that it opens a new connection when you open a document. 
  - In our React SPA platform people regularly switching between documents. 
  - Now on changing on document the existing connection closes and a new connection is built. 
  - Which gives a feeling of a very slow document load. 
  - Because the Initial Connection Time, DNS Resolving, SSL Handshake etc takes approx 300-500 ms. 
  - Now if the documents can change within a single connection, all that time can give it a very fast impression.

- If this is added I would hope its optional.
  - Currently I am load balancing documents on the server across multiple hocuspocus instances each on its own process, each document is only ever open on one instance at a time.
  - If a user could change documents along their existing websocket connection that would break this as it would bypass the load balancer and allow them to force the document open on the wrong process.

- I've already played around here a bit, but figured that this requires some major rewrite of both the server and the client, as connections are tightly coupled with the document right now.

- ## [Use 1 WS connection to fetch documents instead of establishing connection for each documents _202205](https://github.com/ueberdosis/hocuspocus/issues/343)
  - Right now hocuspocus provider opens WS connection each time the document needs to change, instead, it should use one connection to handle document changes.
  - In addition to that, hocuspocus provider should have a plugin system like hocuspocus server where it should be possible to store documents in memory/browser's local storage or implement offline capabilities.
- ✨ [Release Multiplexing - now in v2.beta · ueberdosis/hocuspocus _202303](https://github.com/ueberdosis/hocuspocus/releases/tag/v2.0.0-beta.0)
  - Multiplexing has been used in a few test projects now and is considered working. 

- ## [Redis Scaling _202108](https://github.com/ueberdosis/hocuspocus/issues/178)
  - In an ideal world you would be able to add the Redis extension, provide connection details for a redis instance or cluster and then spin up as many instances of the hocuspocus server as you like behind a loadbalancer. The Redis library would do all of the work of keeping documents in sync between instances.

- The other issue for my usage of Yjs/Hocuspocus at least is that my documents are large and the server is stateful. 
  - currently stopping me from running multiple workers of hocuspocus to take advantage of all my server's cores, as I can't afford to have every document be in memory multiple times.

- [Horizontal scalability approach _202107](https://github.com/ueberdosis/hocuspocus/discussions/133)
- We’re waiting for a y-redis rewrite from Kevin, and will start tackling that then. The HA setup we aim for is multiple hocuspocus nodes in the front with a hocuspocs worker (e.g. for Webhooks) in the background.

- ## [scaling hocuspocus _202104](https://github.com/ueberdosis/hocuspocus/issues/87)
- There were a few questions already about how to scale hocuspocus. The Redis extension is a start, but we still need to figure a lot of things out. In my opinion, this is how it should be done at the moment:
  - Have a load balancer as entrypoint
  - Have multiple nodes with hocuspocus running only the Redis extension behind the load balancer - Let's call them "workers"
  - Have a single node with hocuspocus running the Redis extension, RocksDB extension and any application integrations like the onConnect hook or the webhook extension. This node is not connected to the load balancer - Let's call it "manager"
- This way, all incoming traffic is split equally between the workers.

- I’m working on that thing, but I’m closing the issue here as it’s too broad. Feel free to follow up with questions though.
# discuss
- ## 

- ## 

- ## 
