---
title: lib-collab-automerge-community
tags: [automerge, collaboration, community, crdt]
created: 2023-03-07T04:09:57.751Z
modified: 2023-09-01T10:13:59.044Z
---

# lib-collab-automerge-community

# guide

# discuss-not-yet
- ## 

- ## [wishlist: File format v3](https://github.com/automerge/automerge/issues/588)
- Use a tighter leb encoding
- Unify definition of change time
- Making change hashes more robust
- Removing the compressed change chunk option
- Define limits on op/change counts

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Granular merging of nested objects](https://github.com/automerge/automerge/issues/549)
- What you have run into here is what we have been referring to as the "initial data problem". The problem is that individual objects within automerge have their own identity
  - 👉🏻 The solution to this problem for now is to create a skeleton document which contains the top level keys you know you need and ship it with your app.

- ## [Speed Comparisons Between Automerge Implementations](https://github.com/automerge/automerge/issues/41)

- ## A hypercore conflates(合并，混合) several things in hypermerge
- https://twitter.com/pvh/status/1219777305632894976
  - it's not just an append only log, it's a sharable unit, a verifiable signature, and a Merkle tree.
  - I am absolutely ready to move off hypercore as storage if you have the gumption to propose an alternative
- The nice thing about IPFS is that because it's content addressed, you don't need a lot of the metadata hypercores include, so for static content I think it would make a ton of sense. There are substantial privacy downsides if you advertise all your content to the world though.

- ## We run automerge over hypercore + hyperswarm and call it hypermerge. Works reasonably well.
- https://twitter.com/pvh/status/1246144720474005505

- ## I'm exploring ways to put docs synced by hypermerge into a query layer to give "realtime" updates of views into my data.  (give me all the docs that contain these words/tags)
- https://twitter.com/pvh/status/1259375354952572928
  - Are there technologies you recommend checking out?
- streaming queries/subscriptions are definitely what you're talking about. this was a key painpoint in building pushpin, since things like FTS were crazy slow for the lack of it. 
  - @conradirwin pointed me to baobab as an inspiration but i haven't tried it.
- the way path here is uncharted (welcome to the frontier) but i suspect GIN + subscriptions + "derived documents/materialized views" are probably all elements of the path forward
  - also, if you haven't already seen it, there's a ton of interesting documentation about how the Postgres internals work for GIN which might help guide a design, though you may also want to look at things like tf-idf to improve relevance.

- ## We explored some of this in hypermerge, but it's tricky to do on hypercore, or was at the time.
- https://twitter.com/pvh/status/1544890917668106240
  - The hard parts, roughly, were deciding what the names should be and keeping track of all the network connections and file handles. 
  - We used a private set intersection algorithm for deciding the list of mutual feeds to synchronize.

- ## hypermerge used to provide a p2p gateway for automerge but was forsaken because it uses an outdated automerge version
- https://automerge.slack.com/archives/C61RJCM9S/p1687580301244489
  - I also noticed that it had a couple shortcomings, wondering if those would be solved with the current versions of both libraries.
- I'd be interested in seeing an automerge-repo-network-hyperswarm but I don't have any current plans to implement it. I'm not sure exactly how it would work but having written a few takes on it with hypermerge, I'm sure it's doable.
- We would love to explore that one and not waste time on hyperswarm if it does not meet automerge requirements

- ## Is there any chance that we can eventually get an improved Text API on the roadmap?_202308
- https://automerge.slack.com/archives/C61RJCM9S/p1692886056954899
  - I still don't think it's possible to do real text editor integration without linear scans of text to reconcile javascript vs automerge string representations, but it seems like that stuff could be hidden behind an API anyway (which I believe libraries like yjs do). I understand that this may not be a priority, but is there an intention to improve this situation eventually?
- Good text editor bindings are the next thing on the list after we get the automerge-repo release out. 
  - I already have half complete prosemirror and codemirror bindings which we will be officially supporting so yes, a good text API is on the list

- ## [is amfs means AutoMerge Filesystem?](https://github.com/ConradIrwin/amfs/issues/1)
- That’s correct, and it uses automerge-go under the hood.
  - the goal was to play with file systems that sync in real time, so as you type in VSCode it is immediately reflected on the filesystem. 
  - It’s currently using NFS, because I found a simple nfs server template, but it’s a little slow (and very “works on my machine”).
  - The end goal was to build a replacement for git that you didn’t have to remember to use, but I am currently thinking about doing something that doesn’t use NFS instead.

- ## 🆚️ [how does automerge compare to holochain?](https://github.com/automerge/automerge/issues/566)
- Automerge is like Docs. 
  - Holochain is Bittorrent.
  - Both attempt to ensure data integrity in different circumstances.
  - Automerge (a CRDT) tries to ensure data integrity when two different people are working on the same file at once, **solving the problem of data integrity via eventual consistency**.
  - Holochain tries to ensure data integrity of a file across the network. However, if you change the file, it is no longer part of the network consensus and your version of the file is no longer the same file. The network is not interested in your changes and merging them, it is interested in maintaining the ground truth. Hence the "-chain" part. The majority (ledger) is king.
  - These two bits of software are both interested in maintaining data integrity, but with completely different goals in mind.

- The most noticeable difference between Automerge and Holochain is that the former doesn't require a specific network and the latter does; 
  - Automerge can synchronize data between peers over a LAN.

- ## is there an accompanying paper to describe the CRDT behind ‘micromerge’ or is ‘A Conflict-Free Replicated JSON Datatype’ the closest?
- https://automerge.slack.com/archives/C61RJCN9J/p1683034175607929
- There isn't really a good paper describing this, sorry. Micromerge/Automerge differ from the JSON CRDT paper in terms of the deletion semantics: the paper implements deletion as recursive clearing, which leads to the weird behaviour shown in Fig. 6. Micromerge/Automerge instead implement deletion as removing the reference to the deleted object, which means that any concurrent changes to the deleted object are simply discarded.

- ## [Automerge 2.0_202301](https://automerge.org/blog/automerge-2/)
- Earlier versions of Automerge were implemented in pure JavaScript. 
  - Our initial implementations were theoretically sound but much too slow and used too much memory for most production use cases.
  - JavaScript support on mobile devices and embedded systems is limited. 
- Instead of trying to coordinate multiple distinct versions of Automerge, we decided to rewrite Automerge in Rust and use platform-specific wrappers to make it available in each language ecosystem. 
  - This way we can be confident that the core CRDT logic is identical across all platforms and that everyone benefits from new features and optimizations together.
- For JavaScript applications, this means compiling the Rust to WebAssembly and providing a JavaScript wrapper that maintains the existing Automerge API.
