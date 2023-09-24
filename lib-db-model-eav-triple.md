---
title: lib-db-model-eav-triple
tags: [database-design]
created: 2023-09-24T18:20:30.236Z
modified: 2023-09-24T18:21:38.495Z
---

# lib-db-model-eav-triple

# guide

- tips
  - EAV performance at large scale is really dreadful
# dev
- [Triplestore - Wikipedia](https://en.wikipedia.org/wiki/Triplestore)
  - A triplestore or RDF store is a purpose-built database for the storage and retrieval of triples through semantic queries. 
  - A triple is a data entity composed of `subject–predicate–object`, like "Bob is 35" or "Bob knows Fred".
# examples

## eav

## triple-store

- https://github.com/spy16/fabric /go
  - Fabric is a triple-store written in Go. 
  - Fabric provides simple functions and store options to deal with "Subject->Predicate->Object" relations or so called triples

- https://github.com/google/badwolf /go
  - BadWolf is a temporal graph store loosely modeled after the concepts introduced by the Resource Description Framework (RDF). 
  - BadWolf began as a `triplestore`, but triples have been expanded to `quads` to allow simpler and flexible temporal reasoning
  - Because BadWolf is designed for generalized relationship storage, most of the web-related idiosyncrasies of RDF are not used and have been toned down or directly removed and focuses on its time reasoning aspects.

- https://github.com/eBay/akutan /go/archived
  - a distributed knowledge graph store, sometimes called an RDF store or a triple store.

## rdf

- https://github.com/linkeddata/rdflib.js /ts-js
  - Javascript RDF library for browsers and Node.js.
  - Reads and writes RDF/XML, Turtle and N3; Reads RDFa and JSON-LD
  - Read/Write Linked Data client, using WebDav or SPARQL/Update
  - Real-Time Collaborative editing with web sockets and PATCHes
  - Compatible with RDFJS task force spec
  - SPARQL queries (not full SPARQL - just graph match and optional)
# blogs

## 📝 [A Graph-Based Firebase_202208](https://stopa.io/post/296)

- In A Database in the Browser(blog), I wrote that the schleps(艰难的旅途) we face as UI engineers are actually database problems in disguise(装扮；伪装)
- my co-founder Joe and I decided to build one and find out. This became Instant. 
  - I’d describe it as a graph-based successor to Firebase.
  - You have relational queries and basic auth. Optimistic updates come out of the box, and everything is reactive. 
- we started with SQL but ended up with a triple store and a query language that transpiles to Datalog.
- Why triple store? What query language? read on.

- Delightful Apps
  - Optimistic Updates
  - Multiplayer
  - Offline-Mode

- Bespoke Solutions
  A. DB
  B. Permissions
  C. Sockets
  D. In-Memory Store
  E. IndexedDB
  F. Screens
  G. Mutations

- Inspiration
  - if we look at how Figma, Linear, and Notion work, we find clues. Squint, and their architecture looks like a database!
- If our Local DB and Backend DB spoke the same language, both could understand and apply the same mutations. 
- Databases handle replication. So what if we made the client a special node? The Local DB already knows the queries to satisfy. So it can talk to the backend and get the data it needs.

- A SQL-based tool is closest at hand. I enjoyed looking at absurd-sql. This uses sql.js (SQLite compiled to webassembly) and persists state into IndexedDB.
- SQL has a schema. Schema is useful, but it make things less easy than Firebase. 
- SQL isn’t simple or easy. It’s a tough combination of lots of features, with little of it being useful for the frontend.

- So we wrote a graph database to find out. 
  - We chose Triple Stores, one of the simplest kinds of graph databases. 
- If you haven’t tried one, here’s a quick intuition:
  - we need to be able to express a node with attributes. These sentences translate to lists
  - Then we want a way to describe references.these translate to lists just as well
- Put these lists in a table, and you have a triple store! Triple is the name of the list we’ve been writing
  - The first item is always an `id`, the second the `attribute`, and the third, the `value`. 
  - Turns out triples are all we need to express a graph. 
- once you’ve expressed a graph, you can traverse it. 
  - Triple stores have interesting query languages. 
  - Here’s Datalog

## 👥 [A Graph-Based Firebase | Hacker News_202208](https://news.ycombinator.com/item?id=32595895)

- I came to many similar conclusions completely independently, even attempted to build a typesafe in memory datalog in typescript.
  - I also came to the conclusion that just exposing datalog triples as a query language would never feel right and tried to expose a graphql like language that generated the datalog triples.
  - IMO react relay offers a great similar offering with their normalized cache. Relay has great DX too and can be totally type safe. To my knowledge datalog is way too dynamic for static analysis.

- I have built my own similar reactive in-memory triple store with typescripts type safety, but then I realized I still need transactions which are a bit of a pain, because transactions are bundling the otherwise separete triplets, so the atomic, independent logic of triplets and related effects breaks a bit. (I am sure it's solvable.)
  - The example code uses a `transact` function. But it really depends on what you mean by “transaction”. 
  - 👉🏻 We don’t use a triple store at Notion, but we do use an abstraction that ensures a collection of operations either all succeed or all fail. 
  - We don’t support “interactive” transaction, where you can read, modify, write as an atomic group. 
  - This just isn’t desirable in a multiplayer or offline system - in cases we need that kind of consistency we use a normal HTTP API which is online-only.
- As jitl points out, in multiplayer settings, what you need is some way to commit a series of transactions all-together or not at all. We support this.
  - In the case where you want to read the database inside your transaction, we take inspiration from Datomic. **Datomic runs all mutations in one high-memory box**. You can provide functions that run in that box. This way, you can guarantee that the reads inside your transaction have the latest value. There's a lot of UX to figure out there, and this would be something to try to avoid in an offline-available setting.

- Datalog isn't even really a query language. It's a class of query languages with a specific expressive power.
  - Whereas SQL is essentially conjunctive queries with non-stratified Negation, Datalog is recursive conjunctive queries with no or only stratified negation.
  - Datalog also has nothing to do with triples, they are two completely orthogonal concepts.

- tripletstore/datalog actually seems like a decent compromise between SQL and no-SQL that could actually work out! Awesome idea!

- Another product that does all this (relations, reactivity, offline, permissions, sync, etc…) really well, is Realm.
