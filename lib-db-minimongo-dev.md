---
title: lib-db-minimongo-dev
tags: [database, minimongo, mongodb]
created: 2022-12-02T11:12:05.223Z
modified: 2022-12-02T11:12:29.905Z
---

# lib-db-minimongo-dev

# guide

# discuss
- ## 

- ## 

- ## 

- ## [Use IndexedDB as alternative storage for minimongo · Issue #407 · meteor/meteor-feature-requests](https://github.com/meteor/meteor-feature-requests/issues/407)
- Using IndexedDB as a data-storage for minimongo would give us several advantages, I think, e.g. of automatically having indexes built in
- One major downside I see so far is that many of the calls are asynchronous (based on callbacks) and could therefore only be introduced on the client if we would switch to a promise-based interface for database-calls.
- One issue with IndexedDB is that data has a same origin policy, so if you have multiple tabs open all tabs can see data from all other tabs. This means you have to query Minimongo for exactly what you want instead of just assuming that what's there is only what you're subscribed to. (This is already good practice.)

- ## [Is GroundDB the best for offline storage? - help - Meteor forums_202109](https://forums.meteor.com/t/is-grounddb-the-best-for-offline-storage/56654)
- I found that the internal API in LocalCollection that ground:db uses switched from an object to a Map sometime around Meteor 2.4.
  - I did a from-the-ground-up (pun unintended) rewrite, which I’m calling GroundedCollection. 
  - I switched to Typescript, added the ability to specify compression/decompression functions for writes/reads to IndexedDB, and switched from localforage to Dexie, but otherwise tried to keep the API similar.
  - As a bonus, Dexie allowed me to use bulk reads/writes, which decreased load times by an enormous amount
  - https://gist.github.com/banjerluke/554cb2274c4f55c2254288aa243994ed

- 
- 
- 

- ## why Minimongo in Meteor don’t support indexeddb or websql like Minimongo official project?_202101
- https://forums.meteor.com/t/minimongo-and-store/54877
- What would you like to do offline?
  - Minimongo was designed for something different, it is a mirror of a batch of data from Mongo. Minimongo is almost Mongo.
  - Where the whole offline concept fails is when you want to offline-edit a note which is not on your phone. Or if you want to book a ticket offline, paginate some posts, etc. There are so many case that don’t work in any app not only Meteor.
  - Offline we can both generate documents like in a chat.
  - However, when we both have the same document and we both want to edit it offline… if online, there is conflict
  - What I am saying here with this story is that you can very well do a lot of offline, away from Minimongo, using Methods and writing to a local DB (I prefer RealmDB because it is … possibly the best mobile JS DB). It is not that you cannot and it is not that it can be built natively into Meteor (my opinion). This is subject to application design for each an every individual app.

- Is to difficult ? is not right to do because is not suitable for Meteor ?
  - One major downside I see so far is that many of the calls are asynchronous (based on callbacks) and could therefore only be introduced on the client if we would switch to a promise-based interface for database-calls.
  - Such a change would force virtually everyone to make a lot of changes to their projects.
- I tested a few of these offline-minimongo packages in the past (at least 3 years back) and I think ground:db was the one that worked for us the most.
