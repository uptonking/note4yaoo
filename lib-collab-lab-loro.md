---
title: lib-collab-lab-loro
tags: [collaboration, crdt, loro]
created: 2024-01-06T15:36:32.941Z
modified: 2024-01-06T15:37:08.031Z
---

# lib-collab-lab-loro

# guide

# dev

# discuss-stars

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [Loro: Reimagine state management with CRDTs | Hacker News_202311](https://news.ycombinator.com/item?id=38248900)
- The demo code for Loro looks very easy to use, I love how they infer a CRDT from an example plain JS object. I’ve played with a Zod schema <-> Yjs CRDT translator and found it kinda annoying to maintain. 
  - However this looks so easy I worry about apps building with too little thought about long term data modeling. 
  - Migrations on CRDTs are challenging, so it’s important to “get it right” at the beginning. 
  - I’m curious how this design works with longer term, more complex CRDT apps.
- The code in the blog is from Vue Pinia, a state management library, and not from Loro. It serves as an example demonstrating that CRDTs can be modeled similarly. Thus, you might expect to use Loro in a similar way.
  - Indeed, schema migration is challenging. There is a lot to explore, both in reducing the need for migration and in ensuring a smooth transition when it's required. We plan to tackle this issue in the future.
- Any tips or dos/don'ts you could share for how to "get it right" at the beginning? 
  - I don’t have anything better for you than “be careful” and “prototype a lot”. Adding new fields is fine, changing the meaning or type of existing fields is annoying.
  - 🧐 It’s more challenging because you need to accept updates in format v1 indefinitely even after you apply the v1->v2 migration, which makes it more like maintaining an API with backwards compatibility than the usual SQL migration pattern.

- I wonder if this is something that can be used for versioning database columns / fields.

- We've been using https://github.com/electric-sql/electric for real-time sync for the past month or so and it's been great. Rather than make you think about CRDTs explicitly, Electric syncs an in-browser sqlite db (WASM powered) with a central postgres instance. As a developer, you get local-first performance and real-time sync between users. And it's actually faster to ship an application without writing any APIs and just using the database directly. Only downside is Electric is immature and we often run into bugs, but as a startup we're willing to deal with it in exchange for shipping faster.
