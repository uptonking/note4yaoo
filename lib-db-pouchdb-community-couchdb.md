---
title: lib-db-pouchdb-community-couchdb
tags: [community, couchdb, pouchdb]
created: 2023-10-07T17:28:56.496Z
modified: 2023-10-07T17:29:16.871Z
---

# lib-db-pouchdb-community-couchdb

# guide

# discuss-stars
- ## 

- ## 🚀 [Realm Mobile Platform – Realtime Sync Plus Fully Open Source Database | Hacker News_201609](https://news.ycombinator.com/item?id=12589426)
- So this is like alternative to Firebase? How different is their offering?
  - Realm is self-hosted compared to Firebase which is an MBass.
  - Native objects all the way down vs. a JSON structure

- Hi, former Apache CouchDB guy, former Cloudant employee, and former Realm employee here… I (still) love CouchDB but at the end of the day I think its sync is a better fit for server-to-server or web client-to-server use-cases, not mobile-to-server.
  - There’s tons of stuff CouchDB sync doesn’t support that end up being a huge problem with mobile apps
  - Here are the top 3 things Realm adds in my opinion: great client-side performance, native models that are extremely easy to use, and conflict-free sync (not conflict resolution!). 
  - With my own eyes I’ve seen a generation of developers try CouchDB for mobile apps and then abandon it because of the limitation of its approach. I think this is the first general-case true sync (à la Google Docs) for mobile, and I hope it will continue to spur more iterations & innovation in other open-source projects as well.
- As I understand PouchDB is performant, uses JSON (pretty much the definition of "Native Models"), and allows server-arbitrated conflict resolution with stored revisions, making the simplest conflict resolution "last-in-wins" with user UI for "undo" (or any JS-object merge library).
  - I think you're misunderstanding what "Native Models" means in the context of iOS work. Saying that a database uses JSON immediately, to many ios devs, recalls years of writing very fragile json serialization code. Looking through CouchDB's iOS example apps confirms that yes, basically everything that isn't a string or int has to be serialized into JSON. That's a pretty enormous annoyance, and incorporates a lot of additional cognitive overhead when dealing with data that Realm simply handles properly for iOS from the beginning.

- ## 🆚️ [Comparison: PouchDB vs. NeDB_201507](https://github.com/pouchdb/pouchdb/issues/4031)
- I dont have experience with NeDB so only making a comparison by reading the README, but from a brief look it looks like the main differences are PouchDB does synchronisation between the server and the browser, and that PouchDB was designed with the browser in mind. 

- **PouchDB will definitely have overhead compared to the other databases, because it stores everything in a "revision" model where the history of every document is preserved**. (Think of it as git vs just overwriting files.) Hence it tends to have overhead, even for gets/puts.

- Personally, NeDB has become my go-to for most projects. The sole exception I've, thus far, had was an app that had 2.4 million rows of data. NeDB worked, but it created significant lag so I switched to SQLite and made calls to a backend handler for DB interaction.
  - I considered PouchDB, and it definitely looks like a better alternative for very large datasets ... but I think I'd still go with SQLite in those cases. For most things, according to the benchmarks posted by @user8614, NeDB appears to perform as well or better.
- I work on PouchDB, in terms of those points:
  - "great client-side performance": PouchDB is more than fast enough for most use cases, its just a wrapper over indexedDB. (there are areas we can improve, particularly performance of map reduce / mango queries).
  - "native models that are extremely easy to use": Not sure what that means, PouchDB and CouchDB use json, its native and easy to use in JavaScript
  - "conflict-free sync (not conflict resolution!)": Certainly going to have to take a look at this, any conflict free sync protocol I have seen put a lot of limitations on how data within your application is structured but conflict resolution certainly is something that can be improved within Pouch / Couch.
  - I do think there is a bunch we can (and are) improving in PouchDB and its great to see alternatives, will be looking into this further now. But I certainly do not agree that (C|P)ouchDB are not suited for mobile <-> web sync, thats the primary use case I work on Pouch for.
- In general, I tend to be skeptical of systems that hinge(依赖；装上铰链) on last-write-wins, but LWW is definitely a model that works in a lot of cases where you're not too concerned about the possibility of losing data, and it's also a simpler mental model for the app developer.
- 👉🏻 Realms approach to conflict resolution is very different from what you see in products like Couch.
  - Realm is an _object_ database, so in contrast to document databases where conflict resolution happens very coarse grained at the document level, in Realm it happens at the object level (and actually all the way down into individual properties).
  - This essentially means that the entire object graph is treated as one big CRDT, transparently handling conflict across individual objects, properties and relations.
  - When talking about ordering by time, both in the context of LWW and insertions in lists, we are talking about **vector clock time**, not necessarily device time (or though that is taken into account as well).
- LWW is a tradeoff. You'll be better off selling it as an automated-resolution option on top of manual resolution, instead of an innovation over manual resolution. (MV registers are a CRDT as well!)
- Adam from Realm. Our approach differs in building off our object database. We couple this with low-latency sync that only transmits changes and deterministic conflict resolution, making collaborative experiences really easy to build
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# discuss-couchdb/couchbase
- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
