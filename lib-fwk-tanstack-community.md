---
title: lib-fwk-tanstack-community
tags: [community, frontend, router, tanstack]
created: 2025-12-16T06:24:30.759Z
modified: 2025-12-16T06:25:32.663Z
---

# lib-fwk-tanstack-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## 
# discuss-tanstack-db
- ## 

- ## 

- ## 

- ## Why is @tan_stack DB a database?
- https://x.com/samwillis/status/1996216487204315412
  - It's both something new, but also very much based on the architecture of any traditional database.
  - All the same parts are there, and data flows through it in the same way.
  - Only difference is it can load data from anywhere...

- what's your answer to the split-brain problem à la CAP theorem?
  - The remote database is the single source of truth. Dataflow is unidirectional, with a thin optimistic layer applied locally that is removed on confirmed writes being seen back on the sync path.

- Will it ever support FTS
  - The index system is pluggable, so all possible. We're working to make custom query operators an options too.
  - I have my eye on https://github.com/Michael-JB/bm25 in WASM as way to do FTS with DB...

- i'm a huge fan of this project so this is coming from a place of love but when i think database i think this part. the rest (what ts db does) is super important and most of what the application touches though, so others may not have the same idea
  - 🛢️👀 Yep, and I get it. There is enormous call for local persistence in DB. It's on the roadmap. That for many will be when we can finally convince them of the name. 
  - I like to think of DB a little like Neon, separate storage and compute. We've been building the concept part.
  - In-memory will always be the default, with persistence as an opt-in.
# discuss
- ## 

- ## 

- ## 

- ## 
