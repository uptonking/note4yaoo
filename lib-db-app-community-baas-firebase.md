---
title: lib-db-app-community-baas-firebase
tags: [baas, backend, community, database, firebase]
created: 2024-01-06T07:02:22.857Z
modified: 2024-01-06T07:02:42.007Z
---

# lib-db-app-community-baas-firebase

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-supabase
- ## 

- ## 

- ## 

- ## [Supabase – Realtime: Multiplayer Edition | Hacker News_202208](https://news.ycombinator.com/item?id=32510405)
- supabase ceo here
  - Realtime is built with Elixir and Phoenix
  - We've moved to a single, global cluster - We're using Phoenix. Tracker to globally distribute the Erlang PIDs of all of our Postgres connections. This guarantees there is only a single connection to each database.

- For a collaborative text editor, you need two things: (1) a full-stack system that maintains a running list of data events such that everyone sees everyone else's events eventually, and (2) frontend code that adapts that set of events, along with your text cursor position and current changes, into a cohesive view of a document at any moment in time.
  - Supabase and Replicache can absolutely help with (1). But for (2) you will need OT or CRDT.

- Anyone from Supabase here, do you have any plans to build in support for CRDT toolkits such as Yjs or AutoMerge for these features?
  - It's definitely something we'll support. We'll extend this service so that it works well with WebRTC, and we have a few ideas for making it easy for development.

- > difference between Supabase open-source and the paid versions
  - Yes, you can self host and everything is open source (including the Dashboard). Everything is either MIT, Apache2, or PostgreSQL licensed.
  - On the paid version we handle some of additional database management (like daily backups, PITR, etc). These are technically available for self-hosting too, because the database is just a Postgres database, but I point it out here because it's not something you'll get "out of the box" from the Docker setup.
  - 💰 Our philosophy with open source is "offer everything" and then charge for usage. There aren't any features completely gated. Our Enterprise plan just adds additional SLAs and support packages for our cloud platform.

- What happens over an unreliable network connection such as mobile?
  - Client will seek to continuously reconnect to the WebSocket when there's a connection issue and server must receive at least one heartbeat in a 60 second window; otherwise it will clean up the WebSocket connection.
  - We built Supabase Realtime on top of Phoenix Channel, and along with our clients, handles unreliable network connections gracefully, including on mobile.

- ## [Supabase (YC S20) – An open source Firebase alternative | Hacker News_202005](https://news.ycombinator.com/item?id=23319901)
- As a Firebase user, I find it invaluable. Their free plan and limits are very generous. The fact they offer not only a database, but authentication, hosting and perhaps one of their biggest features besides authentication: Firebase Functions. 

- I've been using Firebase since 2016 in production and after all these years I find the service quite lacking.
  - Both databases are super limited and put all the burden of work to the client(s) for anything beyond very simple queries.
  - The functions have some of the worst cold starts I've experienced. Until very recently the dev experience was terrible but Firebase local dev was released a couple of days ago so this should be solved.

- > We want to nail the auth and we're looking at leveraging Postgres' native Row Level Security. This is a tricky task to "generalize" for all businesses but we have some good ideas 

- In my mind, Firebase is a very flexible CMS with sane defaults.
# discuss
- ## 

- ## 

- ## [Ask HN: The state of Firebase alternatives in 2020? | Hacker News_202010](https://news.ycombinator.com/item?id=24843664)
- There really isn’t a competitor. 
  - Supabase is trying to combine OSS tooling into a somewhat similar offering but it’s not nearly as feature rich as Firebase. 
  - That having been said, most people use Firebase for real time DB and auth, and Supabase supports that now. 
  - It doesn’t, however, support offline use cases, or any of the advanced functionality of firebase.

- Pouch and couch solve the offline data scenario and live replication, but no auth story and the mapping of users to data is problematic (unless you build a proxy layer, there’s not an easy way to have some data be public, some private, and some shared).

- Realm is paid these days, I believe, and it solves the data replication, but again, no auth.

- Is there/will there be multi-tenant support for auth in Supabase?
  - We use Postgres Row Level (RLS) security, so you can do some very advanced rules. For example, one of our team built a social network with PG and RLS
  - RLS is flexible enough to cover multi-tenant scenarios, though it's up to you how you structure your schema to make it work.

- 🆚️ How does Parse compare to something like Firebase or Supabase?
- I'm not sure about Supabase, but compared to Firebase...
  - Pros: Free, though you self-pay for server and MongoDB. Continuously improving. Much, much easier to set up for CRUD - I can get one up within half an hour. Web support seems better. Handles relations very well, whether it's one to one, many to many. God forbid you want to upload images direct to MongoDB, it handles that well. Integrates into some email adapters as well. The dashboard that accesses the DB is sexy and powerful, and has improved a lot since Facebook abandoned Parse.
  - Cons: Self-hosted. Poor support. And won't land you any full yome jobs. Database is not real time unlike Firebase. Analytics and bug tracking is probably worse.
  - Similar: Cloud hosted functions, authentication. I don't remember if Firebase does sessions, but it handles that too, on web and apps.

- PouchDB is amazing. You can use their server side components and scale into couchdb later.
