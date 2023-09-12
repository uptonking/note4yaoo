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
  - undo/redo
  - 工程类、科学类数据的观测分析
# dev
- [EventSource - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)
  - Warning: When not used over HTTP/2, SSE suffers from a limitation to the maximum number of open connections, which can be specially painful when opening various tabs as the limit is per browser and set to a very low number (6)
  - This limit is per browser + domain
  - The issue has been marked as "Won't fix" in Chrome and Firefox.
  - When using HTTP/2, the maximum number of simultaneous HTTP streams is negotiated between the server and the client (defaults to 100).
  - 对于移动端是够用的
# blogs
- [kappa architecture vs event sourcing](https://github.com/tschudin/ssb-icn2019-paper/issues/6)

## [wix: Event Driven Architecture - 5 Pitfalls to Avoid_202208](https://medium.com/wix-engineering/event-driven-architecture-5-pitfalls-to-avoid-b3ebf885bdb1)

- At Wix we have been gradually migrating our growing set of microservices (currently at 2300) from the request-reply pattern to event driven architecture over the last few years
- Below there are 5 pitfalls that Wix engineers have encountered during our experimentation with event driven architecture.
  - For each pitfall I provide battle-tested proven solutions used at Wix today.

### 1. Write to db and then fire event without atomicity

- Consider for example a simple ecom flow (we will use this example throughout this article)
  - Once the payment processing is done, the product inventory should be updated to reflect that the product is reserved for the customer.
  - Unfortunately, writing the payment-complete status to the database and then producing a “payment completed” event to Kafka (or some other message broker) is not an atomic operation. 
  - There could be situations where only one of the actions actually happens
  - For example, cases such as the database being unavailable, or Kafka being unavailable, could lead to data inconsistency between different parts of your distributed system. 
  - In the case above Inventory levels may become inconsistent with actual orders.

- There are several ways to mitigate this issue. At Wix we utilize two ways

- Atomicity Remedy I — Greyhound resilient producer
  - The first one is our own messaging platform called Greyhound, that allows us to make sure the event is eventually written to Kafka via a resilient producer.
  - One downside of this mitigation is that you can end up with out-of-order processing of events downstream.

- Atomicity Remedy II — Debezium Kafka source connector
  - The second way to make sure both DB update action and Kafka produce action happen and that data remains consistent is using the Debezium Kafka connector. 
  - Debezium connector allows to automatically capture all the change events (CDC) that happen in the database (For MySQL via binlog) and produce them as Kafka events.
  - Kafka Connect together with Debezium DB connectors guarantees that events will eventually be produced to Kafka. 

### 2. Using Event sourcing everywhere

- Event sourcing is a pattern where instead of updating an entity’s state upon a business operation, the service saves an event to its database. 
  - The service reconstructs an entity’s current state by replaying the events.
  - These events are also published on an event bus such that other services can also create materialized views on other databases that are optimized for queries by replaying the events.
- While there are certain advantages to this pattern (a reliable audit log, performing “time travel” — the ability to get the state of your entity at any point in time, and building multiple views over the same data), it is by far more complex than CRUD services that update the state of an entity stored in a database.
- 👎🏻 Disadvantages of event sourcing include:
- 👉🏻 Complexity 
  - In order to make sure read performance is not affected by a growing list of events you need to play, entity state snapshots have to be taken from time to time to reduce the performance penalty.
  - This increases the system complexity with a background process that may have its own issues and when it does the data remain stale. 
  - On top of this, having 2 copies of the data means they might get out of sync.
- 👉🏻 Snowflake nature 
  - Unlike CRUD ORM solutions, It’s harder to create common libraries and frameworks to ease development that can globally solve snapshotting and read-optimizations that can fit for every single use case.
- 👉🏻 Only supports eventual consistency (problematic for read-after-write use-cases)

- 💡 Event Sourcing alternative — CRUD+CDC
- Utilizing both simple CRUD capabilities and publishing database change events (CDC) for downstream uses (e.g. creation of query-optimized materialized views) can reduce complexity, increase flexibility and still allow for Command-Query Responsibility Segregation (CQRS) for specific use cases.
  - For most of the use-cases, the service can expose a simple read endpoint that will fetch the entity’s current state from the database. 
  - As scale increases and more complex queries are needed, the additional published change events can be used to create custom materialized views specifically tailored for complex queries.
- In order to avoid exposing DB changes as a contract to other services, and creating a coupling between them, the service can consume the CDC topic and produce an “official” API of change events similar to the event stream created in event-sourcing pattern.

### 3. No Context Propagation

- Unlike with the request-reply model, there is no explicit chain of HTTP/RPC requests to follow. 
  - Debugging code is harder as event handling code is spread out across the service code instead of being sequentially traceable by clicking into function definitions usually found in the same object/module.

- Automatic Context Propagation
  - Automatically adding identification of the broader request context for all of the events, makes it really simple to filter for all events related to the end-user request. 
  - At Wix, Greyhound automatically propagates the end-user request context when events are produced and consumed. 
  - In addition, the request context is found also in logs infrastructure, such that logs can be filtered for specific user requests.

### 4. Publishing Events with Large Payloads

- When processing large event payloads (payloads bigger than 5MB, e.g. Image Recognition, Video Analytics, etc…) it may be tempting to publish them to Kafka (or Pulsar) but there is a risk of greatly increasing latency
- Large Payloads Remedy I — Compression
  - Both Kafka and Pulsar allow compression of payloads. You can try several compression types (lz4, snappy, etc.)
  - 👉🏻 Compression on Kafka level is usually better than application level, as payloads can be compressed in batches and thus improve compression ratio.
- Large Payloads Remedy II — Chunking
  - to split the messages into chunks.
  - While chunking is already a built-in feature of Pulsar (with some limitations), for Kafka chunking has to happen on the application level.
  - The basic premise is for producers to send out the chunks with additional metadata that helps consumers to re-assemble them.

- Large Payloads Remedy III — Reference to Object store
  - The final approach is to simply store the payload in an object store (such as S3) and pass a reference (a URL usually) to the object in the event payload. 
  - These object stores allow to persist any required size without impacting first byte latency.
  - It’s important to make sure the payload is fully uploaded to the object storage before the link is produced, or else the consumer will need to keep retrying until it can start downloading it.

### 5. Not handling duplicate events

- The term for making sure a side-effect of a duplicate event only happens once is Idempotency.

- Idempotency Remedy — revisionId (versioning)
- Optimistic locking technique can serve as inspiration in cases where idempotency of event processing is needed. 
  - With this technique, the current revisionId (or version) of the stored entity is first read before any update occurs. 
  - If more than one party tries to update the entity (while incrementing the version) at the same time (concurrently), the 2nd attempt will fail as the version will no longer match with what it read before.
- In the case of idempotent handling of duplicate events, the revisionId has to be unique and part of the event itself in order to make sure that two events don’t share the same id and that 2nd updates on the same revisionId will (silently) fail even if does not happen concurrently.
- Specifically With Kafka, there is a possibility to configure exactly once semantics, but still DB duplicate updates can happen due to some failure. 
  - Luckily the txnId in this case can just be the topic-partition-offset which is guaranteed to be unique.

### Summary

- A migration to event-driven architecture can be gradual in order to reduce risks involved with it including harder debugging and mental complexity.
- As a consequence of this gradual migration approach, I strongly recommend to adopt the CDC pattern (Database changes streamed as events) as a way to both ensure data consistency (pitfall #1) and avoid the complexity and risks associated with full blown event-sourcing (pitfall #2). 
- The CDC pattern still allows to have the request-reply pattern in place side by side with the event processing pattern.
- The CDC pattern still allows to have the request-reply pattern in place side by side with the event processing pattern.
- Remediation for Pitfalls #4 and #5 are for more specific uses cases

- ### twitter: Event Driven Architecture — 5 Pitfalls to Avoid_202208
- https://twitter.com/boyney123/status/1559837875834945536
- I'm curious what database and framework you used for event sourcing?
  - I think most cases at @WixEng use #mysql. There are 2-3 custom made libraries created at wix to help with ES implementation.
- One thing I would say is that eventual consistency isn't a requirement of event sourcing.  For instance @marten_lib leverages Postgres transactions to create strongly consistent projections.

- ### [Event Driven Architecture — 5 Pitfalls to Avoid : coding](https://www.reddit.com/r/coding/comments/wor4h2/event_driven_architecture_5_pitfalls_to_avoid/)
- Looks overcomplicated to me. Why just save an event in queue (async) or trigger (sync), and if it fails, rollback the transaction?
  - Wix services don't usually implement the saga pattern (with transaction aborting) but go for best-effort retry mechanism (see more in this post in pattern #4)

- Indeed at Wix there is a hybrid architecture of both request-reply and event-driven.
  - how come 2300? Wix hosts and renders more than 100 million websites, with complete back-office/business solutions as well and an open platform for plugins. with many different verticals (e.g. stores, restaurants, hotels, events, photography). It's a huge production eco-system

- 3 No Context Propagation. This should be number 1 on any list, unless the list also contains something about emergent behavior.

## [wix: The Reactive Monolith - How to Move from CRUD to Event Sourcing_202109](https://www.wix.engineering/post/the-reactive-monolith-how-to-move-from-crud-to-event-sourcing)

- While the traditional CRUD approach to system design focuses on state and how it is created, updated and deleted in a distributed environment by multiple users, the event sourcing approach focuses on domain events, when they happen and how they express business intent. 
  - The state, in the event sourcing approach, is a materialization from events, which is just one of many possible usages of the domain events. 

- 
- 
- 

- ### [How to Move from CRUD to Event Sourcing | Hacker News_202109](https://news.ycombinator.com/item?id=28691728)
- I used to be really excited about event sourcing but yeah, its usually just **over-engineering**. 
  - It appeals to the nerd in me because its a powerful & clean model - events are immutable, your entire database can theoretically be reconstructed at any point in time by just replaying an event log up to time X. 
  - In the ideal form its sort of the highest fidelity version of data storage, throwing nothing away, supporting all ways of querying as materialized views or dependent DBs built on the stream. Its beautiful.
- But also we live in reality. 
- 👉🏻 DBs use checkpoints because storing/replaying an event log from time 0 would take ungodly(骇人的；无法容忍的) amounts of space and time. 
  - You deleted or resized a column to save some space? Lol no, the event log lives forever. 
  - You wanted to use SQL, a battle tested language to query your data? Lol no, the database is "inside out" so tough luck buddy, you're building the database now. 
  - Sure you might have to rebuild compaction, joins, query languages, concurrency control and the other 100 things a DB gives you, but on the plus side that one audit log that you could have built with some glue and a few INSERT triggers in Postgres is now an elegant map/reduce on your 100TB dataset! Yay!

- For non-trivial amounts of data you should combine event sourcing with snapshots - i.e. a somewhat up-to-date materialized view/DB table - so you don't have to start for 0. At that point you can delete older events or move them to cold storage.
  - A valid question then is: "what do you gain over just using the table"? You gain a well-described model of your business domain, with very clear actions about what should happen on which real-world event, and an audit log. Whether that's worth it depend on your use case.
- Secondary benefits include easily being able to share events for new apps or use-cases, business analysts really like them, and making it unlikely things go wrong because data is in an inconsistent state.

- ES is the C in CQRS though. If you're using it for the Q too, then it's no wonder you'll quickly get in a bad way. It's specifically not designed for that.
  - the benefits of ES come on the write side of the equation. Expecting it to solve read-side problems will inevitably lead to disappointment.

- Materialized views are what you should be using, not reconstructing the state from the event log every time. That gives you access to SQL and everything to do with it.
  - And in reality, the event log does live forever in the real world outside of your system. Attributes of your aggregates from last year are still valid for events related to last year, even if they're now deprecated or no longer in use.
  - CQRS/ES is about system design that evolves. It evolves in a much cleaner and easier way if you follow it.
  - Is it perfect? No. There are some gnarly problems related to, for example, GDPR's "right to be forgotten", but that needs to be solved across database backups as well.

- I would like to see answers to the question: why move from Crud to event sourcing. Because I have seen at least 5 moderate projects trying to integrate ES. They all failed in the sense that either people didn't understand the code anymore, huge integration times, performance issues and even complete project cancellation because of all people walking away

- I understand this thread is about dumping on ES... However, I must notice in your case it was an audit log. An ES system wouldn't work at all without access to events.
  - If the ES is "unnecessary", then it's not ES by definition. If events are not your source of truth, it's not event sourcing, just event logging.

- 👉🏻 Two examples of systems that use a variant of event sourcing:
  - relational database systems (their journals and async replication in particular)
  - git
- Git doesn't really store file changes as events, rather, it's a long chain of state snapshots, in something like a persistent data structure. Sure, the history is all there, but so is the current state in its most efficient form.
- DB transaction logs might be considered event sourcing by some definition, but their use is very different. It's purely a technical trick. As a consequence, logs are truncated as often as possible/reasonable, and you never rerun the transaction log from time zero. Very different from the event sourcing idea to keep events as long as possible.

- I have never implemented ES, although it seems to be useful to have the most simple version of it in place: just a queryable log of versioned events and the ability to replay it.

- Event sourced systems are actually great, as long as they aren’t branded as such. Most of the time it’s totally stupid and the state of the system isn’t reproducible anyway unless the event code is never modified.

- Extra layer of complexity. More development time. More tech dependencies. Don't use it when not needed.

- Event sourcing is decent when you ingest a lot of things that are mostly one way and immutable once they come into your system.
  - If you have bidirectional communication, you wind up contorting yourself into a pretzel to bury "state" into your event streams.

- It is striking that this thread attracts so much negative commentary, while a similar thread 49 days ago is the exact opposite. 
  - this one is about moving from CRUD, that is the most mainstream paradigm on software development into what is solution to a very niche problem, while the other is just about the solution

- As a proponent of Radical Simplicity, I'm always sceptical about event sourcing.
  - There are some benefits (I found it useful to replay events for example), but where I have seen it at work it makes things much more complex, the understanding of the system and the development of new features takes much longer.

- then you realize that the CRUD db you moved away from operates on event sourcing (WAL) anyway. And thus you’re just doing inner platform effect.
  - Correct, and many applications are using WAL via **CDC (Change Data Capture)** to gain some of the benefits of the CQRS/ES.
  - The problem is that the CRUD is only recording "What" change/mutation was done, but not "Why" by "Whom", and "When" it was done. With tailing WAL / CDC you can also capture the "When".
  - This can be partially mitigated by adding audit fields
# more

# discuss-cons
- ## 

- ## [Ask HN: When should event-driven architecture be avoided? | Hacker News](https://news.ycombinator.com/item?id=30206046)
- No concurrency? No events. 
  - No more than a single team running a single service (even a monolith)? No events. 
  - Not dealing with asynchronous 3rd party APIs (eg: webhooks)? No events. 
  - Not dealing with arbitrarily many hosts/processes/tasks/objects communicating with each other, potentially asynchronously? No events. 
  - Not streaming? No events.

- When unrestricted, event driven systems don't have a well defined overall state or consistency. Avoid if you have rules that depend on a system "state" Having said that, toy systems aside, almost all systems require reasoning of their overall state at some point, so in general - avoid.

- The approaches you listed are useful, and the dissent I have isn’t so much on the approach, as the timing of when it gets used. Tons of software will never need its benefits and shouldn’t pay the tax ever. Paying the tax before you have to is very rarely worth it in my experience.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## there are various reasons to choose event sourcing:
- https://twitter.com/SKleanthous/status/1464271243146891289
  1. To just remove the issue of db migrations
  2. Persisting context along data
  3. Temporal aspect of data
  4. Immutability as an enabling constraint
  5. Easier data design process
- to be clear: I'm not saying that event sourcing should be used in all cases blindly! I am referring to situations where one of the benefits described above apply, so event sourcing would provide some value.

- https://twitter.com/SKleanthous/status/1469325575160537094
- Building an aggregate root by reading the event stream, replaying events to build up the current state (projection). Invoking a command that validates against the current state. Persisting new events to the stream... this doesn't require more than the SDK for the event store.
  - Just to be clear, that's what I was trying to convey too: that reading, replaying events to get the current state, persisting new events don't need anything other than the SDK to a good event store.
  - I do believe that a library could help, by reducing the amount of cross-cutting concerns that need to be built, but opinionated frameworks could be a problem to remove if they end up not being good.

- ## [Ask HN: Has anyone fully embraced an event-driven architecture? | Hacker News_202108](https://news.ycombinator.com/item?id=28034882)

- using events like this requires a very tight integration between event producer and consumer, so I don't think this will translate well to distributed systems or microservices.

- We used Kafka for event-driven micro services quite a bit at Uber. 
  - A large portion of the topics we had went on to become analytical tables in Hive. Breaking changes would break those tables. 
  - If you absolutely have to break the schema, make a new topic with a new consumer and phase out the old. This puts a lot of onus on the producer, so we tried to make tools to help. 

- I've been working on a contract for 6 months where the architecture is microservices and queues.
  - IMO: It's over-complicated. They can ship a change to a microservice while insulating the other services from risk, but that's just kicking the can for technical debt.
  - IMO: Don't get too hung up on microservices and events. Focus on writing simple, straightforward code that's easily testable. 

- Where I currently work we are all in on event-driven architecture. 
  - For our DLQs, we have alerts on when the queue is growing in size or if messages are in the queue too long. 
  - When those alerts come in, we manually move the messages back to the normal queue for reprocessing and if they get DLQed again after that we will look into the reason it is failing.
- One of the benefits of this architecture for us is the ability to easily share information between services. 
  - We utilize SNS and SQS for a pub/sub architecture so if we need to expose more information we can just publish another type of message to the topic or if we need to consume some information then we can just listen to the relevant topic.
- There are two big issues that I've run into while at this company. 
  - One is tracking down where events are coming from can be a big pain, especially as we are replacing services but keeping message formats the same. 
  - The other big issue is setting up lower environments (dev, qa, etc) can be difficult because you pretty much need the entire ecosystem in order for the environment to be usable, which requires buy-in from all teams in the organization

- If you want to use event driven + microservices, first make sure microservices make sense. Event driven is just a cool way to tie monstrous collections of services together if you have to go down that road.

- It was great for certain use cases, bad for others. The architecture made it so it took days to do simple features like adding a sortable column.

- 👉🏻 I work for a big AI consultancy. Most of the time we build ETLs for the data-engineering side, in a client driven capacity-building effort. We do this because our focus is on Data Science, not data engineering, and we often work in situations where the client doesn't have an existing data science platform. It's simpler to build, to handover and later to maintain.
  - Even-driven systems are much more robust than traditional ETLs with a central data warehouse, but they are also **much more complex to understand and operate**. 
  - In the end, we rarely deploy them because they cost us way too much engineering time compared to the benefits. That's mostly because we spend >70% of our time dealing with "security teams" and "access issues". Seriously.

- Operational support is more interesting with this kind of an architecture. Dealing with message queues and all that can be challenging for a traditional organization.

- Yes. It's my preferred architecture for any non trivial system. The single biggest downside to it is it's really hard to find people with experience building event driven systems.

- No. In my programs I try to hold John Carmack's advice, that there is no better understandable structure than a large program that you can read from start to end. He is talking about a main game loop, but I found that this advice holds. Nothing beats being able to step the function step by step and see all the variables.

- we're building a database software called TypeDB. The internals are quite event-driven mainly realised with the actor model and event-loop concurrency.
  - It has allowed us to scale mainly in two ways: maximising parallelism with respect to CPU, and doing other works while waiting for an RPC call to return.
  - Event-driven architecture by nature is more parallel and efficient, but comes with a weaker consistency guarantee when it comes to the ordering of events coming from multiple parallel sources.

- I maintain a legacy application which was written in a fully event-driven way
  - The original author(s) of this application also embraced a multi-threaded paradigm and use their own homegrown asynchronous serial message and event system (built on top of Windows messages).
  - It's terrible. The reason it's terrible is that you can't use function call graphs, single stepping, or call stacks to debug this application. Everything happens indirectly by one part of the application throwing a message in a bottle into the ocean, and another part of the application (running on another thread) finding the bottle at a later time. And every message is written in a different binary format (different memcpy'd structs) which is mutually intelligible to each sender-receiver pair and no one else.
  - Troubleshooting and understanding this system is more akin to endocrinology or ecology than math or engineering.

- The problems we face are:
  - it's slow to evolve the very core of the system
  - we need perfect ordering, there will always be time wasted at the sequencer to transform unordered "commands" for the various services into perfectly ordered events
  - testing and debugging is an art that takes time to acquire
  - it takes up to a year for a new Java dev to get productive on such an exotic mindset
  - management cannot understand why they can't cut cost using the cloud, virtual machines, vendor databases etc

- If you think about it, modern front end web development (with React + Redux) is event-driven! In a way, there are tons of people embracing it’
- Window systems are classically event-driven. Especially earlier single-thread ones from Microsoft.

- ## [技术选型：消息队列应该选 ActiveMQ、RabbitMQ、RocketMQ 还是 Kafka ？ - 知乎](https://www.zhihu.com/question/381653287)
  - [mq选型：rocketMq和kafka对比 - 知乎](https://zhuanlan.zhihu.com/p/163246737)

- 这些消息队列工具都有自己的特点和应用场景
  - ActiveMQ是Apache出品的开源消息队列系统，支持多种传输协议和多种编程语言。它适合于中小规模的应用场景
  - RabbitMQ是一个开源的AMQP消息代理，由Erlang语言编写。它适合于处理大量的消息、实时应用和高可用性的场景
  - RocketMQ是阿里巴巴出品的开源消息队列系统，适合于大规模的分布式系统。它支持丰富的消息模型和高可用性的特性，比如分布式事务、数据重放和消息轨迹等。
  - Kafka是一个高吞吐量的分布式发布订阅消息系统，由Scala语言编写。它适合于大规模的分布式系统、流处理应用和大数据处理场景。Kafka使用基于磁盘的存储方式
- ActiveMQ和RabbitMQ使用的是队列模式，它们将消息发送到队列中，消费者从队列中获取消息。
  - ActiveMQ使用JMS API来实现，而RabbitMQ使用AMQP协议来实现。
- RocketMQ和Kafka则使用的是发布/订阅模式。
  - 在这种模式下，生产者将消息发布到一个主题(topic)中，消费者订阅该主题并从中获取消息。
  - RocketMQ使用了类似于JMS的API来实现，而Kafka则使用了自定义的API和协议。
- 此外，这些消息队列工具在实现上还有一些不同之处，比如消息存储方式、集群管理方式、性能表现等方面。

- Kafka 的吞吐量极高，但可能会丢失数据，社区活跃。

- 如果是对可靠性要求较高的服务（如订单服务），可考虑使用 RabbitMQ/RocketMQ，
  - 如果对可靠性要求不太高、追求高吞吐量的服务（如日志服务），可考虑使用 Kafka。

- ## what ORM or library do you use to query your data?
- https://twitter.com/Gabriel_RABHI/status/1656171263373586433
- In the past, I've used Dapper. Good. But now... no more database.
  - Event Sourcing -> in Memory projections. 
  - I use my own transactional, in virtual memory object repository : ACID, secure and 1000x time faster than any Entity Framework DB.
- I have too few time left to publish the lib... It use LMDB underway, and use the "no copy" b+tree data access mechanism.
- The main benefits are :
  - Zero latency to get objectifs (if hot datas fits in memory, to avoid disk reads)
  - No more async code (no need of)
  - Really fast : 3 M individual, lazy loading / 15 M enumeration, per thread per second
  - Lockless concurrent access to objects
- I use it to develop web solutions in Blazor Server Side (LOB kind of software). It is extremly productive to access instantly to any object without lantecy, fully lazy (no group queries). It can manage up to terybytes of objects.
  - I'm working on this concept since 2009... many versions, based on many approaches. The full in-memory . Net (simply put billions objects in lists), was a fail because GC freeze becomes a big problem. That's why this objects have to be in native memory.
  - So, I've redefined the way to store objects in memory. They are "single block of memory" (even with strings and arrays in it) with a "body" class that works like any C# class from developper point of view, but internaly manage this external virtual memory.
  - Because it use a "single memory block" approach, it can be faster than native . Net objects in many use cases : init, creation, serialization, immutability, deep copy or compare are faster than POCO !
  - And of course, this objects can be stored in a LMDB key/value store, wich is near a "silver bullet" when used in the right way, a f***in piece of C code... So, the most critical part - the persistance, ACID -  is based on a robust, fast, well tested OS lib.
