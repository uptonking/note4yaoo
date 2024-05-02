---
title: lib-editor-codemirror-community-collab
tags: [codemirror, collaboration, community]
created: 2024-05-02T05:50:24.220Z
modified: 2024-05-02T05:51:12.370Z
---

# lib-editor-codemirror-community-collab

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🔀 [CRDTs & Positions in CodeMirror 6 __202008](https://discuss.codemirror.net/t/crdts-positions-in-codemirror-6/2571)

- ProseMirror and CodeMirror 6 now both implement a similar approach for transforming positions. 
  - From a developer experience, this is great. This allows third-party plugins to provide features such as commenting on ranges of the document to unique map positions while accounting for remote changes.
- the current position mapping approach is unsuitable for yjs/CRDT-bindings to *Mirror editors. So third-party plugins won’t work with CRDT approaches to provide shared editing.

- I think there are several good arguments to reconsider using a CRDT for shared editing in CodeMirror.
  - Better position handling
  - The author of ShareJS and ShareDB openly speaks out against OT: https://news.ycombinator.com/item?id=24194091
  - The web has evolved to a point where web applications do work peer-to-peer over WebRTC. One of many real-world examples is room.sh 13. They use Yjs & CodeMirror 5 to provide collaboration in peer-to-peer WebRTC sessions.

- My goal is to power shared editing on the web with Yjs. Different editors can use the same technology to provide shared editing over different backends. 
- I think the Y. Text type would be a great data model for CodeMirror 6. 
  - If you are interested, I’d love to help you to integrate the Y. Text type into CodeMirror 6 and work with you on a better approach for position mapping. 
  - Another advantage of Yjs is that it supports selective Undo/Redo for free (no additional data structure to hold operations, just ranges on the vector clocks).
- Alternatively, it would be helpful if CodeMirror 6 would allow CRDT editor bindings to hijack position mappings. 
  - Although, as you explained, index positions don’t always accurately describe ranges in collaborative documents. 
  - With CRDTs, it is possible to refer to deleted characters. This is not possible if positions are described as index positions. With any change around the mapped position, some information gets lost. 
- Another alternative is to abstract positions in CodeMirror. 
  - A CRDT implementation could add markers to the abstract position to describe the position relative to the CRDT model without doing index transformations (i.e. map to the unique ID of the character).

- I just realized that the example in your blog post shows that positions in OT also don’t always converge. This was surprising to me. 
  - I’m currently educating people using y-prosemirror not to use the default position mapping because they don’t work in peer-to-peer scenarios. 
  - If this is the expected behavior for CodeMirror & ProseMirror, I can be more lenient(宽容的) to the fact they they also don’t converge with Yjs.
  - Although, I still think that in some cases this behavior is not acceptable. For example when implementing a shared-cursor plugin, or when implementing a commenting plugin.

- If it was possible to hijack the position mapping and provide a custom mapping based on the CRDT model, it would be possible to have positions converge.
  - If your input is still a plain (and thus ambiguous in the face of deletions) position, I don’t see how you can provide a better mapping. A position next to a deletion will correspond to multiple CRDT character IDs, and you don’t have information to disambiguate that.
- You are right… this wouldn’t work either. For the few cases when convergence is required I will provide a different position abstraction that doesn’t need to be native to CodeMirror. Thanks for your feedback.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
