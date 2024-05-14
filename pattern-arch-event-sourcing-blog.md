---
title: pattern-arch-event-sourcing-blog
tags: [blog, event-sourcing]
created: 2023-09-13T14:37:36.816Z
modified: 2023-09-13T14:37:51.659Z
---

# pattern-arch-event-sourcing-blog

# guide

# blogs-cqrs
- [Simple CQRS in NodeJS with Typescript _202301](https://itnext.io/simple-cqrs-in-nodejs-with-typescript-6da6d3e8a420)
  - [How to create simple and scalable event driven NodeJS services. | by Ilija | ITNEXT](https://itnext.io/how-to-create-simple-and-scalable-event-driven-nodejs-services-14e9dee75a74)
# blogs
- [kappa architecture vs event sourcing](https://github.com/tschudin/ssb-icn2019-paper/issues/6)

## [Why Event Sourcing?](https://abdullin.com/post/event-sourcing-why/)

- Flexibility
- Messaging Capabilities
- Improve performance
- Simplify Developer's Life
- Downsides
  - Defining these events is a complex art of it's own, which requires skills in domain modeling 
  - There is little software and hardware to support event sourcing

## 👨🏻‍🏫 microsoft-learn event sourcing

- [Event Sourcing pattern - Azure Architecture Center | Microsoft Learn](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)
- [Materialized View pattern - Azure Architecture Center | Microsoft Learn](https://learn.microsoft.com/en-us/azure/architecture/patterns/materialized-view)
- [CQRS pattern - Azure Architecture Center | Microsoft Learn](https://learn.microsoft.com/en-us/azure/architecture/patterns/cqrs)

- 📕 [Exploring CQRS and Event Sourcing_201207](https://learn.microsoft.com/en-us/previous-versions/msp-n-p/jj554200(v=pandp.10))
  - The project is focused on building highly scalable, highly available and maintainable applications with the Command & Query Responsibility Segregation and the Event Sourcing patterns.

- https://github.com/MicrosoftArchive/cqrs-journey /201207/csharp
  - http://cqrsjourney.github.com/
  - Microsoft patterns & pratices CQRS Journey sample application

## [Implementing event sourcing using a relational database_202106](https://softwaremill.com/implementing-event-sourcing-using-a-relational-database/)

- Event sourcing is a pattern in which a stream of events constitutes the primary source of truth in a system. These events capture facts — state changes that occur to the entities and aggregates in our system — and hence are immutable

- This article is an extension of the "transactional event sourcing" mechanism I've written about before and presents step-by-step how to implement event sourcing using a relational database as well as event sourcing best practices

- Snapshots are a special type of a projection, which store the entire reconstructed state of each stream (of a given type)
- Instead of a snapshot, it might be easier to maintain a consistent projection, containing partial state data, especially as the events evolve. This is also the topic of the next section on migrations.

## [Picking the Event Store for Event Sourcing_202105](https://blog.jaykmr.com/picking-the-event-store-for-event-sourcing-988246a896bf)

- In a relational database, event sourcing can be implemented with only two tables, 
  - one to store the actual Event Log, storing one entry per event in this table 
  - and the other to store the Event Sources. 
- The event itself is stored in the [Data] column. The event is stored using some form of serialization, for the rest of this discussion the mechanism will be assumed to be built-in serialization although the use of the memento pattern can be highly advantageous.

- In conclusion, each data store has its strengths and limitations for Event Sourcing. 
  - It is essential to consider factors such as scalability, consistency, sequencing, transactionality, and query support when selecting a suitable data store for an event-sourced system.

## 📈🌰 [Event Source your Spreadsheets for Flexibility and Maintainability_202208](https://berk.es/2022/08/16/event-source-your-spreadsheets-for-flexibility-and-maintainability/)

- Spreadsheets can be kept clean, clear, extendable, by organizing them with ideas from Event Sourcing.
  - It is an architecture to clearly distinguish logic from input from presentation in a spreadsheet. 

## 🌰📝 [Building offline-first web and mobile apps using event-sourcing_201907](https://flpvsk.com/blog/2019-07-20-offline-first-apps-event-sourcing/)

- Today CRUD is the default paradigm for managing data in a user-facing application. 
  - It works fine if the user’s device has a stable internet connection, but makes the app unusable in the case of an absent or poor connection. 
  - Even when online using CRUD eventually leads to loss of data and ordering issues due to the concurrent nature of network communication.
- This post is a detailed description of how I use event-sourcing to overcome limitations of CRUD and some of the problems that come with this approach.
- When we use CRUD, we tether our frontend application to the server. 
  - The server’s database becomes the ultimate source of truth. 
  - The UI becomes a view of the server’s database. Keeping that view up to date is hard. 
  - Adding layers of caching and processing in between the frontend and the database makes it even harder.

- There are tricks we could employ to improve the situation, without having to get rid of CRUD. For example:
  - Poll data from the server at regular intervals to make sure UI is up to date with the server; 
  - Restrict offline edits, using regular ping-style checks to the API host to determine whether we’re offline; 
  - Use a versioning system similar to the one in CouchDB. Only allow those updates that have the up-to-date version number of the object attached.
- These tricks might make the system a bit more reliable, but they will worsen user experience.

- A better way is to untether the frontend from the server. 
- The client app needs to be able to:
  - Work online, offline or on a slow or unreliable connection; 
  - It should provide full, unrestricted experience when offline; 
  - Once two instances of the app had a chance to exchange messages (via a server or directly), they need to be able to converge on the same value; 

- To do that we need to move the app logic to the client. Make the user-facing app behave more like Winamp less like Soundcloud.

- In the client-server model, the server is the ultimate authority and hence the ultimate bottleneck. 
- We need to move towards a peer-to-peer or local-first model.

- 🌹 Pros of event-sourcing
  - The app can work online / offline and with poor connectivity; 
  - We can share most of the code for working with events and snapshots across the server and different clients; 
  - Concurrency issues become possible to detect and debug; 
  - The amount of traffic the app generates decreases; 
  - We can add offline features gradually; 
  - We can vary depending on a feature or even user preferences how much data we want to store for offline use; 
  - Client devices can sync with each other without relying on the server; 
  - We can change business logic retroactively by changing reducers, as long as events contain all the necessary data for the new reducer to work; 
  - We can store additional metadata with the event. Things like the user that made the edit and the timestamp.

- 🐛 Cons of event-sourcing
  - The amount of data we need to store on devices and especially on the server grows significantly. That issue is still an area of active research. If you’re curious about the subject, check out Victor’s work on RON
  - We’re bringing business logic to the client, that might be a security or an intellectual property concern; 
  - It’s a new paradigm for many developers. It takes time and effort to get a hang of it and there’s not much information out there.

- I use CRUD for the data that rarely changes, doesn’t need to be updated offline or by several users at a time. 
  - I use event-sourcing for everything that needs offline and real-time functionality: chat, collaborative editing, local-first applications.

### 👥 [Building offline-first web and mobile apps using event-sourcing](https://www.reddit.com/r/javascript/comments/cfz5aj/building_offlinefirst_web_and_mobile_apps_using/)

- There's another con to the approach which the article doesn't state explicitly - the requirement to move the business logic to the client, which may be an issue due to intellectual property. By the way, finally Redux "reducers" make sense to me.

## 📝 [Mistakes we made adopting event sourcing (and how we recovered)_201906](http://natpryce.com/articles/000819.html)

- [Mistakes made adopting event sourcing (and how we recovered) - Nat Pryce - DDD Europe 2020 - YouTube_202010](https://www.youtube.com/watch?v=osk0ZBdBbx4)

- Event-sourcing is a good fit for our needs because the organisation wants to preserve an accurate history of information managed by the system and analyse it for (among other things) **fraud detection**. 

### 🐛 Not separating persisting the event history and persisting a view of the current state

- The app maintained a relational model of the current state of its entities alongside the event history. 
  - That in itself wouldn’t be a bad thing, if it had been implemented as a “projection” of the events. 
  - However, we implemented the current state by making the command handlers both record events and update the relational model. 
  - This meant that (a) there was nothing to ensure that entity state could be rebuilt from the recorded events, and (b) managing the migrations of the relational model was a significant overhead while the app was in rapid flux.
- we didn’t know how this hybrid architecture would work out
  - Therefore we continued down this road until the difficulties outlined above were clearly outweighing the benefits. 
  - Then we had a technical retrospective in which we examined the differences between canonical event-sourcing and our architecture. 
- The outcome was that we all understood why canonical event-sourcing would work better than our application’s current design, and agreed to change its architecture to match.

### 🐛 Confusion between event-driven and event-sourced architecture

- In an event-driven architecture, components perform activity in response to receiving events and emit events to trigger activities in other components. 
- In an event-sourced architecture, components record a history of events that occurred to the entities they manage, and calculate the state of an entity from the sequence of events that relate to it.
- We got confused between the two, and had events recorded in the history by one component triggering activity in others.
- We realised we’d made a mistake when we had to make entities distinguish between reading an event in order to react to it, and reading an event in order to know what happened in the past.

### 🐛 Using the event store as a message bus

- We added notifications to our event store so services could subscribe to updates and keep their projection up to date. Bad idea! 
- Our event store started being used as an event bus for transient communication between components, and our history included technical events that had no clear relationship to the business process
  - We noticed that we had to filter technical events out of the history displayed to users. 
- We came to realise that clearly distinguishing between commands that trigger activity and events that represent what happened in the past is even more important than Command/Query Responsibility Segregation, especially at the modest scale and strict consistency requirements of our system. 
- The word “event” is such an overused term we had many discussions about how to name different kinds of event to distinguish between those that are part of the event-sourcing history, those that are emitted by our active application monitoring, those that are notifications that should trigger activity, and so on. 
  - In our new applications we use the term Business Process Event for events recorded in our event-sourcing history.

### 🐛 Seduced by eventual consistency

- Initially we gave the event store an HTTP interface and application components used it to read and store events. 
  - However, that meant that clients couldn’t process events in ACID transactions and we found ourselves building mechanisms in the application to maintain consistency.

### Noticing our mistakes

- 👉🏻 We decided to **replace our use of HTTP between command processors and the event store with direct database connections** and serialisable transactions.
  - We kept the HTTP service for traversing the event history, but only for peripheral(次要的；不重要的) services that maintain read-optimised views that can be eventually consistent (daily reports, business metrics, that kind of thing).

- We decided to **stop using notifications from the event store to trigger activity and went back to REST for passing data and control between components**.

- We decided to not update the record of the current state of the entities in command handlers. 
  - Instead **the application computes the current state from the event history** when the entity is loaded from the database. 
  - The application still maintains a “projection” of the current entity states, but **treats the projection as a read-through cache**, used to optimise loading entities, so that it doesn’t have to load all of an entity’s events on every transaction, and to select subsets of the currently active entities, so that it doesn’t have to load all events of all entities. 
  - Entries are expired from the cache by events: each projection is a set of tables and function is passed each event and creates, updates and deletes rows in its tables in response.
- Logic to execute commands now looks like:
  - Load the recent state of the entity into an in-memory model
  - In a write transaction
    - load events that occurred to the entity since the recent projection into the in-memory model
    - perform business logic
    - record events resulting from executing the command
  - **Save the in-memory state as the most recent projection** if it was created from more recent events than that the projection that is currently persisted (the persisted state may have been updated by a concurrent command)
- Read transactions don’t record events and can therefore run in parallel with each other and write transactions.

- We decided to **replace the relational model**, which required so much effort to migrate as the app evolved, **with JSON blobs serialised from the domain model** that can be automatically discarded and rebuilt when the persisted state becomes incompatible with the latest version of the application. Thanks to Postgres’ `JSONB` columns, we can still index properties of entity state and select entities in bulk without adding columns of denormalised data for filtering.

- The application also maintains projections for other uses, which have less stringent(严格的; 精确的) consistency requirements. 
  - For example, we update projections for reporting in the background on a regular schedule.

### Re-engineering the system architecture

- We were concerned that such significant changes to the systems architecture would deliver a blow to our delivery schedule. But it turned out to be very straightforward. 
- As well as using event-sourcing, the application has a Ports-and-Adapters (aka “hexagonal”) architecture. 
  - Loading the current state of an entity was hidden from the application logic behind a Port interface that was implemented by an Adapter class.
  - My colleague was able to switch the app over to calculating an entity’s current state from its event history and treating persistent entity state as a read through cache (as described above) in about one hour.
  - The team then replaced the relational model, which required so much effort to migrate as the app evolved, with JSON blobs serialised from the domain model that could be automatically discarded and rebuilt when the persisted state became incompatible with the latest version of the application. The change was live by the end of the day.
- We also have extensive functional tests that run in our continuous deployment pipelines.
  - The functional tests serve two purposes that paid off handsomely when we had to make significant changes to the application’s architecture.
  - Firstly, they force us to follow the Ports-and-Adapters architecture. 
  - second purpose: to rapidly verify that the application still performs the same user visible behaviour as we made large changes to its architecture.
  - changes to the technical architecture of the application were strictly segregated from the definition and implementation of its functional behaviour, neither of which needed to be changed when we changed the architecture

### Conclusions

- It’s inevitable that you’re going to make mistakes when implementing a system
  - A system’s architecture has to address how you recover from those mistakes.

### 👥 [Mistakes we made adopting event sourcing and how we recovered | Hacker News_201907](https://news.ycombinator.com/item?id=20324021)

- Ports and Adapters(aka “hexagonal”) is great, though I found it hard to sink my teeth into as it has a thousand different names. But regardless, I am never doing n-layer architecture again if I can help it.

- Not separating persisting the event history and persisting a view of the current state.
  - This seems like the classic half-way that people take when adopting ES without buying into CQRS
  - If I understand OP correctly they are saying that rather than deriving state by consuming their events, they were maintaining a kind of snapshot that served as both the read/write model representation of a given aggregate in addition to storing the events.

- I worked on multiple Event Sourcing CQRS based systems and I see no advantages vs traditional databases.
  - The event stream is exactly the same as a commit log in a regular DB. Building "projections" is the same as making views or calculated columns. In my experience storing the whole event history is not useful and consumes huge amounts of space. Just like everyone compacts their commit logs, you don't have to, and if you don't, isn't ES the same thing with extra steps? It stores all the changes to tables and views, which are exactly the same as projections. With ES + CQRS combined you're basically replicating a database, badly.
  - Sorry to be so negative about this topic but I've worked on several of these projects at a decent scale and it's been the biggest disaster of my professional life. The idea may be viable but tooling is so bad that you're almost surely making a huge mistake implementing these patterns in production code.
- 🤔 This(es) assumes the content in the commit log are client events, not CRUD on table data actions (events are higher order). When a greenfield project is starting up, data is gold
  - I disagree. The events tend to relate directly to what would be regular database tables in my experience.
  - And data is the new oil is definitely a businessweek cargo cult. None of the event data was of any use on the projects I worked on. We were under mandate to find something to do with it and still couldn't. The closest useful thing was allowing undo and replaying past events but we already had that on Postgres with hibernate auditing on interesting tables (money related stuff)
- 👉🏻 I agree (es)it's a nice pattern. **What you really need though is a "database in code"**. A library that handles all the projections, event stream, and especially replays and upgrading event versions automatically.
- One thing you do get "for free" pretty much is an audit log though. 
  - And if you store events with both an event_timestamp and effective_timestamp, you get bi-temporal state for free too.
  - Invaluable when handing a time series of financial events subject to adjustments and corrections
- You get audit logs for free on a regular database with an ORM like Hibernate or even support on database snapshot level with Postgres or MSSQL. You get the logging capabilities of CQRS without any of the complexity.
  - **After working on several such systems, I strongly believe you should keep data storage concerns in the database. Moving it to code implementation is a massive amount of overhead for no benefit**.

- In most relational database management systems (RDBMS) views are not persisted/materialized or indexed separately.
  - Some RDBMS have materialized views that update concurrently and meet atomicity, consistency, isolation, and durability (ACID) requirements, but others do not and a separate command is needed to update views, in those cases you lose many of the benefits, but the view is fine for say, analytical queries in which a little lag is fine.

- Views are popular for projecting denormalized information. I pity the fool who inserts into views.

- Event sourcing is most powerful when the data necessary to recompute the state is small but the amount of state you are potentially interested in subsequently accessing is large, most of which is computed.
  - It is also incredible useful for financial applications where risk models (credit risk, market risk, fraud, etc) need backtesting. 
  - If you can't read the time-ordering of state events directly, a Risk/Data Science team spends an inordinate amount of time reconstructing time histories of events inferred from a mix of static db tables, audit logs and periodic data warehouse snapshots.

- You almost certainly shouldn't be doing EventSourcing with Kafka. EventStreaming sure, Kafka is pretty idea for this (as your source of truth).
  - EventSourced aggregates need to reload their entire history (unless you are snapshotting too) before applying a command, so you shouldn't have all your aggregates in a single Kafka topic, as you would have to read all events since forever, for all aggregates, every time you loaded one.
  - If you put each aggregate into a separate topic, everything is fine, until you want to add projections - how do your projections know to subscribe to all the new topics being created for each aggregate?
  - You can probably engineer your way around these limitations, but at that point, why not use a tool which is more suitable for the eventsourcing and keep Kafka for the "Business Process Event"?

- Seduced by eventual consistency
  - Indeed. I work at a very, very large firm suffering from problems caused by this. The system crawls and is quite expensive to run. But it's so entrenched there are no plans to replace it, only more layers put on top to mitigate it.
  - RDBMS people took a bit more time before implementing temporal features (SQL 2011).

- The biggest problem (of es) is the lack of available tooling.
  - The only custom built ES database is Eventstore, and it has many issues.

### 👥 [reddit: Mistakes we made adopting event sourcing (and how we recovered)](https://www.reddit.com/r/programming/comments/ca56q7/nat_pryce_mistakes_we_made_adopting_event/)

- It helps if you start by understanding that "event-sourced" is someone trying to rebrand "log-structured" for their VC.

- I highly recommend adopting a proper cqrs+es framework as there are so many nuances to this architecture that you don't think about. Highly recommend axon framework (Java)
  - I have the opposite advice. If you are doing ES, avoid frameworks at all cost, especially Axon.
  - Axon promotes a series of patterns (such as sharing domain events outside your aggregates) which can pass as scalable but fail the test of long term evolution and fairly moderate scales. I'll admit it can work as a good learning framework or first generation system but you'll soon need a replacement.

- And there appears the #1 rule in all of software: whatever opinion you hold on a particular subject, there is someone who strongly believes the exact opposite is true.

- Second the recommendation for Axon. We use it for a financial transaction processing system at work and, while it is not a silver bullet, it has been a big help in keeping our architecture clean and consistent and scalable. I especially like how easy it makes writing meaningful, high-quality tests (though that is likely true of any event sourcing framework).
# blogs-es-crdt
- [Replicated Event Sourcing • Akka Documentation](https://doc.akka.io/docs/akka/current/typed/replicated-eventsourcing.html)
  - The rule for operation-based CRDT’s is that the operations must be commutative
  - in other words, applying the same events (which represent the operations) in any order should always produce the same final state. 
  - You may assume each event is applied only once, with causal delivery order.

## [Downsides of Local First / Offline First | RxDB - JavaScript Database](https://rxdb.info/downsides-of-offline-first.html)

- You do not have to handle conflicts if they cannot happen in the first place. 
  - You can achieve that by designing a write only database where existing documents cannot be touched. 
  - Instead of storing the current state in a single document, you store all the events that lead to the current state. 
  - Sometimes called the "everything is a delta" strategy, others would call it Event Sourcing. 
  - Like an accountant that does not need an eraser, you append all changes and afterwards aggregate the current state at the client.

- There is this thing called conflict-free replicated data type, short CRDT. 
  - Using a CRDT library like automerge will magically solve all of your conflict problems. 
  - Until you use it in production where you observe that implementing CRDTs has basically the same complexity as implementing conflict resolution strategies.

## [CRDTs _202209](https://www.gatlin.io/content/crdts)

- Regarding internal state management, you can think of operation-based CRDTs as analogous to event sourcing. It is an implementation detail, but presumably a "pure" operation-based CRDT will store "just" the events, and compute the state from that (which it may or may not store, internally). 
  - State-based CRDTs will store the state internally (and may or may not store message events depending on how broadcasting is implemented).

- An ORSet, or "Observed-Remove Set", is the same as an AWSet, or "Add-Wins Set". 
  - It is a way of defining the tie-breaking semantics of conflicting, concurrent updates. 
  - If concurrent operations call for a remove and an add, the add wins.

## 🆚️ [LWW vs P2P Event Log – vlcn.io](https://vlcn.io/blog/lww-vs-dag)

- [SQLite Peer to Peer Event Log / Matt](https://observablehq.com/d/dc2bbfad6d64fb5e)

- 🤔 Event sourcing is a fairly common design pattern for deriving application state from a history of events. But **is it possible to turn an event log into a CRDT**? 
  - **This is possible**. What's even better is that it is more powerful than other approaches, such as last write wins, to solving the problem of distributing application state.

- We'll do a brief review of how we can distribute state with last write wins registers, cover how that is a less powerful version of an event log and then build an distributed event log.
- A common approach to distributing application state is to use last write wins registers. 
  - Last write wins (LWW), however, is just one interpretation of the events in the system. 
  - This interpretation discards all the information that was used to derive it. 
- A distributed event log on the other hand:
  - A distributed event log on the other hand:
  - Can be interpreted as LWW in addition to other ways
- Unpacking that a bit. Say I have an TODO list application. I can save just the current state of each todo or I can save all of the events that have transpired and build the state later.
  - Saving just the current state is what LWW does
  - Saving just the current state is what LWW does
- The event based approach gives you a set of facts about the system that never change.

- We know that a grow only set of LWW registers is a CRDT from the last article but how do we turn an event log into a CRDT? 
- we're going to set up two different examples. One for LWW and one for a P2P event log. Each example will have three todo lists that are running on different peers.

- The LWW state is pretty straightforward.
  - a drawback is that we're locked into this specific way of resolving conflicts and we don't have a history of how we got into a given state.
  - Note that the clock columns could be a variety of options. Here we've done an independent lamport timestamp per column.

- the DAG example keeps a record of every event
  - These events are linked together into a "causal graph" to represent which events caused which others. 
  - Processing the graph gives us the final state.
  - the DAG example is notional and thoroughly un-optimized. 
  - We currently re-pull and re-apply the entire DAG on sync rather than doing incremental updates. 
  - We also sync the entire DAG between nodes rather than delta states. 
  - How to incrementally process the DAG is a separate topic.

## [Event Sourcing V1 - Dima Korolev _202309](https://dimakorolev.substack.com/p/event-sourcing-v1)

- The kryptonite for the CRDT approach is any problem where the order of mutations matters, and thus contention is impossible to avoid.

- It is then often best to persuade the product owners to drop the strong consistency requirement, as it is orders of magnitude easier to build a system that is allowed to drop or overwrite a bit of data once in a blue moon, compared to building a bulletproof strongly consistent system. The designs then quickly get into the CRDT- and eventual-consistency territory, where a wealth of knowledge exists on how to do things right.

## [Eventuate - A service framework for operation-based CRDTs _201610](https://krasserm.github.io/2016/10/19/operation-based-crdt-framework/)

- The two CmRDT update phases, prepare and effect, are closely related to the update phases of event-sourced entities, command handling and event handling, respectively

## [Data Laced with History: Causal Trees & Operational CRDTs _201803](http://archagon.net/blog/2018/03/24/data-laced-with-history/)

- CmRDTs, or operation-based CRDTs, only require peers to exchange mutation events, but place some constraints on the transport layer. 
  - (For instance, exactly-once and/or causal delivery, depending on the CmRDT in question.) 
- With CvRDTs, or state-based CRDTs, peers must exchange their full data structures and then merge them locally, placing no constraints on the transport layer but taking up far more bandwidth and possibly CPU time. 
- Both types of CRDT are equivalent and can be converted to either form.

- Usually, operations in a distributed system are executed and discarded on receipt. However, we can also store the operations as data and play them back when needed to reconstruct the model object. (This pattern goes by the name of event sourcing in enterprise circles.) An event log in causal order can be described as having a partial order, since concurrent operations may appear in different positions on different sites depending on their order of arrival. If the log is guaranteed to be identical on all devices, it has a total order. Usually, this can be achieved by sorting operations first by their timestamp, then by some unique origin ID. (Version vectors work best for the timestamp part since they can segregate concurrent events by site instead of simply interleaving them.) Event logs in total order are especially great for convergence: when receiving a concurrent operation from a remote site, you can simply sort it into the correct spot in the event log, then play the whole log back to rebuild the model object with the added influence from the new operation. But it’s not a catch-all solution, since you can run into a O(n2) complexity wall depending on how your events are defined.
- Now, there are two competing approaches in strong eventual consistency state-of-the-art, both tagged with rather unappetizing initialisms: Operational Transformation (OT) and Conflict-Free Replicated Data Types (CRDTs).
- In contrast to OT, the CRDT approach considers sync in terms of the underlying data structure, not the sequence of operations. 
  - A CRDT, at a high level, is a type of object that can be merged with any objects of the same type, in arbitrary order, to produce an identical union object. CRDT merge must be associative, commutative, and idempotent, and the resulting CRDT for each mutation or merge must be “greater” than than all its inputs. (Mathematically, this flow is said to form a monotonic semilattice. For more info and some diagrams, take a look at John Mumm’s excellent primer.) 
  - As long as each connected peer eventually receives the updates of every other peer, the results will provably converge—even if one peer happens to be a month behind. 
  - This might sound like a tall order, but you’re already aware of several simple CRDTs. 
  - For example, no matter how you permute the merge order of any number of insert-only sets, you’ll still end up with the same union set in the end. Really, the concept is quite intuitive!
- CmRDTs, or operation-based CRDTs, only require peers to exchange mutation events, but place some constraints on the transport layer. (For instance, exactly-once and/or causal delivery, depending on the CmRDT in question.) With CvRDTs, or state-based CRDTs, peers must exchange their full data structures and then merge them locally, placing no constraints on the transport layer but taking up far more bandwidth and possibly CPU time. Both types of CRDT are equivalent and can be converted to either form.
# blogs-vendors

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

- ### Event Driven Architecture — 5 Pitfalls to Avoid-/twitter_202208
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

- ### 👥 [How to Move from CRUD to Event Sourcing | Hacker News_202109](https://news.ycombinator.com/item?id=28691728)
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

- 👉🏻 then you realize that the CRUD db you moved away from operates on event sourcing (WAL) anyway. And thus you’re just doing inner platform effect.
  - Correct, and many applications are using WAL via CDC (Change Data Capture) to gain some of the benefits of the CQRS/ES.
  - The problem is that the CRUD is only recording "What" change/mutation was done, but not "Why" by "Whom", and "When" it was done. With tailing WAL / CDC you can also capture the "When".
  - This can be partially mitigated by adding audit fields
- Yup a few fields gets you a long way, though I would recommend an audit log updated by triggers, rather than audit fields.
  - For example on my CRUD rails app, we use audit triggers in combination with setting a postgres local config variable with the username, the audit triggers pull the user info from the variables and record them into the DB. 
- What kind of technology/data model do you use for the audit log? A timeseries db, just another table, or something else?
  - Another table in a different schema. Roughly this https://wiki.postgresql.org/wiki/Audit_trigger_91plus
- If you use log-based CDC, you typically don't need those timestamps, the WAL will contain and expose that information.
  - One way for capturing these intents is to log that information transaction-scoped in a separate table and then use downstream stream-processing to enrich actual change events (which contain the TX id themselves) with that metadata. 
  - I've blogged about one way for implementing this using Debezium and Kafka Streams a while ago

- It seems the benefits of eventsourcing can be had from using an immutable database. Auditing, Backing up state while the db is running, previous states and diffs.

## [GAT TechTalk #5 – Journey to DDD Through the Land of Dungeons, Dragons and Other Daemons_202210](https://www.globalapptesting.com/engineering/gat-techtalk-5-journey-to-ddd)

- 

- [GAT TechTalk #4 (DDD in Ruby)_202107](https://www.globalapptesting.com/engineering/gat-techtalk-4-ddd-in-ruby)
- 
- 

## 📝💬 [How Discord Stores Trillions of Messages_202303](https://discord.com/blog/how-discord-stores-trillions-of-messages)

- 
- 
- 
- 
- 

- [summary](https://medium.com/@iBMehta/how-discord-stores-trillions-of-messages-31ed9195c3e8)
- the evolution of message storage at Discord:
  - MongoDB ➡️ Cassandra ➡️ ScyllaDB
- In 2015, the first version of Discord was built on top of a single MongoDB replica. 
  - Around Nov 2015, MongoDB stored 100 million messages and the RAM couldn’t hold the data and index any longer. 
  - The latency became unpredictable. 
  - Message storage needs to be moved to another database. 
- Cassandra was chosen.
  - In 2017, Discord had 12 Cassandra nodes and stored billions of messages.
- At the beginning of 2022, it had 177 nodes with trillions of messages. 
  - At this point, latency was unpredictable, and maintenance operations became too expensive to run.
- reasons
  - Cassandra uses the LSM tree for the internal data structure. The reads are more expensive than the writes. There can be many concurrent reads on a server with hundreds of users, resulting in hotspots.
  - Maintaining clusters, such as compacting SSTables, impacts performance.
  - Garbage collection pauses would cause significant latency spikes
- ScyllaDB is Cassandra compatible database written in C++. 
  - Discord redesigned its architecture to have a monolithic API, a data service written in Rust, and ScyllaDB-based storage.

- [How Discord Stores Billions of Messages_201701](https://discord.com/blog/how-discord-stores-billions-of-messages)
  - [How Discord Stores Billions of Messages (2017) | Hacker News](https://news.ycombinator.com/item?id=28292369)

- ### [reddit: How Discord Stores Trillions of Messages : programming](https://www.reddit.com/r/programming/comments/11kj91n/how_discord_stores_trillions_of_messages/)
- Well this is big for Tokio. It's hard to imagine a bigger usecase for that technology than this, turns out it scales to it. Very impressive.
- There are certainly times when I think the Discord model would be better for productivity than how Slack does it.
- ScyllaDB and Rust weren't new for them tho, they've been using them since 2020.

### [How Discord Stores Trillions of Messages | Hacker News_202303](https://news.ycombinator.com/item?id=35048410)

- 🤔 Solid article. Is it fair to say that the "data services" layer is essentially a cache sitting in front of the database, or am I misunderstanding it's function?
- I work at Discord in infrastructure.
  - We use data services to do "data related things" that make sense to do at a central proxy layer. This may include caching/coalescing(联合；合并)/other logic but it doesn't always, it really depends on the particular use case of that data.
  - For messages, we don't really cache. Coalescing gives us what we want and the hot channel buckets will end up in memory on the database, which is NVMe backed for reads anyway so the performance of a cache wouldn't add much here for this use case.
  - In other places, where a single user query turns into many database queries and we have to aggregate data, caching is more helpful.
- In essence, yes, but strictly speaking, no. Instead of caching responses, that layer seems to only bundle equal requests.
  - So once a request is sent to the database, every other instance of the same request (e.g. "hey, fetch me all messages from server id 42") is put on hold. 
  - Once the initial request gets an answer from the database, that answer is distributed to the initial requester and all those which were on hold. 
  - Now if someone is late to the party, they will initiate a new request to the database, because the response is not cached.
# more
- [Datomic: Event Sourcing without the hassle | Hacker News_201811](https://news.ycombinator.com/item?id=18431382)

- [CQRS + Event Sourcing – Step by Step](https://danielwhittaker.me/2020/02/20/cqrs-step-step-guide-flow-typical-application/)

- [Event Sourcing with Apache Kafka — Trustbit](https://www.trustbit.tech/blog/2023/7/14/event-sourcing-with-apache-kafka)

- [A more functional approach to Event Sourcing and DDD - DEV Community _202207](https://dev.to/n1ckdm/a-more-function-approach-to-event-sourcing-and-ddd-491d)
