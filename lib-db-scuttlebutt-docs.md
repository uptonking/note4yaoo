---
title: lib-db-scuttlebutt-docs
tags: [docs, scuttlebutt]
created: 2023-09-07T15:46:28.729Z
modified: 2023-09-07T15:56:25.565Z
---

# lib-db-scuttlebutt-docs

# guide

- [Scuttlebutt · GitBook](https://handbook.scuttlebutt.nz/)
# blogs
- [Comparing Peer to Peer Protocols_202203](https://blog.mauve.moe/posts/protocol-comparisons)
  -  BitTorrent, IPFS, Secure Scuttlebutt (SSB) and Hypercore

- [Nostr v SSB](https://mattlorentz.com/weblog/2023/01/18/nostr-v-ssb.html)
  - [How is this different than Secure Scuttlebutt? I remember following that for a w... | Hacker News](https://news.ycombinator.com/item?id=35691461)
  - After using Nostr a bit, I don't think there's a huge difference between SSB and it except that Nostr has no blob sync and they abandoned append-only logs and use different signing key cryptography.
  - Scuttlebutt just suffers from an inaccessible implementation at the moment, but there is a team coming together to make a working implementation again.
# overview

# docs

## [Introduction to Using ssb-server](https://handbook.scuttlebutt.nz/guides/ssb-server/tutorial)

- ssb-server is a peer-to-peer log store. 
  - Its data model is similar to that of Apache Kafka, and it's part of a pattern that's now referred to as the Kappa Architecture.
- Kappa Architecture is a software architecture pattern. 
  - Rather than using a relational DB like SQL or a key-value store like Cassandra, the canonical data store in a Kappa Architecture system is an append-only immutable log. 
  - From the log, data is streamed through a computational system and fed into auxiliary stores for serving.

- 
- 
- 
- 
