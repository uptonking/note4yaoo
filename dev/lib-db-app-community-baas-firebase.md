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

- ## [Supabase – Realtime: Multiplayer Edition | Hacker News _202208](https://news.ycombinator.com/item?id=32510405)
- supabase ceo here
  - Realtime is built with Elixir and Phoenix
  - We've moved to a single, global cluster - We're using Phoenix. Tracker to globally distribute the Erlang PIDs of all of our Postgres connections. This guarantees there is only a single connection to each database.

- after thinking it through, I'm not clear on what Supabase is calling multiplayer.

- ## [Supabase (YC S20) – An open source Firebase alternative | Hacker News _202005](https://news.ycombinator.com/item?id=23319901)
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
