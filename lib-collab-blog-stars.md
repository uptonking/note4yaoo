---
title: lib-collab-blog-stars
tags: [blog, collaboration]
created: 2021-10-14T11:18:06.356Z
modified: 2022-04-05T10:10:22.091Z
---

# lib-collab-blog-stars

# guide

- 没必要执着于通用且高性能的全场景协作方案
  - 具体的业务对于协作的粒度要求不同，特别是是否要支持字符级别的协作
  - 子元素是否要支持协作编辑，如编辑器内的表格、白板内的表格

- 协作示例小结
  - jlongster/crdt-example-app-hlc
    - 实时通信基于前端setInterval轮询
    - 冲突处理基于crdt-hlc的数据结构
    - 每次客户端执行sync都会发送自己的merkle-tree数据到服务端，让服务端快速计算需要返回的op记录
  - idb-side-sync，架构不适合实时协作
    - 同步通信通过手动触发请求执行sync
    - 每次客户端会请求本地最新时间戳之后的服务端op，这个设计不适合协作
  - otjs
    - 以服务端接受op的version/时间戳为中心authority，逐个op按顺序处理
    - 客户端首次连接服务端时，会获取doc最新内容和version

- local-first + realtime协作的示例
  - https://github.com/gongojs/project
  - https://github.com/a-type/lo-fi
# 🔀🌵 [GitHub Next | Realtime GitHub - Multiplayer collaboration for your whole repo](https://githubnext.com/projects/rtgh/)
- At GitHub Next we’ve been exploring this question for some time: 
  - In the Collaborative Workspaces concept design, we imagined cloud workspaces that integrate different modes of development (ideation, design, coding, etc.) into a single interface, and provide realtime multiplayer collaboration in all these modes. 
  - And in the GitHub Blocks prototype, we made the GitHub repository page customizable, with interactive blocks to tailor it to your team’s development process.

- With Realtime GitHub, you can share a link (“meet me in this branch!”) and instantly edit repository files together with your team. 
  - It’s still GitHub, so you can still work asynchronously—pull changes from another branch and merge your changes back when you’re ready.
- While our north star is the fully-integrated cloud environments envisioned in Collaborative Workspaces, we know that we can’t replicate the features of a modern development environment overnight. 
  - But we want to build something that we can use for real work, in order to learn and improve our prototype. 
  - So we’ve focused so far on workflows involving editing rich-text documents: taking meeting notes, drafting site copy, writing design documents, and so on.
- Realtime GitHub provides a rich-text editor like Google Docs, built on the excellent ProseMirror and Tiptap projects. 
  - Documents are stored as JSON files in your project's GitHub repo—so they can be edited on a branch and included in PRs, searched along with other files, backed up, or used in other ways.
- Realtime GitHub is collaborative like Google Docs, providing realtime multiplayer editing, cursor and selection presence, and threaded comments (with emoji reactions, a critical feature 😻!)
  - But it also supports GitHub-style async collaboration: a branch in your repository becomes a distinct "room" for multiplayer collaboration; you can work privately or with others, and merge it back to the main branch when you're ready.

- There are many approaches to collaborative editing, of which CRDTs are perhaps the best known, with well-engineered implementations like Yjs and Automerge available off the shelf. 
- For Realtime GitHub we've taken a different direction. 
- The vision we're working toward, of fully-integrated cloud environments for development, comes with some unusual requirements:
  - we want to provide asynchronous as well as realtime collaboration
  - users collaborate on an entire codebase
  - we want to support many different types of collaborative artifacts
  - we want to support straightforward integration with external tools (e.g. build systems, or AI assistants) as participants in a collaboration
- 🌵 Our approach takes inspiration from Git, as well as from the ProseMirror collaborative editing design, Replicache, Irmin, and others. 
  - The main idea is to think of each client as a Git clone, communicating local changes by pulling, rebasing, and pushing them to the server.
- In more detail:
  - the state of a branch is represented by a commit with a corresponding hash (just as in ordinary Git), and 🧐 the server maintains the authoritative current hash for the branch.
  - clients are notified when the server's branch hash changes, and pull the changes.
  - when a client makes a change, it applies it locally, then submits the change to the server, along with the most recent branch hash the client has (which may no longer match the server's hash).
- Git object graphs have some nice properties: Different Git objects (commits, trees, and blobs) have different hashes (with high probability), so hashes can be used as pointers. 
  - Git trees are a kind of hash tree, where a change anywhere in the tree produces a different hash for the root. 
  - And they are a kind of persistent data structure, where updating the tree produces a new tree with pointers into the old tree to the parts that haven't changed.
- Since our approach is just a way of using Git, it's straightforward to implement branching and merging for async collaboration; and it's straightforward to expose a branch via the filesystem to integrate external tools.
- One way Realtime GitHub diverges from Git is how it does merges and rebases: Git knows about states of a codebase, but not the changes that get it from one state to another. 
  - When you merge or rebase one branch onto another, Git compares the states of the branches and their common ancestor and reconstructs changes using diff3, which works line-by-line and doesn't consider the syntax or semantics of the file.
  - For ProseMirror documents, which are stored as JSON, this isn't a good approach—it works at too coarse a grain for realtime edits (e.g. edits to different parts of the same line produce a conflict), and can produce invalid JSON at the syntactic or semantic levels.
- Realtime GitHub uses two strategies:
  - for fine-grained realtime changes, clients write a ProseMirror transaction, which produces a new Git state on the server, and also sends the transaction to other clients to apply to their local state (rebasing local changes if needed).
  - (not implemented yet) for coarse-grained changes (e.g. merging one branch into another), we do a Git-style three-way merge on the JSON structure of the document, producing a semantically valid document. Conflicts are marked as special document nodes, which are displayed in the editor UI for manual resolution.
# [figma: How Figma’s multiplayer technology works__201910](https://www.figma.com/blog/how-figmas-multiplayer-technology-works/)

# [figma: LiveGraph: real-time data fetching at Figma | Figma Blog_202110](https://www.figma.com/blog/livegraph-real-time-data-fetching-at-figma/)

- how do we empower our product engineers to build these real-time views easily, while abstracting away the complexity of pushing data back and forth?
  - 👉🏻 To provide a general solution to this fundamental business need, we developed LiveGraph, **a data fetching layer on top of Postgres that allows our frontend code to request real-time data subscriptions expressed with GraphQL**. 
  - It issues queries directly to the database and provides live updates in the order of(~of/in the order of sth, 大约、数量级) milliseconds by reading the database replication stream.

- We realized that we needed a more general framework that would allow product developers to declaratively define data subscriptions. 
  - A natural choice for this interface was to use GraphQL, which would allow the system to automatically fetch and keep the data live-updated. We decided to build it in-house and call it LiveGraph.
# Portable Text
- portabletext /1kStar/MIT/202202/md/text
  - https://github.com/portabletext/portabletext
  - Portable Text is a JSON based rich text specification for modern content editing platforms.
  - Portable Text is presented by Sanity.io

- Portable Text is an agnostic abstraction of rich text that can be serialized into pretty much any markup language, be it HTML, Markdown, SSML, XML, etc. 
  - It's designed to be efficient for real-time collaborative interfaces, and makes it possible to annotate rich text with additional data structures recursively.
- Portable Text is built on the idea of rich text as an array of blocks, themselves arrays of children spans. 
  - Each block can have a style and a set of mark definitions, which describe data structures distributed on the children spans. 
  - Portable Text also allows for custom content objects in the root array, enabling editing- and rendering environments to mix rich text with custom content types.
# [Collaborative Editing in ProseMirror__201508](https://news.ycombinator.com/item?id=10002553)
- Hi! Joseph Gentle here, author of ShareJS.
  - You're right about OT - it gets crazy complicated if you implement it in a distributed fashion. 
  - But implementing it in a centralized fashion is actually not so bad. Its the perfect choice for google docs.
- Here is my implementation of OT for plain text
  - https://github.com/ottypes/text
  - https://github.com/josephg/appstate
  - Note that its only 400 lines of javascript, with liberal comments. 
  - To actually use OT code like that, you need to do a little bookkeeping. 
  - Its nowhere near as bad as you suggest.

- Yes, but that implementation deals only with plain text. The complexity seems to ramp up pretty quickly as you support more types of operations, and since extendability is an important concern for my project, I decided to avoid OT.

- If you have insert, update, and delete then you can build any other operation from those primitives as long as you have the ability to batch a composite operation. 
  - So there's no need to extend the OT algorithm to support other kinds of primitive operation. 
  - For nested structures, addressing via ids or linear addresses has to be taken into account but that doesn't affect the OT transforms, it's one layer above. 
  - So it's possible (though not easy) to have an extensible OT system without exponential complexity. 
  - Still, avoiding OT has led to some interesting new ideas and I look forward to seeing how things progress.

- Initially, I thought to wire this all up using the sharejs project, but never could quite grok that codebase.
  - Instead, I've been working on a similar system to one you describe, with changes applied in order based on sequential version number, and concurrent updates forced to "rebase" against earlier changes 
  - Because applying changes in a different order might create a different document, rebasing isn't quite as easy as transforming all of our own changes through all of the remotely made changes.
  - Can you explain more about how you arrived this conclusion? From my understanding, a correct transform function should allow exactly this, according to transformation property 1. Perhaps your algorithm doesn't exactly satisfy this property; what characteristics does it have instead?
- A correct OT transform, yes. But I'm not using OT's invariants, so this is not something my transforms do. For example, in my system, if you have "insert X at pos 5" and "insert Y at pos 5", the document will contain "XY" or "YX", depending on which arrived first.

- A minimal backend can be extremely simple, just relaying changes, but if you want it to keep a running snapshot of the current document, you'll need the capacity to apply those changes to document, so you'd need to use the module used by the client, or a port of that.
# blogs-ot-crdt

## [tinymce: To OT or CRDT, that is the question_202001](https://www.tiny.cloud/blog/real-time-collaboration-ot-vs-crdt/)

- At a very high level, this is what we're dealing with:
  - OT relies on an active server connection (not quite correct but we'll get to that in a moment) to coordinate and guarantee all clients operate correctly.
  - CRDT is capable of working peer-to-peer with end-to-end encryption; if a server is used at all it only needs to coordinate connections between clients. It is resilient to transient network connections. It even works if clients go offline for a period of time, make changes, and synchronise when the network returns.
- There is a reason Google, Microsoft, CKSource and many others depend on OT. 
  - Tiny has chosen to also build our solution around OT; 

- In OT, every user action is broken down into one or more operations. 
  - These operations are transmitted between clients along with their baseline reference; 
  - if two users perform actions at the same time, incoming operations must be transformed to include the local operations that have happened since that baseline. 
  - They are then applied locally and form the new baseline.
  - This constant transformation of operations turned out to have too many edge cases where clients were found to not produce the same baseline (the "wrong" papers above). 
  - When that happens, the clients will never converge on the same result and break the fundamental assumption of collaboration.

- Only two reliable forms of OT have survived the test of time
- Server-based OT
  - splitting multi-user collaboration into groups where each client pairs individually with the server. 
  - The server coordinates the document state and operation list to ensure that transformation only ever occurs within these pairs, thus avoiding the complexity (and edge cases) of three-way transforms.
- OT with what's known as "transform property 2". 
  - CP2/TP2 finally gave the community a provably correct multi-way transformation algorithm, but it turned out to be so complex that very few data structures have working TP2 implementations.

- The magic of CRDT is due in large part to how it breaks down data into such small pieces that it generally doesn't need to transform the change itself, only the position of the change. 
  - For example, text data collaboration with CRDT treats every character as a separate entity.
- The limitations of CRDT are similar to what happened when the TP2 restriction was proposed for OT; the difficulty is in the data type. 
  - It is not as difficult as TP2 - there is a working OT+TP2 for JSON, but my impression is the CRDT implementation was easier to achieve - but it's still only appropriate for simple use cases.
- When it comes to more advanced structures such as rich text editing, the crux of the problem with CRDTs is user intent. 

- Conclusions
- CRDT is the holy grail of collaboration, it's an active area of research, and the prospect of peer-to-peer editing with end-to-end encryption is an exciting one. 
  - The technology isn't ready for our needs yet, but I believe in the future some incredible products will be made possible. 
  - In the meantime TinyMCE will rely on OT for collaboration, coming later this year.

- [Real-time collaboration is the new responsive design_20212](https://www.tiny.cloud/blog/real-time-collaboration-essential/)

- [How to migrate from Slate.js to TinyMCE_202209](https://www.tiny.cloud/blog/migrate-from-slatejs-to-tinymce/)
- The Real-Time Collaboration plugin built for TinyMCE makes use of Slate.js for the core model.

## [tinymce: Collaboration needs a clean Slate_202002](https://www.tiny.cloud/blog/real-time-collaborative-editing-slate-js/)

- 👉🏻️ Note: this model will only be used for RTC, not the default editing experience

- Although we may eventually decide to write our own model, we quickly settled on Slate as the library to use to build a high-quality product.

- Our real-time collaboration project has been split into a collection of sub-projects:
  - A custom VDOM rendering engine for the Slate model, and reverse-map logic for selection and content input, targeting a pure ContentEditable div so it is not TinyMCE specific
  - An implementation of low-level editor features built on Slate core APIs
  - A layer that loads TinyMCE configuration and content to set up and compose the low-level features into a working editor
  - Collaboration control (transforms, cursors, server interaction)
  - Hooks in the TinyMCE core to relinquish control of ContentEditable and redirect all model APIs to the external RTC code

## [ckeditor5: Lessons learned from creating a rich-text editor with real-time collaboration_201802](https://ckeditor.com/blog/Lessons-learned-from-creating-a-rich-text-editor-with-real-time-collaboration/)

- Our take on Operational Transformation
  - CKEditor 5 uses OT to make sure it is able to resolve conflicts. 
  - OT is based on a set of operations (objects describing changes) and algorithms that transform these operations accordingly, so that all users end up with the same editor content regardless of the order in which these operations were received. 
- Therefore, in 2015 we started working on our take on OT implementation.
- OT in its basic form defines three operations: insert, delete, and set attribute. 
  - These operations are meant to be executed on a **linear data model**.
  - They are responsible for inserting text characters, removing text characters and changing their attributes 
- The linear data model is a simple data model that is sufficient to represent plain text. 
  - On the contrary, an HTML document is represented in the browser as the Document Object Model (or DOM), which is tree-structured.
  - It is possible to represent simple, flat structured data in a linear model, but this model falls short when it comes to complex data structures, like tables, captioned images or lists containing block elements. 
  - Elements simply cannot contain other elements. For example, a block quote cannot contain a list item or a heading.
- Hence, we needed to make a step further and provide Operational Transformation algorithms that work for a tree data structure. 
- We quickly realized that the basic set of operations (insert, delete, set attribute) is insufficient to handle real-life scenarios in a graceful way. 
- The most important enhancement that we made was adding a set of new operations to the basic three (insert, remove, set attribute). 
  - The rename operation, to handle element’s renaming (used, for example, to change a paragraph into a heading or a list item).
  - The split, merge, wrap, unwrap operations to better describe the user intention.
  - The insert text operation, to differentiate between inserting text content and elements.
  - Unrelated to conflict solving, we have also introduced the marker operation.

- Dedicated collaboration features
  - Our editing framework is built in a way to support all rich-text editor features in the collaboration mode. 
    - From simple ones like text styling, through image drag and drop and captioning, to complex ones like undo and redo, nested lists or tables.
    - Support for third-party plugins
  - Comments feature
    - Adding comments in real time, as other users edit, to any selected part of the content (commenting in “read-only mode” is supported, too).
  - Users’ selection feature
    - Visual highlights at exact places where other users are editing
  - Presence list feature
    - Showing photos or avatars of users who are currently editing the document.
  - more collaborative features
    - Suggestion mode (aka track changes) 
    - Mentions feature – insert and link names or phrases
    - Versioning and diffing – Save versions of your document and compare them

- Real-time collaboration requires a server (backend) to propagate changes between connected clients.
  - Your changes will not be lost if you accidentally close the document. A temporary backup in the cloud will always be available.
  - Your changes will be propagated to other connected users even if you temporarily lose your internet connection.

- Summary
  - We started building our next generation rich-text editor with the assumption that real-time collaborative editing must be the core feature that lies at its very foundation — and this meant a rewrite from scratch. 
  - we created an Operational Transformation implementation, extended to support tree-based data structures (rich-text content) for advanced conflict resolution. 
# blogs-collab

## [Ready Player Two – Bringing Game-Style State Synchronization to the Web_202310](https://rocicorp.dev/blog/ready-player-two)

## [A light exploration of collaborative editing and synchronization algorithms_202108](https://blog.jakubholy.net/2021/light-exploration-of-collaborative-editing/)

- 引用和总结了很多协作编辑器相关的技术选型
# more
