---
title: lib-db-hypercore-community
tags: [community, hypercore]
created: 2023-09-07T15:58:12.036Z
modified: 2023-09-07T15:58:27.967Z
---

# lib-db-hypercore-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## The real-time syncing immutable, append-only log that hypercore provides can also be accessed randomly, 
- https://news.ycombinator.com/item?id=15468295
  - allowing for lots of cool parallel/distributed log processing architectures (**Kappa architecture**), similar to Kafka (which is also based on immutable, append-only logs). 
  - We have just focused on syncing a filesystem at first because we had a strong use case there, but **you could totally build a CRDT on top of an append only log**.

- ## Hyperbee is just one writter. If you want "multiple writters" (which is multiple hypercores combined into one) then you can use autobase
- https://discord.com/channels/985129863348371516/985129863348371519/1034609699552776222
  - use the GitHub branch directly (npm i hypercore-protocol/autobase), because the npm package is outdated
- is autobase supposed to replace a regular database for hypercore?
  - Not necessarily, because you could use hyperbee without autobase
