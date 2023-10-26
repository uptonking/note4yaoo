---
title: lib-db-scuttlebutt-community
tags: [community, scuttlebutt]
created: 2023-09-07T15:56:31.007Z
modified: 2023-09-07T15:56:52.778Z
---

# lib-db-scuttlebutt-community

# guide

# discuss-sync
- ## 

- ## 

- ## [👉🏻 DAG sync_202303](https://github.com/ssbc/ssb2-discussion-forum/issues/10)
  - Sliced replication is a MUST in SSB2, so we can forget the past.
  - Sliced replication: replicating a `[lowerBound, upperBound]` slice/range of a certain feed
  - Partial replication: an abstract umbrella concept for "not replicating everything"
  - Subset replication: fetching a subset of messages from a feed, in random order, based on a certain query

- I considered the idea of having **"synchronization points"**, other names for this are "consensus points", or "anchors".
  - An anchor is a msg on the feed, which merges several previouses, and happens with a rare-enough frequency. Let's say the frequency is once per week. Or, once every 100 messages. The anchor message would have a special field "anchor": true.
  - The problem with this idea is if Bob has (for some reason) a forked anchor, say 9 ⚓ versus 9' ⚓. What do we do with forked anchors?

- You get it. This is exactly where I wanted to go with the Feed Bootstrap Message. Let's call is Anchor Message.

- I came here to drop this important link from Aljoscha on tangle sync (aka "set reconciliation") and precursor AljoschaMeyer/set-reconciliation.
  - I'll also drop a link to the earthstar implementation of aljoscha's set replication: earthstar-project/range-reconcile

- https://github.com/staltz/dagsync
  - I started writing a dagsync proof of concept
# discuss
- ## 

- ## 

- ## 

- ## 

- ## I'm super excited about the new earthstar project.
- https://twitter.com/rabble/status/1265795078263435265
  - It's a decentralized open source database and protocol. 
  - Think Firebase meets Scuttlebutt.
- The big difference between SSB (and earthstar, pigeon protocol, etc) is that they're based around the idea of being social with multiple people writing to what is read as a combined local social db

- ## 🚀🔥 [Scuttlebot: Peer-to-peer database, identity provider, and messaging system | Hacker News_202004](https://news.ycombinator.com/item?id=22909984)
- 
- 
- 
