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

- ## I love Discord, but I wish it had a better text editor for message input. 
- https://twitter.com/trueadm/status/1645797085768458240
  - The amount of times it messes up autocorrect and IME is so frustrating. 
  - It also often breaks completely when using some complex IME functionality and I'll have to restart the entire shell.
  - I did some digging into it and it looks like it's because they use Slate. That explains everything.
  - Ironically, Lexical would fix all these issues and be smaller in code size, have better React 18+ compatibility and have much faster runtime performance. Just saying.
- I spent a ton of time making Lexical so much better than what there already was. To be fair ProseMirror got a lot right and we learnt a lot from their tricks. I think there ultimately needs to be a new way of doing this on the web as a standard.
  - Battling web extensions that mutate the DOM directly, to having document.execCommand, to having differences in how different browsers implement `keydown` , `compositionstart` , `input` and `beforeinput` just compels the probem.
- I'm curious - what does lexical do differently that avoids these issues?
  - For one, Lexical has its reconciler rather than using React’s. This means that Lexical’s internal editor state is the source of truth, and any external mutations to the DOM get detected and reverted, enforcing this.
- Lexical is really good. We’re building a bunch of new stuff on top of it at Adobe. 

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
