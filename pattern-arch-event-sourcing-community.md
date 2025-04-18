---
title: pattern-arch-event-sourcing-community
tags: [community, event-sourcing]
created: 2023-09-13T14:27:35.584Z
modified: 2023-09-13T14:28:01.426Z
---

# pattern-arch-event-sourcing-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🆚️ Can you explain the difference between Event Sourcing vs. Change Data Capture (CDC)?
- https://x.com/RaulJuncoV/status/1896911947167060097
  - Event Sourcing and CDC are related concepts that distributed systems use to propagate data changes to interested consumers and downstream services.
  - They both deal with events, but they serve different purposes.
- With Event Sourcing, the event log is the source of truth. 
  - Instead of storing only the latest state, you persist every state change as an event. 
  - This enables: • Auditing • Debugging • State reconstruction
- CDC listens to database-level changes and propagates them to other services. 
  - It ensures data consistency across systems without requiring them to query the source database directly.
  - This works at the database level and tracks: • Inserts • Updates • Deletes

- While distinct, these concepts can be complementary:
  - You can use Event Sourcing to manage internal domain events and preserve history.
  - And use CDC to capture relevant changes and distribute them to external systems.

- Event sourcing is commonly used in financial systems, a must know pattern.

- ## 🆚️ [Event driven vs Event sourcing _202205](https://tarunjain07.medium.com/event-driven-vs-event-sourcing-a943d223299c)
- In domain-driven design, domain events are described as something that happens in the domain and is important to domain experts.
- Event Driven Architecture is about components communicating via publishing events rather than making (e.g.) RPC calls against each other or manipulating shared state. It’s a communication strategy (albeit one which often relies on messages being persisted for fairly long periods).
- Event Sourcing ensures that all changes to application state are stored as a sequence of events.

- The term Event driven architecture is used for any kind of software system which is based on components communicating mainly or exclusively through events. For example, almost any major GUI framework on any popular platform uses event-driven mechanics. The term "event" usually means "notification" in this context.
- Event sourcing is a much more special term, referring to systems where the whole application state is stored as a sequence of events. 
  - A well-known popular class of examples are transactional database systems, which store any state changes in a transaction log. Here, the term "event" refers more to "state change", not only to "notification".

- ### [Where does DDD Aggregate come in under event sourcing & CQRS? : r/csharp _202403](https://www.reddit.com/r/csharp/comments/1bj6v0o/where_does_ddd_aggregate_come_in_under_event/)
- An aggregate is effectively a transaction boundary. It contains all the things that must always remain transactionally consistent.
  - If you aren't doing event sourcing, then it would be all the things that you would update in a single save operation. There may be other things (possibly in other services) that are eventually consistent, that get updated from messages you send at that point of performing the save. Those things are in separate aggregates.
  - With event sourcing, that usually maps to a single event stream. Some event stores, like EventStoreDB, enforce this by only allowing a transaction to save data to a single event stream.
  - In terms of aggregate modelling, think about what invariants you have that must always hold to help guide you towards what your aggregate boundaries could be.

- In DDD, an aggregate is a cluster of domain objects that can be treated as a single unit. The aggregate root is a specific entity within the aggregate, and it's the only way to access the other objects in the aggregate. This helps maintain consistency and enforces the rules of the domain model.

- ### [Domain Events vs. Event Sourcing : r/programming _201902](https://www.reddit.com/r/programming/comments/amdm95/domain_events_vs_event_sourcing/)
- I disagree with the author. Event sourcing is a mechanism. You can store whatever kinds of events you want. Whether you call them domain events, subdomain events, or something else is semantics and irrelevant
  - An aggregate is a time augmented state machine. You can have a hierarchy of aggregates and emit events at any level of abstraction you like. That’s entirely the point of event sourcing. That point is crucial for this article and the fact that the author missed it is a big red flag

- ### [Why DDD for CQRS and Event Sourcing application? - Stack Overflow](https://stackoverflow.com/questions/70835529/why-ddd-for-cqrs-and-event-sourcing-application)
- CQRS pattern might be useful even when you aren't doing event sourcing.
- Event sourcing is really a pair of ideas
  - changes should be first class citizens in our model
  - our authoritative data model should be a sequence of changes (aka a history)
- This kind of data model is great for writes (just append a new change on the end of the list), and has the additional benefit that edits are non-destructive; all of the information added to the system is still there, so you can easily time machine back to understand what things looked like prior to some change.
  - But histories suck for low latency query. Therefore: caches - we'll pre-compute the answers to some questions, and stick them in a property bag.
- Now we have two models: the history, and the cache. And what is CQRS?
  - CQRS is simply the creation of two objects where there was previously only one -- Greg Young 2010

- ## I remember this talk from Martin Fowler years ago where he described an event sourced system that kept all the application state in memory (because as we all know the DB is the log).
- https://twitter.com/LewisCTech/status/1762786070574633046
  - TIL it's the same system Tigerbeetle bases its architecture on - LMAX.

- ## [Partial Event Sourcing (ES + CRUD)_201305](https://groups.google.com/g/dddcqrs/c/v8Pd1ixx0vI)

> es与crud结合的方案，参考cdc

- What I am having trouble with is not event sourcing everything.  I get that ES is overkill for CRUD but there are quite a few objects in the database that themselves contain little to no behavior beyond CRUD but they are used as references to other objects which contain a lot of behavior.

- For me, I only store aggregates (i.e. my domain) in my event store. All those other things (e.g. names of countries) come from somewhere else. Perhaps from a sql database, or a bunch of text files, hard-coded, even.
- The real question is - if you model something as an entity and your *commands* persist it in an event store, how do you *query* for them in different, useful ways? CQRS is the answer, and essentially you write projection code that takes events generated by your entities and uses them to build an additional Read Model that's whatever you need it to be. 

- ## [Real World Microservices: When Services Stop Playing Well and Start Getting Real | Hacker News_201605](https://news.ycombinator.com/item?id=11649999)
- From my own experience building a platform of products on top of microservices, I find that the most difficult part about this architecture (and the one that nobody ever talks about) is how to share data between microservices via message bus instead of direct requests. If you can get this down the rest, in my opinion, is just pure bliss and a piece of cake.
  - Event sourcing is the thing you're looking for and something that will probably be the focus of many building microservice platforms.
- About 2 years ago, I started to notice the incredible usefulness of event sourcing and its applicability at various layers of the stack.
  - 👉🏻 From the React/Flux frontend paradigm, to the "everything is a stream" philosophy of Unix systems, to Erlang actors, to event sourcing for application backends, to databases like Datomic and CouchDB.
  - This is why I'm so excited about Elm right now - it explicitly puts this at the core of every application, and gives you a really nice language and type system for encoding your domain logic and manipulating data.
- I think the real network-level win comes from rigorous events, period. 
  - Event sourcing, on the other hand, is an internal implementation detail of a particular service... 
  - Which happens to get you a good stream of events as a side-effect.
- Have you tried Erlang? It's basically designed around solving that problem. Many people use RabbitMQ to solve that problem and it's no coincidence that RabbitMQ is written in Erlang. Elixir is possibly a similar option (don't know, haven't tried it).
  - Erlang's raison d'etre is not message passing but fault tolerance. 

- ## 🛋️ [Damn Cool Algorithms: Log structured storage (2009) | Hacker News_201705](https://news.ycombinator.com/item?id=14447727)
- event sourcing seems like a very powerful pattern that I haven't seen wide adoption. The best documentation seems to be some MS dev library notes and a discussion from M Fowler.
- 🤔 Are there any open source implementations of a database that uses event sourcing?
- I built https://github.com/amark/gun after I was using MongoDB to event source data. The key piece for me was wanting to have Firebase-like realtime sync for my event sourcing.
- I've become a bit of a CouchDB zealot(狂热者) of late for this exact reason... Native support for incrementally updating map-reduce combined with change-feeds makes implementing event sourcing straightforward. 
  - If you wanted to reimplement event sourcing in couch, it can be implemented as a versioned merge in a map-reduce view that takes a sequential ordered events (e.g. ui-event:0000025) and maps those changes into a "versioned" JSON. This versioned JSON changes leaf values into versioned objects like "fieldValue": { "_val": 34.00, "_ver": 25 } which I call property fields. 
  - This is necessary because CouchDB is a B+Tree implementation and reduce operations are sequential but not contiguous(相邻的). 
  - 👉🏻 The reduce phase merges all events sequentially by choosing property fields with the latest event – making it a CRDT type – and resulting in a single JSON document with the latest fields with "_ver" info for each. 
  - This scheme has a drawback that each event needs to have a unique serially ordered ID to work. Not sure how time stamps would work. I chose the ID based scheme to allow the UI be able to know when a user interaction conflicts (a vector clock between) and let it display the conflict to the user or decide how to merge the knew state.

- ## 💡 This confluence of things is going to unlock some stellar new infrastructure.
- https://twitter.com/tantaman/status/1715046327892025526
  - Event sourcing
  - CRDTs & Causal Graphs
  - Incremental View Maintenance
  1. Event source your entire app.
  2. Incrementally maintain app state as a view of events.
  3. Rebase events for multiplayer.
- I'm experimenting with this stuff - I believe that massively scalable multi-master even stores could be implemented with an append only log and some kind of index of event ID -> index-in-log. The index could just be resident in memory too.

- 🤔 Any thoughts on compressing the log? People have made a ton of progress in terms of compacting sequence crdt event logs. Not sure about generic event logs.
  - I do feel as if history pruning would go against event sourcing though. Compaction makes a lot of sense - probably for events that have gone offline? (IE not accepting any more writes for last years events... following business rules).
- Abtimatter is interesting since it finds history that doesn’t matter and can be dropped even if peers never saw it and things still converge to the same state without those events.
- Ideas for log pruning exists almost from the very beginning. The problem is always the same - you need to be able to restrict the set of writers or deny concurrent updates.
- No I just naiively assume storage will keep getting better and it's fine

- ## [Local-first software: You own your data, in spite of the cloud | Hacker News_201905](https://news.ycombinator.com/item?id=19804478)
- I think OT systems are way simpler to reason about, because they’re just an extension of event sourcing. Also CRDTs type implementations have been trailing OT algorithms in terms of features forever. OT got JSON editing support first, and JSON1 also supports arbitrary tree reparenting, which as far as I know is missing from all CRDT algorithms. That’s needed to implement apps like workflowy, where you can drag trees around.
  - CRDT algorithms have documents which grow without bound. With OT, the documents are always minimal and it’s easy to reason about (and implement) trimming operations.
  - CRDTs are a better tool for distributed applications, but for server client stuff OT works fine.

- I do agree tho, most CRDT implementations have just as many scaling and compaction problems as any append-only log system.

- ## 👥 [Show HN: Pg_CRDT – an experimental CRDT extension for Postgres | Hacker News_202212](https://news.ycombinator.com/item?id=33931971)

- Just store all updates - as if you do event sourcing - ordered by a timestamp. 
  - The list of updates will eventually converge as will any function of that list, including any function that merges all the updates into a current state. 
  - You might have to [partially] reevaluate the function in case a delayed update shows up and has to be inserted into the middle of the list of updates. 
  - So I guess there are additional requirements in order to qualify as a CRDT, bounded additional space or bounded amount of computation on updates. But I don't know as it turned out my understanding of what qualifies as a good CRDT was too narrow.
- Yeah **event sourcing and what you described is what these libraries are calling delta CRDTs**. The appeal is they’re hiding away the actual event log, metadata and rebasing/merging parts and exposing data types that look something like what you’d normally use.
  - And if you tie the conflict resolution logic to the individual delta operations, you get Operational Transforms.

- ## [What they don’t tell you about event sourcing | Hacker News_201808](https://news.ycombinator.com/item?id=17817375)
- The ideal situation is to create migrations that can always be rolled back, but sometimes this is not possible to do operationally. 
  - The problem with undoing operations via new events is the same thing -- unless you have foreknowledge of this kind of problem, it is very easy to accidentally create events that perform un-undoable actions. A very simple example of a problematic event would be something that modifies a foreign-key relationship
- Basically implement double entry accounting.
  - I think ideally you want something like Rich Hickey speaks about when he speaks of Datomic. An append only database. You can see what the previous values for that row were, along with schema changes.
- I worry about GDPR with respect to Kafka and other append-only databases.
  - You can encrypt events and throw away the keys, if data should be made inaccessible. Of course, it adds complexity. But its already being done.
- If you need to change history you can just create new events that accomplish your mutation -- and even mark them as a type 'change history' or some such obvious identifier so when you inspect the event stream you know exactly what you are looking at.

- I've spent the last year migrating to an event sourced system, so thought I'd share some thoughts.
  - On the eventual consistency point, I've found you can get quite far with having the read model managing the race condition. This probably doesn't work everywhere
  - Coming up with the event schema and versioning/granularity are hard. We have version numbers on all our events to make this a bit more manageable/explicit
  - Storing events in a relational database does make it a bit easier to go back and edit/upgrade/delete them (sort-of cheating, but also relevant for GDPR). 
  - Also, I think we're going to end up suffering a bit from the 'whole system fallacy', but at the moment namespacing all the events (keeping in mind their expected volume) makes it a lot easier to manage

- I don't see much discussion of event-sourcing simply using a SQL database (i.e. skipping the CQRS part). This would allow you to keep your CP (strongly-consistent) semantics.
  - TLDR: orm’s + large transactions resulted in a lot of unexpected complexity.

- I was doing event sourcing in 2010, and loved it. It was incredible. But by the time I started hearing people call it "event sourcing" I had already moved on to: State-based, graph CRDTs. They combine the best of event sourcing with the best of distributed state replication. 
  - Now even the Internet Archive[1] is running it (in 2014 I implemented it into a library that they are now using gundb)

- ## 💡 [What every software engineer should know about Apache Kafka | Hacker News_202005](https://news.ycombinator.com/item?id=23206566)
- Is using a distributed log as the WAL component of a event-sourcing or distributed database entirely a bad idea? I am of the opinion that it is a viable but sophisticated approach.

- I worked on a project that used CQRS and Event Sourcing years ago. It was an unmitigated disaster, never made it out of prototype phase.
  - By using Kafka (or anything else) as a "commit log" you've just resigned yourself to building the rest of the database around it. In a real RDBMS the commit log is just a small piece of maintaining consistency.
  - Every time I've worked on a project where we handle our own "projections" (database tables) we ended up mired(陷入困境/陷入泥潭) deep in the consistency concerns normally handled by our database.
- 🤔 Whats so hard? 
- **Compaction is an evil problem**. We figured we could "handle it later". Well it turns out maintaining an un-compactible commit log of every event even for testing data consumes many terabytes. This and "replays" sunk the project indirectly.
- Replays. The ES crowd pretends this is easy. It's not. If you have 3 months of events to replay every time you make certain schema changes you are screwed. 
- Data duplication. Turns out "projecting" everything everywhere is way worse on memory and performance than having the DB thats handling your commit log also store it all in one place. Who knew.
- Data corruption. If you get one bad event somewhere in your commit log you are cooked. This happens all the time from various bugs. We resorted to manually deleting these events, negating all the supposed advantages of an immutable commit log. We would have been fine if we let the db handle the commit log events.
- Questionable value of replays. You go through a ton of bs to get a system that can rewind to any point in time. When did we use this functionality? Never. We never found a use-case. When we abandoned ES we added Hibernate Auditing to some tables. Its relatively painless, transparent, and handled all of our use cases for replays

- In DBMS the "source of truth" is the log
  - that's only true in the (frequent) case of write-ahead logs. 
  - Some database engines may use Rollback logs, or undo logs.

- 
- 
- 

- ## 💡 [Sagas should rather be totally autonomous · redux-saga/redux-saga](https://github.com/redux-saga/redux-saga/issues/8)
- You have to consider the source of truth according to what you will want to record / replay and how the derived source of truth should behave after code change.
- 👉🏻 state sourcing
  - If you consider state as a source of truth, then you can record state and replay them in the same React app.
  - If you record only state, you don't have the event log and then if you change a reducer the state history will remain the same: you can only hot-reload React views
- 👉🏻 event sourcing
  - If you record events (or actions) of what has happened, then you can replay these events into redux reducers to recompute the whole history of states, and replay this state history into React to show something. 
  - If you change a reducer, then you can compute a new history of state: this is how Redux hot reload works. However you can not modify the event log.
- 👉🏻 command sourcing
  - If you choose to record the commands (ie the user intent) then you can recompute an event log from the intent log, and then a state log from the event log. 
  - The intent is generally translated to events in actionCreators and jsx views where we transform low-level dom-events to Redux actions.
  - Command sourcing would permit to hot-reload the interpretation layer too and would replace the "WentLeft" by a"Jump" in the event log before computing the state log and before injection states in React. In practice it has not much interest and may be more complicated to do (not sure but maybe ELM is doing this no?)

- ## 🤔 [What do you mean by “Event-Driven”? | Hacker News_201702](https://news.ycombinator.com/item?id=13593683)
- Event-sourcing implies CQRS, but the reverse is not true.

- I see CQRS as an implementation detail orthogonal to ES, but which dovetails nicely as they both work well with distributed systems. ES has immutable events (monotonically increasing), and CQRS implies a distributed system and allows for more efficient retrieval, leveraging ES's immutability.

- I think that most of the time event-sourcing will impact your model/business-logic layer, because you often want to capture the intent of changes, rather than calculating a naive combined delta of all changes that occurred in memory.

- A good summary. However too many choose to view it only as Event-Sourcing/CQRS, a silver-bullet applicable to a minority of applications.
  - Event-Driven as an architecture that is based on recording changes to a baseline state, should be applied only where really suited.

- ## 🤔 [Why did you reinvented Event Sourcing, a concept that had existed for almost a decade, and renamed it to "Redux" instead of keeping the original name?_201607](https://github.com/gaearon/ama/issues/110)
- Redux is JS library inspired by Flux, Elm and Om. **Both Flux and Elm are inspired by event sourcing**. Redux is not called EventSourcing.js (is this what you propose) for the same reason Flux and Elm are not called EventSourcing.
  - PS. Redux is actually somewhat different from event sourcing (see all those discussions) but again, I’m not claiming it’s somehow better, or that Redux is a pattern.

- ## [Redux and it's relation to CQRS (and other things) · reduxjs/redux](https://github.com/reduxjs/redux/issues/351)
- event sourcing, if you haven't come across it before, treats everything that happens in your domain as an "event", records every event, and regards the events as the source-of-truth. 
  - All other data is just viewed as derived state, and should be able to be regenerated by replaying events.
- There's a very strong analogy(相似) with Redux here, I think. Actions are events, and using pure reducer functions to change state guarantees that replaying the actions will get you back the same state.
  - Event sourcing and CQRS go hand in hand, but it is possible to do either one without the other. 

- ## [Towards a text editor construction kit · xi-editor/xi-editor](https://github.com/xi-editor/xi-editor/issues/1187)
- Maybe I'm imagining your system as having 2 levels of architectural decoupling/distance:
  - Stuff that happens synchronously, inside the same process / called directly from your onEdit event handler.
  - Stuff triggered from witnessing a CRDT edit operation. This could be in another process, on another computer.
- Traditional IDEs do everything in (1), and so they become monoliths which struggle to have clean architectural separation. 
  - In response, you've been doing lots of things in (2) - which makes decoupling easier, and collaborative editing easier, but maybe its not the right fit for something like for bracket matching. 
  - I acknowledge that CRDTs are probably the right approach if you want to do P2P editing. 
  - But having a swarm of small pieces communicating in loosely defined ways seems like a huge source of unexpected / unwanted complexity. 
  - (I think this is also the reason why I think dataflow style programming > OO style programming.)
- 👉🏻 So with that in mind I've been approaching this problem space with another architectural layer - basically considering **realtime edits moving through the system as an event sourcing problem**. 
  - Unfortunately this still doesn't solve your bracket matching issue - you might be right there; maybe the right answer is to just do it synchronously in the editor. 
  - But for things like compilers, and for generating syntax highlighting information, I think the DDD / Event sourcing / FP / etc philosophy that "data only flows one way" is a really solid grounding. 
  - It makes a lot of things easy to reason about, and because its async by nature you can still do magic tricks like pull any parts of your system out into separate threads, processes, or run them on different computers.
- I could imagine doing the whole thing with just synchronous changes and an event sourcing system, but that would struggle with p2p collaborative editing. 
  - And it sounds like synchronous changes + CRDTs struggle with complexity issues around ordering and priority. As you say, without the CRDT model some problems become quite trivial. 
  - I'm not sure if it makes sense to use CRDTs + event sourcing. There's overlap there, so you're paying a complexity cost. But maybe its worth it.

- ## [What tools/frameworks do you use for event sourcing and CQRS](https://www.reddit.com/r/node/comments/q5u3pj/what_toolsframeworks_do_you_use_for_event/)
- Use NestJS. It has a package for CQRS. For Aggregates (and Entities, etc) read up on Domain Driven Design. 
- For DDD I would recommend an ORM like Mikro-orm

- Why do you think Mikro orm is better for DDD? (comparing to something like typeorm?)
  - Because Mikro-orm has a Unit of Work pattern and as far as I can tell TypeORM does not (or it has to be added in).

- I learned a very valuable lesson. Event Sourcing is not a silver bullet, and I'd wager that 80% of the time it is probably more trouble than it's worth. It takes a long time to implement, and comes with a lot of boilerplate, but that's not the main problem. The problem is onboarding developers who are not used to Event Sourcing. That takes a long time.

- ## [Hybrid CQRS-Request/Response with Event Store - EventStoreDB](https://discuss.eventstore.com/t/hybrid-cqrs-request-response-with-event-store/1636)
  - Would it be possible to have a hybrid system that would have mainly request/response operations and some commands
- FWIW, we do this. We have a request/response REST API which creates
commands into aggregates, then events. On return from POST we redirect
to the view with an extra `?t=<commit position>` query parameter. When
that GET hits, on any server in the cluster, a filter will pause the
request until the read model database has been updated with at least
that commit position, thus providing "read your own writes" semantics.

- ## [Dolt is like if Git and MySQL had a baby._201912](https://www.reddit.com/r/programming/comments/ec5jez/getting_to_one_9_of_correctness_for_our/)
- Two big use cases:
  - Data provenance. For every cell in the table, you know who put it there, when, the commit message associated with it, who approved it, and the full history of all its values it's ever had.
  - Collaboration. Anytime there is a crowd-sourcing element to data collection, the branching and merging capabilities of dolt let the maintainer of a data set get all the benefits that maintainers of open source software projects already get with GitHub. Your collaborators submit pull requests that you can then merge.

- Why this instead of tried and true methods like date effective records, event sourcing, and annotation tables?
  - For an **online** production database, the methods you name are the way to go. No question.
  - Dolt is an **offline-first** database meant for collaboration and distribution of data. We don't just want versioning: we actually want a commit graph so that we can implement git semantics on top of it. This is what allows multiple parties to fork each other's repos and still meaningfully contribute their changes back upstream.

- What database is being used to store the changes to the database? 
  - The database itself is a Merkle DAG, like Git. That's how we get the branch / merge / diff semantics. It's built on top of a heavily modified fork of noms.

- ## 🤔 Has anybody tried using Dolt? It looks quite young._202006
- https://news.ycombinator.com/item?id=23533223
- I think this idea is really valuable, but I usually see it implemented as a time-series extension on top of Postgres or MySQL, like SQLAlchemy-Continuum or TimescaleDB. 
  - i.e. you caan get most of the useful git-like time-travel semantics (modulo schema migrations) out of timeseries data with a separate transaction history table.
  - I'm curious what Dolt's performance profile looks like (i.e. how reads and writes scale vs "branch"-count, row-count, and how they handle indices across schema migrations), since the aforementioned solutions on Postgres are building on an already-very-performant core.
- we(dolt) are quite young. We are also focused at this stage on the data distribution use case (ie. use Dolt instead of putting a CSV or JSON file on GitHub). So, we haven't spent much time on query performance or scale. 
  - The current model is that the database and all of its history have to fit on the user's hard drive. 
  - The format is easily distributed (ie. put content addressed chunks on different servers, optimize for fewer network hops) but that's not how it works today.

- 👉🏻 for time-travel. One of the most evident architecture when dealing with AI/ML/Optimisation is to design your application as a mesh of small, deterministic, steps (or scripts) reading input data and outputting results. 
  - As you would expect, output of one step is reusable by another one.
  - Script A is reading Sales data from source S, Weather data from source W; writing its result to A. Script B is reading data from source A, and Calendar from C; writing its result to B
  - in the real-world, S, W, C, progress at different speed : new sales could be inserted by the minute, but the weather data would likely change by the day. So, you need a system that would allow you to read S@2fabbg and W@4c4490 while being in the same "repository".
  - That's why git semantics are not a good fit: you need to have only one "branch" to ensure consistency and limit misunderstandings, but you want to "commit" datasets in the same repository at different pace. For that purpose, event sourcing is much better (BTW, git at its core, is basically event-sourcing). Kafka's architecture is actually the best solution.
  - I use something very similar to https://www.snowflake.com/. An event-based system sitting on top of s3, indexed with a postgresql, influxDB, or anything else.

- ## [Limits of Event Sourcing? · reimagined/resolve](https://github.com/reimagined/resolve/discussions/1789)
  - Would Event Sourcing be an appropriate technology/usecase for a company like Discord? 
  - They want to store every message for all time which seems like a good usecase for Event Sourcing, but im wondering if you have a single event store with billions of eventsin it (growing 40 million events per day) then would it still be appropriate?
- In this example, i would divide the problem. Even if they deal with billions of events, app is divided by "discord servers" - whether it physical servers or not - does not matter.
  - Any particular server is dealing with its events and its read models and can not care about other servers.
  - So, if it needs to rebuild its read model it can only deal with own events.
- Snapshots - in reSolve meaning they are not very usable here. Snaphot is a state of one aggregate. Snapshot is useful when aggregate has a lot of events. If aggregate has 10 events, it is faster to load these events and run reducer. So in Discord - if aggregate is a message, then it is usually has 1 event, rarely several.
  - If aggregate is a chat log, then state is almost identical to event log (it is a history of messages), so again, it is easier to process events...

- Regarding read models being duplication of data. In event-sourced Discord I would probably keep only recent chat history in read models, and compute anything older on-the fly from event store. Or keep those historic read models not in DB, but in files or S3 buckets. 
  - Again, ES/CQRS makes this quite easy - just set up read model that writes to files.

- 👉🏻 We are thinking about splitting read models into independent parts/shards. This will allow a parallel and independent read model rebuilding. 
  - For instance, in multi-tenant app like, say, Slack, each tenant does not depend on other tenant's events.
  - In future reSolve release we will let developer provide a way to map event to partition and all partitions will be processed in parallel.

- How would you evict(evict) old messages from the read model DB? Do it when you insert a new message?
  - Yes. Or you can do this as a part of maintenance job. Like, once a week. 
  - It can be done outside of reSolve. 
  - Or you can do system event in the app to trigger this.
# discuss-cons
- [When not to use Event Sourcing?](https://event-driven.io/en/when_not_to_use_event_sourcing/)

- ## 

- ## 

- ## [Don't Let the Internet Dupe You, Event Sourcing is Hard](https://www.reddit.com/r/programming/comments/r5p8qj/dont_let_the_internet_dupe_you_event_sourcing_is/)

- ## [Event Sourcing Is Hard (2019) | Hacker News_202111](https://news.ycombinator.com/item?id=29390483)

> [Don't Let the Internet Dupe You, Event Sourcing is Hard_201902](https://chriskiehl.com/article/event-sourcing-is-hard)

- I've worked with several event sourcing systems 
  - it's just too complex for non-infrastructure software without resources measured in the 10s or 100s of man years.
  - 99% of the time when ES sounds like a good idea, the answer is to just use Postgres. 
  - Use `wal2json` and subscribe to the WAL stream - if you really need time travel or audit logs or whatever, they'll be much cheaper to implement using WAL. 
  - If you need something more enterprisey to sell to the VP-suite, use Debezium.

- Thanks a lot for mentioning Debezium. Agreed that a CDC-based approach will be simpler to implement and reason about than ES in many cases.
  - Semantics are different a bit of course (e.g. ES events capturing "intend"); we had a post discussing the two things a while ago on the blog [1]. 
  - Speaking of capturing intend, we just added support for Postgres's pg_logical_emit_message() function in today's release of Debezium 1.8.0

- 🤔 Am I crazy for wanting a standardized WAL format that can be treated as an event stream for anything from replicas to search services to OLAP? Why can't we drink straight from the spigot instead of adding abstractions on abstractions?
  - Its honestly not that hard to build a WAL-style solution exactly the way you want it for your own application
  - Do you know how to model your events using a type system?
  - Can you be bothered to implement a Serialize and Deserialize method for each event type, or simply use a JSON serializer?
  - Do you know how to make your favorite language compress and uncompress things to disk on a streaming basis?
  - Do you know how to seek file streams and/or manage a collection of them all at once?
  - Can you manage small caches of things in memory using `Dictionary<TK,TV>` and friends?
  - Are you interested in the exotic performance possibilities that open up to those who leverage the ring buffer and serialized busy wait consumer?
  - If you responded yes to most or all of the above, you are now officially granted permission to implement your own WAL/event source/streaming magic unicorn solutions.
- 👉🏻 The hard part happens after you get the events to disk. 
  - Recovery, snapshots, garbage collection - that's where the pain kicks in. 
  - But, none of these areas is impossible. 
  - Recovery/Snapshots can again be handily defeated by the mighty JSON serializer if one is lazy enough to succumb to its power. 
  - Garbage collection can be a game of segmenting log files and slowly rewriting old events to the front of the log on a background thread. 
  - The nuance is in tuning all of these things in a way that makes the business + computer happy at the same time.

- Most common issue I've ever encountered with event sourcing is that devs submit events that when replayed, lead to invalid states.
  - And if you're using an immutable log (Kafka/Pulsar/Liftbridge etc.) fixing those mistakes is hard.
  - But, I'm a big fan of streaming DB change events for auditing purposes - but those are coming from software that already enforces valid state changes.

- Adding something like change-data-capture to a system and using that for some of the purposes that event sourcing touts seems like it goes a lot further and doesn't require making a complex, hard-to-understand system. 
  - Having a CDC system to publish events and record those can give the biggest benefits and sit alongside a much simpler system. 
  - A downside is that the real-time feature goes away.

- ## 💡 [Event Sourcing is Hard | Hacker News _201902](https://news.ycombinator.com/item?id=19072850)
- I worked on a fairly large system using event sourcing, it was a never-ending nightmare.
  - Events are pretty much a database commit log. This is extremely space innefficient to keep around. And not nearly use useful as you might think.
  - it eventually took DAYS to re-run the events. 
  - De-centralizing your data storage is a bad idea. We ended up not only with a stupidly huge event log, but multiple copies of data floating around at each service. Not fun to deal with changes to common objects like User. Sometimes you would have to update the "projection" in 5-10 different projects.
  - Some of these problems are fixable in theory. Perhaps a framework to manage projection updates, something to prune old events by taking snapshots, a DB migration style tool to "fixup" mistakes that are otherwise immortalized in the event stream.

- 🧩 Event Sourcing = everything that happens is an event. 
  - Save all the events and you can always get to the latest state, as well as what things look like at any time in the past. 
  - This concept is used pretty much everywhere. 
  - Redux is event sourcing front-end state for React. 
  - Most database replication is event sourcing by using a write-ahead log as the stream of mutations to apply. All
  - that being said, I completely with this article that it's the wrong solution for most cases and creates far more problems and limitations than it solves.

- Redux often does not have to keep track of versions, because the event stream is consistent for that session.
  - The most common approach is to add versions to the events.
  - Downstream apps and consumers that don't need to be compatible with the entire timeline can then migrate code over time and only deal with the latest version.

- Basic event sourcing is quite simple to implement.
  - Your typical application presents a user interface based on data in a set of database tables (or equivalent), the user takes some action, the database tables get updated.
  - The equivalent event-sourced application presents a user interface based on data in a set of database tables (or equivalent), the user takes some action, the outcome of that action is written to one table, the other database tables get updated.
- 👉🏻 You need to know beforehand how exactly you’re going to pull out the data, how it’s going to be indexed, updated, etc. 
  - You can get nice benefits out of it especially if you’re doing transaction states, but your **query times are going to suffer unless you’re caching the end-state**.
  - This can make “simple” things take a lot of effort. It’s a really significant departure in terms of effort to deal with your data.

- I think one thing can not be repeated often enough:
  - 💡 Eventsourcing can be an incredibly valuable approach, but almost **always only for a very SMALL SUBSET of your system**.

- Datomic is, at its core, an event sourced datastore, and it works really well. I don’t think event sourcing is something that should be solved in application space — you wouldn’t write a database from scratch for your products yet implementing an in-house event sourcing system is for some reason more acceptable.
  - I was thinking about Datomic when I read this, and yet came to exactly the opposite conclusion. Datomic may be something like 'event sourcing' internally, but it works so well because it abstracts and hides the naked overreach that the article pounds against. Datomic users think of it as a DB, not a stream of events. So I don't think that Datomic users are following the 'event sourcing' model.
- For "real" events (e.g. "Transaction fraud detected") possibly I wouldn't use Datomic at all even if it was my primary DB. There are more suitable pub-sub systems.
  - And that results in a neat separation of concerns: data changes in one store, actual business-valuable events in the other.

- 🤔 One of the problems I think I see with event sourcing is its inability to scale. You have to guarantee the order of events, right? How do you do that in a large scale distributed system with eventual consistency, without incurring an insane synchronization time penalty?
- You generally only have to guarantee the ordering of _some_ events--not all of them. Ideally you want a way to partition your data such that ordering is only important per partition.
- This depends on the nature of your scaling issue. Are you having trouble with consuming events? Or with adding all of your events whilst trying to ensure that they are ordered?
  - For the former, you might use something like ZooKeeper in your consumers to control parallelisation.
  - For the latter, you order by time of insertion. I think you might have some constraints you haven't mentioned that may be the real problem you are trying to solve. What is distributed?
- Vector Clock, which is a good solution for where it's usually applied, but I think this is different. Having everything bottlenecks through your vector clock isn't going to be feasible.
- Exact order of events should be guaranteed for one DDD aggregate, it is doable with simple **optimistic locking**. So unless your system consists of one aggregate - you should not have scalability issues.

- If you want to do event sourcing. Look at persistent actors from akka (jvm and clr). It solve a lot of features as discussed here with replay, snapshotting, event upgrades etc.

- EventSourcing is not a Framework, but a concept. The idea is to store not the current state of your app, but the transitions (events) that derive into the current state. In theory it is a beautiful idea; in the real world, it is hard to implement.
  - In fact, git stores a full snapshot of your entire repo with every commit. It does not store diffs from the previous commit. When you do `git show <COMMIT_SHA>` it generates a diff from the parent commit on the fly.
  - There's a huge optimization though: it uses a content-addressed blob store, where everything is referenced by the sha1 of its contents. So if a file's contents is exactly the same between two commits, it ends up using the same blob. They don't have to be sequential commits, or it could even be two different file paths in the same commit. Git doesn't care - it's a "dumb content tracker". If one character of a file is different, git stores a whole separate copy of the file for it. But every once in a while it packs all blobs into a single file, and compresses the whole thing at once, and the compression can take advantage of blobs which are very similar.

- 
- 
- 

- ## [Event Sourcing made Simple | Hacker News _201805](https://news.ycombinator.com/item?id=17061019)
- If you're already using react/redux, there's one really nice pattern to make eventsourcing easy to implement. I learned it from the boardgame.io google project
  - Basically redux is more or less already doing eventsourcing on the client. You have actions("events") that tells your global state what the next state should be, and replaying the history of all actions will deterministically get you to your current state. The only thing you need to do is persist that history of actions in your state also (which is already commonly done for implementing undo and time-travel).
  - Then all that is left is to make your server use these same events too! This means whenever you save to the server, rather than doing GraphQL/REST-style per resource updates, you just sync any unsaved redux actions from the client. The server will save these actions and optionally replay them to get a snapshot of current state
  - Afterwards realtime collaboration, undo/time-traveling, history/audit logging, etc all come for free.
  - This is a really nice way to unify event shape design that is consistent on client and server.
  - I am making it sound a little simpler than it is. There's a lot of details to get right with state design, tagging actions as relevant to be persisted, multiplayer conflict resolution, app versioning issues, event queue compaction, serverside permissions validation, etc. But to get a prototype up and running quickly what I said above will work. Boardgame.io didn't worry about those details but it's still a nice codebase to study

- The event sourcing pattern (or something akin to it) can also be applied on the data structure level to create very resilient and flexible CRDTs: http://archagon.net/blog/2018/03/24/data-laced-with-history/

- See cloud event spec https://github.com/cloudevents/spec

- ## [Ask HN: When should event-driven architecture be avoided? | Hacker News](https://news.ycombinator.com/item?id=30206046)
- No concurrency? No events. 
  - No more than a single team running a single service (even a monolith)? No events. 
  - Not dealing with asynchronous 3rd party APIs (eg: webhooks)? No events. 
  - Not dealing with arbitrarily many hosts/processes/tasks/objects communicating with each other, potentially asynchronously? No events. 
  - Not streaming? No events.

- When unrestricted, event driven systems don't have a well defined overall state or consistency. Avoid if you have rules that depend on a system "state" Having said that, toy systems aside, almost all systems require reasoning of their overall state at some point, so in general - avoid.

- The approaches you listed are useful, and the dissent I have isn’t so much on the approach, as the timing of when it gets used. Tons of software will never need its benefits and shouldn’t pay the tax ever. Paying the tax before you have to is very rarely worth it in my experience.
# discuss-cqrs
- ## 

- ## 

- ## The Jakarta Data discussions have clarified for me that this notion of an “aggregate” does represent something totally real in document or hierarchical databases—a thing that doesn’t exist in relational data. 
- https://twitter.com/1ovthafew/status/1733452432716267884
  - Trying to shoehorn relational entities into “aggregates” is a mistake.
- Not so sure. Aggregates (in DDD terms) are a notion of a domain model (e.g. Java objects), independent from a specific persistent representation. 
  - They control/define access and transaction boundaries, both to ensure only valid state transitions of an aggregate and its parts are executed. 
  - They can be mapped to different persistent representations, more easily to documents, slightly more involved to relations. Now whether this should be baked into as spec...

- I think the thing you are missing in this DDD world is that the aggregate is defined for a specific bounded context which might not exist in a different one. Don't think of modeling to be something absolute or global. It's a valuable abstraction on top of ORM to manage complexity.

- following DDD is a mistake, because it pushes you to design a system decoupled from the nature of the database you choose, everything needs to be coupled to it.
  - No, that's not my view. My view is that the DDD notion of an "aggregate" not an intrinsic part of OOP, and I have spent 20 years of my life doing OOP without needing it. Rather, it's something extra and unnecessary that DDD glues onto the side of OOP.
- "Aggregate" is unnatural in _both_ the relational model, _and_ in OO data modeling. It's very natural in document databases, however.

- ## 7 reasons why an Event Broker is essential in Event-Driven Architecture
- https://twitter.com/dunithd/status/1729046649983668276

- ## How do you apply the 𝗖𝗤𝗥𝗦 𝗽𝗮𝘁𝘁𝗲𝗿𝗻 to your system? Here's my approach to implementing the 𝗹𝗼𝗴𝗶𝗰𝗮𝗹 𝗮𝗿𝗰𝗵𝗶𝘁𝗲𝗰𝘁𝘂𝗿𝗲.
- https://twitter.com/mjovanovictech/status/1717076357434179852
  - I prefer using MediatR - but this idea works fine without it.
  - MediatR implements the mediator pattern. It decouples the in-process sending of messages from handling messages.
  - [CQRS Pattern With MediatR](https://www.milanjovanovic.tech/blog/cqrs-pattern-with-mediatr)

- ## [CQRS and Event Sourcing Intro for Developers | Hacker News_201905](https://news.ycombinator.com/item?id=19978091)
- Like anything else, it's one tool in the tool bag, but like that giant pipe wrench that you're always looking for a reason to use, it's almost always the wrong tool for the situation. 
  - CQRS carries horrific complexity and requires commitment to a handful of golden rules or the entire thing comes crashing down.
- What are the golden rules?
- Two bigs ones for me:
  - Don't use the read side from the write side.
  - Each aggregate should own its data (or more abstractly, the basics of DDD, bounded contexts).
- Every state change needs to be reflected as event. Does your function need to save something to DB? Then your functionality should create event which will perform the DB save.

- Has anyone tried doing Event sourcing with a redux app? I'd be pretty interested to see the same "store" working on frontend and backend and every redux event being queued up and (eventually) synced to the server to provide a log of what happened. Obviously this leads to building an analytics system for your product quite quickly.
  - Redux pretty much is CQRS + event sourcing, as applied using functional paradigms.
  - Same for Re-frame in CLJS

- ## [CQRS in Node.js](https://www.reddit.com/r/node/comments/tm33nh/cqrs_in_nodejs/)
- It is advisable to begin with the simplest architectures and add complexity when needed. 
- If this proves to be non-viable, check to see if a materialized view (or a materialized projection via $out in case of MongoDB) can fulfill your needs. 
- If data recency is a requirement and the system does not expose Domain Events in any meaningful way, CDC (change data capture) may be an option. 
- Fun fact: implementations of so-called incremental or live materialized views in commercial SQL RDBMSes often rely on triggers under the hood. It's possible to build an incrementally-updating materialized view using triggers.
- And now, the last option for common Entity-driven applications, which impacts the domain-side (write-side) architecture to the greatest degree, is having Domain Events.
- Wolkenkit implements the last option with Event Sourcing. However, the licensing is commercial unless you can accommodate AGPL
- Another option, with a clearly-functional style, is resolvejs
- Last but not least, EventStoreDB has built-in support for projections. As a dedicated database built for Event Sourcing, it has drivers for many popular languages. Then, more of the CQRS machinery is pushed to the DB side.
- Other design possibilities exist, however. Some systems may benefit from a message-first approach, where things are put on a stream/queue first, and only processed later, with only minimal, stateless validation performed.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Event sourcing is essentially as if your database only had a WAL but no table files. Key lookups? Queries? Unique constraints? 
- https://x.com/gunnarmorling/status/1847953333937467864
  - You'll be on your own with all of that, and more. 
  - Not saying there isn't a place for this, but be sure to do a really thorough cost/benefit analysis.
- You can always have whatever derived projections you find beneficial.
Always reaccumulating from a scratch is doing event sourcing wrong.
  - yes, yes, yes! Let’s add cache invalidation to the mix.

- seems like generalizing the outbox pattern affords the best of both persistence mechanisms: the wal maintains the eventing part of the system while a traditional relational system maintains the other. ofc both should be part of a single transaction

- Which is why you rarely use event sourcing in its own. You project whatever state you want into whatever tables or indices are convenient for your queries. ES is a pattern for writing data.
  - In fact ES plays the same role in an app that the WAL in a database. You wouldn’t have an eventsourced app without projections for the same reason you wouldn’t have a WAL without tables. It just extends the same idea to your app.

- Event Sourcing + current state snapshot is the way

- ## Drasi combines CDC with event processing, using @Neo4j 's Cypher language. 
- https://x.com/rmoff/status/1842110663008649324
  - In another vindication(澄清；证实) for open source standards, it supports Debezium's CDC format for output.
  - It's worth noting that the docs call out that it's not intended for stream processing over high volume data streams
- That incubation team publishes interesting experiments. In this case, equivalent functionality exists (done differently) inside of Microsoft Fabric as a combination of Eventstreams and Data Activator. Data Activator is derived from an internal, hyperscale stream pattern matcher.

- ## 🆚️ Choosing the right architecture will make or break your systems. EDA vs. REST
- https://x.com/RaulJuncoV/status/1832413686964551708
- Event-Driven Architecture (EDA)
  - EDA uses asynchronous communication, where components interact by emitting and consuming events. 
  - This design is particularly effective for systems that demand high scalability, real-time responsiveness, and loose coupling among services. 
- REST
  - It is a popular choice for building web services that require synchronous, request-response communication over HTTP. 
  - It's ideal for applications where strong consistency, simplicity, and standard CRUD operations are necessary. 
- Many modern systems benefit from a hybrid approach. Choose wisely

- ## If you like logs and databases and event sourcing stuff, definitely check out this article from @PatHelland .
- https://twitter.com/LewisCTech/status/1762034969243943107
  - This is a really intuitive model of Eventual Consistency
- > From this perspective, the contents of the database hold a caching of the latest record values in the logs. The truth is the log. The database is a cache of a subset of the log. /@PatHelland

- I love the concept of logs as a first class distributed database (or at least the write model)
  - Tbh, this was eye-opening for me and since then influenced how I think about systems and design - and everything else causally related to it 

- https://twitter.com/ifesdjeen/status/1762012801847960047
- Performance retrieval seems like a fundamental need to me.
- if performance is not a concern, then Event Sourcing is fine. Problem is, in real world, performance is a major concern. Don’t get me wrong, I think Event Sourcing is a great concept, but only in theory.
- Goog luck replaying 5 years of events when your new server boots.
  - Not sure if you have worked with event sourcing before, but not every time you have to read all messages. You have consumers that store the position to read from it when server reboots. Also sometimes you have snapshot mechanism to not read the whole stream again.
- Snapshots + log is not just the log.

- You mean the actual WAL vs the b-trees?

- ## [The Ever Growing Event Store _201009](https://groups.google.com/g/dddcqrs/c/Ohdi49e9R5w)
- I'm able to cover off most of the common questions, but wound up not having a good story for "If the event store just keeps on growing, how do you manage that data?"
  - backup and restore (10 years of events is a lot of events)
  - size of event store over time (what's your load)
  - keeping inserts performant on an ever-growing database
  - Also, has anyone ever deleted old events, and if so, what was the outcome?

- ## [Why use Event Sourcing : programming](https://www.reddit.com/r/programming/comments/2yqg50/why_use_event_sourcing/)
- I'm using ES in a point-of-sale application that's backed by CouchDB. The events are logged in Couch, which means I can reconstitute in a couple ways (map reduce for example) but clients mostly read "query" events as a subscribable changes streams. 
  - To deal with the problem of strong typing, the events are versioned. In this way, it's not really much different than schema changes or API changes, ie. if your restructure your RDBMS, you'll have a migration headache as well.
  - Ultimately, I think CQRS is more vital to adaptation. By divorcing "mutation" (commands) concerns from the "read" (query) concerns, I think I've sidestepped a lot of the problems that other MVC formulations face. Also, a pretty standard ES technique is check-points. If your obsolete types "roll-up" into a modern "check-point" type (or types actually), it provides another avenue for migration.
  - None of this diminishes your point. The system depends on its events and the structure of those events as the Source of Truth and unlike most designs, you ideally carry forward old types. I don't know if this is the "tough" part though. I think reasoning about ES systems might be more natural to functional programmers where ideas like immutability or persistent data reign.

- You are taking "replaying" too literally. No one ever "replays" events as in reproduce all the real world actions.
  - It is no different than replaying database transaction log. You simply restore the state of the database itself to the latest snapshot, or to any point in time if you like.
  - As for the actions you are confusing events with commands. Event is simply the result of a successful command that is recorded to the database.
- Exactly. That's one of the key pieces to understand about event sourcing -- commands are ephemeral, events are permanent and the only source of truth. You get a command to process a credit transaction, you process it, and you record the result in an event. In the future, you're just reconstituting state by looking at what happened, you're not making it happen again.

- ## [Show HN: Bemi, enabling Event Sourcing for any database | Hacker News_202311](https://news.ycombinator.com/item?id=38164797)

- [Show HN: Bemi – data versioning and time travel for PostgreSQL | Hacker News_202311](https://news.ycombinator.com/item?id=38305527)

- ## 🔥 [EventStore: Open-Source, Functional Database with Complex Event Processing in JS | Hacker News_201811](https://news.ycombinator.com/item?id=18377219)
- 
- 
- 

- ## I’ve built and over-engineered the hell out of this before. The ideal solution for me was push-based event sourcing the feed in memory for each user and the type of feed, i.e., following, notifications, etc., 
- https://twitter.com/ImSh4yy/status/1716882569260597619
- Here's a tl; dr, keep in mind that this is likely way over-engineered for what you may need.
  - Create and update the feeds on push (when a post is published or updated), not on pull (when a feed is requested).
  - Event-source the feed into a time-series database, and store the last X entries in memory for quick retrieval.
  - To reduce costs, only create feeds for users who have been active in the last X days. If they come back, we can create their feed then, which will be a bit slower, but that's fine. 
  - For users with large followings, switch to "pull-based" feeds to avoid touching millions of feeds on every push (the Justin Bieber problem).
- To be clear, each user has their own feed and, at times, multiple of them, depending on how your product works: user feed, timeline feed, notification feed, etc. The same principles apply to all of them. The only difference is how you populate them and sometimes the schema.
  - This also gets a bit more complicated once you have to handle deletes, unfollows, and blocks, but at the end of the day, it's a fan-out queue system under the hood.

- [The Architecture Twitter Uses to Deal with 150M Active Users, 300K QPS, a 22 MB/S Firehose, and Send Tweets in Under 5 Seconds - High Scalability -](http://highscalability.com/blog/2013/7/8/the-architecture-twitter-uses-to-deal-with-150m-active-users.html)

- This is basically what this article I was reading earlier says haha
  - [Design a News Feed System - System Design](https://liuzhenglaichn.gitbook.io/system-design/news-feed/design-a-news-feed-system)

- At scale a pull based solution is way better than a push based one
  - Pre-materialized feeds will require persisting multiple copies of each record which increases data size. When you consider personalized feeds, it will need to be persisted based on your relevance algo, and accommodating new relevance models and scores will require reordering
  - evicting records with low scores and ingesting new ones with higher scores, which is IO intensive and makes A/B iteration much harder
  - I work on the feed at another company and everything is done on the fly. I guess there's no one size fits all when it comes to a system as complex as this

- 
- 

- ## 🤔 [Why Are People into Event Sourcing? | Hacker News_201610](https://news.ycombinator.com/item?id=12627944)
- 👉🏻 Event sourcing isn't nearly as common knowledge among new programmers as the CRUD-one-row-per-entity pattern, and it really should be. 
  - I liken it to introducing version control for your data; when immutable updates are your canonical source, no matter how much the system behind them changes, or the business requirements change, and no matter how many teams are deriving different things from them in parallel, they can all work off of the same data and "merge" their efforts together.
- The one 🐛 downside is that shifting your business logic to read-time means that you need to have very efficient ways of accessing and memoizing derived data. 
  - For some applications, this can be as simple as having the correct database indices over your WhateverUpdates tables, fetching all updates into memory and merging on each request. 
  - For others, you'll need to have a real-time stream processing pipeline to preemptively(抢先的；先发制人的) get your derived data into the right shape into a cache. 
  - And those are more moving parts than your typical monolith app
- One 👍🏻 benefit to actually using event sourcing with a stream processing system is that, in many cases, it can be the most effective way to scale both traffic capacity and organizational bandwidth, much in the same way that individually scalable microservices can (and fully compatible with that approach!).

- The CRUD one-row-per-pattern is common because it's enough for most projects. It works well with ORMs so you can build quickly and securely. 
  - And most of the time, performance isn't an issue and having a history of an entity is unnecessary.

- Considering immutable facts tables are the most stable data model; companies often have to re-invent it (poorly) on top of relational at some point; that storage is often not a problem; and that having clean historical data is crucial for data science; there are increasingly fewer excuses to not adopt a sane data model from day one.
  - I agree partially w.r.t. to tooling - few implementations aid adopting this pattern, but I believe the value of historical data, over time, overcomes not being able to slap some quick Rail CRUD together and then being stuck at local minima.

- For tons of projects it's totally acceptable, has worked for years, nobody paying to implement them cares about historical data and their leverage. In fact the majority of web apps is like this.
- I've probably implemented 300 CRUD projects, and I've never had a single angry person complaining about lack of access to historical data.
  * I keep hourly backups of mysqldumps which can be restored in the case of catastrophic mistakes.
  * I explain that this kind of data collection would be out of scope, and require significantly more budget.
  - Just because it's technically possible, it doesn't mean you need to do it. YAGNI.

- Event sourcing is an extremely expensive design pattern to implement, and it's also very easy to get wrong. Implementing it tends to preclude junior developers from working on the project, makes it harder for database admins to understand the data, and it requires a lot of thought on how to structure the events.

- Here's the term I wish was unfashionable with the kids: reshaping.
  - Did you spot all those command-to-query-to-event-to-log-to-storage data type conversions in those pretty diagrams? That's a whole bunch of needless reshaping of data as it flows through the system.
  - every time you have to make a change to your events, you'd have a data migration project for any running event streams.
  - Naming things is hard too, and there's a lot more naming of entities needed in a CQRS-ES system.
  - I like all the promised benefits of a CQRS and ES, but I can't imagine a case where I'd take the risk of attempting it on anything but a toy project. 

- Maybe some day there will be a system that helps with this. Until then, my main advice is to make sure you have solved your system with a naive solution before you move on.

- Architecting around events has several ramifications(衍生结果, 派生影响; 后果; 分支).
  - For building up a picture of the world, it's pretty good.
  - For decoupled related action, it's not too bad.
  - For coordinated action OTOH, e.g. a high-level application business-logic algorithm, you need to start thinking in terms of explicit state machines and, in the worst case, COMEFROM-oriented programming. Depending on how the events are represented, published and subscribed to, navigating control flow involves repeated whole-repo text searching.

- I was looking into Event sourcing for a system I built recently, and the tooling just doesn't seem to be that widespread yet. How do you read out of the entire event stream to figure out the current state? While there are tools, they seem to be .net focused. Just didn't seem to be a "standard" answer yet.
  - We ended up going with microservices that pub/sub events into Kafka, but maintain their own databases. There's another microservice that lets you query past events for statistics.
- We find that a simple in-memory synchronous message bus + event logging to files goes a long way
  - For something more out-of-the-box, see https://geteventstore.com/ . It has clients in a variety of languages. Comes with a nice HTTP API too.
  - I wouldn't normally read the entire event stream; usually, only the state of a particular object (aggregate, in Domain Driven Design speak) is of interest, E.g. the customer with id 12345. Events contain the aggregate ID, so the query to whatever event store you use would be "give me all events with aggregate ID 12345".

- As an interesting comparison, some people see the Redux/Flux pattern as a front-end parallel to event sourcing.

- ## [Possible innovations in Event Sourcing frameworks. : microservices](https://www.reddit.com/r/microservices/comments/z10u7s/possible_innovations_in_event_sourcing_frameworks/)
  - So, I want to propose solutions (provided by frameworks) to the following issues that haunt developer: Event Versioning & Migration, Transactions Between Aggregates. 

- This is totally the opposite of DDD btw. Like, the spirit of DDD is being more specific and using the ubiquitous language.

- Liveness and linearizability were something I was trying to reuse from existing EventStores. But what you propose is probably something rebuilt from scratch.

- ## [CRDTs are the future : programming](https://www.reddit.com/r/programming/comments/j1iy5h/crdts_are_the_future/)
- How about event sourcing?
  - You could think of CRDTs as a form of event sourcing with the property that events can be processed in any order and still arrive at the same end result.
- Event Sourcing is just a technique for producing and recording a history using events. By itself it provides no guarantees: it’s up to the devs to design the events and the application to produce them, whether the events are actually useful is dependent on the devs and what they built.
  - CRDT’s are backed by probable mathematical theory, which lets them provide guarantees about behaviour.
  - You could, for example, use event sourcing to produce events that are CRDT’s.

- ## [The Future Needs Files | Hacker News_202109](https://news.ycombinator.com/item?id=28391570)
- I agree with the author on the merits(优点; 价值) of the file abstraction, but I think the concept should be updated for networked devices. **We need file formats that support both offline usage and seamless sync over the network**.
- For example, here I use a merkle DAG-based file format to represent CRDT-like types: https://www.hyperhyperspace.org
- I am interested in the distributed computing/P2P space and study it.
  - I think a combination of event sourcing and CRDTs could be used to provide arbitrary synchronisation and merging between peers that handles bad actors through web of trust.
- There are other projects that take an approach similar to what you're describing (Automerge and its derivatives, mainly).
  - I guess there is a distinction between distributed databases and permission-less p2p applications. Having a data center where you can trust the compute nodes running your distributed database is very different than having random untrusted peers over the net. But maybe data validation can be done in a less intrusive way, something like what Automerge does for JSON merging (maybe in a typed setting?).
- I see you're going for a zero trust model where you have baked identities into the data structure. Which is very cool.
  - One idea is to strictly review all distributed apps, so sign them by a central party.

- ## [Ask HN: How does your development team handle database migrations? | Hacker News_201905](https://news.ycombinator.com/item?id=19880334)
- Would be cool to have git for databases.
  - That’s basically the proposition of any event sourcing system. but you’re kinda right, that involves a level of code complication (but then it would be so simple as you described to restore / rebase / etc)

- ## [Ask HN: Options for handling state at the edge? | Hacker News_202205](https://news.ycombinator.com/item?id=31342436)
- 
- 

- There are many technical solutions to this problem, as others have pointed out. What I would add is that data at the edge should be considered immutable.
- Event Sourcing is the most popular implementation of a history of immutable events. But I have found that a different model works better for data at the edge. An event store tends to be centrally localized within your architecture. That is necessary because the event store determines the one true order of events. 
  - But if you relax that constraint and allow events to be partially ordered, then you can have a history at the edge. 
  - If you follow a few simple rules, then those histories are guaranteed to converge.

- Check out Macrometa, a data platform that uses CRDTs to manage state a N number of pops and also does real time event processing. - https://macrometa.com (full disclosure, I work at Macrometa)

- ## 💡 [Eventual Business Consistency | Hacker News_202308](https://news.ycombinator.com/item?id=37009296)
- Another approach to this kind of thing would be storing most of your data as a log of events ("event sourcing") and having "Retroactive Address Change" as its own business-process, one which can be linked to the other steps like sending a refund check or crediting an account.
- I have never seen a productive application of event sourcing at scale. The idea is super elegant but there’s so much extra overhead. Your data size is easily 10x bigger, unless things nearly never change anyway (and then why do it, right?). Even simple things such as fixing a typo require a Command to be stored as an Event etc etc. Fixing fuckups by manual database edits / script runs gets harder because it means you’ll create a mismatch between the events and the main db, so you ought to inject events instead, but you’re under time pressure so what to do, and the list goes on. I wish these things weren’t issues because in a very real way event sourcing feels like the “obviously best way” to deal with pretty much any kind of structured data storage. I want it to succeed.
- Does anyone know of a system that successfully did/does event sourcing at scale?
  - The git version control system.
  - Git doesn't really. It does have a (more or less) immutable, append-only model, but the things stored in git are state snapshots, not events. The UI does tend to present it as if it were events but that's just for convenience.
- I've implemented a system that uses event sourcing at "scale" (YMMV at what is "scale").
  - it has distinct advantages when in production and in the CI/CD deployment. It has additional complexity at the architecture and high level design phase and it needs some standardized libraries and infrastructure to support the necessary features (primarily the internal synchronization of entity/event processing between threads/processes to ensure monotonic updates of the state of the entity).

- Event sourcing and CRDT like distributed data using something like the Event Calculus?

- 
- 

- ## [Library for building event sourced systems in Go_201508](https://www.reddit.com/r/golang/comments/3i7kgx/library_for_building_event_sourced_systems_in_go/)
- I've been experimenting a lot with event sourcing, explaining the concept to people and building small applications using this approach. After many iterations I've finally settled on a way of doing things and cast that into code.
  - The main criticism of event sourcing seems to be that it is "complex". My experience is that it is just a different, unfamiliar kind of complexity. The underlying principles are simple.

- I haven't had the need for snapshotting yet, hence why it is missing here. I'm trying to avoid putting too many things into this package, lest it grows into a framework (it already is a bit too "frameworky" by prescribing a lot of structure).

- Great stuff. I think more libraries and articles about event-based systems would be great. At a high level it feels like your library could have leveraged channels more aggressively though. They do fit event-based models very well.
- Meteor DDP is a protocol for synchronising incremental model changes, and there are some non-Meteor-backed implementations.
- PouchDB is another approach, but ties you to CouchDB.

- ## [Can edgeDB as "Graph Relational Database" be used for Data Graphs (\~Graph Database)? · edgedb/edgedb](https://github.com/edgedb/edgedb/discussions/3964)
- A bit of clarification: EdgeDB is not a classic ORM, i.e. there is no query result post-processing on the "application level" in any case whatsoever. Instead, each EdgeQL query (regardless of its complexity) is always compiled into a single SQL query the results of which are returned to EdgeDB clients directly. Think of EdgeDB not as an ORM but as an alternative frontend to the Postgres query engine.
- For now, you would have to insert these changes via your application, but the upcoming triggers feature will allow you to do it on the database.

- ## [Architecture decisions -- retrieving DB data from mysql](https://www.reddit.com/r/node/comments/cd3nb4/architecture_decisions_retrieving_db_data_from/)
- Event sourcing is an architectural pattern where you store changes over time to an object, instead of object’s entire current state. 
  - Take a customer object, for example. You might have events like customer moved, order placed, product returned, etc. Events are timestamped and denote something that has happened and is immutable. 
  - Event sourcing is related to Domain Driven Design (DDD). It can be implemented in a variety of ways, including SQL. 
  - But in the case of SQL, the database design doesn’t look anything like a traditional normalized relational database. 
  - However it’s implemented, one of the benefits of an event sourced architecture is the ability to replay through the entire history of all changes made to any object. This in turn allows for a microservice architecture on the backend and disconnected operation on mobile apps

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
  - So, I've redefined the way to store objects in memory. They are "single block of memory" (even with strings and arrays in it) with a "body" class that works like any C# class from developper point of view, but internal manage this external virtual memory.
  - Because it use a "single memory block" approach, it can be faster than native . Net objects in many use cases : init, creation, serialization, immutability, deep copy or compare are faster than POCO !
  - And of course, this objects can be stored in a LMDB key/value store, which is near a "silver bullet" when used in the right way, a f***in piece of C code... So, the most critical part - the persistance, ACID -  is based on a robust, fast, well tested OS lib.
