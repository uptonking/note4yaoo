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
# discuss-tanstack-router
- ## 

- ## 

- ## With TanStack Router and Start gaining popularity, React Query may become optional.
- https://x.com/YBenlemlih/status/2002846358609256932
  - You can now load data directly in the router using a loader function. So you get built-in loading and error states.
  - So should you load the data in React Query or TanStack Router?
  - Bonus: you can combine both to get the best of both words.
  - Using loaders also unlocks prefetching, i.e. faster navigation/loading times.
- In Start you also unlock isomorphic features: 
  - the page is initially rendered on server (instant UI thank to ssr) and SPA-like smooth navigation (client side subsequent navigation)
  - better SEO: custom head fields based on the loader result 

- query still gives you a whole suite of tools for mutations, revalidation, and optimistic updates. router loaders are great for initial fetches, but not a full replacement
  - yep, I just use query in loader for initial fetch, then can do extra stuff with it if needed in actual function

- use the two to get the best result. So loader function fetches the data while loading the page on server side, then I pass is as initialValue to TanstackQuery to handle refresh, invalidating, etc on the client side.

- How will you handle the case when you need same data over different routes? route loaders are good for some specific cases but react query is good for almost all the cases.

- Same was for server components and loaders in remix/react router. But if you need data fetching on client, react query is still the way to go
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
