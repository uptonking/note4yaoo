---
title: lib-editor-codemirror-collab
tags: [codemirror, collaboration, editor]
created: 2021-10-14T17:12:36.915Z
modified: 2021-10-14T17:13:04.791Z
---

# lib-editor-codemirror-collab

# guide

# community

## CRDTs & Positions in CodeMirror 6__202008

- https://discuss.codemirror.net/t/crdts-positions-in-codemirror-6/2571
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
# blogs

## [Collaborative Editing in CodeMirror_202005](https://marijnhaverbeke.nl/blog/collaborative-editing-cm.html)

- This post describes the considerations that came up in designing the document-change data structure and built-in collaborative editing feature in the upcoming version of CodeMirror 6
- **the design I ended up with is a very boring non-distributed operational transformation**.
- In a way, this post is publishing a negative result: I looked into a bunch of interesting alternative approaches, but found they didn't meet the requirements for this system.

- Distributed vs coordinated collaborative editing
- There's quite a disconnect between the scientific literature on collaborative editing and what most collaborative editors are doing. 
  - The literature is largely concerned with truly distributed collaboration
  - A typical web system, on the other hand, has clients talking to a server, which orchestrates the exchange of updates.
  - These problems are very different, and if you're aiming to implement the latter, about 95% of collaborative editing literature is discussing a problem you do not have.
- Working in a truly distributed fashion is very attractive in principle, of course.
  - It is strictly more general, and has connotations of escaping the over-centralized modern web. 
  - But it does drag in a lot of problems, even outside of the document convergence—peers have to store the document along with, depending on the technique used, its entire history. 
  - They have to somehow discover each other, maintain connections, and so on.
- So for the core of a JavaScript-based library, I decided that support for a distributed model wasn't important enough to justify the additional complexity. 

- Operational transformation involves, in its simplest form, a transformation function 
  - that takes two changes A and B, which both apply to the same document, and produces a new pair Aᴮ (a version of A that applies to the document produced by B) and Bᴬ (B but applies to the document created by A), such that A + Bᴬ and B + Aᴮ (where + indicates change composition) produce the same document.
- You can roughly think of the transformation as moving a change through another change.
  - For a plain-text document model, such a transformation function is not very hard to define.

- why is OT considered hard?
  - When the document structure is more complicated than plain text, and change structure is more complicated than just insertions and deletes, it becomes very hard to define a converging transformation function. 
  - And when you don't have a centralized party to determine the order in which changes get applied, you need, as far as I understand the literature, to keep data beyond the current document (“tombstones” that describe where deletions happened), to guarantee convergence.
- The **main problem is that this technique is hard to reason about**. 
  - It has many practical advantages but, being a hack, doesn't provide the kind of mental framework that would allow you to confidently apply it in different situations.

- CRDT: Conflict-free Replicated Data Types
  - They are another approach to convergence that, contrary to operational transformation, does provide a way for us mortals to reason about convergence.
  - Basically, CRDTs complicate the way they represent data and changes to the point where you can apply changes in any order, and as long as you applied the same changes, you get the same result.
  - For text-style data, CRDT approaches roughly work by assigning every character a unique ID.
  - Given such a data type, collaborative editing becomes a matter of making sure everybody ends up receiving everybody else's changes, eventually.
- Compared to OT, where your document representation can just be a minimal representation of the text inside it, these techniques **require an extra data structure to be stored for every character in the document**.
  - And with some of them, you don't get to delete those characters either.
- For CodeMirror's core, data structures and complications like this conflict with the goal of supporting huge documents and having a pleasant programming interface. 
  - So I've decided not to introduce a CRDT in its internal data structures.
  - It may be entirely reasonable to wire an instance of the library up to an external CRDT implementation, though, as has been done for ProseMirror with Yjs.

- CodeMirror's approach
  - So the plan is to support centralized collaborative editing out of the box, and punt(踢走；用平底船托运) on the complexities of decentralized collaboration.
- I started the project with the idea that I'd just do what ProseMirror does, since that worked well before.

- To recap, ProseMirror uses something similar to OT, but without a converging transformation function. 
  - It can transform changes relative to each other, but not in a way that guarantees convergence. 
  - ProseMirror's document structure is a tree, and it supports various types of changes, including user-defined changes, that manipulate this tree. 
  - I didn't have the courage to try and define a converging transformation function there. 
  - When a client receives conflicting remote changes, it first undoes all its local pending changes, applies the remote changes, and then the transformed form of its local changes. 
  - This means that everybody ends up applying the changes in the same order, so convergence is trivial.

- In CodeMirror, the document model is a lot simpler, 
  - so though I got pretty far with the ProseMirror approach, it seemed needlessly awkward. 
  - A sequence of individual changes, each of which applies to the document created by the previous one, isn't really how the user thinks about updating the document.
- So I moved to a system where you don't deal with individual changes, but rather with change sets, which represent any number of changes in a flat format, as a sequence of untouched and replaced spans.
  - In fact, it'd get another kept span at the end covering the rest of the document. 
  - This representation knows the length of the document it applies to, and will refuse to perform operations where these lengths do not match. 
  - This dynamically catches a whole class of programmer errors that would be silently ignored before.
  - To create a change, you specify your changes with offsets into the current document, and the library will sort and combine them into a single change set.
- Given this representation, it seemed an obvious optimization to use real OT, rather than ProseMirror's faux(人造的；人工的；假的) OT, since for this domain it's not hard to define.

- This is a large part of the reason why I spent weeks researching CRDTs even though my document convergence needs are well covered by OT. 
  - If you have a more fine-grained way to address positions (specifically, one that can refer to deleted positions), and you define position mapping in terms of that, you do not have this problem.
