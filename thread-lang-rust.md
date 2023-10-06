---
title: thread-lang-rust
tags: [lang, rust, thread]
created: 2023-10-06T16:26:26.532Z
modified: 2023-10-06T16:26:57.557Z
---

# thread-lang-rust

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## tokio IS "thread-per-core" - the controversy in the Rust community is about a tradeoff between work-stealing and share-nothing
- https://twitter.com/withoutboats/status/1710279468206485941
  - [Thread-per-core - Without boats, dreams dry up](https://without.boats/blog/thread-per-core/)
- I have never implemented work-stealing approach so cannot really comment on its effectiveness. My paper was investigating the impact of thread-per-core (with partitioning) on tail latency in comparison to traditional share-everything model. As you rightly point out in your post, you cannot draw any conclusions from my findings about partitioning vs. work stealing.
- I’ve always referred to thread-per-core with work-stealing as thread-per-core-until-things-get-tough. It’s a slippery slope from work-stealing to not pinning threads to CPUs but yeah usually the hot partition issue is the motivator for WS
