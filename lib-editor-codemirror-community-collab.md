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
# discuss-diff/track-changes
- ## 

- ## 

- ## [CodeMirror Merge Slow Diff - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-merge-slow-diff/7005)
- Seems at some document size, even the fast path is still too slow. Attached patch adds an even faster path (just treat the entire range as unchanged) for situations like this.

- ## 🐛 [incorrect diff for large files in merge view - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/incorrect-diff-for-large-files-in-merge-view/7411)
- Computing the diff for such large (and different) files is too expensive to do interactively, so the editor falls back to an overapproximation of the diff.
  - If people are allowed to edit the document, it seems that having a slow (and this is super-linear, so it gets very slow quite quickly) UI update cycle would make it unusable pretty quickly.
  - If users aren’t allowed to edit, maybe just statically rendering the text is easier than having it in a CodeMirror editor.

- ## [Merge View Implementation - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/merge-view-implementation/5072)
  - Not in scope are 3-way merges and spacer-less scroll synchronization, which the old implementation did support. If someone has a need for those we can talk about including them.

- A first implementation of this exists. Take a look at the code and a demo, and let me know how it looks. _202211

- ## 🆚️ [Github-styled unified text diff viewer (read-only) - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/github-styled-unified-text-diff-viewer-read-only/4913)
- The general idea would be to put a data structure describing the lines in some state field, and have separate gutters for the old and new line numbers, plus a gutter for the +/- signs, rendering markers based on the content of that data structure.
  - Or, if this is read-only, just render it without an editor, optionally using Lezer to highlight the code. That’s what the Chrome devtools do.

- @codemirror/merge also has a unified merge view 62 feature now.

- ## [I vaguely remember I saw an example of codemirror with tracking changes.  _202305](https://discuss.codemirror.net/t/track-changes/6561)
  - Any changes done in one editor was showing as a diff in the second one and one could take a snapshot of the current status. 
  - Can someone point me to the right direction to find it? Searching here and on google didnt help.
- Maybe the merge view (example) is what you mean?

# discuss-undo/history
- ## 

- ## 

- ## [More conventional undo behaviour? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/more-conventional-undo-behaviour/5565)
- I don’t think there is anything like a consensus on that. This forum seems to rely on the browser’s native behavior, which for (tried Firefox and Chrome Linux) seems to undo all text typed together in one go. 
  - Google Docs seems to use a similar system to CodeMirror.
  - This patch adds such a configuration option.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
