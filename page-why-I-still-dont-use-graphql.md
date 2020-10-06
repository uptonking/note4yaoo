---
title: page-why-I-still-dont-use-graphql
tags: [api, page]
created: '2020-08-06T08:48:07.770Z'
modified: '2020-08-17T07:29:23.887Z'
---

# page-why-I-still-dont-use-graphql

- Some thoughts I've gathered over the years on what I think about GraphQL. 
  - All of this is subject to change of course, and some of it may be "hot-take"-ish, 
  - but at the end of the day, I've made decisions regarding GraphQL with my customers, users, and fellow developers in mind and with the mantra that if it ultimately doesn't make a big difference for any of those people and justify the work that it requires, it's not the best investment of time. 
  - It's more important to please your users, ship products in a timely manner, and use tools that keep processes simple and familiar.

- A majority of the world still runs on REST and probably will for a while.
- The challenges of larger companies that originally benefitted from GQL are not everyones challenges and they likely never will be.
- I don't want to require my API users to have knowledge of GQL.
- Strongly typed APIs are good, but I don't particularly enjoy the tools in the ecosystem right now to use them via GQL
- GraphQL seems to have been born out of the requirement of "deep" querying of assets via graph-like relationships
- Deep querying without field masking presents a problem with bandwidth and overfetching, thus GraphQL forced field masking on you. You cannot `select *` so to speak.
- Deep querying with field masking can end up producing a massive amount of partially-saturated entities/objects from a server.
- You can implement field masking and relational graph-style querying via REST *if you need it*. I rarely have.
- Because of this "fragmentation", GQL uses query fragments as part of it's "benefits"
- Fragments to some extent assume that any clients or consumers of the API have a reliable way of keeping all of these fragments up to date, but doesn't (to my knowledge) offer anything official to do this.
- Tools like Apollo approach this with semi-automated normalized caching (based on the schema) and stitch together fragments and keep entities/fragments up to date as different queries are consumed on the client. This seems extremely complex for most use cases.
- Relay is another tool that people swear by, but seems to have a high level of buy-in/commitment. Not only do you have to use GQL, but you have to do things in the Relay way.
- At the end of the day, I would wager that a vast majority of apps won't benefit enough from GQL to justify the costs (opinionated and relatively proprietary syntax, specialized tools/libraries for interacting with it) that it currently requires.
- If you have a massively public API that needs to be generally queryable for general purpose things, then you may want GQL and it will likely be worth it. I think of companies like Facebook and Github here, or essentially any company that needs to have some type of ecosystem built upon it.
- The benefit that is the most alluring of GQL is the type safety, but that is not the only way to have a type safe API. You can do this with other tools like `buf` , JSON-schema, and typescript. I think I would go after these first.
