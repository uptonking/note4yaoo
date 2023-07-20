---
title: lib-editor-prosemirror-community-collab-transform
tags: [collaboration, community, prosemirror]
created: 2022-08-30T21:50:15.380Z
modified: 2022-10-22T18:47:16.228Z
---

# lib-editor-prosemirror-community-collab-transform

# guide

- 编辑器协作在线示例
  - https://atlaskit.atlassian.com/examples/editor/editor-core/collab
  - https://github.com/jure/pubsweet-blogger/tree/master/server/component-atlaskit-collab
  - [How to implement real time collaboration in atlaskit editor? 参考 yjs-atlaskit](https://stackoverflow.com/questions/59622112)
# discuss-collab-transform-operation
- ## 

- ## 

- ## 

- ## 

- ## yjs 提供的 y-prosemirror 的 undo plugin还有点bug
- https://t.me/xheldon_tech/2982
  - undo-plugin 会对ydoc进行监听变化
  - 这个挂载监听的逻辑写在了 pluginState 的 init 钩子里面 而 销毁监听的逻辑 写在 pluginView的destory里面
  - 现在我对pm的state调用一次reconfigure，这个destory会执行一次，但是这个plugin会被复用所以init不会执行，然后监听就丢失了
  - undo功能就无效了

- tiptap 2.0 已经采用了 这个 issue114 的方案临时修复了

- 官方说众筹到 3w 刀就重构

- ## ❓ 仍未解决 [Implementing google docs like "suggest edit" mode](https://discuss.prosemirror.net/t/implementing-google-docs-like-suggest-edit-mode/5033)
  - Implementing comments was easy enough, however I’m a bit at a loss when it comes to implementing something like Google Doc’s “suggest edit” mode.
- What you’re trying to do is one of the hardest things that you could try 
  - What I’ve seen working at various products is changing the default `dispatchTransaction` method, and replacing every transaction with another one that includes the added “removal” / “addition” marks.
  - That puts everything on its head, there are a ton of corner cases.
  - For example: Since a transaction can have multiple steps you have multiple steps and now you replace every step you have to re-map all the steps before transforming them.
  - I ( with my company ) plan to come out with a plugin that can solve this this problem since a ton of people try to solve this, hopefully we’ll find a time for that.

- ## [Question about track-changes with prosemirror-changeset](https://discuss.prosemirror.net/t/question-about-track-changes-with-prosemirror-changeset/3801/7)
- Yes each Span has was it data payload that can contain arbitrary data. Then you can define your own method for joining spans to merge them properly.

- 🤔 Is there a way to persist changeset? Maybe in a DB in JSON format?
  - Not currently, I think. **The typical approach is to persist steps and rebuild changesets on-demand**.

- ## [How to combine multiple transactions](https://discuss.prosemirror.net/t/how-to-combine-multiple-transactions/4386)
- This isn’t supported in ProseMirror—because they may include opaque metadata that describes exactly the changes that transaction makes, arbitrary transactions can’t be combined.

- ## [Combine Multiple transactions into one history step](https://discuss.prosemirror.net/t/combine-multiple-transactions-into-one-history-step-solved/2486)
  - How would I go about it if I wanted all the changes to be included in just one history step ? 
- Combine the changes into a single transaction.
- I have now added every change as a step to a transaction and dispatch that transaction only once. Seems to work fine

- ## [Merging steps in collab](https://discuss.prosemirror.net/t/merging-steps-in-collab/602)
- Can collab be extended to support merging ?
  - As I repeatedly said in the other thread, no.

- ## [Collab editing — step grouping](https://discuss.prosemirror.net/t/collab-editing-step-grouping/1168)
- a collab implementation should batch transactions at least on the same granularity as applyTransaction

- ## ProseMirror, YJS and decorations tip__202201
- https://discuss.prosemirror.net/t/prosemirror-yjs-and-decorations-tip/4368
  - since a ton of people are using YJS now I thought I’d share a workaround for the decorations mapping issue 
  - ( when external changes are coming into YJS it replaces the whole document, causing DecorationSet.map to return an empty array, effectively deleting decorations ).
- Just use YJS absolute positions in the plugin state, and create decorations from that.

- ## Offline, Peer-to-Peer, Collaborative Editing using Yjs__202001
- https://discuss.prosemirror.net/t/offline-peer-to-peer-collaborative-editing-using-yjs/2488
- I haven’t dug into the y-prosemirror code in depth yet, but, is there any way with Yjs fragments to model changes that happen to a fragment as steps rather than replacing the whole document? 
  - It seems like in the current implementation of the sync plugin, **every synced change ends up replacing the whole document**  (taking care to maintain the local selection state, and managing the undo state with a Yjs specific plugin). 
  - Basically what I’m curious about is whether you could replicate ProseMirror data using Yjs, but still write ProseMirror plugins without needing to “know” that Yjs was handling remote state updates (e.g. where you could, for example, rely on transaction steps + step maps to figure out what ranges have changed during a given remote sync).
- Oh, no, that does seem like a sure way to break almost every ProseMirror plugin ever written.
- Yes, there is. I gave an outline here: ProseMirror + CRDT's? . 
  - 👉🏻️ The idea is to compute the steps based on the diff of the new and the old state of the document.
  - From my personal experience computing “minimal diffs” is a bit expensive and unnecessary for my use-cases. I’m still a bit indifferent about this feature. 
- From a p2p point of view, transactions (especially the order in which transactions are applied) are not as expressive as the Yjs document changes combined with relative positions. Still, I’m looking for ways to combine these two worlds in a way that makes sense.
- I’m not denying that it will break some ProseMirror plugins (i.e. plugins that render using decorations and ProseMirror mappings). 
  - But I have tested y-prosemirror successfully in Atlaskit and TipTap. 
  - For the reasons mentioned above I also needed to replace ProseMirrors history plugin with Yjs-based history plugin (y-undo-plugin).

- my question was not because it’s wrong to route around ProseMirror transactions, just that it will complicate plugins that rely on transactions containing valid steps/step maps. 
- The main thing that we use, by way of example, that wouldn’t work without some kind of transaction mapping is indeed decorations; the ability to map positions transaction-wise is what allows us to do efficient transaction-wise computations only when needed (e.g. only recalculating a data structure for the parts of the document that have changed). 
  - If the tradeoff here is how expensive it is to compute the diffs that happen as part of a Yjs update vs. how full resolution the diffs are, for my part, I’d be happy with marginally lower resolution diffs 

- >　From my personal experience computing “minimal diffs” is a bit expensive
  - **Comparing structure-sharing trees should actually be doable really efficiently** (since you can skip all the shared nodes right away). 
  - (There was an implementation of this in a very early ProseMirror system that relied on it for its redrawing algorithm, and it wasn’t very complicated.)

- what I think is the crucial feature is that it works serverless. No central instance you need to trust and end-to-end encryption is also doable.

- I do use the prosemirror state. 
  - But for me, the question was if it makes sense to use ProseMirror transforms to represent document changes. 
  - Currently, I simply replace the document state. This is easier to do for me.
  - I didn’t see any immediate benefit in Transforms, because they are mainly used to calculate change maps and to provide undo-redo functionality. 
  - y-prosemirror has an equivalent to change maps and undo functionality, that work better in p2p scenarios. 
  - But @saranrapjs brought up a good point for ProseMirror transforms.
  - Today I started to adapt the code to use ProseMirror transforms instead. So don’t worry, you will get your transforms; I also think it makes sense to support existing plugins.

- The use of Web RTC and peer-to-peer is impressive, however if I understand correctly this relies on at least one PC up and running and accessible over the Internet at all times, in order for other devices to come and go and all instances keep in sync.
  - I can envisage this becoming a problem in the real world. Instead I’d like to (optionally) see the ability to have a central server which was always up to date as these clients come an go. Ideally all data on this server would be encrypted by a key only the end-users know, therefore maintaining data privacy.
- Isn’t this solved by websockets? There’s a yjs websocket client and server library
- you also need a database adapter for persistence while offline. Indexeddb is one way to do that.

- Yjs by itself is just a small CRDT implementation. 
  - There are several modules around Yjs that allow you to do different things.
  - Editor bindings, like y-prosemirror, y-codemirror, or y-quill make a specific editor collaborative. 
  - Connectors, like y-webrtc, or y-websocket handle how to sync to other peers
  - Persistence adapters handle how to persist data to a database to make it available offline (e.g. y-indexeddb for the browser, or y-leveldb for the server).
- The idea is to make Yjs as modular and unopinionated as possible and build a huge ecosystem around it. 

- It looks as if replacing the entire doc at once when syncing changes is a bit of a deal breaker in many contexts, especially for large documents and when you have to track positions or create lots of decorations. Has anyone been able to do an approach that utilizes a diff or some other mechanism to do smaller, more targeted updates?
  - Basically you could serialize the Y.js document to an HTML document, parse it into a prosemirror document, run a diff between the parsed doc and the current doc, then dispatch the recreated transform

- 👉🏻️ The current(202201) approach will work fine as long as you don’t use too many decorations. 
  - Replacing sounds bad, but as I explained before, ProseMirror will only apply the diff to the DOM. 
  - The replacement is efficient because y-prosemirror preserves the identity of the nodes.
- However, working with decorations and y-prosemirror has been one of the biggest pain points. It’s particularly hard to share decorations between collaborators. 
  - Not that it’s impossible, it just requires working directly with Yjs based relative positions that rever to the Yjs model and sync them to the ProseMirror state. I feel we need better abstractions.
- The y-prosemirror binding is one of the most used editor bindings for Yjs. This was my first implementation and I think there is a lot of room for improvement. Especially the change-tracking / versioning extension is just an ugly hack that I made possible for the FOSDEM demo.
- I’d like to create a rewrite this year with the feedback that I accumulated. A big focus will be to enable offline-editing scenarios. This will include:
  - A cleaner codebase.
  - Applying minimal diffs to ProseMirror without losing decorations.
  - A better abstraction around tracking shared positions that will replace the too complex relative position API.
  - An extension to track shared decorations that are synced between collaborators (e.g. for implementing comments).
  - A rewrite of the snapshots API to create a nice abstraction for implementing change tracking.
  - Potentially using the new move API to handle split-node scenarios better. 
- I talked to another editor project and we thought about creating a common abstraction around editor bindings. There are a lot of similarities between editor projects and how they represent editor state. The “editor abstraction” will handle representing editor state efficiently using Yjs’ types and provide a common abstraction for editor projects.

- 👉🏻️ I think it’s more than just decorations that are problematic. You run into the following the problems with replacing the whole doc
  - Tracking positions in plugin state becomes nearly impossible. You have to use Y.js positions only which may not work
  - Nodeviews get constantly re-rendered. For example if you have a React integration, all of your React node views re-render which causes a huge performance bottleneck
  - Plugins that use appended transactions on just affected positions will now have to iterate over the entire document to apply their changes. This can cause a giant bottleneck for larger notes
- We’ve also had issues with how opinionated the structure of the Y.doc is. 
  - It uses a 1-1 mapping of whatever the schema is defined as and bypasses any use of serialization. 
  - This means that if you want to save your content with a different structure than the exact Prosemirror document, you can’t use the bindings. 
  - We also have scenarios where certain Prosemirror nodes have children that are never saved due to privacy concerns and that is also not possible with the current bindings.
- I think the current bindings work if you are starting a new project and you lock yourself in to using Y.js from the beginning. However, we are experimenting with adding Y.js to a current project and we had to create our own bindings because of these limitations.

- There is another good reason why y-prosemirror syncs the ProseMirror model and not the serialized document. Concurrent edits can break a schema, resulting in a document that cannot be rendered by ProseMirror anymore. y-prosemirror syncs ProseMirror’s schema and recovers when the schema is broken due to concurrent edits.
  - For backend serialization, I suggest that you use the utility functions 9 to transform the Yjs document to a ProseMirror JSON. You can use the ProseMirror JSON and serialize it to your custom format. I wouldn’t know how to make this process less opinionated.

- ## ProseMirror + CRDT’s?__201802
- https://discuss.prosemirror.net/t/prosemirror-crdts/1190

- 💡️ I recently(201904) implemented ProseMirror plugin for Yjs (an operation-based CRDT).
  - I map ProseMirror block nodes to `YXmlElement` (a shared data type that has a node name, attributes, and a list of children) and ProseMirror text nodes to `YXmlText` (a shared text type that supports formatting attributes - a.k.a. marks).
- When the ProseMirror state changes, I compute a diff and apply the changes to the Yjs document. 
  - When the Yjs document changes, I simply create a new state based on the Yjs document and replace the old one.
- Mapping a CRDT to a ProseMirror document is not always possible, because ProseMirror has a schema that the document needs to comply to. E.g. given a blockquote that must have at least one child. 
  - If client1 deletes the first child, and client2 concurrently deletes the second child, you may end up with a blockquote without children (well, that depends on the CRDT). 
  - In this case I simply delete the node that does not comply with the schema anymore. 
  - This is why I went for the above approach of recreating the state based on the Yjs model, because manipulating the state with transformations would involve a lot more overhead. 
  - The disadvantage of my approach is that it destroys all decorations. 
  - The next step would be to find a method that only applies the diff between the old and the new state.
- Before every Yjs transaction, the current PM selection is rebased on the structure of the Yjs document so it won’t be affected by remote changes. 
  - Yjs based positions fulfill the same use-case as PM position mappings, but they work directly on the Yjs document. Internally they map to the unique id (lamport timestamp) of the character that the selection points to. 
  - After the change is applied, the Yjs based position is transformed back to an absolute PM based position that takes into account any remote change that happened.
  - I can’t omit this step, because otherwise PM might destroy the local selection when I replace nodes. 
  - Once I figure out how to apply the diff between the old and the new state, I can make use of PM mappings again and this step may not be necessary anymore.

- why CRDT didn’t work out as well for xi-editor as I had hoped
  - The title of this post is very misleading for people who don’t know about the XI project. 
  - The goal of the XI editor was to put editor components (like language server and syntax highlighting) in separate processes and let them concurrently modify the CRDT. 
  - They hoped that this would improve input latency, but explained that a synchronous model is better suited for their use case. 
  - The mentioned post is not about CRDTs for collaboration.

- ## A simple implementation of prosemirror-collab for tiptap.v1__201905
- https://discuss.prosemirror.net/t/a-simple-implementation-of-prosemirror-collab/1930
  - the prosemirror-collab example on the ProseMirror website is very complex
  - On my example a websocket-server on glitch.com is used (nice service which you can run a public socket server for free). There is also support to debounce all changes so everything is asynchronous.

- https://glitch.com/edit/#!/tiptap-sockets?path=server.js%3A31%3A0

- ## Collaborative Editor: Show Other Users Cursor Position
- https://discuss.prosemirror.net/t/collaborative-editor-show-other-users-cursor-position/1862
- A widget decoration is the easiest way to do this. Alternatively, use `coordsAtPos` to overlay something over the editor.

- [Showing selections/carets of collaborators](https://discuss.prosemirror.net/t/showing-selections-carets-of-collaborators/3155)

- ## Horizontally Scaling the Central Authority
- https://discuss.prosemirror.net/t/horizontally-scaling-the-central-authority/1356
  - By that I mean having more than one process running (potentially on different machines) and then always sending the requests to a given canvas doc to the right process and also handing what has to be done when one of the nodes goes down and things like that.

- Having that many authors in a single document likely never makes sense.
  - 👉🏻️ What makes more sense when scaling up to many servers, is to filter by URL and have different servers handle different individual documents. 
  - So for example one server can handle all messages for document 4, 10, 15, 21 and 78 and another for document 5, 6, 7, 12, 14, 99 and 278.

- ## I believe ProseMirror's OT handles all the intent-preservation requirements in the article. Without being truly distributed, of course, unless you add a vector clock or something.
- https://twitter.com/MarijnJH/status/1463272309544861706

- ## Rails Gem for Collaborative Editing with ProseMirror_202008
- https://discuss.prosemirror.net/t/rails-gem-for-collaborative-editing-with-prosemirror/3055
- I’m working on a Rails gem to make collaborative editing with ProseMirror drop-in for Rails apps.
  - I also plan to use prosemirror-recreate-steps to handle a client who goes offline for a long period with uncommitted changes. 
  - The gem stores old steps, but a client could go offline for long enough that old steps were thrown out - in this case, it would be important to not only recover the changes, but support some type of interactive merging. 
  - Again though, this likely would require UI which would have to be implemented by library users. 
  - How has this been handled by others?
- 👉🏻 prosemirror-collab’s OT algorithm isn’t ideal and wastes a lot of bandwidth retransmitting steps unnecessarily
  - but it’s basically possible to implement any OT algorithm on top of prosemirror.
  - For rails-collab, I rewrote the collaboration algorithm based on Apache Wave/Google Doc’s approach to OT. 
  - I’ve actually extracted that into an npm module
  - https://github.com/benaubin/prosemirror-collab-plus
- If you’re not doing collaborative editing, you need to somehow generate the diffs yourself. 
  - Manuscripts app released a package to handle this 
  - https://gitlab.com/mpapp-public/prosemirror-recreate-steps
  - We’ll likely be using prosemirror-recreate-steps to handle syncing after offline editing & branching
- However, we decided to avoid interactive merging if possible - the hard part is designing a UI/UX for conflict resolution that makes the process intuitive & painless for non-technical users. Git conflicts are a headache for developers - it’s not something that we want to force our writers to deal with, if possible.

- 👉🏻️ Steps need to get stored to a) catch clients up who feel behind due to a network issue or b) map a step targeting a past version of the document to apply to the current version (“rebasing”). 
  - But steps are really only useful short term - for long term history, your approach of storing the entire document is likely better for long term diffing - having to rollback the document via steps sounds painful.
- The gem approach stores steps in the database. 
  - In reality, for collaborative editing, you only need to store up to the oldest unconfirmed steps.
- Our standalone service keeps steps in memory and (at least right now) only persists the most recent version of the document. 
  - Basically, an app starts a session by providing a serialized document to our server. 
  - We spin up a V8 isolate and clients use a session key to connect to our gateway. 
  - Later, your the app issues an HTTP request to get the edited document.

- 202009 https://discuss.prosemirror.net/t/freelance-implementation-with-yjs/3115
  - to get decent performance and scaling for collaborative editing, you want to keep documents in RAM to avoid having to serialize and deserialize them, which means you preferably want to keep have every client on a document connected to the same server. We’re building custom infrastructure for this, and are considering offering it as a service.

- ## What is the difference between ProseMirror, and Quill + ShareDB?
- https://discuss.prosemirror.net/t/what-is-the-difference-between-prosemirror-and-quill-sharedb/879
  - I have a product that relies on collaborative editing for which I use Quill and ShareDB.
  - Did Prose Mirror write its own operational transforms library or is it using ShareDB? ShareDB should handle syncing of all the operations so the main thing left is to sync the cursors, using Quill’s cursor module.

- ProseMirror doesn’t use ShareDB, it has its own collaborative editing system (not based on OT, strictly speaking).

- I’ve never done it before, but my impression (please anyone correct me if I’m wrong) is that you should simply save the editor state in JSON to your DB of choice (Firebase, ShareDB, Fauna, etc) and update the editor state on the client(s) whenever there is a change of the state.

- I’ve read your article about collaborative editing on prosemirror, and I think you’re confused when you say that one of the features of OT is that “no matter in which order concurrent changes are applied, you end up with the same document.”
  - That explains why in this thread and in other articles on the internet, Prosemirror has been understood as a different model from the OT. 
  - It is true that many models like ShareDB require convergence in different orders of operations. 
  - But if you check the OT literature, you will see that there are other undo-do-redo type algorithms, like GOT, which are still OT after all, since as the name suggests, they somehow “transform operations”.

- ## How we went about prosemirror-collab at the New York Times__201908
- https://discuss.prosemirror.net/t/how-we-went-about-prosemirror-collab-at-the-new-york-times/2119
