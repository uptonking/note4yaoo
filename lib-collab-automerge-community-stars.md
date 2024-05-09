---
title: lib-collab-automerge-community-stars
tags: [automerge, collaboration, community]
created: 2023-09-01T10:16:55.484Z
modified: 2023-09-01T10:17:33.439Z
---

# lib-collab-automerge-community-stars

# guide

# discuss-text-editing
- ## 

- ## 🌰 We shipped rich text & prosemirror support for Automerge! 
- https://twitter.com/pvh/status/1788409904543269347
  - It was HARD and took many combined brains, but the result is something we're proud of
  - One really interesting and difficult challenge has been to ensure all operations -- including every possible combination of text entry and formatting -- can be done *incrementally*. This ensures stable performance even as documents get very large.
  - Another interesting feature of this design is that again, because it is patch-based, we can perform efficient "time travel" to any possible point in time in the history of the document. In our CodeMirror implementation we use this to render highlighted diffs.
  - The underlying rich text format is designed to be editor-agnostic. The reference implementation is ProseMirror, but we hope in time to see bindings for other platforms and editors that can interoperate. (There is a non-trivial schema problem here.)

- Curious on how it differentiates itself from Tiptap and its collaboration features?

- ## Is there any chance that we can eventually get an improved Text API on the roadmap?_202308
- https://automerge.slack.com/archives/C61RJCM9S/p1692886056954899
  - I still don't think it's possible to do real text editor integration without linear scans of text to reconcile javascript vs automerge string representations, but it seems like that stuff could be hidden behind an API anyway (which I believe libraries like yjs do). I understand that this may not be a priority, but is there an intention to improve this situation eventually?
- Good text editor bindings are the next thing on the list after we get the automerge-repo release out. 
  - I already have half complete prosemirror and codemirror bindings which we will be officially supporting so yes, a good text API is on the list

- ## [Modeling RichText with Automerge](https://github.com/automerge/automerge/issues/193)
- I have spent a while thinking about this too, and I also think that a single document sequence with marker characters is the way to go. 
  - If you represent a document as a tree, there are a lot of operations that require deleting and re-inserting nodes (e.g. hitting enter in the middle of a paragraph, causing it to split into two paragraphs), which don't merge well in a concurrent setting. 
  - If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence.
- My intention was that Automerge. Text should be usable for this purpose. That is, I want Automerge. Text to be able to contain marker objects as well as characters from the text
- Maybe I am overlooking something, but "If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence." means we can not express tree structures. I can not imagine WYSIWYG without at least an anchor which has to be split as well.

- there is new development going on: next month, @geoffreylitt and @sliminality will be kicking off a research project to figure out the best way of handling rich text in CRDTs such as Automerge, with the support of the @inkandswitch research lab. 
# discuss-sync
- ## 

- ## 

- ## 🔁 it should not download the entire doc2 rather the changes from last know position. Some thing like git pull. Is that something we can do in automerge?
- https://automerge.slack.com/archives/C61RJCM9S/p1702742583333909
- The sync protocol in Automerge will do exactly this, pretty much exactly as git does but more efficiently in many cases
  - It's an implementation of this idea
  - [Using Bloom filters to efficiently synchronise hash graphs — Martin Kleppmann’s blog_202012](https://martin.kleppmann.com/2020/12/02/bloom-filter-hash-graph-sync.html)
- Can you help me to find out where does Automerge implement it? Specifically in the Java layer
  - The Java library is a wrapper around the rust library, the implementation in the rust library is here: https://github.com/automerge/automerge/blob/main/rust/automerge/src/sync.rs
- I have a half finished kotlin port which I can clean up and we can take a look at it that's of interest?
  - It uses coroutines heavily though so probably only useful for Android

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
