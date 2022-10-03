---
title: lib-editor-prosemirror-community-collab-transform
tags: [collab, community, prosemirror]
created: 2022-08-30T21:50:15.380Z
modified: 2022-08-31T00:15:07.200Z
---

# lib-editor-prosemirror-community-collab-transform

# guide

# discuss-transform-operation
- ## 

- ## 

- ## 

- ## 

- ## I believe ProseMirror's OT handles all the intent-preservation requirements in the article. Without being truly distributed, of course, unless you add a vector clock or something.
- https://twitter.com/MarijnJH/status/1463272309544861706

- ## Rails Gem for Collaborative Editing with ProseMirror
- https://discuss.prosemirror.net/t/rails-gem-for-collaborative-editing-with-prosemirror/3055
  - I also plan to use prosemirror-recreate-steps 11 to handle a client who goes offline for a long period with uncommitted changes. 
  - The gem stores old steps, but a client could go offline for long enough that old steps were thrown out - in this case, it would be important to not only recover the changes, but support some type of interactive merging. 
  - Again though, this likely would require UI which would have to be implemented by library users. 
  - How has this been handled by others?
- prosemirror-collab’s OT algorithm isn’t ideal and wastes a lot of bandwidth retransmitting steps unnecessarily - but it’s basically possible to implement any OT algorithm on top of prosemirror.
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
# discuss-server
- ## 

- ## 

- ## Editing different “views” of the same document
- https://discuss.prosemirror.net/t/editing-different-views-of-the-same-document/3156
- I think it should be possible, if you use size-1 leaf nodes for the redacted nodes on the client but have the unredacted document on the server, to create a step map that conceptually replaces each of these (in the pre-change doc) with their actual size (by directly building up the vector and wrapping it in a StepMap). That represents the mapping from the client document to the full document, and mapping the client’s step through that should be able to create a step that can be applied to the full document. (And the other way around, you could map server steps through its inverse to get steps that the client can apply locally.)
