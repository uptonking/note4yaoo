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
# discuss-server
- ## 

- ## 

- ## Editing different “views” of the same document
- https://discuss.prosemirror.net/t/editing-different-views-of-the-same-document/3156
- I think it should be possible, if you use size-1 leaf nodes for the redacted nodes on the client but have the unredacted document on the server, to create a step map that conceptually replaces each of these (in the pre-change doc) with their actual size (by directly building up the vector and wrapping it in a StepMap). That represents the mapping from the client document to the full document, and mapping the client’s step through that should be able to create a step that can be applied to the full document. (And the other way around, you could map server steps through its inverse to get steps that the client can apply locally.)
