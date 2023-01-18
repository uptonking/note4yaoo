---
title: lib-editor-slate-community
tags: [community, slate]
created: 2022-05-15T18:42:49.773Z
modified: 2022-05-15T18:42:59.469Z
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
- 
