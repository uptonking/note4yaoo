---
title: lib-collab-automerge-community-stars
tags: [automerge, collaboration, community]
created: 2023-09-01T10:16:55.484Z
modified: 2023-09-01T10:17:33.439Z
---

# lib-collab-automerge-community-stars

# guide

# discuss
- ## 

- ## 

- ## 

- ## [Should the backend be Send + Sync?](https://github.com/automerge/automerge/issues/75)
  - Given the ideas proposing to have a single backend with multiple frontends, I think it would make sense for the backend to be Send + Sync. 
  - This means we could send a backend across threads as well as use it in shared memory settings with, for example, a Mutex. 
  - I can see this being particularly useful for server implementations in Rust where clients for a document may not always land on the same thread.

- my preference would be for the message passing wrapper. 
  - Automerge is intended to be a foundational library so I don't think we should make decisions about what kind of performance is acceptable to users when we don't have to. 
  - I think the message passing wrapper makes sense in the case of using one backend for multiple frontends anyway because you'll still need to ship patches from individual changes off to each of the frontends on every change, so there will be additional glue code to write (I think, I haven't thought about this in detail).

- ## [Modeling RichText with Automerge](https://github.com/automerge/automerge/issues/193)
- I have spent a while thinking about this too, and I also think that a single document sequence with marker characters is the way to go. 
  - If you represent a document as a tree, there are a lot of operations that require deleting and re-inserting nodes (e.g. hitting enter in the middle of a paragraph, causing it to split into two paragraphs), which don't merge well in a concurrent setting. 
  - If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence.
- My intention was that Automerge. Text should be usable for this purpose. That is, I want Automerge. Text to be able to contain marker objects as well as characters from the text
- Maybe I am overlooking something, but "If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence." means we can not express tree structures. I can not imagine WYSIWYG without at least an anchor which has to be split as well.

- there is new development going on: next month, @geoffreylitt and @sliminality will be kicking off a research project to figure out the best way of handling rich text in CRDTs such as Automerge, with the support of the @inkandswitch research lab. 

- ## [Automerge 2.0 | Hacker News_202301](https://news.ycombinator.com/item?id=34586433)
- It looks like Automerge 2 latest is faster than Yjs, but still uses 2x more memory.
  - Yjs (pure javascript?) is quoted on the paper benchmark at 1, 074ms and 10, 141, 696 bytes of memory, compared to Automerge 2.0.2-unstable at 661ms and 22, 953, 984 bytes of memory. 
  - I wonder if this is comparing usage from JS via bindings, or directly comparing two different rust implementations, or comparing Automerge 2.0.2-unstable via Rust to Yjs via NodeJS.
  - I am still not sure which set of tools I would recommend; I believe Yjs is more actively deployed in production since the Automerge implementation was so far behind performance wise until now. 
  - However one of the Peritext authors (https://twitter.com/sliminality who is on my team at Notion) tells me that 👉🏻 Automerge is better at text because it doesn't suffer from interleaved characters like Yjs does. So consider it instead of Yjs!
- 👉🏻 I’ve spent a lot of time benchmarking both libraries and talking to the authors. The main difference is that yjs has an extra optimization that’s still missing from automerge: Yjs does internal run-length encoding of adjacent inserted items. And adjacent inserts come up a lot in real text editing traces.
  - Adding this optimization to diamond types, in pure rust, improved performance by another order of magnitude (25ms for the same test with this tweak). It also dropped memory usage to about 2MB. 
  - The automerge engineers know about this trick (I’ve talked to them about it). So I assume it’s in the pipeline somewhere. And yjs is working on a rust reimplementation, which should bring its performance in line too.
- This optimization is indeed in the pipeline, although there are other things nearer the front because performance is currently Good Enough ™ that other things are more pressing (other things being e.g. completing the Peritext implementation, improving the sync protocol).

- diamond-types (for reference for others [0]) still only supports plain text, is that right? I was thinking of using it for more general use cases such as an offline habit tracker, which isn't text of course, but I was interested to hear more on the progress towards other data types such as generic JSON data.
  - Currently for this use case I've been using autosurgeon [1] so far which has a nice Rust API for structs, even if it might be slower than yjs (or yrs, its Rust implementation) or diamond-types.
- Yep; sadly still true. I started some work last year to simultaneously add support for arbitrary JSON data and add a database-like storage layer to allow us to safely stream changes to disk. (Automerge and yjs usually require the entire data set to be re-saved in its entirety when updates happen). Its taken longer than I thought, because I've gone through a bunch of different designs for both pieces. We'll get there; everything just takes longer than you want when you do it for the first time. I'll look at autosurgeon. Having similar APIs is good for everyone.

- As it stands CRDTs are only really useful for a narrow subset of data. Data is guaranteed to converge, but there is no guarantee that the final result makes any kind of semantic sense in the application domain.
  - One can write custom conflict resolution and treat the data structures as a convenient baseline for event sourcing, but that requires a lot of work and potentially often user guided resolution.
  - I'd really love to see some research into deriving CRDT merge semantics from a formal description of application behaviour.

- 
- 
- 
