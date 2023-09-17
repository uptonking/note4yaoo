---
title: pattern-arch-event-sourcing-examples
tags: [event-sourcing, examples]
created: 2023-09-12T09:37:11.161Z
modified: 2023-09-12T09:37:22.608Z
---

# pattern-arch-event-sourcing-examples

# guide

- es-db
  - 还可参考stream/kappa架构

- https://github.com/heynickc/awesome-ddd
  - A curated list of Domain-Driven Design (DDD), Command Query Responsibility Segregation (CQRS), Event Sourcing

- [@resolve-js/core vs eventstore vs wolkenkit vs create-resolve-app | npm trends](https://npmtrends.com/@resolve-js/core-vs-eventstore-vs-wolkenkit-vs-create-resolve-app)
# popular
- https://github.com/xolvio/typescript-event-sourcing /ts
  - Domain Driven Design, Event Sourcing & Command Query Responsibility Segregation with Typescript

- https://github.com/oskardudycz/EventSourcing.NodeJS /ts
  - Examples and Tutorials of Event Sourcing in NodeJS
  - I already have samples of Event Versioning and Snapshots in my sample repo. 
  - [Introduction to Event Sourcing - Self Paced Kit_202203](https://event-driven.io/en/introduction_to_event_sourcing/)
  - https://github.com/oskardudycz/EventSourcing.JVM
  - https://github.com/PDMLab/mongo-eventstore /ts
    - Eventstore for Node.js build on top of MongoDB
    - https://github.com/AlexZeitler/mongo-eventstore-sample

- https://github.com/sugarandmagic/sequelize-mv-support /MIT/ts
  - This package adds support for Views and Materialized Views in Sequelize.
  - We're heavy users of views and materialized views, but we use Sequelize a lot for bootstrapping and testing database schema. 
  - this module adds support for both views and materialized views to Sequelize, as well as properly exporting typescript declarations.
  - All the original Sequelize methods and options still work with this module

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
  - https://github.com/thenativeweb/wolkenkit-eventstore /AGPLv3/ja
    - eventstore for Node.js that is used by wolkenkit.
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
    - https://github.com/saperiuminc/node-eventstore

- https://github.com/cloudnativeentrepreneur/sourced /ts
  - https://github.com/mateodelnorte/sourced /js
  - Tiny framework for building models with the event sourcing pattern (events and snapshots) that works in Node.js and the browser
  - Unlike Active Record where entity state is persisted on a one-model-per row database format, event sourcing stores all the changes (events) to the entity, rather than just its current state. 
  - The current state is derived by loading all events, or a latest snapshot plus subsequent events, and replaying them against the entity.
  - Sourced makes no assumptions about how you store your events and snapshots. 
    - The library is small and tight with only the required functionality to define entities and their logic, enqueue and emit events, and track event state to later be persisted. 
  - https://github.com/mateodelnorte/sourced-repo-mongo
    - mongo data store and repository for sourced-style event sourcing models
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
  - Making Event Sourcing easy
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

- https://github.com/snatalenko/node-cqrs /MIT/js
  - CQRS backbone with event sourcing for Node.js
  - The package provides building blocks for making a CQRS-ES application. 
  - It was inspired by Lokad. CQRS, but not tied to a specific storage implementation or infrastructure. 
  - It favors ES6 classes and dependency injection(di0), so any components can be modified or replaced with your own implementations without hacks to the package codebase.

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

- https://github.com/Silly-Goose-Software/event-sauced-ts /ts/inactive
  - started out as a re-implementation of ASOS/SimpleEventStore in TypeScript. 
  - What was initially just a simple re-write, is slowly becoming a more featured library.
  - The goal is to be provide a database-agnostic API for an event store.
  - https://github.com/Silly-Goose-Software/event-sauced-ts-postgresql

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

- https://github.com/cms-DQM/runregistry /js
  - run registry is a full-stack javascript application. 
  - With a frontend built with React and a backend built with Node.js, it uses a PostgreSQL database instance running in CERN DB on demand and a redis microservice to handle the job queue for backend processing.
  - Run registry is designed using loosely-coupled microservices
  - There are two ways that Run Registry uses Event Sourcing: for configuration, and for data.

- https://github.com/zeppaman/mongo-event-sourcing /js/inactive
  - An open-source fully configurable and extendible tool that enables event sourcing in MongoDB.
  - implement event sourcing listening event from mongodb. 
  - For who is used to play with traditional RDBMS it's something like triggers, but fire events outside database. This application uses the built-in mongodb feature called `ChangeStream`.
  - So, adding MESS in your architecture you can forward event for data changes to applications by using webhook or simply add event to a queue like rabbitMQ or Kibana.

- https://github.com/message-db/message-db
  - http://docs.eventide-project.org/user-guide/message-db/
  - Microservice Native Event Store and Message Store for Postgres
  - A fully-featured event store and message store implemented in PostgreSQL for Pub/Sub, Event Sourcing, Messaging, and Evented Microservices applications.
  - The message store is a single table named messages. 
  - Interaction with the message store is effected through Postgres server functions that ensure the correct semantics for the writing of messages to streams, and the reading of messages from streams and categories.

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

- https://github.com/khaosdoctor/event-sourcing-demo-app /vue
  - Demo application to demonstrate the power of the event sourcing architecture
# es-collab
- https://github.com/andykswong/mithic /MIT/ts
  - https://andykswong.github.io/mithic/
  - Modular library for real-time, offline-first isomorphic JavaScript applications
  - provides the building blocks for creating real-time, offline-first client-server or decentralized applications, using CQRS architecture with CRDT eventsourcing for storage and data replication.
  - minimal example to get started. Uses the Redux store preset
  - crdt基于自己实现的lseq
  - Linear sequence of values based on `ORMap` of base64 fractional index to values
  - timestamp基于逻辑时钟

- https://github.com/soundcloud/roshi /3.1kStar/bsd/go/soundcloud
  - Roshi implements a time-series event storage via a LWW-element-set CRDT with limited inline garbage collection. 
  - Roshi is a stateless, distributed layer on top of Redis and is implemented in Go. 
  - It is partition tolerant, highly available and eventually consistent.
  - [Roshi: a CRDT system for timestamped events | SoundCloud Blog_201405](https://developers.soundcloud.com/blog/roshi-a-crdt-system-for-timestamped-events)

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
# non-js
- https://github.com/serverlesstechnology/cqrs /rust
  - A lightweight, opinionated CQRS and event sourcing framework targeting serverless architectures.
  - Event sourcing uses the generated events as the source of truth for the state of the application.
  - https://github.com/serverlesstechnology/cqrs-demo

- https://github.com/get-eventually/eventually-rs /rust
  - Collection of traits and other utilities to help you build your Event-sourced applications in Rust.
  - https://github.com/pholactery/eventsourcing /rust/inactive

- https://github.com/primait/event_sourcing.rs
  - opinionated library used to achieve cqrs/es in Rust.
  - Event Sourcing RS uses under the hood sqlx.

- https://github.com/tomcumming/simples /rust/inactive
  - tiny event sourcing database for prototype and small projects.
  - Designed to preserve data even when crashing mid-write. Ready to relaunch immediately.
  - Written in Rust, using Tokio and Hyper.
  - Uses little more disk space than the contents of the topics.

- https://github.com/palfrey/potboiler /rust
  - an AP Event Sourcing system. it's an MVP/research prototype 
- https://github.com/cosmonic/concordance /rust
  - opinionated event sourcing framework from Cosmonic
  - Building on the power, portability, speed, and scalability of wasmCloud, Concordance allows you to reason about your application using the fundamental building blocks of event sourcing: Aggregates/Projectors
  - https://github.com/wasmCloud/wasmCloud
    - https://wasmcloud.com/docs/intro

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

- https://github.com/alicanli1995/clean-hexagonal-architecture-kafka-saga-outbox /java
  - Food Ordering Project with Clean and Hexagonal Architecture With Kafka Messaging System And Outbox Table
  - Hexagonal (Clean) Architecture -> Port & Adapter Style
  - CQRS Pattern : Materialized view & Event Sourcing
  - SAGA Pattern : process & rollback ( compensating transactions )
  - Outbox Pattern : Pulling Outbox Table With Scheduler , Saga Status

- https://github.com/andreschaffer/event-sourcing-cqrs-examples /java
  - examples of how to use Event Sourcing and CQRS applied to a minimalistic bank context.
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

- https://github.com/pyeventsourcing/eventsourcing /python
  - https://eventsourcing.readthedocs.io/
  - A library for event sourcing in Python.

- https://github.com/EventStore/EventStore /csharp
  - https://eventstore.com/
  - The stream database optimised for event sourcing
  - https://github.com/EventStore/samples
  - https://github.com/qooroo/EventStore /legacy
    - Event Store is written in a mixture of C#, C++ and JavaScript. It can run either on Mono or .NET, however because it contains platform specific code (including hosting the V8 JavaScript engine), it must be built for the platform on which you intend to run it.
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
# event-driven
- https://github.com/Judahh/flexiblePersistence /ts
  - A CQRS and Event Sourcing platform
  - It's possible to use different databases or services implementing IPersistence interface, like MongoDB does (MongoPersistence).
  - Other implementations: DAO, Sequelize, Service
  - https://github.com/Judahh/sequelizePersistence

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

- https://github.com/remesh-js/remesh /ts
  - https://remesh-js.github.io/remesh/dist/index.html
  - CQRS-based DDD framework for large and complex TypeScript/JavaScript applications
  - Framework-agnostic(officially supports React/Vue)
  - Time-Travel/Undo/Redo supports(via remesh/modules/history)

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
# state-management
- tips
  - redux/logux

- https://github.com/event-storm/event-storm /js
  - In-memory event store. A powerful, framework-agnostic store management library.
# examples
- https://github.com/TomaszRewak/TimeWriter /js/依赖少/inactive
  - https://text-sourcing.tomasz-rewak.com/
  - An online collaborative text editor based on event sourcing architecture.
  - Everything here is written from a scratch: including the text editor as well as the event sourcing logic on the server and the client sides.
  - 依赖socket.io、express

- https://github.com/StratoKit/strato-db /js
  - MaybeSQL with Event Sourcing based on SQLite
  - It works fine with multi-GB databases, and if you choose your queries and indexes well, you can have <1ms query times.
  - Multi-process behavior is not very worked out for the EventSourcingDB

- https://github.com/power-cms/power-cms /ts/inactive
  - a Domain Driven, CQRS based CMS project in Microservices architecture, written for developers.

- https://github.com/dmfrey/event-store-demo /java
  - We recently finished work on a system in which we built an Event Source system. This application is a demo of the architecture we produced.
  - This application is a simple Kanban. It only allows for minimal board and story management.
  - The API application is a common gateway layer between Command and Query applications. The lower applications are separated in typical CQRS fashion. It is a Spring Boot 2 application and is simply a proxy service to the lower apps.
# more
- https://github.com/digidem/unordered-materialized-kv /js/inactive
  - materialized view key/id store based on unordered log messages
  - This library presents a familiar key/value materialized view for append-only log data which can be inserted in any order. 

- https://github.com/boyney123/eventcatalog
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
