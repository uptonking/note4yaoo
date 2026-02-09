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

- ## Lamport's Time, Clocks, and the Ordering of Events in a Distributed System is one of the most important systems papers of all time.
- https://x.com/jamesacowling/status/2020203010119594134
It formalizes something kinda obvious: Within a timeline everything happens in an order defined by events it observed (I threw a ball, you caught it), but on two separate timelines, like two people offline on their laptops, two events *aren't* ordered with respect to each other.

It's impossible to merge these timelines together in the general case, no matter how accurate clocks are. It's like those movies where two people go down different timelines: you can't merge those together no matter how good their watches are.

To build local sync you have to accept one of three things:
1. Sometimes data loss will occur, e.g., last-writer wins.
2. There's a specific lossy or domain-specific API you can use, e.g., operational-transforms, CRDTs, or client-side merge logic.
3. Different people see different timelines forever, which is fine for some applications.

A lot of the interesting work in local-first happens around option #2. How to limit operations users can perform to those that can be acceptably merged together or where it's ok to have certain kinds of data loss.

- OT&CRDTs' most difficult (& 1st) algorithms solve a narrow problem: in a text doc, if my "insert A @ index 6" op reaches a node before your "insert B @ index 10" op, the node needs to instead insert B @ index 11. This isn't a real semantic conflict, just a flaw w/ using indexes.

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
