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
  - [GitHub Next | Collaborative Workspaces](https://githubnext.com/projects/workspaces/)
  - And in the GitHub Blocks prototype, we made the GitHub repository page customizable, with interactive blocks to tailor it to your team’s development process.

- With Realtime GitHub, you can share a link (“meet me in this branch!”) and instantly edit repository files together with your team. 
  - It’s still GitHub, so you can still work asynchronously—pull changes from another branch and merge your changes back when you’re ready.
- While our north star is the fully-integrated cloud environments envisioned in Collaborative Workspaces, we know that we can’t replicate the features of a modern development environment overnight. 
  - But we want to build something that we can use for real work, in order to learn and improve our prototype. 
  - So we’ve focused so far on workflows involving editing rich-text documents: taking meeting notes, drafting site copy, writing design documents, and so on.
- Realtime GitHub provides a rich-text editor like Google Docs, built on the excellent ProseMirror and Tiptap projects. 
  - Documents are stored as JSON files in your project's GitHub repo—so they can be edited on a branch and included in PRs, searched along with other files, backed up, or used in other ways.
- Realtime GitHub is collaborative like Google Docs, providing realtime multiplayer editing, cursor and selection presence, and threaded comments (with emoji reactions, a critical feature!)
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
# 🌰🔀 [figma: How Figma’s multiplayer technology works__201910](https://www.figma.com/blog/how-figmas-multiplayer-technology-works/)
- As a startup we value the ability to ship features quickly, and OTs were unnecessarily complex for our problem space

- When a document is opened, the client starts by downloading a copy of the file.
  - From that point on, updates to that document in both directions are synced over the WebSocket connection. 
  - Figma lets you go offline for an arbitrary amount of time and continue editing. When you come back online, the client downloads a fresh copy of the document, reapplies any offline edits on top of this latest state, and then continues syncing updates over a new WebSocket connection. 
- It’s worth noting that we only use multiplayer for syncing changes to Figma documents. 
  - We also sync changes to a lot of other data (comments, users, teams, projects, etc.) but that is stored in Postgres, not our multiplayer system, and is synced with clients using a completely separate system that won’t be discussed in this article
- Our primary goal when designing our multiplayer system was for it to be no more complex than necessary to get the job done. 
  - A simpler system is easier to reason about which then makes it easier to implement, debug, test, and maintain. 
  - Since Figma isn't a text editor, we didn't need the power of OTs and could get away with something less complicated.

- Figma's tech is instead inspired by something called CRDTs
  - All CRDTs satisfy certain mathematical properties which guarantee eventual consistency
- Figma isn't using true CRDTs though. 
  - CRDTs are designed for decentralized systems where there is no single central authority to decide what the final state should be. 
  - Since Figma is centralized (our server is the central authority), we can simplify our system by removing this extra overhead and benefit from a faster and leaner implementation.
- It’s also worth noting that Figma's data structure isn't a single CRDT. Instead it's inspired by multiple separate CRDTs and uses them in combination to create the final data structure that represents a Figma document
- 🧮 Every Figma document is a tree of objects, similar to the HTML DOM. 
  - There is a single root object that represents the entire document. 
  - Underneath the root object are page objects, and underneath each page object is a hierarchy of objects representing the contents of the page. 
  - This tree is is presented in the layers panel on the left-hand side of the Figma editor.

- Figma’s multiplayer servers keep track of the latest value that any client has sent for a given property on a given object. 
  - This means that two clients changing unrelated properties on the same object won’t conflict, and two clients changing the same property on unrelated objects also won’t conflict
  - A conflict happens when two clients change the same property on the same object, in which case the document will just end up with the last value that was sent to the server.
  - 🔀 This approach is similar to a last-writer-wins register in CRDT literature except we don’t need a timestamp because the server can define the order of events.
- An important consequence of this is that changes are atomic at the property value boundary.
- The most complicated part of this is how to handle conflicts on the client when there’s a conflicting change. 
  - Property changes on the client are always applied immediately instead of waiting for acknowledgement from the server since we want Figma to feel as responsive as possible. 
  - Since our change we just sent hasn’t yet been acknowledged by the server but all changes coming from the server have been, our change is our best prediction because it’s the most recent change we know about in last-to-the-server order. So we want to discard incoming changes from the server that conflict with unacknowledged property changes.
- Arranging objects in an eventually-consistent tree structure is the most complicated part of our multiplayer system.
  - The complexity comes from what to do about reparenting operations (moving an object from one parent to another).
  - Many approaches represent reparenting as deleting the object and recreating it somewhere else with a new ID, but that doesn't work for us because concurrent edits would be dropped when the object's identity changes
  - The approach we settled on was to represent the parent-child relationship by storing a link to the parent as a property on the child. That way object identity is preserved. We also don’t need to deal with the situation where an object somehow ends up with multiple parents that we might have if, say, we instead had each parent store links to its children.
- However, we now have a new problem. Without any other restrictions, these parent links are just directed edges on a graph. There’s nothing to ensure that they have no cycles and form a valid tree. 
  - Figma’s multiplayer servers reject parent property updates that would cause a cycle, so this issue can’t happen on the server. But it can still happen on the client.
  - Figma’s solution is to temporarily parent these objects to each other and remove them from the tree until the server rejects the client’s change and the object is reparented where it belongs. This solution isn’t great because the object temporarily disappears, but it’s a simple solution to a very rare temporary problem so we didn’t feel the need to try something more complicated here such as breaking these temporary cycles on the client.
- 🧮 To construct a tree we also need a way of determining the order of the children for a given parent. 
  - Figma uses a technique called “fractional indexing” to do this. 
  - At a high level, an object’s position in its parent’s array of children is represented as a fraction between 0 and 1 exclusive. 
  - The order of an object’s children is determined by sorting them by their positions. 
  - You can insert an object between two other objects by setting its position to the average of the positions of the two other objects.

- undo in a multiplayer environment is inherently confusing.
  - We had a lot of trouble until we settled on a principle to help guide us: if you undo a lot, copy something, and redo back to the present (a common operation), the document should not change. 
  - This is why in Figma an undo operation modifies redo history at the time of the undo, and likewise a redo operation modifies undo history at the time of the redo.

## [figma: Realtime Editing of Ordered Sequences | Figma Blog _201703](https://www.figma.com/blog/realtime-editing-of-ordered-sequences/)

- Instead of OT, Figma uses a trick that’s often used to implement reordering on top of a database. 
  - Every object has a real number as an index and the order of the children for an element of the tree is determined by sorting all children by their index.
  - To insert between two objects, just set the index for the new object to the average index of the two objects on either side. 
  - We use arbitrary-precision fractions instead of 64-bit doubles so that we can’t run out of precision after lots of edits.
- In our implementation, every index is a fraction between 0 and 1 exclusive. 
  - Being exclusive is important; it ensures we can always generate an index before or after an existing index by averaging with 0 or 1, respectively. 
  - Each index is stored as a string and averaging is done using string manipulation to retain precision. 
  - For compactness, we omit the leading “0.” from the fraction and we use the entire ASCII range instead of just the numbers 0–9 (base 95 instead of base 10).

- Benefits:
  - Easy to understand and implement
  - Reordering an object only involves editing a single value
- Drawbacks:
  - Index length can grow over time
  - Merging new elements from multiple clients may interleave them
  - Averaging between two identical indices doesn’t work

- We’ve been using fractional indexing for multiplayer editing in Figma from the beginning and it’s worked out really well for us. 
  - Even though OT provides some additional benefits around performance and interleaving, it’s much more beneficial for the Figma platform to use simple algorithms that are easy to understand and implement than to use the most advanced algorithms out there. 
  - It means more people can work on Figma, the implementation is more stable, and we can develop and ship features faster.
# 🌰 [figma: LiveGraph: real-time data fetching at Figma | Figma Blog_202110](https://www.figma.com/blog/livegraph-real-time-data-fetching-at-figma/)
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
# blogs-ot-crdt 🔀🆚️

## 🆚️ [Architectures for Central Server Collaboration - Matthew Weidner _202406](https://mattweidner.com/2024/06/04/server-architectures.html)

- 提供了对比表格

- This blog post records some thoughts on how to architect a real-time collaborative app when you do have a central server.

- Here are three common solutions to the server-side rebasing challenge.
- Serialization
  - I call this approach “Serialization” by analogy with SQL’s serializable isolation level.
  - The server rejects Bob’s operation. His client must download the new state S + A and then retry with an updated operation B'.
  - The ProseMirror rich-text editor’s built-in collaborative editing system rejects operations like B. Upon learning of this rejection, Bob’s client will compute a rebased operation B' that “does the same thing” to the new document state, using ProseMirror’s built-in rebasing function, then submit B' to the server.
  - In git, if you git push to a remote branch that has more commits (= operations) than your local branch, the remote branch will reject your push. You can then use git pull --rebase && git push to download the new state, rebase your local commits, and retry. Note that unlike in most real-time collaborative apps, this might require human input.
  - Note that serialization does not actually solve the rebasing problem; it just defers it to clients, who must rebase the operations themselves. Also, in apps with many active users, frequent rejections can lead to performance issues and even lock out users—see StepWise’s ProseMirror blog post.
- CRDT-ish
  - Operations are designed to “make sense” as-is, even when applied to a slightly newer state. 
  - I call this approach “CRDT-ish” because CRDTs also use operations that can be applied as-is to newer states. Thus studying CRDT techniques can help you design operations that “make sense” like in the examples above.
  - Note that you don’t need to use literal CRDTs, which are often overkill in a central server app. In particular, your operations don’t need to satisfy CRDTs’ strict algebraic requirements (commutativity / lattice axioms). Whether operations “make sense” in new states is instead a fuzzy, app-specific question: it depends on your app’s business logic and what users expect to happen, and it’s okay to be imperfect.
  - I personally find designing CRDT-ish operations a lot of fun, though it can require a special way of thinking. From the server’s perspective, it just needs to apply operations to its state in serial order, which is dead simple.
  - Performance-wise, literal CRDTs were historically criticized for storing lots of metadata. This is less of a problem with modern implementations, and the central server can help if needed.
- OT-ish
  - the server transforms B against A, computing a new operation B' that is actually applied to the state. More generally, the server applies a transformation function T to each intervening concurrent operation in order
  - I call this approach “OT-ish” because Operational Transformation (OT) systems also transform each operation against intervening concurrent operations. As in the previous section, literal OT algorithms are probably overkill. In particular, your transformation function doesn’t need to satisfy OT’s strict algebraic requirements (the Transformation Properties).
  - OT-ish systems are well established in practice. In particular, Google Docs is a literal OT system. However, most published info about OT focuses on text editing, which is difficult but only a small part of many apps.
  - Performance-wise, OT-ish systems can struggle in the face of many simultaneous active users: the server ends up doing O(# active users) transformations per operation, hence O((# active users)^2) transformations per second. Also, the server needs to store a log of past operations for transformations, not just the current state. You can garbage collect this log, but then you lose the ability to process delayed operations (e.g., users’ offline edits).

- There is one case where server-side rebasing is especially tricky, no matter which of the three above solutions you use: editing text and lists. (Extensions to text, like rich text and wiki pages, are likewise hard.)
  - This “index rebasing” challenge is best known for real-time collaborative apps like Google Docs, but technically, it can also affect non-real-time apps—e.g., a web form that inserts items into a list. The problem can even appear in single-threaded local apps, which need to transform text/list indices for features like annotations and edit histories.
- Solutions to the index-rebasing problem fall into two camps:
  - Immutable Positions (CRDT-ish). Assign each character / list element an immutable ID that is ordered and moves around together with the character. I call these positions.
    - Fractional indexing is a simple example: assign each character a real number like 0.5, 0.75, 0.8, …; to insert a character between those at 0.5 and 0.75, use an operation like “add character 'x' at position 0.625”, which will end up in the right place even if the array index changes. Text/list CRDTs implement advanced versions of fractional indexing that avoid its main issues.
  - Index Transformations (OT-ish). Directly transform index 17 to 22 in situations like Figure 2, by noticing that a concurrent operation inserted 5 characters in front of it. This is normal OT-ish server-side rebasing, but it is hard because there are a lot of edge cases—e.g., how do you transform an insert operation against a delete operation at the same index?
- Typically, solutions to the index-rebasing problem are implemented as literal CRDT/OT algorithms inside of a full-stack CRDT/OT collaboration system. This can be quite restrictive, if you need the algorithms for text editing but otherwise want to make your own collaboration system (for custom server-side business logic, more control over the network and storage subsystems, etc.).
- To alleviate these restrictions, I’m interested in tools that solve the index-rebasing problem using local data structures, independent of a specific collaboration system:
  - For CRDT-ish systems, I created the list-positions library.
  - For OT-ish systems, ProseMirror’s built-in rebasing function is a good example. ProseMirror’s author provides some perspective on why literal OT is overkill here.

- To incorporate optimistic local updates into our earlier abstract model, let us assume that each client has access to a reducer function à la Redux.

## 🆚️ [tinymce: To OT or CRDT, that is the question_202001](https://www.tiny.cloud/blog/real-time-collaboration-ot-vs-crdt/)

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

## 🆚️ [ckeditor5: Lessons learned from creating a rich-text editor with real-time collaboration_201802](https://ckeditor.com/blog/Lessons-learned-from-creating-a-rich-text-editor-with-real-time-collaboration/)

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
