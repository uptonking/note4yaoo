---
title: lang-rust-community-concurrency
tags: [community, concurrency, rust]
created: 2023-08-28T04:42:10.075Z
modified: 2023-08-28T04:43:32.352Z
---

# lang-rust-community-concurrency

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## tokio IS "thread-per-core" - the controversy in the Rust community is about a tradeoff between work-stealing and share-nothing
- https://twitter.com/withoutboats/status/1710279468206485941
  - [Thread-per-core - Without boats, dreams dry up](https://without.boats/blog/thread-per-core/)
- I have never implemented work-stealing approach so cannot really comment on its effectiveness. My paper was investigating the impact of thread-per-core (with partitioning) on tail latency in comparison to traditional share-everything model. As you rightly point out in your post, you cannot draw any conclusions from my findings about partitioning vs. work stealing.
- I’ve always referred to thread-per-core with work-stealing as thread-per-core-until-things-get-tough. It’s a slippery slope from work-stealing to not pinning threads to CPUs but yeah usually the hot partition issue is the motivator for WS
