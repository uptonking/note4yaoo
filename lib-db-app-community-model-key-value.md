---
title: lib-db-app-community-model-key-value
tags: [community, database, key-value]
created: 2023-10-26T15:02:34.035Z
modified: 2023-10-26T15:02:47.068Z
---

# lib-db-app-community-model-key-value

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 🔥 [What's the big deal about embedded key-value databases? | Hacker News_202208](https://news.ycombinator.com/item?id=32566851)
- 
- 

- ## [FoundationDB's Lesson: A Fast Key-Value Store Is Not Enough | Hacker News_201504](https://news.ycombinator.com/item?id=9306297)
- The underlying organization of a database is not about what can be expressed in theory, it is about what can be expressed efficiently. 
  - Not only is there a very rich set of data structure designs that can be used with varying tradeoffs, but most sophisticated databases use an ecosystem of different, tightly interwoven data structures that smooth over the sharp corners that any single data structure has.
- Efficient expressiveness follows from the relationships directly preserved in the organization. Generally from least-to-most expressive you have:
  - cardinality preserving (hash tables, most KV stores)
  - order preserving (LSM, btree, skiplist, space-filling curves*)
  - space preserving (space decomposition e.g. quad-tree, a zoo of exotics)
- SQL was designed for databases built on order-preserving structures. While you can implement it on a KV store, it will never be as efficient as a database organized in the more expressive organization that SQL assumes.
- KV stores are popular because they are relatively simple to design and implement, not because they are expressive. It is an architectural impedance(阻抗) mismatch to add query functionality that tacitly assumes a more expressive organization. It will never perform well against a database actually organized for the expressiveness of the query layer.
- Any database can only do a few things really well. It is inherent in the tradeoffs. You can add mediocre support for a laundry list of other "good enough" capabilities but you never want to market and position your product around those mediocre capabilities.

- In this case though FoundationDB's KV store was order preserving. The API supported (& efficiently implemented) ranged reads, not just individual get's.
  - Implementing layered architectures always looks good 'on paper' but the details often throw up performance issues that are hard to deal with without punching some holes in the abstractions.

- ## 🔥 [LevelDB: a fast and lightweight key/value database library | Hacker News_201105](https://news.ycombinator.com/item?id=2526032)
- 
- 
- 
