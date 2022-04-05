---
title: lib-collab-crdt-community-stars
tags: [collaboration, community, crdt]
created: '2021-11-24T17:08:48.275Z'
modified: '2022-04-05T10:09:51.343Z'
---

# lib-collab-crdt-community-stars

# discuss

- ## The future of apps is local-first and CRDTs
- https://twitter.com/AdventureBeard/status/1495973698846736387
  - [Local-first software](https://www.inkandswitch.com/local-first/)

- ## Peritext: a CRDT for rich text collab

- https://twitter.com/geoffreylitt/status/1463244227412824066
- It's a data structure for async collaborative editing of rich text documents. 
- I believe the tools we use to collaborate can deeply shape the outcomes.
  - Real-time writing tools like Google Docs are an incredible step forward from emailing files, but they do promote a very specific workflow: "one live doc", that everyone is editing at the same time
  - This is fine for light docs, but in my experience it's not great for serious writing, like an essay or academic paper.
  - I want private calm space to try out edits; I want to suggest changes and discuss them as a batch... I want version control; "one live doc" is not enough! 
  - BTW, if you've ever developed software, you're probably familiar with the benefits of version control and branching workflows--maybe overkill for a tiny solo project, but indispensable for serious collaborative work.
- collaboration algorithms underpinning services like Google Docs are generally designed with "one live doc" in mind, not async collaboration. 
- So that brings us to this project.
  - CRDTs are a kind of data structure that allow people to asynchronously make local changes, and then merge those changes back together when people are ready to sync. 
  - The thing is, there has been a _ton_ of research on CRDTs for plain text, but barely any on rich text... which is essential for real writing.
- So that brings us to Peritext: a CRDT for rich text.
  - We've tried to pin down how async edits on rich text should be merged in a bunch of example cases, and proposed an algorithm that just always does the right thing.

- Circa 2012, I did CRDT rich text along the same lines. Compared to your case, I cut some corners though. 
- https://twitter.com/gritzko/status/1463404022212304898
  - Regarding the performance, the key trick was to use paragraph ids along with character ids (paragraph id is the id of the '\n'). Paragraphs/lines have manageable size, can put them in a hash table, then just scan them.

- Any thoughts on how @ProseMirror does this ?
  - One difference is that Prosemirror's collaboration system is designed to work with a single central server, whereas CRDTs are designed to work in distributed settings without a central authority.

- https://twitter.com/geoffreylitt/status/1463291185032679425
  - In my view the main problem with non-realtime merging is that undesirable merges (which any algorithm will sometimes produce) are harder to notice, so you'll want some kind of interactive UX that detects and points out potential conflicts to the user.
  - I'm curious, does Prosemirror's OT system have a notion of conflicts? We currently just arbitrarily resolve conflicts, but our approach would support detecting + showing conflicts a different way
  - Would also love to chat more sometime about Prosemirror's OT and understand better. It seems like key differences are:
  - 1) CRDT works in distributed setting, as you note (if you care about that property)
  - 2) It seems more straightforward to me to reason about correctness of CRDT w/ char IDs and commutative ops, than position mappings and rebasing operations. But that's subjective and I'm curious if you agree
- That's definitely true wrt to OT that supports reordering, but dumbed-down OT where every client ends up applying the operations in the same order converges pretty much trivially, and is not hard to reason about.
  - That being said, there's definitely advantages to adressable tokens, if you can afford the general conceptual complexity it introduces

- https://twitter.com/simonw/status/1463352229746786307
- I'm really excited for one with robust JavaScript and Python libraries that's well suited to using SQLite as the backend data store - I want to build a collaborative editor on top of Datasette which supports offline editing that can be merged back in when the client reconnects. Basically I want to build my own version of Apple Notes, crossed with Google Docs, crossed with a Markdown wiki
- Interesting! Offhand, **maybe could store/sync a SQLite table storing the history of CRDT operations, and replay that into a text doc format?** Although that table would get fairly large, and wouldn't get the benefit of a custom file format to compress down at all
  - That's pretty much what I want to do - I figure I can have a table of operations and every 10 days or so compress it down to a single savepoint and start building up the operations again to avoid size problems
  - Yeah seems sensible, and not much of a loss if you rarely have edits come in on top of a really stale version
