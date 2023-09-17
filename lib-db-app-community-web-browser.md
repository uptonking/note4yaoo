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
