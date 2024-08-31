---
title: lib-collab-crdt-community-hlc
tags: [collaboration, community, crdt, hybrid-logical-clock]
created: 2023-02-07T09:12:11.909Z
modified: 2023-02-07T09:12:37.761Z
---

# lib-collab-crdt-community-hlc

# guide

# discuss
- ## 

- ## 

- ## 

- ## guests say that they don't need CRDTs b/c they're "too complex" but then go on to explain their custom solution which is... a CRDT
- https://twitter.com/tantaman/status/1691083925060227075
- I've been guilty of similar things in the past. "That paper looks long. I'll just implement my idea." Some time later: "Oh.. I just implemented a worse version of what was in that paper"
- I've seen data synchronization code in a real app that looked exactly like a CRDT merge function, but the authors never heard or know anything about the CRDT literature and lattice algebra. It was much more complex than it should have been though.

- ## 🦀 [What do you recommend for conflict-free replicated data type (CRDT) support in Rust? : rust_202301](https://www.reddit.com/r/rust/comments/1064f9s/what_do_you_recommend_for_conflictfree_replicated/)

- May or may not be useful for you, you may find the hybrid logical clock approach more convenient than trying to maintain and manage a vector clock etc...
- That's the exact same talk I watched too! It's what started me down this path of offline-first apps. And I'm assuming if the timestamps produced by the client and the ones produced by the server are not compatible (due to a mistake in the code, or implementation language, or whatever) then the CRDT would be basically unusable right? Since the timestamps must be compatible in order to be compared.
  - Yes, although there are a few things you could do to prevent the case of an implementation being incorrect:
  - You make some compatibility methods which extracts the raw information out and back into an HLC.
  - You use the string format for communicating rather than the bit packed u64 which has a common way of serializing and deserializing their information so they're the same.
  - u should provide 100% test coverage including testing that the clock accuracies 

- Another Rust-based offline-first CRDT framework is Holochain. It frequently gets mistaken for blockchain due to the name and its proximity to that space, but it is not a blockchain in any way
