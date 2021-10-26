---
title: lib-editor-atlassian-community
tags: [atlaskit-editor, community]
created: '2021-06-30T19:44:25.914Z'
modified: '2021-06-30T19:45:14.504Z'
---

# lib-editor-atlassian-community

# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Meet `prosemirror-utils` package_201804
- https://discuss.prosemirror.net/t/meet-prosemirror-utils-package/1289
- Here at Atlassian we’ve been using ProseMirror quite heavily for about two years now. 
  - It’s an awesome library and it satisfies most of our requirements.
  - While working on complex features we’ve found that it takes quite a bit of time and effort to get document and selection manipulation right. 
  - We’ve found certain patterns that we follow from plugin to plugin, and a copy-pasted pieces of code around the codebase. 
  - We wanted an abstraction layer that’d encapsulate that complexity into a set of utility functions that we’d reuse.
  - We created a small library: `prosemirror-utils` with the idea in mind that we’d become more efficient and focus on developing features.

- One of the things that I’ve been wanting to do is decomposing `prosemirror-commands` into a reusable set of functions that would operate on transactions. 
  - We found that sometimes we need a slightly different behaviour from what the standard commands offer, or we need to alter the behaviour because our UX requirements change (e.g. based on user feedback). 
  - **In my mind a command could accept a `transaction` object as an argument, call a few of those transform utils and the `dispatch`**. 
  - That way it would make commands more flexible.
- Another thing that we’re planning to do is extracting lists commands from `prosemirror-schema-lists` for the same reason - we often copy the internals of a command and modify it to meet our requirements.
