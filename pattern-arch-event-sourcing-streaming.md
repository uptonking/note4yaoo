---
title: pattern-arch-event-sourcing-streaming
tags: [architecture, event-sourcing, oplog, streaming]
created: 2023-09-12T09:33:59.003Z
modified: 2023-09-12T09:34:51.108Z
---

# pattern-arch-event-sourcing-streaming

# guide

- who is using #event-sourcing
  - wix
  - products: undb

- usecases
  - logux/redux ? 
  - gundb
  - undo/redo
  - 工程类、科学类数据的观测分析

- tasks
  - model domain objects and events
  - serialize/des
  - compress 
  - streaming and seek
  - cache
  - offline/local-first
  - es-orm: es是一种pattern，成熟的方案都会支持多个db/orm
  - integrations: cms的实现可参考通用fwk
# dev
- [EventSource - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)
  - Warning: When not used over HTTP/2, SSE suffers from a limitation to the maximum number of open connections, which can be specially painful when opening various tabs as the limit is per browser and set to a very low number (6)
  - This limit is per browser + domain
  - The issue has been marked as "Won't fix" in Chrome and Firefox.
  - When using HTTP/2, the maximum number of simultaneous HTTP streams is negotiated between the server and the client (defaults to 100).
  - 对于移动端是够用的
# more
