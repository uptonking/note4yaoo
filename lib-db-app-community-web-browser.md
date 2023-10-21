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

- ## 

- ## 
# discuss
- ## 

- ## 

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

- ## 👥 [Web Applications from the Future: A Database in the Browser | Hacker News_202106](https://news.ycombinator.com/item?id=27424496)
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
