---
title: lib-editor-slate-community
tags: [community, slate-editor]
created: 2022-05-15T18:42:49.773Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-community

# discuss

- ## 

- ## 

- ## 

- ## What was the reason that made you migrate from slate.js to prosemirror?
- https://twitter.com/Priest748/status/1615524405031100419
- It crashed the whole app randomly at a very high frequency.
The team can not find a way to handle such situation because it's just a react component, you can use error boundary to avoid whole app crashing, but some random render error do nothing for debugging. Then I step in.
- I invested the quill.js, slate.js, and prosemirror. Prosemirror support all the features the others can support.
  - It's pure JavaScript, you can debug it like a normal app.
  - It more extendable with the plugin system. more mature and still under development.

- ## [consider migrating from Immutable.js "Records" to plain objects_201810](https://github.com/ianstormtaylor/slate/issues/2345)
- Ian suggested (#259 (comment)) that Slate should be unopinionated about OT/CRDT considerations.
  - as far as I know, the Slate data model doesn't consider absolute reference of its atoms, which is the key point in CRDT : the problem with indexes is that they shift, how would you find the location of a Slate change in the counterpart model ?
- I'm interested in Slate being able to support CRDT, however I have yet to see a CRDT approach that I think feels viable for nested documents and for real-world use cases where documents don't balloon to huge sizes. For that reason most of Slate's collaborative support has been focused on making OT possible first, which it already is today with the current codebase.
- 
- 
- 
