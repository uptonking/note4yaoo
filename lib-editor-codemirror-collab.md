---
title: lib-editor-codemirror-collab
tags: [codemirror, collaboration, editor]
created: '2021-10-14T17:12:36.915Z'
modified: '2021-10-14T17:13:04.791Z'
---

# lib-editor-codemirror-collab

# [Collaborative Editing in CodeMirror_202005](https://marijnhaverbeke.nl/blog/collaborative-editing-cm.html)
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

- This is a large part of the reason why I spent weeks researching CRDTs even though my document convergence needs are well covered by OT. 
  - If you have a more fine-grained way to address positions (specifically, one that can refer to deleted positions), and you define position mapping in terms of that, you do not have this problem.
