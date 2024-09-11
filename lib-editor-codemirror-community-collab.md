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
# discuss-undo/history
- ## 

- ## 

- ## [Is there a way to customize the undo history list? - v6 - discuss. CodeMirror _202310](https://discuss.codemirror.net/t/is-there-a-way-to-customize-the-undo-history-list/7343)
  - I don’t want to add this insert operation to the undo history list. When using “Mod-z” for an undo operation, I want to skip this text insertion and directly return to an earlier historical state. What should I do?
- There’s an annotation you can add to transactions to get this effect.

- ## [Disable CTRL-Z (undo) for the very first change - v6 - discuss. CodeMirror _202203](https://discuss.codemirror.net/t/disable-ctrl-z-undo-for-the-very-first-change/4202)
  - The problem I have is that if a user presses CTRL-Z after the initial setting of the value, the whole content disappears. 
- If you create the new state with the content already in it, instead of firing a separate transaction that sets it, undo won’t delete it.
- You can also annotate your transaction with an `AddToHistory.of(false)` , can be any change.

- ## 💡 [editor.setHistory(), clearHistory() equivalent in Codemirror #6 - v6 - discuss. CodeMirror _202304](https://discuss.codemirror.net/t/editor-sethistory-clearhistory-equivalent-in-codemirror-6/6291/1)
  - each file has its own undo-redo history. We store history of each file by calling editor.getHistory() and storing in a Map. Whenever you switch the files, we load the history for that file and call editor.setHistory. This worked well in CM 5
- Usually, in situations like this, you just want to store the entire editor state (either as a JS object, or, if you need to serialize it, via EditorState.toJSON) rather than storing the document and history separately.
  - You can’t clear history. Just create a new state. When creating a new state with fromJSON, you can provide your serialized history in the JSON object.

- https://x.com/puruvjdev/status/1780560310547436002  
  - Anytime you change documentId, it stores the state in a map, and when the documentID changes back to the one stored, we apply the history. It's quite neat

- ## [More conventional undo behaviour? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/more-conventional-undo-behaviour/5565)
- I don’t think there is anything like a consensus on that. This forum seems to rely on the browser’s native behavior, which for (tried Firefox and Chrome Linux) seems to undo all text typed together in one go. 
  - Google Docs seems to use a similar system to CodeMirror.
  - This patch adds such a configuration option.

# discuss-crdt
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
# discuss-ot
- ## 

- ## 

- ## 
# discuss-cursor
- ## 

- ## 

- ## [How to show peers' cursors on CM6 collab editor? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-show-peers-cursors-on-cm6-collab-editor/3996)
- This isn’t a feature that any of the core modules provides—you’ll have to implement it yourself, by sharing the cursor positions over the network and displaying some widget or tooltip at those locations.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
