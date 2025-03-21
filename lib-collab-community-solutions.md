---
title: lib-collab-community-solutions
tags: [collaboration, community, solutions]
created: 2024-01-28T09:04:55.644Z
modified: 2024-01-28T09:05:12.586Z
---

# lib-collab-community-solutions

# guide
- 协同的使用场景非常广泛
  - 包括多人操作
  - 包括在线面试的画板
# discuss-stars
- ## 

- ## 

- ## As modern web apps become more realtime and collaborative (Figma, Canva, Notion, Linear, etc.), systems and frameworks are being actively developed to support this need. 
- https://twitter.com/joygao/status/1784012670263550129
- On a high level, I find them bucketing into one of these approaches:
- 1) Via a modern database with built-in subscription features. 
  - Examples: - @supabase - @rethinkdb - @convex_dev - @fauna - @skiplabs 's SKDB (and of course our good ol' @Firebase )
- 2) Via a sync engine that hooks into existing database and subscribe for changes. 
  - Examples: - @figma 's Multiplayer - @linear 's sync engine - @asana 's Luna Framework - @prisma Pulse
  - sorry, r/Multiplayer/LiveGraph. Our multiplayer is more like a standalone sync engine, so perhaps it's worth separating this into 2a) and 2b).
- 3) Via a local-first storage, with option to sync to a managed or self-hosted database (or even client-side peer-to-peer sync, shoutout to Ditto). 
  - Examples: - @ditto - @ElectricSQL - @liveblocks - @replicache
- There's no clear answer in terms of approaches and is case-by-case depending on your need for offline functionalities, permissions, scalability, and team expertise.
- In general, as we are pushing more complexity to the edge/client (need for responsiveness, offline, scale, data ownership and security), I think 3) is currently the most actively developed space, and likely will continue to gain popularity over time.

# discuss-partykit
- ## 

- ## 

- ## PartyKit is just great for building super fast applications *even if you're not doing multiplayer*. _202401
- https://twitter.com/tomus_sherman/status/1742538924587634881
- How about we make the realtime part more pervasive? Change the industry instead of changing the messaging Even the most basic CRUD app could have improved UX with realtime, hard to implement right now even with something like PartyKit though
  - The framework needs to provide absurdly easy-to-use and reason about primitives. Makes me think of Meteor, which did this very thing with minimongo and op-log tailing.

# discuss-remote-control
- ## 

- ## 

- ## Cloudflare now provides clientless, browser-based support for the Remote Desktop Protocol (RDP)
- https://x.com/Cloudflare/status/1903076650952335699

# discuss
- ## 

- ## 

- ## [A simple way to build collaborative web apps | Hacker News _202108](https://news.ycombinator.com/item?id=28209736)
- I've worked in the space for a while (Fluid Framework) and there's a growing number of libraries addressing realtime collab. 
  - One of the key things that many folks miss is that building a collaborative app with real time coauthoring is tricky. Setting up a websocket and hoping for the best won't work. 
  - The libraries are also not functionally equivalent. Some use OT, some use CRDTs, some persist state, some are basically websocket wrappers, fairly different perf guarantees in both memory & latency etc. The very different capabilities make it complicated to evaluate all the tools at once.
- PouchDB+CouchDB work well out of the box with minimal fuss for open pieces you can just plug into this role. PouchDB handles the client's state persist and replication on the client, couchdb is the reliable cloud service you can replicate to. 
  - Meteor, at least their pre-apollo stack had realtime collab type features with their mini-mongo client and oplog tailing.
- You could build this with couchdb multi master regional servers and pouchdb on the client and have full consistency with the replication both to clients and servers as well as conflict resolution (in case of collision) done for you.

- We implemented all that manually, more or less in swift (and sqlite), then react+redux, and on the back end - postgres and python+flask. Works flawlessly so far. We do have the same setup more or less, with listeners triggering UI updates and push messages signalling the clients to fetch data from the server. Then, on the server, we have two dbs -> one where we store each update or create message, in a postgres-based queue, and another one, in a normalised format which we use for login (it's way faster than replaying all messages from the queue). 
  - We gave up on the websocket part and implemented basic polling, because they were not supported by App Engine at the time (things might have moved on since then, which is a couple of years ago). Yet, for a note/todo/habit tracking app, it simply doesn't need to be real-time from our experience

- Thanks for mentioning Meteor, which also impressed me a lot when it first came out. I think it didn't take off because it tries to do too much (frontend + backend + db). And one smart move by Replicache is that it tries to integrate nicely with the rest of your stack.

- Replicache's creator Aaron has a pretty good Twitter thread explaining the difference among Replicache, WebSocket and (classic) CRDTs. I will summarize briefly here:
  - WebSocket (and Phoenix Channel) is just a communication method. To maintain consistency and resolve conflict, you need something like Replicache.
  - CRDTs are more suitable for p2p scenario while Replicache works better for client-server apps.
  - Phoenix's Presence is built with CRDT but it's just a single feature, not a general CRDT toolkit.

- At FastComments we store every change as an event, which can either be pushed or polled. Clients subscribe, and poll on reconnect.
  - The integrations work kind of like DB slave replication. They do an initial sync and then maintain state via the event stream.
