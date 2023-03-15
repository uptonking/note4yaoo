---
title: lib-collab-yjs-hocuspocus-community
tags: [community, hocuspocus, yjs]
created: 2023-03-15T15:51:43.944Z
modified: 2023-03-15T15:52:29.437Z
---

# lib-collab-yjs-hocuspocus-community

# guide

# issues-not-yet
- ## 

- ## 

- ## [Need Single Websocket Connection to open different docs](https://github.com/ueberdosis/hocuspocus/issues/460)
- Right now Hocuspocus is developed in a way that it opens a new connection when you open a document. 
  - In our React SPA platform people regularly switching between documents. 
  - Now on changing on document the existing connection closes and a new connection is built. 
  - Which gives a feeling of a very slow document load. 
  - Because the Initial Connection Time, DNS Resolving, SSL Handshake etc takes approx 300-500 ms. 
  - Now if the documents can change within a single connection, all that time can give it a very fast impression.

- If this is added I would hope its optional.
  - Currently I am load balancing documents on the server across multiple hocuspocus instances each on its own process, each document is only ever open on one instance at a time.
  - If a user could change documents along their existing websocket connection that would break this as it would bypass the load balancer and allow them to force the document open on the wrong process.

- [Use 1 WS connection to fetch documents instead of establishing connection for each documents](https://github.com/ueberdosis/hocuspocus/issues/343)
  - I've already played around here a bit, but figured that this requires some major rewrite of both the server and the client, as connections are tightly coupled with the document right now.
# discuss
- ## 

- ## 

- ## 
