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
  - Would Event Sourcing be an appropriate technology / usecase for a company like Discord? 
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

- ## [Event Sourcing is Hard | Hacker News_201902](https://news.ycombinator.com/item?id=19072850)
- I worked on a fairly large system using event sourcing, it was a never-ending nightmare.
  - Events are pretty much a database commit log. This is extremely space innefficient to keep around. And not nearly use useful as you might think.
  - it eventually took DAYS to re-run the events. 
  - De-centralizing your data storage is a bad idea. We ended up not only with a stupidly huge event log, but multiple copies of data floating around at each service. Not fun to deal with changes to common objects like User. Sometimes you would have to update the "projection" in 5-10 different projects.
  - Some of these problems are fixable in theory. Perhaps a framework to manage projection updates, something to prune old events by taking snapshots, a DB migration style tool to "fixup" mistakes that are otherwise immortalized in the event stream.

- Event Sourcing = everything that happens is an event. 
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

- If you want to do event sourcing. Look at persistent actors from akka (jvm and clr). It solve a lot of feaures as discussed here with replay, snapshotting, event upgrades etc.

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

# discuss-collab
- ## 

- ## 

- ## My favourite thing about CRDTs (and event sourced data in general) is that they force us to consider the meaning of time and order as it relates to information.
- https://news.ycombinator.com/item?id=14304306
  - When handled with clarity of thought there are flow on effects in correctness of processing
  - The downside is that popular frameworks don't mesh well, or at all, with this paradigm. Trying to shoehorn(强挤硬塞) event-based data into say, Rails (which I've done), is an frustrating exercise in resolving massive impedance mismatches and growing technical debt. 
  - Turns out most database-driven MVC frameworks have a very limited understanding of time and order.
  - CQRS helped here, because I realised that my MVC can and should just be a view & query layer, and I should be building the event sourced/CRDT-based logic elsewhere.
- I've found that many of the modern JavaScript UI libraries play very well with event sourcing, IMHO. React and Vue.js in particular work very well when combined with Redux/Vuex and a CRDT database. Both of those stores are essentially event sources themselves, where the actions and mutators are separated and the data store itself is updated only in one place. 
- What CRDT databases do you use in this sort of application?
  - Currently leveraging CouchDB and it's incremental map-reduce to handle the "CRDT" merging of an event stream. Technically I'm not using a CRDT library or DB, but it's surprisingly easy to implement the core "commutative operations" of CRDT's via a modified deep-merge versioning algorithm.

- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

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
