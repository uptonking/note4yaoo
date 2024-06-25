---
title: toc-lib-utils-web-storage
tags: [cookies, indexeddb, localStorage, sessionStorage, toc, web-storage]
created: 2023-11-23T09:58:09.728Z
modified: 2023-11-23T09:58:47.558Z
---

# toc-lib-utils-web-storage

# guide

# popular
- https://github.com/unjs/unstorage /1.2kStar/MIT/202311/ts
  - provides an async Key-Value storage API with conventional features like multi driver mounting, watching and working with metadata, dozens of built-in drivers and a tiny core.
  - Designed for all environments: Browser, NodeJS, and Workers
  - Default in-memory storage
  - Asynchronous API
  - Binary and raw value support
  - HTTP Storage with built-in server
  - State snapshots and hydration

- https://github.com/tweedegolf/storage-abstraction /71Star/MIT/202311/ts
  - Provides an abstraction layer for interacting with a storage; 
  - the storage can be local or in the cloud.
  - Currently local disk storage, Backblaze B2, Google Cloud and Amazon S3 and compliant cloud services are supported.

- https://github.com/aykutkardas/lookie
  - Store your data in localStorage with optional expiration time.
# cache
- https://github.com/graphql/dataloader /MIT/202303/js/NoDeps/单文件/inactive
  - DataLoader is a generic utility to be used as part of your application's data fetching layer to provide a consistent API over various backends and reduce requests to those backends via batching and caching
  - A port of the "Loader" API originally developed by @schrockn at Facebook in 2010. DataLoader is a simplified version of this original idea implemented in JavaScript for Node.js services
  - This mechanism of batching and caching data requests is certainly not unique to Node.js or JavaScript, it is also the primary motivation for Haxl(haskell)
  - Each `DataLoader` instance represents a unique cache. Typically instances are created per request when used within a web-server like express
  - DataLoader provides a memoization cache for all loads which occur in a single request to your application
  - https://github.com/stephenh/joist-ts /IMT/202402/ts
    - An opinionated ORM for TypeScript/node/postgres.
    - Schema-driven code generation (continually-generated classes w/the getter/setter/relation boilerplate)
    - Guaranteed N+1 safe, pervasive use of Facebook's dataloader
    - All relations are async/await (with an ergonomic, type-safe escape hatch)
# event
- https://github.com/RubaXa/wormhole
  - It's better EventEmitter for communication between tabs with supporting Master/Slave.


# more
