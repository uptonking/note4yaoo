---
title: lib-editor-prosemirror-community-view-render
tags: [community, prosemirror, render]
created: 2022-08-30T22:01:06.845Z
modified: 2022-08-30T22:01:29.263Z
---

# lib-editor-prosemirror-community-view-render

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-pagination
- ## 

- ## 

- ## 

- ## 

- ## [A new text editor with pagination - Show - discuss. ProseMirror _202409](https://discuss.prosemirror.net/t/a-new-text-editor-with-pagination/6667/6)
  - https://www.badon.app/
  - https://github.com/BadonWriter  /未开源_202607
  - it comes with a completely new way of approaching the pagination problem, and thus it can even handle long documents (~300+ pages), with headers and footers.
  - It’s not a 100% finished, The project will be open sourced in the short future.
  - The pagination largely relies on CSS for the bulk of the layout work, so there’s no node splitting and barely any calculation related to height and width dimensions, which is why it’s quite performant. There are a few drawbacks though, as every element must adhere to specific constraints (I had to write a table plugin from scratch).

- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Editing different “views” of the same document
- https://discuss.prosemirror.net/t/editing-different-views-of-the-same-document/3156
  - I’ve got a use case where the editor of a document can embed “redacted(编辑，修改；草拟)” blocks. 
  - These blocks are completely stripped out of the document when it’s delivered to a consumer, who views the document in a read-only mode. 
- I think it should be possible, if you use size-1 leaf nodes for the redacted nodes on the client but have the unredacted document on the server, to create a step map that conceptually replaces each of these (in the pre-change doc) with their actual size (by directly building up the vector and wrapping it in a StepMap). That represents the mapping from the client document to the full document, and mapping the client’s step through that should be able to create a step that can be applied to the full document. (And the other way around, you could map server steps through its inverse to get steps that the client can apply locally.)

- ## List editing UX considerations
- https://discuss.prosemirror.net/t/list-editing-ux-considerations/3812
- For the sake of backward compatibility, 👉🏻 we’re not going to change the way the existing list commands work. But providing alternatives might be possible.

- ## Why is prosemirror-tables not maintained?_202204
- https://discuss.prosemirror.net/t/why-is-prosemirror-tables-not-maintained/4522
- I wrote prosemirror-tables for Atlassian with the understanding that it would be something that I’d hand off to them, rather than maintain myself.

- Marijn: I am not planning to maintain prosemirror-tables either._202111
- https://discuss.prosemirror.net/t/why-selectedcell-decoration-so-slow-in-large-document/4175/10
