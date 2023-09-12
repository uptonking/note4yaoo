---
title: pattern-arch-event-sourcing-examples
tags: [event-sourcing, examples]
created: 2023-09-12T09:37:11.161Z
modified: 2023-09-12T09:37:22.608Z
---

# pattern-arch-event-sourcing-examples

# guide

# popular
- https://github.com/xolvio/typescript-event-sourcing /ts
  - Domain Driven Design, Event Sourcing & Command Query Responsibility Segregation with Typescript

- https://github.com/cloudnativeentrepreneur/sourced /ts
  - https://github.com/mateodelnorte/sourced /js
  - Tiny framework for building models with the event sourcing pattern (events and snapshots) that works in Node.js and the browser
  - Unlike Active Record where entity state is persisted on a one-model-per row database format, event sourcing stores all the changes (events) to the entity, rather than just its current state. 
  - The current state is derived by loading all events, or a latest snapshot plus subsequent events, and replaying them against the entity.
  - Sourced makes no assumptions about how you store your events and snapshots. 
    - The library is small and tight with only the required functionality to define entities and their logic, enqueue and emit events, and track event state to later be persisted. 
  - https://github.com/mateodelnorte/sourced-repo-mongo
    - mongo data store and repository for sourced-style event sourcing models

- https://github.com/castore-dev/castore /107Star/MIT/202303/ts
  - Making Event Sourcing easy
  - Event Sourcing is a data storage paradigm that saves changes in your application state rather than the state itself.
  - After years of using it at Kumo, we have grown to love it

- https://github.com/oskardudycz/EventSourcing.NodeJS /ts
  - Examples and Tutorials of Event Sourcing in NodeJS
  - I already have samples of Event Versioning and Snapshots in my sample repo. 
  - https://github.com/oskardudycz/EventSourcing.JVM

- https://github.com/reimagined/resolve /MIT/202212/ts/提供了很多示例
  - https://reimagined.github.io/resolve/
  - Full stack CQRS, DDD, Event Sourcing framework for Node.js
  - using events as a source of truth and calculating read models from them.
  - Integrates with React and Redux for seamless development experience.
  - ReSolve implements the write side as a set of aggregates. 
  - The read side is implemented as a set of read models. 
    - ReSolve also implements a reactive extension of the read model concept called a view model. 
    - A view model rebuilds its state on the fly and uses WebSockets to reactively synchronize the state with the client.
  - A saga describes a long running process as a sequence of events.
  - reSolve application stores its data(a chain of immutable events) in a centralized event store, which can be configured to use different underlying data storages through the mechanism of adapters.
  - [A Redux-Inspired Backend. Extending React+Redux ideas to the_201901](https://medium.com/resolvejs/resolve-redux-backend-ebcfc79bbbea)
  - [Why is mongodb adapters discontinued?](https://github.com/reimagined/resolve/issues/1429)
    - The current main goals of the reSolve framework and cloud platform are high load capability and high performance of the event store and read models. 
    - All reSolve adapters, except for MongoDB, are SQL-based and support operations that are especially useful under high loads, including transactions and lightweight mutexes. 
    - you can write your own adapters, including a MongoDB event store and read model, but you should be aware that they may not meet high load requirements, which is the reSolve cloud platform’s main focus.
    - The main reasons for MongoDB adapter removal were the lack of transaction support and the absence of the serverless MongoDB implementation at that time. We decided to focus more on the framework's core features and performance and don't spent much time on maintaining various adapters.

- https://github.com/thenativeweb/wolkenkit /AGPLv3/202201/ts/inactive
  - https://docs.wolkenkit.io/
  - an open-source CQRS and event-sourcing framework based on Node.js
  - The following databases are supported for the domain event store, the lock store, and the priority queue store: in-memory, mysql, postgresql, redis, mongodb
  - https://github.com/thenativeweb/wolkenkit-eventstore
  - https://github.com/thenativeweb/wolkenkit-boards /js
    - a tool for collaboratively organizing notes.
    - backend is powered by wolkenkit.
  - https://github.com/thenativeweb/cqrs-sample /js
  - [Wolkenkit 3.0 – a CQRS and event-sourcing framework for JavaScript | Hacker News_201812](https://news.ycombinator.com/item?id=18705853)
    - es store deltas instead of the current state
    - Git stores complete snapshots of objects, not diffs 

- https://github.com/valkyrjs/valkyr /ts
  - https://valkyrjs.com/
  - toolkit for creating event sourced applications using javascript/typescript.
  - A collection of TypeScript + JavaScript tools and libraries to build full stack software applications.
  - Valkyr is designed to be framework agnostic and can be used with any framework or no framework at all. We provide initial base support for SolidJS and ReactJS
  - https://github.com/cmdo-toolkit/events /ts/legacy
    - A distributed event sourcing solution written in TypeScript.
    - Logical hybrid clock timestamp representing the wall time when the event was created.
  - https://github.com/cmdo-toolkit/react-starter
    - A full stack cmdo boilerplate for react.js, node.js and typescript
    - 全家桶架构: client-db + store + api
  - https://github.com/cmdo-toolkit/db
    - Client side database solution written in TypeScript.
    - 依赖mingo(MongoDB query language for in-memory objects)
  - https://github.com/valkyrjs/valkyr /ts
    - toolkit for creating event sourced applications using javascript/typescript.

- https://github.com/snatalenko/node-cqrs
  - CQRS backbone with event sourcing for Node.js
  - The package provides building blocks for making a CQRS-ES application. 
  - It was inspired by Lokad. CQRS, but not tied to a specific storage implementation or infrastructure. 
  - It favors ES6 classes and dependency injection(di0), so any components can be modified or replaced with your own implementations without hacks to the package codebase.

- https://github.com/assafg/osiris
  - Simple event sourcing for nodejs

- https://github.com/Azure/fetch-event-source /ts
  - A better API for making Event Source requests, with all the features of fetch()
  - This library provides an alternate interface for consuming server-sent events, based on the Fetch API. 
  - It is fully compatible with the Event Stream format

- https://github.com/rexxars/eventsource-parser
  - A streaming parser for server-sent events/eventsource, without any assumptions about how the actual stream of data is retrieved. 
  - It is intended to be a building block for clients and polyfills in javascript environments such as browsers, node.js and deno.

- https://github.com/mafintosh/event-source-stream
  - EventSource implemented in node and the browser as a readable stream

- https://github.com/qas/examples-nodejs-cqrs-es-swagger
  - A Node.js CQRS and Event Sourcing Microservice Example Using Nest.js, Event Store, and Swagger

- https://github.com/binaryminds/react-native-sse
  - Event Source implementation for React Native. 
  - Server-Sent Events (SSE) for iOS and Android

- https://github.com/jordanbyron/react-native-event-source
  - react-native interface for EventSource: Server-Sent Events for iOS and Android

- https://github.com/EventSource/eventsource
  - EventSource client for Node.js and Browser (polyfill)

- https://github.com/fraktalio/fstore-sql
  - event store based on the Postgres database
  - Append events to the ordered, append-only log, using entity id/decider id as a key

- https://github.com/khaosdoctor/event-sourcing-demo-app /vue
  - Demo application to demonstrate the power of the event sourcing architecture
# non-js
- https://github.com/serverlesstechnology/cqrs /rust
  - A lightweight, opinionated CQRS and event sourcing framework targeting serverless architectures.
  - Event sourcing uses the generated events as the source of truth for the state of the application.
  - https://github.com/serverlesstechnology/cqrs-demo

- https://github.com/get-eventually/eventually-rs /rust
  - Collection of traits and other utilities to help you build your Event-sourced applications in Rust.

- https://github.com/eugene-khyst/postgresql-event-sourcing /java
  - A reference implementation of an event-sourced system that uses PostgreSQL as an event store
  - Run PostgreSQL, Kafka and event-sourcing-app
  - We can store all changes to the domain object state as a sequence of events in an append-only event stream. 
    - Thus, **event streams will contain an entire history of changes**.
    - But how can we be sure that this history is authentic and error-free? We can use event streams as a primary source of truth in a system.
    - To get the current state of an object, we have to replay all events in the order of occurrence. This pattern is called event sourcing. 
  - The audit trail (also called the audit log) is a chronological record of the history and details of the actions that affected the system. 
    - Event sourcing is an industry standard for implementing audit trail.
  - State-oriented persistence (CRUD) applications store only the latest version of an entity. Database records present entities. 
  - Event sourcing applications persist the state of an entity as a sequence of immutable state-changing events.
  - An entity in event sourcing is called an aggregate.
  - A sequence of events for the same aggregate is called a stream.
  - Event sourcing is best suited for short-living entities with a small total number of events (e.g., orders).
  - For endlessly stored entities (e.g., users, bank accounts) with thousands of events restoring state by replaying all events is not optimal, and snapshotting should be considered.
  - Snapshotting is an optimization technique where a snapshot of the aggregate's state is also saved, so an application can restore the current state of the aggregate from the snapshot rather than from all the events.
  - On every `nth` event, make an aggregate snapshot by storing an aggregate state and its version.
  - The read model is a "denormalized" view of the write model
    - Read models are projections of the system state. Therefore, read models are also known as projections.
  - CQRS is a self-sufficient architectural pattern and doesn't require event sourcing. 
    - But in practice, event sourcing is usually used in conjunction with CQRS. 
    - Event store is used as a write database, and SQL or NoSQL database as a read database.
    - Commands generate events. 

- https://github.com/andreschaffer/event-sourcing-cqrs-examples /java
  - examples of how to use Event Sourcing and CQRS applied to a minimalistic bank context.
- https://github.com/dmart28/reveno /java
  - an in-memory transactional event-driven framework with CQRS and Event Sourcing intruded
  - modular - use only components you really need to.
  - lightweight. The core is about 300kb only.
  - reveno-cluster – makes it possible to run Reveno in cluster with Master-Slave architecture, thus providing decent failover ability.

- https://github.com/looplab/eventhorizon /go
  - a CQRS/ES toolkit for Go.
  - NOTE: Event Horizon is used in production systems but the API is not final!

- https://github.com/pyeventsourcing/eventsourcing /python
  - https://eventsourcing.readthedocs.io/
  - A library for event sourcing in Python.

- https://github.com/EventStore/EventStore /csharp
  - https://eventstore.com/
  - The stream database optimised for event sourcing
# server-sent events
- https://github.com/dpskvn/express-sse
  - An Express middleware for quick'n'easy server-sent events.
- https://github.com/toverux/expresse
  - A better module for working with Server-Sent Events in Express

- https://github.com/triblondon/node-sse-pubsub
  - Server sent events for NodeJS
  - A simple NodeJS module to generate Server-Sent-Events streams with a publish/subscribe interface and simple integration with either Node's built in HTTP library or any framework that exposes it, eg. ExpressJS.

- https://github.com/EventSource/node-ssestream
  - Send Server-Sent Events with a stream
  - A zero-dependency node stream for writing Server-Sent Events.

- https://github.com/mpangrazzi/redis-subscribe-sse
  - Stream Redis "SUBSCRIBE" or "PSUBSCRIBE" events to browsers using HTML5 Server-Sent Events (SSE)

- https://github.com/tomkersten/sses-node-example
  - Example of Express.js application providing Server-Sent Events (SSEs) on top of Redis pub/sub connection

- https://github.com/simonprickett/server-sent-events-demo
  - A small Server Sent Events demo for San Diego JS Meetup using Node, HTML, JavaScript, CSS. 
  - [A Look at Server Sent Events](https://simonprickett.dev/a-look-at-server-sent-events/)

- https://github.com/WebReflection/bidi-sse
  - Bidirectional Server-sent Events

- https://github.com/rexxars/sse-channel /202011/js
  - Server-Sent Events "channel" where all messages are broadcasted to all connected clients, history is maintained automatically and server attempts to keep clients alive by sending "keep-alive" packets automatically.

- https://github.com/einaros/sse.js /201712/js
  - Server-Sent Events made easy for node.js

- https://github.com/chrisdickinson/sse-stream
  - Expose HTML5 Server Sent Events as an installable appliance on Node. JS http servers; connections are emitted as Writable streams.
# more
