---
title: lib-db-app-community-architecture
tags: [architecture, community, database]
created: 2023-09-17T17:37:06.649Z
modified: 2023-09-17T17:37:19.913Z
---

# lib-db-app-community-architecture

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [For Want of a JOIN | Hacker News](https://news.ycombinator.com/item?id=34092645)

- With that said, the JOIN is a very powerful concept which, unfortunately, has been given a terrible reputation by the NoSQL community. Moving such logic out of the database and into to DB's client is just a waste of IO and computing bandwidth.
  - SQL has been the ONLY technology/language that has stuck with me for > 25 years. The fact that it is (apparently) not being taught by institutions of higher learning is just a shame.
- I agree. It took me 3 years or so to actually land in a project and learn SQL for the first time. Before it was all with ORMs. I didn't know what a join was for the first couple of years of my career. Understanding SQL and being able to work with data interactively has made me a better software engineer. This tech is important enough that it should be taught in university/coding camps.

- I often wonder how often this exact problem happens, but where A and B are [micro]services owned by two different teams, one is required by company policy to use their APIs not their raw databases, and escalation of each of these issues e.g. query size/rate limiting runs the risk of burning political capital on top of everything else.

- ## [Don’t we all just want to use SQL on the front end? | Hacker News_202104](https://news.ycombinator.com/item?id=26822884)
- Because it exposes a lot of inner details and potential security/privacy risks if clients are able to change parameters.

- Why hasn’t this been tried?
  - Of course it's been tried. It's because it's been tried enough that people now tell you to hide SQL behind a middle layer...

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

- 
- 
- 
- 
- 
- 
- 

- ## [Ask HN: Is there a way to efficiently subscribe to an SQL query for changes? | Hacker News](https://news.ycombinator.com/item?id=26901352)
- Source: I worked on Google Cloud Firestore from it's launch until 2020 and was the on responsible for the current implementation and data structures of how changes get broadcasted to subscribed queries.
  - Without joins Google Cloud Firestore does exactly what you're describing.
  - With joins (or any data dependant query where you can't tell a row is in the result set without looking at other data) you need to keep the query results materialized otherwise you can't have enough information without going back to disk or keeping everything in memory, which isn't really feasible in most cases.

- I like this idea a lot. In a sense it's thinking of your application as a spreadsheet, where the database is a data tab and the frontend is the summary tabs. If there's a change to the data tab, the "spreadsheet engine" (or "materialized view engine" in your case) walks the dependency graph and updates all the relevant parts of the summary tabs.
  - The closest thing I'm aware of to this is BigQuery's materialized views, which take care of making otherwise expensive queries cheap fast, but they are rather limited (i.e. no subqueries or joins), and don't have the "streaming output of changes" you describe.
- 
- 
- 
