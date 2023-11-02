---
title: pattern-arch-event-sourcing-examples
tags: [event-sourcing, examples]
created: 2023-09-12T09:37:11.161Z
modified: 2023-09-12T09:37:22.608Z
---

# pattern-arch-event-sourcing-examples

# guide

- tips
  - event-store类似内存数据库，也可作为一种状态管理方式

- es-db
  - 还可参考stream/kappa架构
  - kappa-core is built on an abstraction called a kappa architecture, or "event sourcing".

- https://github.com/heynickc/awesome-ddd
  - A curated list of Domain-Driven Design (DDD), Command Query Responsibility Segregation (CQRS), Event Sourcing
- https://event-driven.io/
  - https://github.com/oskardudycz/event-driven.io
  - Resources about Event-Driven Architectures, Event Sourcing and pragmatic development

- [@resolve-js/core vs eventstore vs wolkenkit vs create-resolve-app | npm trends](https://npmtrends.com/@resolve-js/core-vs-eventstore-vs-wolkenkit-vs-create-resolve-app)
# popular
- https://github.com/xolvio/typescript-event-sourcing /ts
  - Domain Driven Design, Event Sourcing & Command Query Responsibility Segregation with Typescript

- https://github.com/Judahh/flexiblePersistence /ts
  - A CQRS and Event Sourcing platform
  - It's possible to use different databases or services implementing IPersistence interface, like MongoDB does (MongoPersistence).
  - Other implementations: DAO, Sequelize, Service
  - https://github.com/Judahh/sequelizePersistence

- https://github.com/oskardudycz/EventSourcing.NodeJS /ts
  - Examples and Tutorials of Event Sourcing in NodeJS
  - I already have samples of Event Versioning and Snapshots in my sample repo. 
  - [Introduction to Event Sourcing - Self Paced Kit_202203](https://event-driven.io/en/introduction_to_event_sourcing/)
  - https://github.com/oskardudycz/EventSourcing.JVM

- https://github.com/sugarandmagic/sequelize-mv-support /MIT/ts
  - This package adds support for Views and Materialized Views in Sequelize.
  - We're heavy users of views and materialized views, but we use Sequelize a lot for bootstrapping and testing database schema. 
  - this module adds support for both views and materialized views to Sequelize, as well as properly exporting typescript declarations.
  - All the original Sequelize methods and options still work with this module

- https://github.com/Skalar/ddes /ts
  - https://ddes.io/docs/
  - TypeScript framework that facilitates Event Sourcing and CQRS using distributed cloud services.
  - persist and access all relevant events within your domain, in an “immutable” store
  - subscribe to events that are committed to the store
  - Aggregate snapshots allow you to store the state of aggregate instances manually and/or at given version intervals. This allows for more efficient loading of aggregate instances with a large number of commits.

- https://github.com/reimagined/resolve /MIT/202212/ts/提供了很多示例
  - https://reimagined.github.io/resolve/
  - Full stack CQRS, DDD, Event Sourcing framework for Node.js
  - features
    - Full stack scalable modern app
    - cqrs + es 
    - DDD Aggregate support
    - Integrates with React and Redux for seamless development experience.
  - using events as a source of truth and calculating read models from them.
  - ReSolve implements the write side as a set of aggregates. 
  - The read side is implemented as a set of read models. 
    - ReSolve also implements a reactive extension of the read model concept called a view model. 
    - A view model rebuilds its state on the fly and uses WebSockets to reactively synchronize the state with the client.
  - A saga describes a long running process as a sequence of events.
  - reSolve application stores its data(a chain of immutable events) in a centralized event store, which can be configured to use different underlying data storages through the mechanism of adapters.
    - The reSolve framework saves produced events to a persistent event store. 
    - A newly created application is configured to use a SQLite event store. 
  - ReSolve uses the adapter mechanism to provide an abstraction layer above APIs
    - Event store adapters
    - Read model store adapters
    - you may implement a Read Model on top of some arbitrary system, such as a full-text-search engine, OLAP or a particular SQL database
  - you definitely can use only backend part of reSolve, it does not assume anything about client part.
  - [A Redux-Inspired Backend. Extending React+Redux ideas to the_201901](https://medium.com/resolvejs/resolve-redux-backend-ebcfc79bbbea)
  - [Snapshots](https://github.com/reimagined/resolve/discussions/1791)
    - These are low level methods that event store need to implement, app devs unlikely will call them.
    - Aggregate state is json built by running a projection function as a reducer on event stream.
    - If number of events used is greater than N, aggregate state is saved to event store as a snapshot.
    - Next time aggregate state is built from snapshot forward, so building an aggregate state should read not more than N records from event store (including snapshot).
    - The same mechanism is used for view models.
  - [Snapshot is always delayed by 1 event](https://github.com/reimagined/resolve/issues/980)
    - The snapshot is created when reading events, not when persisting
    - Due to the above, the snapshotted state will always be delayed by 1 event until somebody tries to rehydrate the aggregate root
    - Most likely there is no issue there. 
    - Take in mind that snapshot is never used as single source to receive aggregate root (state). Snapshot allows to reduce amount of events, which should be retrieved from eventstore. So, in your case, last event will be used to rehydrate the aggregate root anyway.
  - [Hosting and Scaling?](https://github.com/reimagined/resolve/discussions/1770)
    - reSolve local is a node app, so you can host and scale using any container management system.
    - reSolve 0.28 is tested in multi-instance mode, so it should work in the cluster without problems and additional configuration.
    - concurrent writes are kept consistent using optimistic locking. For read model notification, all instances are registered in the event store, and instance that modified event store notifies others, so they can pull new events and apply to the read models.
    - This means that in case of central read model DB, all instances would try to apply the same updates to the read model, but only one would win. This is probably not an efficient approach, but surely - the simplest thing that will work in all cases.
    - Please note that instances can have different configurations, so some of them can deal with write side, some with read side. Also, it is possible that each instance will have its own read model storage (local db).
    - No redis there, just one instance notifies others via HTTP call. This is just poking "go check event store".
  - [Server clustering configuration possible?](https://github.com/reimagined/resolve/discussions/1803)
    - we have tested multi-instance config, and, as I feared, it doesn't work correctly with the current version. We have fixed the problem, and fix is likely to be included in the next release.
    - We have released reSolve 0.28_202103. There we have removed event broker process. Now all instances are registered in event store and notify each other without explicit configuration.
    - reSolve app deployed to the cloud is compiled into AWS lambdas, lambda@edge, and many AWS infrastructure elements like app gateways, step functions, aurora db instances etc.
    - So here we are describing how to run "local" express-based reSolve version in a multi-instance cluster. I would not call it serverless. It is mostly stateless, works similar to cloud version, but is not serverless.
  - [Why is mongodb adapters discontinued?](https://github.com/reimagined/resolve/issues/1429)
    - The current main goals of the reSolve framework and cloud platform are high load capability and high performance of the event store and read models. 
    - All reSolve adapters, except for MongoDB, are SQL-based and support operations that are especially useful under high loads, including transactions and lightweight mutexes. 
    - you can write your own adapters, including a MongoDB event store and read model, but you should be aware that they may not meet high load requirements, which is the reSolve cloud platform’s main focus.
    - The main reasons for MongoDB adapter removal were the lack of transaction support and the absence of the serverless MongoDB implementation at that time. We decided to focus more on the framework's core features and performance and don't spent much time on maintaining various adapters.

- https://github.com/thenativeweb/wolkenkit /AGPLv3/202201/ts/inactive
  - https://docs.wolkenkit.io/
  - an open-source CQRS and event-sourcing framework based on Node.js
  - features
    - ddd + es + cqrs
    - wolkenkit applications are distributed by default and designed to scale. You can run wolkenkit as a single-process runtime on a single machine, or as a set of distinct services spread across your network.
    - stores domain events from your business over time
    - contains a vanilla HTTP and a GraphQL endpoint that can be used to send commands, execute queries, and subscribe to domain events.
    - ready-made yet configurable manifests for Docker and Kubernetes
  - The following databases are supported for the domain event store, the lock store, and the priority queue store: in-memory, mysql, postgresql, redis, mongodb
  - [Implement architecture for 4.0_201910](https://github.com/thenativeweb/wolkenkit/issues/181)
    - a rewrite from scratch, including support for TypeScript, GraphQL
    - 区分event-store和queue-store
  - https://github.com/thenativeweb/wolkenkit-eventstore /AGPLv3/202111/js/v4未使用
    - eventstore for Node.js that is used by wolkenkit.
    - supported databases: in-memory/mongodb/mysql/pg
  - https://github.com/thenativeweb/wolkenkit-boards /js
    - a tool for collaboratively organizing notes.
    - backend is powered by wolkenkit.
  - https://github.com/thenativeweb/cqrs-sample /js
  - [Wolkenkit 3.0 – a CQRS and event-sourcing framework for JavaScript | Hacker News_201812](https://news.ycombinator.com/item?id=18705853)
    - git stores the state and calculates the deltas, and es stores the deltas and calculates the state.
    - es store deltas instead of the current state
    - Git stores complete snapshots of objects, not diffs 

- https://github.com/thenativeweb/node-eventstore /MIT/js/legacy/inactive
  - http://eventstore.js.org/
  - EventStore Implementation in node.js
  - By default the eventstore will use an in-memory Storage.
  - supported Dbs (in-memory, mongodb, redis, tingodb, elasticsearch, azuretable, dynamodb)
  - load and store events via EventStream object
  - snapshot support
  - I would like to thank Golo Roden, who was there very early at the beginning of my CQRS/ES/DDD journey and is now here again to take over these modules.
  - forks
  - https://github.com/saperiuminc/node-eventstore /js/inactive

- https://github.com/albe/node-event-storage /202306/js
  - An optimized embedded event store for modern node.js, written in ES6.
  - [Project Status](https://github.com/albe/node-event-storage/issues/29)
  - Small event sourced single-server applications that want to get near-optimal write performance. Using it as queryable log storage
  - Non-Goals
    - distributed storage/distributed transactions, therefore no network API
    - arbitrary querying capabilities - only range scans per stream
  - event stores are purely append-only storages, and the only querying is sequential (range) reading (possibly with some filtering applied)
  - no write-ahead log or transaction log required - the storage itself is the transaction log!
  - therefore writes are as fast as they can get, but you only can have a single writer (without implementing complex distributed log with RAFT or Paxos)
  - indexes are append-only and hence gain the same benefits
  - since only sequential reading is needed, indexes are simple file position lists - no fancy B+-Tree/fractal tree required
  - creating backups is easily doable with rsync or by creating file copies on the fly
  - Using any SQL/NoSQL database for storing events therefore is sub-optimal, as those databases do a lot of work on top which is simply not needed. Write and read performance suffer.
  - the storage guarantees a consistent global ordering on all events by managing a global primary index.
  - An Event Stream is implemented as an iterator over an storage index. It is therefore limited to iterating the events at the point the Event Stream was retrieved
  - An Event Stream is implemented as an iterator over an storage index. It is therefore limited to iterating the events at the point the Event Stream was retrieved
  - https://github.com/albe/node-event-storage-ui /js
    - an admin dashboard for inspecting a running node-event-storage on the same machine. 
    - It is built using nextjs with SSR and based on the creative-tim material dashboard dark.

- https://github.com/cloudnativeentrepreneur/sourced /202108/ts
  - https://github.com/mateodelnorte/sourced /js
  - Tiny framework for building models with the event sourcing pattern (events and snapshots) that works in Node.js and the browser
  - Unlike Active Record where entity state is persisted on a one-model-per row database format, event sourcing stores all the changes (events) to the entity, rather than just its current state. 
  - The current state is derived by loading all events, or a latest snapshot plus subsequent events, and replaying them against the entity.
  - Sourced makes no assumptions about how you store your events and snapshots. 
    - The library is small and tight with only the required functionality to define entities and their logic, enqueue and emit events, and track event state to later be persisted.
  - https://github.com/CloudNativeEntrepreneur/sourced-repo-svelte-local-storage-store
    - https://github.com/CloudNativeEntrepreneur/svelte-local-storage-store
    - A store that adds pub/sub to local storage. Supports changes across multiple tabs.
  - https://github.com/mateodelnorte/sourced-repo-mongo /202106/js
    - mongo data store and repository for sourced-style event sourcing models
  - https://github.com/CloudNativeEntrepreneur/sourced-repo-typeorm
    - uses TypeORM to persist events
  - https://github.com/PDMLab/sourced-ts /ts/inactive
    - forked from sourced for building models with the event sourcing pattern (events and snapshots).
    - https://github.com/PDMLab/sourced-repo-mongo-ts

- https://github.com/fraktalio/fmodel-ts /ts
  - https://fraktalio.com/fmodel/
  - This project can be used as a library, or as an inspiration, or both. 
  - It provides just enough tactical Domain-Driven Design patterns, optimised for Event Sourcing and CQRS.
  - The library is fully isolated from the application and infrastructure layers. It represents a pure declaration of the program logic.
  - 官方示例基于Axon
  - State-stored systems are traditional systems that are only storing the current State by overwriting the previous State in the storage.
  - Event-sourced systems are storing the events in immutable storage by only appending.
  - A Materialized view is using/delegating a View to handle events of type E and to maintain a state of denormalized projection(s) as a result. Essentially, it represents the query/view side of the CQRS pattern. It belongs to the Application layer.
  - https://github.com/fraktalio/fmodel-rust /rust
  - https://github.com/fraktalio/fmodel-java /java
  - https://github.com/fraktalio/fmodel /kotlin
  - https://github.com/fraktalio/fmodel-demos /kotlin
- https://github.com/fraktalio/fstore-sql /psql
  - event store based on the Postgres database
  - Append events to the ordered, append-only log, using entity id/decider id as a key
  - This project is enabling event-sourcing and pool-based event-streaming patterns by using SQL (PostgreSQL) only. No additional tools, frameworks, or programming languages are required at this level.
  - Every decider/entity stream of events is an independent partition. The events within a partition are totally ordered. There is no ordering guarantee across different partitions.

- https://github.com/castore-dev/castore /107Star/MIT/202303/ts
  - https://castore-dev.github.io/castore/
  - Making Event Sourcing easy
  - You can code your own EventStorageAdapter (simply implement the interface)
  - Event Sourcing is a data storage paradigm that saves changes in your application state rather than the state itself.
  - After years of using it at Kumo, we have grown to love it
  - **Snapshots are not implemented in Castore yet**, but we have big plans for them, so stay tuned

- https://github.com/valkyrjs/valkyr /ts
  - https://valkyrjs.com/
  - toolkit for creating event sourced applications using javascript/typescript.
  - A collection of TypeScript + JavaScript tools and libraries to build full stack software applications.
  - designed to be framework agnostic and can be used with any framework or no framework at all. We provide initial base support for SolidJS and ReactJS
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

- https://github.com/PDMLab/mongo-eventstore /202110/ts/inactive
  - Eventstore for Node.js build on top of MongoDB
  - https://github.com/AlexZeitler/mongo-eventstore-sample

- https://github.com/flolu/simple-event-sourcing-example /ts/inactive
  - Small Node.js Application to Learn the Concepts of Event Sourcing
  - To handle CQRS, I have to services: one that mutates the event store and one that just consumes events that happened in the past to update a materialized view of the current state.

- https://github.com/mattbishop/sql-event-store /js
  - Demonstration of a SQL event store with de-duplication and guaranteed event ordering. 
  - This event store can be ported to most SQL RDBMS and accessed from concurrent readers and writers, including high-load serverless functions.
  - The database rules are intended to prevent incorrect information from entering into an event stream.
  - This project uses a node test suite and SQLite to ensure the DDL complies with the design requirements
  - This event store can also be ported to most SQL RDBMS and accessed from any number of writers, including high-load serverless functions, without a coordinating “single writer” process. The project includes a Postgres version of the DDL.
  - An Event is an unalterable statement of fact that has occurred in the past. It has a name, like food-eaten, and it is scoped to an Entity, or an identifiable existence in the world.

- https://github.com/assafg/osiris /ts
  - Simple event sourcing for nodejs

- https://github.com/equinox-project/equinox-js /ts
  - https://equinox-project.github.io/equinox-js/
  - Event sourcing library for JavaScript
  - a JS port of jet's Equinox
  - Equinox is a set of low dependency libraries that allow for event-sourced processing against stream-based stores handling: Snapshots, Caching, Optimistic concurrency control
  - [v1.0.0 Checklist_202309](https://github.com/equinox-project/equinox-js/issues/27)
    - It’s stabilising as we speak. The message-db store is being used in production by a few people including my employer. 

- https://github.com/Silly-Goose-Software/event-sauced-ts /ts/inactive
  - started out as a re-implementation of ASOS/SimpleEventStore in TypeScript. 
  - What was initially just a simple re-write, is slowly becoming a more featured library.
  - The goal is to be provide a database-agnostic API for an event store.
  - https://github.com/Silly-Goose-Software/event-sauced-ts-postgresql

- https://github.com/mafintosh/event-source-stream
  - EventSource implemented in node and the browser as a readable stream

- https://github.com/qas/examples-nodejs-cqrs-es-swagger
  - A Node.js CQRS and Event Sourcing Microservice Example Using Nest.js, Event Store, and Swagger

- https://github.com/binaryminds/react-native-sse /202304/js
  - Event Source implementation for React Native. 
  - Server-Sent Events (SSE) for iOS and Android

- https://github.com/jordanbyron/react-native-event-source
  - react-native interface for EventSource: Server-Sent Events for iOS and Android

- https://github.com/EventSource/eventsource
  - EventSource client for Node.js and Browser (polyfill)

- https://github.com/zeppaman/mongo-event-sourcing /js/inactive
  - An open-source fully configurable and extendible tool that enables event sourcing in MongoDB.
  - implement event sourcing listening event from mongodb. 
  - For who is used to play with traditional RDBMS it's something like triggers, but fire events outside database. This application uses the built-in mongodb feature called `ChangeStream`.
  - So, adding MESS in your architecture you can forward event for data changes to applications by using webhook or simply add event to a queue like rabbitMQ or Kibana.

- https://github.com/seikho/evtstore /ts/未实现snapshot
  - https://seikho.github.io/evtstore
  - Type-safe Event Sourcing and CQRS with Node. JS and TypeScript
  - the design is highly opinionated, but still flexible.
  - We front-load the creation of our Event, Aggregate, and Command types to avoid having to repeatedly import and pass them as generic argument.

- https://github.com/irontitan/tardis /ts/inactive
  - Event sourcing library to help developers abstract core concepts
  - The core idea behind Tardis is to implement a generic and easy-to-use interface to interact with the Event Sourcing architecture.
  - two core concepts: The Event and the Reducer, and we'll call anything from our business logic Entity, it can be a car, a person, a ship or anything else.

- https://github.com/domagojk/beenion /ts/inactive
  - Example project using Event Sourcing and CQRS patterns
  - require aws Serverless framework 

- https://github.com/boostercloud/booster /ts/GraphQL
  - https://www.boosterframework.com/
  - framework designed to create event-driven backend microservices that focus on extreme development productivity. 
  - It provides a highly opinionated implementation of the CQRS and Event Sourcing patterns in Typescript, using DDD (Domain-Driven Design)
  - We adopted GraphQL because it's a self-documenting standard. 

- https://github.com/rkaw92/esdf /201906/js
  - A minimal event-sourcing / domain-driven design framework for Node.js
  - This framework is light on the DDD side, only defining an AggregateRoot in terms of the EventSourcingAggregate prototype. It does not deal with ValueObjects (meant to be represented by plain old JavaScript objects) nor embedding aggregates in ARs
  - ESDF is heavily based on Promises/A (namely, the when.js implementation)

- https://github.com/kristopolous/db.js /202109/js/inactive
  - portable Javascript document store event-driven database
  - It's been feature-complete and stable for years
## postgresql

- https://github.com/message-db/message-db
  - http://docs.eventide-project.org/user-guide/message-db/
  - Microservice Native Event Store and Message Store for Postgres
  - A fully-featured event store and message store implemented in PostgreSQL for Pub/Sub, Event Sourcing, Messaging, and Evented Microservices applications.
  - The message store is a single table named messages.
  - Interaction with the message store is effected through Postgres server functions that ensure the correct semantics for the writing of messages to streams, and the reading of messages from streams and categories.
  - [Message DB: Event Store and Message Store for PostgreSQL | Hacker News_201912](https://news.ycombinator.com/item?id=21810272)

- https://github.com/marcopeg/postgres-event-sourcing /202103/js/inactive
  - an attempt to reproduce a Kafka-like data behavior for event-sourcing using Postgres to coordinate write/read concurrency over a topic of messages from multiple producers/consumers instances.

- https://github.com/bahatron/mercurios /ts
  - Event Sourcing with PostgresSQL
  - Event ordering is not guaranteed. However, it's possible to use expectedSeq when publishing to control the order of events in a stream

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

- https://github.com/factcast/factcast /java
  - https://docs.factcast.org/
  - Simple EventStore based on PostgreSQL
  - a 'good enough' event store using PostgreSQL for persistence, and offers remoting via GRPC.
# es-collab
- https://github.com/andykswong/mithic /MIT/ts
  - https://andykswong.github.io/mithic/
  - Modular library for real-time, offline-first isomorphic JavaScript applications
  - provides the building blocks for creating real-time, offline-first client-server or decentralized applications, using CQRS architecture with CRDT eventsourcing for storage and data replication.
  - minimal example to get started. Uses the `Redux` store preset
  - 插件支持level/redis/ipfs
  - crdt基于自己实现的lseq
  - timestamp基于逻辑时钟
  - Linear sequence of values based on `ORMap` of base64 fractional index to values

- https://github.com/josephg/statecraft /ISC/201911/ts/inactive
  - Statecraft is a protocol and set of tools for interacting with data that changes over time. 
  - It is the spiritual successor to Sharedb.
  - The store guarantees that the data is immutable with respect to time. (So if the data changes, the version number goes up).
    - Stores can choose how much historical data to store and return.
  - Stores provide a standard set of methods to interact with the data: fetch/mutate/subscribe
  - A Statecraft store is more than just a database abstraction
    - Unlike traditional transactional databases, Statecraft stores compose together like LEGO. Stores wrap one another
  - The philosophy of Statecraft is to "ship the architecture diagram". 
    - The API is designed to make it easy to re-expose a statecraft store over the network.
  - [Show FDB: A scalable realtime text editor on top of foundationdb_201901](https://forums.foundationdb.org/t/show-fdb-a-scalable-realtime-text-editor-on-top-of-foundationdb/1082)
    - I’m working on a realtime data processing pipeline / event sourcing system lately called statecraft 45. Over the last few days I’ve added foundationdb backend support.
    - The current code also re-stores the whole text document with every edit, but this is just because I haven’t tuned it. 

- https://github.com/soundcloud/roshi /3.1kStar/bsd/go/soundcloud
  - Roshi implements a time-series event storage via a LWW-element-set CRDT with limited inline garbage collection. 
  - Roshi is a stateless, distributed layer on top of Redis and is implemented in Go. 
  - It is partition tolerant, highly available and eventually consistent.
  - [Roshi: a CRDT system for timestamped events | SoundCloud Blog_201405](https://developers.soundcloud.com/blog/roshi-a-crdt-system-for-timestamped-events)
# es-non-js
- https://github.com/EventStore/EventStore /csharp
  - https://eventstore.com/
  - The stream database optimised for event sourcing
  - https://github.com/EventStore/samples
  - https://github.com/qooroo/EventStore /legacy
    - Event Store is written in a mixture of C#, C++ and JavaScript. It can run either on Mono or .NET, however because it contains platform specific code (including hosting the V8 JavaScript engine), it must be built for the platform on which you intend to run it.
- https://github.com/EventStore/EventStore. UI /js
  - The user interface for Event Store. This is included as a submodule in the main Event Store repository.
- https://github.com/x-cubed/event-store-client /js
  - JS client library for connecting to Event Store over TCP/IP
  - Connects to an Event Store server over TCP/IP, to send and receive event information.
  - The Javascript API is intended to mimic the . Net API as closely as possible.

- https://github.com/thalo-rs/thalo /583Star/MIT/202212/rust/inactive
  - https://thalo.rs/
  - Thalo is an event sourcing runtime for building distributed systems. 
  - It is built on top of Wasmtime for components, and uses Message DB for the message store.
  - Aggregates, commands and events are defined in the ESDL schema language.
  - only Rust is supported
  - https://github.com/thalo-rs/esdl
    - Heavily inspired by GraphQL syntax

- https://github.com/get-eventually/eventually-rs /482Star/MIT/202303/rust
  - Collection of traits and other utilities to help you build your Event-sourced applications in Rust.
  - eventually exposes all the necessary abstraction to model your Domain Entities (in lingo, Aggregates) using Domain Events, and to save these Events using an Event Store (the append-only event log).
  - officially-supported backend: in-memory, pg
  - https://github.com/pholactery/eventsourcing /202303/rust/inactive

- https://github.com/meilisearch/MeiliES /326Star/MIT/201910/rust/inactive
  - MeiliES is an Event Sourcing database that uses the RESP (REdis Serialization Protocol) to communicate. 
    - it is possible to use the official Redis command line interface program to communicate with MeiliES.
  - An event store is like a Kafka or a Rabbit MQ but it stores events on disk indefinitely. 
  - MeiliES stores all the events of all the streams that were sent by all the clients in the order they were received.
  - Keep in mind that a message queue is not made for event-sourcing.
  - Full Rust, using `sled` as the internal storage
  - The current implementation has some limitations related to the whole number of streams subscribed
  - [MeiliES - Event sourcing in Rust_201903](https://blog.meilisearch.com/meilies-release/)

- https://github.com/tomcumming/simples /rust/inactive
  - tiny event sourcing database for prototype and small projects.
  - Designed to preserve data even when crashing mid-write. Ready to relaunch immediately.
  - Written in Rust, using Tokio and Hyper.
  - Uses little more disk space than the contents of the topics.

- https://github.com/primait/event_sourcing.rs /202310/rust
  - opinionated library used to achieve cqrs/es in Rust.
  - Event Sourcing RS uses under the hood sqlx.

- https://github.com/PumpkinDB/PumpkinDB /201708/rust/inactive
  - an immutable ordered key-value database engine
  - By guaranteeing the immutability of key's value once it is set, PumpkinDB forces its users to think of their data through a temporal perspective.
  - The core ideas behind PumpkinDB stem from the so called lazy event sourcing approach which is based on storing and indexing events while delaying domain binding for as long as possible.
  - [Show HN: PumpkinDB, an event sourcing database engine | Hacker News_201702](https://news.ycombinator.com/item?id=13738051)

- https://github.com/Actyx/Actyx /apache2/202311/rust/ts
  - https://developer.actyx.com/
  - Actyx is a decentralized event database, streaming and processing engine that allows you to easily build local-first cooperative apps.
  - durable event stream storage in peer-to-peer network using libp2p and ipfs-embed
  - tag-based and time-based indexing of events
  - full-fledged support for event-sourcing, guaranteeing eventual consistency
  - aql: full-fledged support for event-sourcing, guaranteeing eventual consistency

- https://github.com/mit-pdos/noria /202110/rust/inactive
  - Noria is a new streaming data-flow system designed to act as a fast storage backend for read-heavy web applications based on Jon Gjengset's Phd Thesis
  - It acts like a database, but precomputes and caches relational query results so that reads are blazingly fast. 
  - Noria automatically keeps cached results up-to-date as the underlying data, stored in persistent base tables, change. 
  - Noria uses partially-stateful data-flow to reduce memory overhead, and supports dynamic, runtime data-flow and query change.
  - Noria comes with a MySQL adapter that implements the binary MySQL protocol. This lets any application that currently talks to MySQL or MariaDB switch to Noria with minimal effort.
  - At a high level, Noria takes a set of parameterized SQL queries (think prepared statements), and produces a data-flow program that maintains materialized views for the output of those queries. Reads now become fast lookups directly into these materialized views, as if the value had been directly cached in memcached. The views are then kept up-to-date incrementally through the data-flow, which yields high write throughput.
  - Like most databases, Noria follows a server-client model where many clients connect to a (potentially distributed) server. 
  - Noria also uses Apache ZooKeeper to announce the location of its servers, so ZooKeeper must be running.

- https://github.com/palfrey/potboiler /rust
  - an AP Event Sourcing system. it's an MVP/research prototype 
- https://github.com/cosmonic/concordance /rust
  - opinionated event sourcing framework from Cosmonic
  - Building on the power, portability, speed, and scalability of wasmCloud, Concordance allows you to reason about your application using the fundamental building blocks of event sourcing: Aggregates/Projectors
  - https://github.com/wasmCloud/wasmCloud
    - https://wasmcloud.com/docs/intro

- https://github.com/bfil/exar-db /201703/rust
  - http://bfil.github.io/exar-db/exar_db
  - An event store with streaming support, it uses flat-file based collections.
  - The database is split into modules

- https://github.com/mjc-gh/esper /201705/rust
  - Event Source powered by hyper written in Rust
  - Esper is a standalone Event Source / Server Sent Events (SSE) broker. 

- https://github.com/alicanli1995/clean-hexagonal-architecture-kafka-saga-outbox /java
  - Food Ordering Project with Clean and Hexagonal Architecture With Kafka Messaging System And Outbox Table
  - Hexagonal (Clean) Architecture -> Port & Adapter Style
  - CQRS Pattern : Materialized view & Event Sourcing
  - SAGA Pattern : process & rollback ( compensating transactions )
  - Outbox Pattern : Pulling Outbox Table With Scheduler , Saga Status

- https://github.com/dmfrey/event-store-demo /201809/java/inactive
  - We recently finished work on a system in which we built an Event Source system. This application is a demo of the architecture we produced.
  - This application is a simple Kanban. It only allows for minimal board and story management.
  - This application was unique in that we implemented the backend with Apache Kafka, MongoDb and MySQL. 
  - The final solution was based on MySQL. Kafka and MongoDb would not be available in the production environments, so we adjusted.

- https://github.com/andreschaffer/event-sourcing-cqrs-examples /java
  - examples of how to use Event Sourcing and CQRS applied to a minimalistic bank context.
  - In a distributed world, event timestamps are unreliable for ordering - machines have their own clocks.
    - Instead we can make the ordering explicit with an event version. 
  - In this project we use event versioning in two ways
    - In the write/command side, we use it for protecting ourselves from race conditions via optimistic locking;
    - In the read/query side, we use it for commutative reasons, meaning events can come out of order and we can still handle them properly.
    - If you are interested in this topic, we also recommend reading about Lamport timestamps and Vector clocks as alternatives.

- https://github.com/asimkilic/cqrs-event-sourcing-with-kafka /java
  - Use the mediator pattern to implement command and query dispatchers
  - Implement an event store/write database in MongoDB
  - Create a read database in MySQL
  - Produce event to Apache Kafka
  - Consume event from Apache Kafka to populate and alter the read database
  - Replay the event strore to recreate the state of the aggregate
  - Structure your code using Domain-Driven-Design best practices
- https://github.com/dmart28/reveno /java
  - an in-memory transactional event-driven framework with CQRS and Event Sourcing intruded
  - modular - use only components you really need to.
  - lightweight. The core is about 300kb only.
  - reveno-cluster – makes it possible to run Reveno in cluster with Master-Slave architecture, thus providing decent failover ability.
- https://github.com/rieske/event-sourced-account /java
  - lightweight, frameworkless event sourced Account implementation.
  - The purpose of this project was for myself to better understand the complexities of event sourcing and apply the lessons learned from hype-driven event sourcing implementations gone wrong.
- https://github.com/json-event-sourcing/pincette-jes /java
  - a library that implements event-driven state management for the JSON format, which is used in so many tools. 
  - It requires Apache Kafka for messaging and MongoDB for storing state.
- https://github.com/pavankjadda/KafkaStream-CQRS-EventSourcing /java
  - Event Sourcing(CQRS) and Materialized views with Kafka Streams

- https://github.com/egetman/jes /202006/java
  - Java Event Store implementation
- https://github.com/eventsourcing/es4j /201702/java
  - Event capture and querying framework for Java
  - Instead of mutating data in a database, Eventsourcing stores all changes (events) and what caused them (commands).
  - To make this data useful, Eventsourcing builds indices over it.

- https://github.com/Splitet/SplitetFramework /java
  - a Java based Event Sourcing framework 
  - It has a unique architecture called Operation Store™ together with the stack elements including Docker, Kafka, Hazelcast and Cassandra.

- https://github.com/AxonFramework/AxonFramework /apache2/java
  - https://developer.axoniq.io/
  - a framework for building evolutionary, event-driven microservice systems based on the principles of Domain-Driven Design (DDD), Command-Query Responsibility Separation (CQRS), and Event Sourcing.
  - Examples of building blocks are aggregate design handles, aggregate repositories, command buses, saga design handles, event stores, query buses, and more. 
  - The messaging support for commands, events, and queries is at the core of these building block
  - The most accessible and quick road forward would be to use Axon Server to seamlessly adjust message buses to distributed implementations. 
  - https://github.com/m-reza-rahman/gift-card-simple
    - This simple application demonstrates the CQRS and Event Sourcing patterns using the Axon Java Framework. 

- https://github.com/confluentinc/ksql /ConfluentLic/java
  - https://ksqldb.io/
  - a database for building stream processing applications on top of Apache Kafka. 
  - It is distributed, scalable, reliable, and real-time. 
  - Streams and tables - Create relations with schemas over your Apache Kafka topic data
  - Materialized views - Define real-time, incrementally updated materialized views over streams using SQL
  - support push and pull queries
  - ksqlDB allows you to define materialized views over your streams and tables. Materialized views are defined by what is known as a "persistent query". These queries are known as persistent because they maintain their incrementally updated results using a table.

- https://github.com/hallgren/eventsourcing /go
  - an experiment to try to generialize @jen20's way of implementing event sourcing.
  - [Event Sourcing in Go - jen20.dev](https://jen20.dev/post/event-sourcing-in-go/)
    - https://github.com/jen20/go-event-sourcing-sample
  - [Event sourcing a year later](https://www.reddit.com/r/golang/comments/mp8j2h/event_sourcing_a_year_later/)
    - The main pkg is now totally free from dependencies and instead event stores and snapshot stores are implemented as sub modules making there dependencies isolated.
- https://github.com/looplab/eventhorizon /go
  - a CQRS/ES toolkit for Go.
  - NOTE: Event Horizon is used in production systems but the API is not final!
- https://github.com/ThreeDotsLabs/watermill /go
  - library for working efficiently with message streams. 
  - It is intended for building event driven applications, enabling event sourcing, RPC over messages, sagas
  - You can use conventional pub/sub implementations like Kafka or RabbitMQ, but also HTTP or MySQL binlog if that fits your use case.
  - event-driven architecture, messaging, stream processing, CQRS - use it for whatever you need
  - Flexible with middlewares, plugins and Pub/Sub configurations.
- https://github.com/dapr/dapr /go
  - https://dapr.io/
  - a portable, event-driven, runtime for building distributed applications across cloud and edge.
  - Dapr injects a side-car (container or process) to each compute unit. The side-car interacts with event triggers and communicates with the compute unit via standard HTTP or gRPC protocols
  - Dapr uses pluggable component state stores and message buses such as Redis as well as gRPC to offer a wide range of communication methods, including direct dapr-to-dapr using gRPC and async Pub-Sub with guaranteed delivery and at-least-once semantics.
- https://github.com/get-eventually/go-eventually /go
  - Idiomatic library to help you build Event Sourced application in Go.

- https://github.com/inklabs/rangedb /go
  - an event store database written in Go. 
  - This package includes a stand-alone database and web server along with a library for embedding event sourced applications.
  - RangeDB supports various backend database engines: PostgreSQL, LevelDB, EventStoreDB, In Memory
  - DDD-CQRS-ES slack group channel: #rangedb

- https://github.com/dhamidi/ess /go/inactive
  - provides a library for building event sourced systems.

- https://github.com/pyeventsourcing/eventsourcing /python
  - https://eventsourcing.readthedocs.io/
  - A library for event sourcing in Python.

- https://github.com/gklijs/bkes /rust/java
  - Binary Kafka backed Event Store
  - a POC status project and should not be used in production.
  - The main goal is to have a fast, low memory event store backed by a Kafka topic.
  - https://github.com/gklijs/bkes-demo /clojure

- https://github.com/RBMHTechnology/eventuate /scala/201810/inactive
  - http://rbmhtechnology.github.io/eventuate/
  - a toolkit for building applications composed of event-driven and event-sourced services that communicate via causally ordered event streams.
  - Services can either be co-located on a single node or distributed up to global scale.
  - written in Scala and built on top of Akka
  - provides implementations of operation-based CRDTs
  - [A service framework for operation-based CRDTs - Martin Krasser's Blog](http://krasserm.github.io/2016/10/19/operation-based-crdt-framework/)
    - The two CmRDT update phases, prepare and effect, are closely related to the update phases of event-sourced entities, command handling and event handling
# cqrs/event-driven
- https://github.com/awakelife93/msa-ddd-with-event-sourcing-cqrs-pattern /ts
  - Microservice + DDD Architecture + Event Sourcing + CQRS pattern
  - The RDBMS used in the example is MySQL, and NoSQL is MongoDB. And Redis is used as the message queue (MQ)

- https://github.com/Eveble/eveble /ts/提交多
  - event sourcing framework with modular architecture for DDD(Domain Driven Design) applications in Node.js

- https://github.com/ddd-ts/monorepo /ts
  - Tools facilitating Domain Driven Design and Event Sourcing. 
  - Work in progress, but already used in production.
  - traits: A typesafe library for implementing the trait pattern.

- https://github.com/snatalenko/node-cqrs /MIT/js
  - CQRS backbone with event sourcing for Node.js
  - The package provides building blocks for making a CQRS-ES application. 
  - It was inspired by Lokad. CQRS, but not tied to a specific storage implementation or infrastructure. 
  - It favors ES6 classes and dependency injection(di0), so any components can be modified or replaced with your own implementations without hacks to the package codebase.

- https://github.com/coal182/typescript-ddd-shop /ts
  - Bookstore API with CQRS, Event Sourcing, DDD
  - This project uses DDD with Hexagonal Architecture, CQRS & Event Sourcing

- https://github.com/hdev14/store /ts/提交多
  - Application to learn Hexagonal Architecture, DDD, CQS, CQRS and Event Sourcing.
- https://github.com/wesone/blackrik /js/提交多
  - a CQRS and Event-Sourcing Framework for Node.js

- https://github.com/mauriciomoccelin/neutralize-event-store /ts
  - Simple event source using node, mongo and Kafka to handler events.

- https://github.com/nivinjoseph/n-domain /ts
  - Domain Driven Design and Event Sourcing based framework for business layer implementation.

- https://github.com/cms-DQM/runregistry /js
  - run registry is a full-stack javascript application. 
  - With a frontend built with React and a backend built with Node.js, it uses a PostgreSQL database instance running in CERN DB on demand and a redis microservice to handle the job queue for backend processing.
  - Run registry is designed using loosely-coupled microservices
  - There are two ways that Run Registry uses Event Sourcing: for configuration, and for data.

- https://github.com/s4nt14go/white-label /ts
  - Serverless Domain-Driven Design (DDD) with unit tests
  - This project exemplifies a CreateUser use case and how we can trigger an event, signaling we have a new user onboard.
  - DBs: PostgreSQL CockroachDB Serverless and DynamoDB
  - ORM: Sequelize
  - AWS services: Lambda, AppSync, Systems Manager Parameter Store
  - I started this project using Khalil Stemmler's white-label users module and applied some concepts based on Vladimir Khorikov courses where he tackles DDD in a great way.

- https://github.com/CodelyTV/typescript-ddd-example /ts
  - Example of a Typescript application following Domain-Driven Design (DDD), Command Query Responsibility Segregation (CQRS) and Event-Driven Architecture (EDA) principles keeping the code as simple as possible
  - https://github.com/CodelyTV/typescript-ddd-skeleton

- https://github.com/node-ts/ddd /ts
  - Domain Driven Design framework for software simplicity in node
- https://github.com/almin/almin /ts
  - an implementation of Read/Write Stack Architecture that is well-known as Flux/CQRS.
  - Almin provides some patterns, is not a framework.

- https://github.com/YisusYaro/typescript-ddd-example /ts
  - Typescript example using driven domain design and cqrs.

- https://github.com/remesh-js/remesh /608Star/MIT/202307/ts
  - https://remesh-js.github.io/remesh/dist/index.html
  - CQRS-based DDD framework for large and complex TypeScript/JavaScript applications
  - 依赖rxjs
  - Framework-agnostic(officially supports React/Vue)
  - Time-Travel/Undo/Redo supports(via remesh/modules/history)
  - Domain-Driven-Design inspired the conceptual model
  - CQRS/ES inspired the architecture model
  - Redux inspired the implementation of command model
  - Recoil inspired the implementation of query model
  - Rxjs inspired the implementation of the event model

- https://github.com/sebastianwessel/purista /ts
  - A backend framework for keeping professional software development fast, efficient
  - This framework adapts and combines a wide range of different patters from domain driven design, cqrs, microservice, event sourcing and lambda functions.
  - It is built from the ground up in typescript and highly focuses on schema, and auto generation of types, input-output-validation, OpenApi documentation (swagger) and tracing via OpenTelemetry.

- https://github.com/inngest/inngest-js /ts
  - Serverless event-driven queues, background jobs, and scheduled jobs for Typescript.
  - Works with any framework and platform.
  - Reliably respond to webhooks, with retries & payloads stored for history

- ddd-forum /1.8kStar/ISC/202306/ts/hacker-news
  - https://github.com/stemmlerjs/ddd-forum
  - https://dddforum.com/
  - Hacker news-inspired forum app built with TypeScript using DDD practices from solidbook.io.
  - 后端依赖 express、sequelize、redis
  - 前端依赖 react、redux、react-quill
  - https://github.com/dyarleniber/typescript-ddd-forum

- https://github.com/tonyfromundefined/eventive /ts
  - Event Sourcing Framework in MongoDB

- https://github.com/yysun/apprun /MIT/ts
  - https://apprun.js.org/
  - https://dev.to/yysun
  - a JavaScript library for developing high-performance and reliable web applications using the elm inspired architecture, events and components.
  - view is a pure function to display the state
  - State management and routing included
  - No proprietary syntax to learn (no hooks)
  - Use directly in the browser or with a compiler/bundler
  - Advanced features: JSX, Web Components, Dev Tools, SSR, etc.
  - [AppRun runs on both client and server side to allow event firing and handling between the frontend app and backend business logic modules using WebSockets, no REST API.](https://twitter.com/apprunjs/status/1237064423191252992)

- https://github.com/deepstreamIO/deepstream.io /ts
  - https://deepstream.io/
  - deepstream is an open source server inspired by concepts behind financial trading technology. 
  - It allows clients and backend services to sync data, send messages and make rpcs at very high speed and scale.
  - records are schema-less, persistent json documents that can be edited and observed. Changes are persisted and synced across clients and saved in cache/storage.
  - events allow for high performance, many-to-many messaging. deepstream provides topic based routing from sender to subscriber, data serialisation and subscription listening.
  - rpc: Clients can register functions to be called by other clients.

- https://github.com/PipedreamHQ/pipedream /7.1kStar/Paid/202309/ts
  - https://pipedream.com/
  - an integration platform for developers.
  - provides a free, hosted platform for connecting apps and developing event-driven automations. 
  - The platform has over 1, 000 fully-integrated applications, so you can use pre-built components to quickly send messages to Slack, add a new row to Google Sheets, and more.
  - This repo contains: The code for all pre-built integration components
  - Pipedream imposes limits on source and workflow execution, the events you send to Pipedream, and other properties by free/paid tier
  - [If Pipedream doesn't support Self-Host, what's the repo for?_202305](https://github.com/PipedreamHQ/pipedream/issues/6365)
    - contains all the code for Pipedream's app, actions and triggers. The code is deployed to Pipedream system.
    - Currently, Pipedream does NOT offer self-host option.

- https://github.com/moleculerjs/moleculer /js
  - https://moleculer.services/
  - powerful microservices framework for Node.js. 
  - support event driven architecture with balancing
  - https://github.com/davidnussio/moleculer-cqrs-skeleton /js
  - https://github.com/davidnussio/moleculer-cqrs /js
  - https://github.com/moleculerjs/moleculer-db /js
    - Database access service mixins for Moleculer

## cqrs-non-js

- https://github.com/serverlesstechnology/cqrs /278Star/apache2/202309/rust
  - A lightweight, opinionated CQRS and event sourcing framework targeting serverless architectures.
  - Event sourcing uses the generated events as the source of truth for the state of the application.
  - Three backing data stores are supported: mysql, pg, dynamodb
  - https://github.com/serverlesstechnology/cqrs-demo
    - Demo application using the axum http server.

- https://github.com/johnbcodes/cqrs-es-demo-sqlite /rust
  - A demo application for the cqrs-es and sqlite-es crates
  - A demo application using the cqrs-es framework with a backing SQLite repository.

- https://github.com/johnbcodes/sqlite-es /rust
  - An SQLite implementation of a cqrs event store.
  - An SQLite implementation of the PersistedEventRepository trait in cqrs-es.

- https://github.com/cq-rs/cqrs /201909/rust
  - An event-sourced command-query system for Rust
  - cqrs is an event-driven framework for writing software that uses events as the "source of truth" and implements command–query responsibility separation (CQRS).
  - The framework is written to be applicable to a generic backend, with an implementation provided for a PostgreSQL backend.
  - The source repository also contains a binary in the cqrs-todoql-psql directory which demonstrates the use of the todo domain in concert with the `PostgreSQL` backend and a `GraphQL` frontend using the `juniper` crate.

- https://github.com/serverlesstechnology/dynamo-es /rust
  - An implementation of a cqrs event store using AWS DynamoDB.
  - A DynamoDB implementation of the PersistedEventRepository trait in cqrs-es.

- https://github.com/brendanzab/chronicle /201703/rust
  - An event sourced CQRS framework for Rust
  - [A reading list that I'm collecting while building my Rust ES+CQRS](https://gist.github.com/brendanzab/a6073e73f751a6ca9750f960a92f2afe)
# utils
- https://github.com/futurist/edata /js
  - Turn javascript data into observable reactive EventEmitter with value getter/setter, lodash style path, and keep Event Sourcing in mind.
  - the nested observable reactive EventEmitter with .value getter/setter, lodash style path, and keep Observer Pattern in mind.
  - It roughly referenced Object.observe API, but instead **using getter/setter to wrap object, lightweight than Proxy**.

- https://github.com/coriolisjs/coriolis /js
  - Event sourced effect management for Javascript
  - a Javascript library allowing you to set up an event store supplying effects based on projections (a projection is a state deduced from different events )
  - The design of Coriolis was inspired by Redux, seeking to give the role of single source of truth not to the state but to the flow of events, and thus join the concept of Event Sourcing.

- https://github.com/rexxars/eventsource-parser /ts
  - A streaming parser for server-sent events/eventsource, without any assumptions about how the actual stream of data is retrieved. 
  - It is intended to be a building block for clients and polyfills in javascript environments such as browsers, node.js and deno.

- https://github.com/Azure/fetch-event-source /ts
  - A better API for making Event Source requests, with all the features of fetch()
  - This library provides an alternate interface for consuming server-sent events, based on the Fetch API. 
  - It is fully compatible with the Event Stream format

- https://github.com/Sraleik/sorci /ts
  - Small library to be able to do full event sourcing without aggregate easily.
  - an implementation attempt to Dynamic Consistency Boundary (DCB) with typescript & postgres
- https://github.com/sennentech/dcb-event-store /ts
  - Dynamic Consistency Boundary Event Store for nodejs/typescript

- https://github.com/shoonia/storeon-velo /js
  - A tiny event-based state manager Storeon for Velo by Wix.
- https://github.com/wix/velo-external-db /ts
  - https://www.wix.com/velo
  - Velo by Wix is a development platform built on top of Wix, adding a built-in database and node.js backend. 
  - The built-in database is a document based database optimized for websites and content.
  - it can support 10K - 100K records, and for some workloads even more
  - It is globally replicated, has native support for PII encryption, GDPR, and other non-functional features
  - However, requirements for data locality, regulations, data ownership, dedicated infrastructure, or workloads that demand specific engines may require an external database. This adapter enables connecting external database engines to your site.
  - Velo lets you connect an “external database” and map the structures of the underlying tables as wix-data collections. Once connected, you can work with the database and it’s collections in your site just as you would with the built-in database.

## distributed-es

- https://github.com/saarw/flushout /MIT/201910/ts/NoDeps
  - a distributed data model based on event sourcing. 
  - Collaborative applications use it for clients that need responsive interaction without network delay, or need to function offline.
  - Clients interact with a local proxy of a remote master model without accessing the network. They can then periodically flush changes from the proxy to the master in the background when the network is available.
  - Minimizes network traffic by only initializing clients with the latest model snapshot and then only send updates
  - Storing update history is optional and command history is kept separate from the model state
  - A document in Flushout is a simple JavaScript object that may contain primitive fields or additional object fields to form a tree graph. Applications modify the model by applying commands. A snapshot is simply a document and a count of how many commands have been applied to the document.
  - [Building a collaborative React app with Flushout_202003](https://saarw.github.io/dev/2020/03/02/building-a-collaborative-react-app-with-flushout.html)
  - https://github.com/saarw/flushout-example /ts
    - A collaborative todo-list application using Flushout
  - https://twitter.com/saarw/status/1393631422150320133
    - Abandoned the very general approach for my event sourcing-based model Flushout 
    - Figured consistency requirements are app-specific and can be implemented on top with interceptors or even CRDTs, without incurring their impractical model size for other apps
    - Realized models in my side-project apps aren't large enough to really need incremental updates, but get it for free with Flushout if I start saving command history to support undo or history views...

- https://github.com/dasmeta/event-manager-backend /ts
  - Node.js backend that handles event store, monitoring and retries
  - The service is based on Strapi JS framework.
# redux-like-state-management
- tips
  - redux/logux
  - event-store类似内存数据库，也可作为一种状态管理方式

- https://github.com/Skutopia-org/es-reduxed /ts
  - offers an easy way to build an event-sourced backend using the redux pattern javascript developers are familiar with.
  - Comes with a Postgres backed event store
  - Setting up Redux-Devtools for serverside debugging
  - Events and actions are very similar, and the difference is mostly a matter of semantics, but in programming, semantics matter. 
    - Events describe something that occurred in the past tense, and may include a payload of data describing what happened
    - Actions describe an imperative behaviour or command. They are analogous to CQRS style commands, but not strictly. Actions describe a thing that is occurring or must occur
    - es-reduxed recommends always using events written in the past tense for your event sourcing solution.

- https://github.com/flux-capacitor/flux-capacitor /MIT/js/inactive
  - Flux architecture for the backend. Realtime data and time travel capabilities included.
  - Works like Redux. Dispatch events to change database data
  - Events are persisted, thus tracking the database's history
  - Pushing realtime data becomes trivial, since you can subscribe to the store for updates
  - **Isomorphic reducers - Share code between back end and front end**
  - Middleware concept, compatible with Redux middleware
  - No lock-in: Ability to opt-out any time and just use the underlying database directly
  - Finer-grained access control - Control write access by event type, not only by table
  - Works with PostgreSQL, MySQL, SQLite & MSSQL using Sequelize right now
  - It is related to CQRS, but no traditional CQRS. Rather something between common CRUD and traditional CQRS.
  - Differences to Redux
    - Reducer's signature is `(collection, event) => changeset` instead of `(state, action) => state`. The `action` and the `event` are just synonyms.The real difference is that the flux capacitor reducers take a database collection and return a changeset (a set of database operations).
    - This is necessary, since we usually cannot hold the complete database in memory as opposed to Redux' state.
  - Differences to traditional CQRS
    - No distributed system by default, but just one data storage service (can be easily turned into a cluster, though)
    - No aggregates, just one read model to check business rules when handling an event
    - Depends on database transactions to ensure data consistency

- https://github.com/camjackson/redux-eventstore /201710/js/inactive
  - CQRS, event sourcing, and event collaboration made easy with Node.js, Redux, and Event Store
  - Use this library on your Node.js backend to easily write Redux-style events (usually known as actions) to an Event Store stream.
  - You can also subscribe a Redux store (still on the backend) to the stream, allowing you to page through all the events and reduce it to the current, in-memory state.

- https://github.com/pinyin/flock-js /201902/ts
  - Coordinate React components' states with event sourcing.
  - Inspired by Flux, Redux and Redux Saga.

- https://github.com/event-storm/event-storm /js
  - In-memory event store. A powerful, framework-agnostic store management library.

- https://github.com/XSpecs/DDK /ts
  - An Event-Storm to Event-Sourced application library
  - Some versions of this library has been used to build a number of applications for enterprise clients at our sister company Xolvio

- https://github.com/coderwhy/hy-event-store /js
  - 一个基于事件的全局状态管理工具，可以在Vue、React、小程序等任何地方使用。

- https://github.com/ngxs/store /ts
  - State Management for Angular

- https://github.com/MichalPaszkiewicz/cqrs-react-router /ts
  - A cqrs/event sourcing library built directly into a router you can use in your react application
# examples
- https://github.com/thenativeweb/wolkenkit-boards /js
  - a tool for collaboratively organizing notes.
  - backend is powered by wolkenkit.

- https://github.com/TomaszRewak/TimeWriter /js/依赖少/inactive
  - https://text-sourcing.tomasz-rewak.com/
  - An online collaborative text editor based on event sourcing architecture.
  - Everything here is written from a scratch: including the text editor as well as the event sourcing logic on the server and the client sides.
  - 依赖socket.io、express

- https://github.com/stockulus/pouchdb-event-store /201708/js
  - mimimal eventStore on top of pouchdb

- https://github.com/khaosdoctor/event-sourcing-demo-app /vue
  - Demo application to demonstrate the power of the event sourcing architecture

- https://github.com/totollygeek/node-cqrs /ts
  - Demo code for my CQRS and Event Sourcing session for nodejs

- https://github.com/EternalDeiwos/panmnesia /201712/js
  - An action registry and redux-based aggregate store for a PouchDB-based event stream.

- https://github.com/thomastoye/field-journal /ts/pouchdb
  - https://field-journal.pages.dev/
  - An experimental browser-based, offline-first, event-sourced dispatching, messaging, and incident tracking application.

- https://github.com/StratoKit/strato-db /7Star/MIT/202307/js
  - MaybeSQL with Event Sourcing based on SQLite
  - This project is used in production environments.
  - It works fine with multi-GB databases, and if you choose your queries and indexes well, you can have <1ms query times.
  - Multi-process behavior is not very worked out for the EventSourcingDB

- https://github.com/power-cms/power-cms /ts/inactive
  - a Domain Driven, CQRS based CMS project in Microservices architecture, written for developers.

- https://github.com/dmfrey/event-store-demo /java
  - We recently finished work on a system in which we built an Event Source system. This application is a demo of the architecture we produced.
  - This application is a simple Kanban. It only allows for minimal board and story management.
  - The API application is a common gateway layer between Command and Query applications. The lower applications are separated in typical CQRS fashion. It is a Spring Boot 2 application and is simply a proxy service to the lower apps.

- https://github.com/leweohlsen/kiba /ts
  - event-driven kiosk and bank system - built with React and Electron
  - kiosk and bank system for hassle-free management of accounts, groups, products and transactions
  - React is used along with the UI component library Ant Design and Redux Toolkit is used for state-management
  - All transactions (add account, add product, checkout products, ...) are persisted to a JSONL file. When the application is opened, all historic transactions are replayed to generate the current state (e.g. account balances). 
  - The idea is to keep a complete explainable history that can be inspected in a separate view. Historical events can be used to derive statistics.

- https://github.com/sustainablepace/redux-chess /201708/js
  - React and Redux, CQRS and Event Sourcing

- https://github.com/joeltadeu/bank-account /202201/java
  - Learn to build distributed Event-driven Microservices, CQRS, Event Sourcing using Kafka, MySQL and MongoDB

- https://github.com/dgonzo/eventsourcing-kanban /201710/python
  - Example application to document python eventsourcing library
- https://github.com/Shaibujnr/kanban-ddd /python
  - Simple kanban project 
# cdc/change-data-capture
- https://github.com/fuchstim/horton /202308/ts/未完成
  - an unintrusive Change Data Capture library for postgreSQL databases

- https://github.com/celador/cdc /js
  - Change Data Capture POC
- https://github.com/haiaty/mysql-cdc-redis-stream-poc /js
  - A poc of a mysql change data capture to redis stream

- https://github.com/SurajMazar/postgres-kafka /js
  - Postgres CDC (CHANGE DATA CAPTURE) with debezium and kafka
  - Debezium's PostgreSQL connector captures row-level changes in the database and publishes them as events to Kafka, which can be consumed by other systems in real-time.
- https://github.com/uozuAho/postgres_cdc_demo /js
  - Postgres change data capture (CDC) using Kinesis, to maintain an up to date materialized view
  - A demonstration of CDC usage - maintaining an up-to-date materialized view of a document-oriented database. 
  - Uses postgres, wal2json, nodejs & kinesis.

- https://github.com/groeney/streaming-serverless /201812/js/inactive
  - A framework for business automation using change data capture (CDC) and event driven serverless architecture
  - This tool uses Change Data Capture as the event source and Serverless Architecture as the fundamental design pattern for data processing.
  - As opposed to Apache Kafka where all of the streaming components are packaged up into a platform, this tool aims to give you more control of your event-driven system

- https://github.com/debezium/debezium /java
  - https://debezium.io/
  - provides a low latency data streaming platform for change data capture (CDC). 
  - You set up and configure Debezium to monitor your databases, and then your applications consume events for each row-level change made to the database. 
  - Only committed changes are visible
  - since Debezium records the history of data changes in durable, replicated logs, your application can be stopped and restarted at any time, and it will be able to consume all of the events it missed while it was not running
  - Monitoring databases and being notified when data changes has always been complicated. 
    - Relational database triggers can be useful, but are specific to each database
    - Debezium provides modules that do this work for you. 
    - Some modules are generic and work with multiple database management systems
    - Other modules are tailored for specific database management systems
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
- https://github.com/digidem/unordered-materialized-kv /js/inactive
  - materialized view key/id store based on unordered log messages
  - This library presents a familiar key/value materialized view for append-only log data which can be inserted in any order. 

- https://github.com/boyney123/eventcatalog /ts
  - https://www.eventcatalog.dev/
  - https://app.eventcatalog.dev/
  - EventCatalog is an Open Source project that helps you document your events, services and domains. 
  - Over time our Event Driven Architectures (EDA) grow and it can become difficult to discover and understand our events, schemas, producers, consumers and services. 
  - EventCatalog is built to help you document, visualise and keep on top of your Event Driven Architectures.
- https://github.com/diego3g/flowly /ts
  - helps you document your event driven architecture across your team.
  - built with Next.js 13, Tailwind, shadcn/ui, Clerk and Radix UI.

- https://github.com/MaterializeInc/materialize /rust
  - designed to help you interactively explore your streaming data, perform analytics against live relational data, or increase data freshness while reducing the load of your dashboard and monitoring tasks. 
  - Whenever Materialize answers a query, that answer is the correct result on some specific (and recent) version of your data. Materialize does all of this by recasting your SQL queries as dataflows, which can react efficiently to changes in your data as they happen.
  - Materialize can read data from Kafka (and other Kafka API-compatible systems like Redpanda), directly from a PostgreSQL replication stream, or from SaaS applications via webhooks. It also supports regular database tables to which you can insert, update, and delete rows.

- https://github.com/oskardudycz/emmett /ts/wip/inactive
  - This project aims to deliver an opinionated event store based on my experience working on Marten and EventStoreDB.

- https://github.com/eventsauce/eventsauce /201601/js
  - an event-sourcing/CQRS Framework in Javascript, using ES6 language features.
