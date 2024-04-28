---
title: lib-collab-community-solutions
tags: [collaboration, community, solutions]
created: 2024-01-28T09:04:55.644Z
modified: 2024-01-28T09:05:12.586Z
---

# lib-collab-community-solutions

# guide

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

# discuss
- ## 

- ## 

- ## 
