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

- ## 📈 [Speed Comparisons Between Automerge Implementations_202101](https://github.com/automerge/automerge/issues/41)

- ## A hypercore conflates(合并，混合) several things in hypermerge
- https://twitter.com/pvh/status/1219777305632894976
  - it's not just an append only log, it's a sharable unit, a verifiable signature, and a Merkle tree.
  - I am absolutely ready to move off hypercore as storage if you have the gumption to propose an alternative
- The nice thing about IPFS is that because it's content addressed, you don't need a lot of the metadata hypercores include, so for static content I think it would make a ton of sense. There are substantial privacy downsides if you advertise all your content to the world though.

- ## We run automerge over hypercore + hyperswarm and call it hypermerge. Works reasonably well._202004
- https://twitter.com/pvh/status/1246144720474005505



- A good CRDT avoids unnecessary conflicts and surfaces inescapable ones.
  - In the case of ambiguous values in automerge, we provide a multi-value register in _conflicts, and select a stand-in value arbitrarily as a default resolution (because programming is hard when every piece of data in your system can be a multivalue.)
- Interesting. Having an arbitrary stand in is something I want to think about
  - It is unprincipled, but pragmatic, and let me tell you, a whole lot easier to write against. Take a look at Pushpin which is our reference implementation of a production-quality CRDT-based client application.


- The author of the JSON CRDT paper ( @martinkl ) is the author of automerge, and the differences are because we tried writing against the original implementation and found the UX wasn't ideal, so we made some changes
- 
- 
- 

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

- ## hypermerge used to provide a p2p gateway for automerge but was forsaken(抛弃，放弃) because it uses an outdated automerge version _202308
- https://automerge.slack.com/archives/C61RJCM9S/p1687580301244489
  - I also noticed that it had a couple shortcomings, wondering if those would be solved with the current versions of both libraries.
- I'd be interested in seeing an automerge-repo-network-hyperswarm but I don't have any current plans to implement it. I'm not sure exactly how it would work but having written a few takes on it with hypermerge, I'm sure it's doable.
- We would love to explore that one and not waste time on hyperswarm if it does not meet automerge requirements

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

- ## 🆚️ [Automerge: a new foundation for collaboration software [video] | Hacker News_202112](https://news.ycombinator.com/item?id=29501465)
- Main takeaways from toying with both Yjs and Automerge
u1. Extremely difficult to build backend in other programming languages than Nodejs
  - You will cry looking at source code C-binding, FFI, etc, https://github.com/yjs/y-crdt/blob/main/yffi/src/lib.rs
  - you weren't kidding - the rust port is total trash.
  - The internals are still very hot and in a state of flux, as we 1st decided to go with porting the Yjs, then leave cleaning and optimizations for 2nd step after we have something, that's compatible with existing Yjs behavior.
1. Both communities are great.
2. Watch out implementations of underline libraries. Trace lib0 libraries usage and internals in Yjs for example;JavaScript engines use UTF-16 encoding. Golang (my main backend language) is using UTF-8 ... reimplementing Yjs code in Golang with algorithms and optimization and futher scaling might become impossible for small startups.
3. Rich editing similar to Google Doc is very very complicated subject with lot of landmines
4. There's ProseMirror editor for collaborative editing. However you might not like its internals compare to Slatejs 

- > You will cry looking at source code https://github.com/yjs/y-crdt/blob/main/yffi/src/lib.rs
  - Am I missing something? You linked a file that is inherently going to be "un-Rusty" because it's meant to be an FFI shim for _non-Rust_ languages to use through a common C API that this file exposes.

- MeteorJS solved this 12 years ago...but good to see more thoughts being put into this.
  - It did not at all. It solved the problem of how to reflect a source of truth (the server) in somewhat real-time on the client through subscriptions. Also made some attempt to have edits that were persisted to client-side mini-mongo pushed to the server but this was best effort at most.
  - CRDTs are on a completely different level. They provide deterministic conflict resolution strategies through either/or causal and physical timestamps to ensure it's always safe to persist a write locally and later sync it with the server or not even have a server and sync directly which other peers.
- the local mini-mongo is acting a local-state and the JSON/JS all the way is solving the marshalling/ORM issue. I understand it is a centralized way of dealing with this, however, it was operating on the same problem space. Furthermore, automerge can be used as the server, which bring it closer to what Meteor did. I was hinting at the overlap in the problem space, but I should have phrased it better. Anyway, I'm keep to try automerge.

- The key feature of automerge is that it's decentralized like git. Two people could work asynchronously and only occasionally merge their results.
