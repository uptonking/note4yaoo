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
