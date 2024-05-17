---
title: lib-editor-codemirror-blog-collab
tags: [blog, codemirror, collaboration]
created: 2021-10-14T17:12:36.915Z
modified: 2024-05-02T05:51:42.507Z
---

# lib-editor-codemirror-blog-collab

# guide

# blogs

## [Collaborative Editing in CodeMirror _202005](https://marijnhaverbeke.nl/blog/collaborative-editing-cm.html)

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

## [[译] CodeMirror: 协同编辑 - Lewin's Blog _202109](https://lewinblog.com/blog/page/2021/210920-CodeMirror-Collaborative-Editing.md)

- 在我的视野看来，接下来有两个方向的研究：一是后端方向，直接读 gorilla/websocket 的源码，把协议的各种处理细节都熟悉一遍；二是前端方向，探索更多的应用场景。

- 如果不引入新的框架工具，就用手头熟悉的工具，能够实现「协同编辑」吗？
- 实现1：全量同步
  - textarea熟悉对吧，那每次onChange的时候，都把全文发回服务器，让服务器把全文广播给所有客户端。
- 实现2：分行同步
  - 假如先简化一下，假设网络是稳定且迅速的，不考虑多端用户在同一个瞬间做操作的情况。那么做起来也简单，前后端分别split一下，加不了太多工作量。
  - 可是在现实状态下，冲突问题变得无法忽视：假如行本身发生了变化（例如删除了行），这时候怎么处理？遇到网络波动又如何确认和恢复？
  - 为了应对这种冲突，如果只是{行数：内容数据}这样简单的数据结构显然无法满足要求，至少，要增加一个修改前的状态这个东西，才能确保不会发生误操作。
  - 一个简单的思路，可以维护一个顺序号，服务器每次检查顺序号，对于冲突的顺序号的同步请求予以拒绝，然后客户端得知被拒绝之后，要等其他操作同步完毕之后才能提交自己的操作。

- CodeMirror使用一些基于「操作转换原理 operational transformation 」的工具，以及一个用于指定所有操作的确切顺序的「认证中心（服务器）」，来解决这个协作问题。

- 这个库并没有为effects封装序列化操作，所以为了与JSON一起工作你需要自己撸代码。

- 其次@codemirror/collab这个协作库呢，感觉充满了黑魔法，至少我研究了一下午都还没有觉得很有信心能顺利地实现。翻译的这篇文章呢，原理讲得还行，但是操作层面上我觉得没有很好的参考价值。
- 以及有一个重要的缺陷：服务端也要求js运行时才能使用这个库。当然，第一就算我要开一套node.js服务也就是个把小时的事情，第二我也能想到服务端不用js用其他语言加一些取巧的办法也可以实现。
# more
