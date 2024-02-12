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

- usecases
  - logux/redux ?
  - gundb
  - Datomic/CouchDB
  - undo/redo
  - 工程类、科学类数据的观测分析
  - products: undb

- tips
  - event sourcing会记录所有events，可以根据events计算state，但不同client计算的结果不一定一致
    - crdt是通用的能实现最终一致性的数据结构，可将对crdt数据结构的crud操作用events记录，这样计算的state就是一致的
  - event sourcing模式是db无关的，不必执着于标准方案，存储、传输都可替换，可针对场景优化，如offline
  - 探索es pattern的最佳实现，然后总结 examples/kanban/framework
  - es与crud结合的方案，参考cdc
  - commands are ephemeral, events are permanent and the only source of truth

- tasks
  - model domain objects and events
  - serialize/des
  - compress 
  - streaming and seek
  - cache
  - offline/local-first
  - es-orm: es是一种pattern，成熟的方案都会支持多个db/orm
  - event store/db
  - integrations: cms的实现可参考通用fwk
# dev
- [EventSource - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)
  - EventSource interface is web content's interface to server-sent events.
  - Warning: When not used over HTTP/2, SSE suffers from a limitation to the maximum number of open connections, which can be specially painful when opening various tabs as the limit is per browser and set to a very low number (6)
  - This limit is per browser + domain
  - The issue has been marked as "Won't fix" in Chrome and Firefox.
  - When using HTTP/2, the maximum number of simultaneous HTTP streams is negotiated between the server and the client (defaults to 100).
  - 对于移动端是够用的
# more
