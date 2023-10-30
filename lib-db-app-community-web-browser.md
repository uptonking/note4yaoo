---
title: lib-db-app-community-web-browser
tags: [browser, community, database, web]
created: 2023-09-17T18:46:44.600Z
modified: 2023-09-17T18:47:01.460Z
---

# lib-db-app-community-web-browser

# guide

# discuss-stars
- ## 

- ## 

- ## 🫐🤔🔥 [WebAssembly is eating the database? | Hacker News_202305](https://news.ycombinator.com/item?id=36044112)
- Again nothing new on the horizon, DB2, Oracle and MS SQL Server have had JVM and CLR available for UDF for the last 20 years. Naturally one needs to sell WebAssembly as being the first of a kind.
- 👉🏻 Your examples of novelty are all things that were possible decades ago in most mainstream DBMSes. The SQLite one in particular is bizarre: it’s inherently an embedded db with bindings in every language.
  - Supporting user defined functions as compiled objects loaded into the database is as old as the hills. The sandboxing part is silly since no one in their right mind is going to expose their database to untrusted users in the first place.
- > no one in their right mind is going to expose their database to untrusted users in the first place
  - I've seen projects do exactly this, with PostgreSQL row-level security. Though to be clear, it does seem a terrible idea to me too....even when you prevent unauthorized access, there is always the issue of resource usage.
- Apologies, I should have said something more like “exposing the database to untrusted users is a specific and narrow use case that needs way more db-specific planning”. RLS is really cool tech but you need to design your schema and application around it for it to be useful. Slapping some WASM on any existing databases (especially the vast majority which have nothing like the unique capabilities provided by RLS) isn’t going to buy anything that doesn’t exist already.

- 👉🏻 What WebAssembly brings to the table is the ability for unprivileged(无特权的) users to upload their own arbitrary UDF to the DB for execution.
- The whole point of having a sandboxed runtime like WebAssembly is that the code can be executed without user trust, as the user cannot pierce(刺穿; 穿透) the isolation boundary or exceed the resource limits provided by the sandbox.
  - JavaScript and Python have been used for this since literally the 90s.
- How will that work with RLS and similar controls?
  - I don't see why UDFs and RLS would need to interact, they're orthogonal(垂直的；直角的) concepts that can work in tandem(协同地; 一起地). The DB engine filters out the rows that fail the RLS check, then apply the UDF to the remaining rows.
- You’re exactly right that these are orthogonal. The data isolation is the much harder part (the type of sandboxing provided by WASM has long been available via interpreted languages, see pl/v8 et al).
  - Without exception the existing APIs mentioned in this article don’t attempt to handle “data sandboxing” since it’s so application specific. 👉🏻 So it remains the case that exposing your db to user defined functions is dangerous without a ton of work, and WASM in no way reduces the amount of work needed.
- Not necessarily true. E.g. in PostgreSQL, the planner is free to evaluate predicates prior to imposing RLS constraints, so long as the functions in the predicate are marked LEAKPROOF. (They aren't by default.)
  - This is because UDFs can write to tables, and perform I/O in other ways depending on system configuration and security policy. 
  - 👉🏻 Just because the UDFs are in WASM instead of one of the other UDF languages doesn't eliminate the need for a security system.
  - Aside -- curiously in PostgreSQL, the privilege system isn't even strong enough to prevent something as innocuous as e.g. reading a view owned by another user from dropping your own tables

- I remember seeing "gcc/clang/cl -o blah.so/dll/dylib" for an UDF functions (various DBs), and then dlload/loadlibrary/etc it. Nothing new really, but avoids having a compiler, and maybe the wasm sandbox helps with security.
  - My only worry in all this (and wasm) in general is how well you can debug this later - be it interactive, or postmortem dump. 
  - So far the best integration I've seen between different languages/runtimes have been C++ / . NET (C#) and C++/CLI (e.g. their managed C++) - I can debug, step in, post-mortem debug without an issue.
  - I can't even do this properly with GoLang, and had mixed success with Python (+.pyd files).
  - Debugging (interactive, and post-mortem) is often overlooked, and thought about later.
  - I'd encourage you to check out one of our projects, Extism[0], which helps make the kind of integrations you mention way easier! (and using wasm)

- > the ability to bring compute to data eliminates the need for as many microservices — run those in the database instead!
  - We de-linked the two because there was no practical way to autoscale the database, but autoscaling microservices is easy. Obviously you want to be very cautious about how you treat inelastic compute.
  - Today there are lots of practical ways to autoscale databases and colocating data and compute is generally good for performance and simplicity (your mileage may vary for simplicity).
- Decoupled scales, but you end up replicating the dataset in compute node caches, which is expensive. Ideally you want scalable storage with compute (assuming really large datasets), so you can move the computation, which usually is small, close to the data. In any case, it's not one size fits all, and each problem space matters.

- The Web Assembly Component Model can't land soon enough.

- 🤔 Does anyone have any good resources that cover the implementation of wasm as a plug-in system on either a backend or frotend? Just curious to deep dive on this. Could be a video or in-depth article.
- We (Splitgraph) implemented WASM UDFs in Seafowl, a database written in Rust based on Datafusion and optimized for executing queries "at the edge" and returning cache-friendly HTTP responses. Users can call CREATE FUNCTION within an SQL query to create a WASM UDF.
- Fluvio is an open source data pipeline project w/ plugin wasm modules for data transformations as "SmartModules". In our case we can run wasm plugins on frontend or backend (none of which require a browser). 

- WebAssembly: achieving the goals of the JVM two decades later.

- 🤔 as someone who has never used UDFs, how can running them inside of transactions possibly be performant?
  - Depends on a lot of factors, but most databases have some overhead per call, especially if it happens over a network. If you can write some procedural code that runs on the database and eliminate calls and network traffic that may be a win. Then there is the SQL overhead of parsing and compiling queries, various forms of stored procedures can mitigate that by having a function that is compiled once, and then called with different input data. 
  - How this all works varies a lot between databases, so what works in one may not be optimal in another.
- Plenty of conventional applications run code in a transaction; that's not a novelty. There is a valid concern with using extra CPU/RAM on a (hard to scale) database rather than (easy to scale) application servers. But it all depends on what you are doing, your tenant model, etc.
- DB performance tuning is complicated but well-understood. I don’t see any particular reason that functions run in a db would be any more of a problem than “serverless” in another environment.

- WASM's runtime is far simpler than JS's, or even something like the JVM, particularly due to lack of garbage collection. The language was deliberately designed to be straightforward and efficient to JIT compile to a safe virtual machine, e.g. attention was paid to making sure bounds checking could be elided efficiently for constant offsets while being enabled elsewhere. It's also significantly simplified compared to assembly, and lacks functionality like arbitrary jumps that are common sources of vulnerabilities. It's pretty much ideal for the usecase of "I want to run pretty fast code on an untrusted machine" which is the main reason it's taking off.
  - (Obviously, as WASM JIT compilers get more elaborate and it incorporates things like GC'd references, some of the advantages of this design wrt simplicity will disappear, but I anticipate that these kinds of features will mostly not be used in settings like databases).
- Dart/flutter can now target wasm (unstable), so better gc support is coming (e.g. not gc running from whatever you compiled, but rather the wasm vm would do for you)

- 👉🏻 WebAssembly running in the browser runs in an isolated environment whose only access to the outside world is by calling out to JavaScript functions exposed to it when it was initialized. So it doesn’t open up any new APIs.
  - It does get recompiled to bytecode that runs directly on the processor, so in theory there could be vulnerabilities that come up from that, but I think it’s a pretty well-understood surface area at this point.
- That’s what we’ve been doing since the dawn of JavaScript, in a VM with a much larger surface area. A simper VM should be quite a bit safer than the status-quo.

- 😩 Unfortunately, the design of WASM and common compilers targeting it means that your security is at risk as a user, even though your PC is safe. Applications compiled to WASM have a wide variety of fun security vulnerabilities that have been gone on native targets for decades, which means that if (for example) Gmail moved to WASM, it would now be possible for malicious parties to attack your Gmail tab even though they can't attack your PC. Some examples:
  - Address space layout randomization is gone - if an attacker gets a write-anywhere primitive, it will work 100% of the time
  - Page protections are gone - all data is mutable, even things that shouldn't be like string constants compiled into the binary
- Ultimately WebAssembly runtimes are very secure, but you have to protect everything else from the code you're running, because the code itself can easily be attacked by uncontrolled input.

- WASM will eat SPAs and a chunk of the gaming market, it's just a matter of how long it takes.

- ## 🛢️🔥 [Lovefield – A relational database for web apps | Hacker News_201509](https://news.ycombinator.com/item?id=10197672)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 🔥 [How Modern SQL Databases Are Changing Web Development: Part 1 | Hacker News_202308](https://news.ycombinator.com/item?id=37246740)
- 
- 
- 

- ## 🔥 [TabDB: Using browser tabs as a database like only a maniac would | Hacker News_202307](https://news.ycombinator.com/item?id=36548055)
- 
- 
- 

- ## 🤔 [Don’t we all just want to use SQL on the front end? | Hacker News_202104](https://news.ycombinator.com/item?id=26822884)
- Because it exposes a lot of inner details and potential security/privacy risks if clients are able to change parameters. But... it seems like if you're willing to expose your data model to the client, then it seems like some combination of code signing the SQL (with parameters left empty) along with the acceptable list of named parameters

- Why hasn’t this been tried?
  - Of course it's been tried. It's because it's been tried enough that people now tell you to hide SQL behind a middle layer...

- I think when you look at this problem from the viewpoint of local first software - with decentralized sharing and materialized views with a set of private/public relational event source logs - it really comes together well.
  - It doesn't exist yet, but when the tooling is there it's really going to make a splash.

- I’m basically doing this for an app - each endpoint is just a parametrized query and RLS in the database enforces security/auth constraints.
  - The middleware doesn’t do anything except populate query parameters and do a bit of sanity checking.

- Someone else replied that if you have sufficiently advanced build tooling, you can statically extract the SQL/GraphQL from the client side code and replace them with IDs, and then move the SQL to the backend.
  - We’ve taken this approach for implementing database queries in Lowdefy(SQL support will be live in next version, implementation using knex). Also a “shared state” between backend and frontend makes parsing paramaters to queries on the backend really seamless and in return a great dev experience. Also allows to to only parse some parameters like secrets only on the backend.
  - What we are experiencing with Lowdefy apps is that bringing the data model closer to the UI makes coding and UI maintainability of simple projects very easy. This approach works exceptional for us in the BI reporting space where you primarily aggregate data.
  - However as soon as you move out of the CRUD space to more complex backend logic, extracting the logic to a single interface again simplified the implementation a lot, in fact **apps very quickly becomes hard to maintain** in my experience.

- I've spent the last six months working with a codebase that does exactly this. Aside from the obvious problems with exposing your schema to potential attackers, opening up potential DOS vectors, and training front-end engineers on yet another technology, you end up with some code that is very, very difficult to test. If you're using it in your hobby project and you're aware of the pitfalls - fine, go ahead and do whatever you like. But if you're expecting to incorporate this as part of an engineering organization: Save everyone the hassle now and don't.

- The discussion here is frustrating because people are assuming that you'd pass the SQL directly to your database backend and expose your entire schema and all your data.
  - SQL is just a query language, just like GraphQL, and is no less 'secure'. You can still have a layer between the front end and application database.
  - A practical way to use SQL would be to expose the subset of data that is visible to the user and allow that to be queried by SQL, just like it would be by GraphQL or REST.

- Everybody is focused on literally replicating the data model and using SQL which obviously won't work.
  - But the idea is directionally correct. Replicate the subset of data the user has access to and wants locally and work on it disconnected, then sync changes asynchronously to server. This is difficult, but necessary for fully responsive and collaborative applications.
  - Check out https://replicache.dev for a productization of this idea (disclosure: this is my product). We will eventually add a SQL frontend for the cached data.

- Not SQL, but https://pouchdb.com/ looks like a better version of this. Also not SQL, IndexedDB seems like a well-supported document database built into the browser would beat LocalStorage in almost every way. That's what I've found in my experience at least.
  - I use PouchDB for this exact use case and it works great. It solves the storage and replication problems both.
  - If you build it upon SQL, you would also need to create a CRDT schema to make replication sound. That's probably more work than just using REST/GraphQL/RPC.

- I‘m using AlaSQL for years in my projects ... is that the wrong approach or am I missing something here?
  - I think the read/write-through cache to a backend database is the missing piece...at least as far as I can see.

- This is already a thing in Clojure/Script, using datalog instead of SQL. Syncing datoms between Datascript (and/or Datahike) on the front-end and Datomic on the back-end can be almost trivial, and there are libraries like Datsync for that.

- This is, effectively, what Meteor (JS) does; just with MongoDB instead of SQL. It embeds a mini-MongoDB JS client on the frontend to store cached data, queries are ran against that, and missing data is requested, streamed, and rendered asynchronously.
- CouchDB was a really elegant implementation of this strategy without the SQL bit. Local database in all clients, synced back to a server whenever there’s connectivity.

- This is a bad idea for so many reasons. The front-end and back-end data models are vastly different for any non-trivial application.

- As many SQL Injection issues (and various other injection forms, including Javascript) as we have with backend code, fuck no we don't want SQL being issued from the frontend.
  - For one, permissions around SQL are already crap. It takes the smallest screwup to expose data in co-mingled databases. No need to make it even worse.
  - For two, at least if the SQL is on the backend, a fix for an exponential query DDOSing your DB is fairly quick; you don't have to worry about some client keeping a cached copy of the frontend around for months at a time.
  - Finally, if you let the frontend send SQL, you have lost any and all ability to do a static audit against the queries that will be run against your database - because you have no control over what the client does.

- > We need a restrictive SQL parser to run server-side to restrict what can be run and prevent SQL injection. Maybe we need a query-builder/ORM to generate a safe intermediary SQL language in JSON so that we can validate it.
  - What you are describing here is an API.

- The front-end and back-end data models are vastly different for any non-trivial application.

- 
- 

- ## 🔥 [Web Applications from the Future: A Database in the Browser | Hacker News_202106](https://news.ycombinator.com/item?id=27424496)
- Having been a dev on EtherPad, Google Wave, Coda, and other real-time collaborative apps with OT, undo, and so on...
  - I think it's correct that, ideally, there would be a framework that handles real-time collaboration, undo/redo, and offline support for you, and then you build your app with these problems already solved. 
  - I will probably create such a framework eventually. 
  - **I don't see it as a database engineering problem, it's more like a framework or application architecture**, which every app like Google Docs or Figma has its own version of. 
  - Writing such a framework is not too much harder than writing such an app, it just requires a little more abstraction and some documentation.
  - If you've never written an undo manager, sync engine, etc., and you aren't writing a complex app, it's hard to arrive at the right design by thinking about pure data sync. 
  - Also, storing and querying data are solved problems; it's more a question of coming up with a generic data model for an application and defining its semantics.

- Great post. Captured the problem nicely. I went on a similar journey recently.
  - There is a moment when you step back and realize that all the data-wrangling code we write in apps is essentially what an SQL query planner does. 
  - And **our frontend is just one big materialized view that we need to update**.
  - I often think that if we had a database that runs in the browser, and we could subscribe to queries, and missing local data would be fetched on-demand, frontend development would be a lot easier. Its of course much more complicated than that.
  - I think the reality though is that backend scaling requirements always end up dwarfing frontend productivity concerns. And there is also a huge amount of glue between backend data sources, preventing the creation of a clean database on the backend to sync with, meaning we are creating API gateways and GraphQL federation layers, and all we can hope for is a good client-side caching layer.
  - If you look deeper though you will find many projects doing all these kinds of things already. Mobile developers are very familiar with offline techniques and SQLite on the client
  - It's funny though that if you think long enough about these concerns, you always seem to end up wanting some Datalog thing.

- The common abstraction is a shared log. 
  - I'm boiling down my current side project ( http://www.adama-lang.org/ ) into reusable components.
- But you'd want to allow the client query a snapshot before doing a full sync on the shared log.
  - Absolutely, this is a key reason why I strongly believe what goes in the log matters. 
  - If the log is a list of commands, then you have two representations to contend with: the differential/patch form and then the aggregated state.
  - An area that I'm playing around with is a log reducer which transforms a region within a log into a single item. For instance, if the log entries are just JSON (without arrays) then json merge (RFC 7396) is an example reducer.

- We had Meteor with “mini mongo” and you locally subscribed to streams and it was all a quite bloated PÓS IIRC. 
- 🤔 A lot of the principles here echo the same design principles that MeteorJS was built on. Why didn't that work and why now? Is there something about _today_ that makes the web application space different?

- Just use Firebase (firestore) ... It's got: offline first, latency compensation, pubsub, partial sync, authorization rules and serverside timestamps, and global transactions, and 5 9s availability backed by spanner for umpteen languages
  - But then one day your Google account is closed by AI. Or the product is abandoned by Google.
- Firestore is not really offline-first. Your app wont start without internet connection because the auth handler needs that.
  - no, it works as long as you logged in once. You have to ensure auth persistence is on (https://firebase.google.com/docs/auth/web/auth-state-persist...). You cannot login when offline, but if you were already logged in, and expiry is set to indefinite, you can stay logged in while offline.

- There is a very handy RDF DL subset that has all of the desired properties described in the article.
  - Funnily enough we are targeting the browser AND FPGAs, and I think the latter is the much more interesting use case for a distributed reactive CRDT-like database.
  - Datalog is actually trivial to incrementally materialize in open world semantics. Which is why datomic (while a great foundation in theory) turns out to be non ideal. TxnIDs and retractions are essentially nonmononic negation in disguise, and CALM (consistency as logical monotonicity) a.k.a. distributedness, doesn't go well with that.
