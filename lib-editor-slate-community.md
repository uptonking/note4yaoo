---
title: lib-editor-slate-community
tags: [community, slate-editor]
created: 2022-05-15T18:42:49.773Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-community

# discuss

- ## 

- ## render code in text
- https://twitter.com/jitl/status/1649507571386949645
- We've had this in our backlog since 2019 but haven't gotten around to it for a few reasons:
  - Rendering the caret "inside" is tricky
  - Keeping the caret "inside" as you type is a bit more tricky
- We could draw our own caret and hide the browser one, but that breaks native stuff like long-press iOS keyboard trackpad (try in @googledocs @whimsical to see what I mean).
- 💡 it's possible to write a big state machine and sometimes ignore the browser's idea of caret position... and we did... but the more we fight the browser, the more bugs we get.
  - We could break free with totally custom text rendering & input (like Google Docs), but that's a huge investment – one we're not ready to make yet.

- I’m no longer at Facebook but I don’t think there’s much appetite(强烈欲望) perusing a canvas based solution. 
  - There’s far too many trade offs that you’ll make - not to mention that lack of using the DOM means hooking up existing content via React will not be possible or very difficult.
- Canvas only is a non-starter, but what about separating the input element from the rendered UI and building enough layout smarts like Google Doc’s current architecture?
- You’d be best doing what VSCode does in that case with the hidden input. Except that breaks web a11y tooling and that is just an unacceptable compromise imo, unless you want to ship MBs of JS and reimplement the world. There’s no ideal thing here, if there was, we’d be doing it.
  - I think that we can possibly tackle this holistically with WASM and canvas someday when we have access to the IME and low level input interfaces directly.
- I’ve been thinking about a system where the input and render elements are almost identical and layered on top of each other in the Z axis. Need to work hard to have low latency, but at least you can mutate the render DOM without disrupting IME
- I think Coda does it this way too. For selection, focus would be on the back-layer “input” contentEditable=true, but you’d need to draw your own artificial selection range on the foreground contentEditable =false “render” element
- Yeah that’s what I meant about selection issues. Drawing a fake selection range over adjacent block nodes is complex, slow and buggy. So those editors just forbid complex inline embeds. They also don’t support speech to text, so you have tons of complaints from Dragon users.

- Any reasons why Notion wasn't built on top of an abstraction like Prosemirror?
  - Notion predates ProseMirror. We’ve assessed rebuilding on it, but found limitations in CJK & Android. The risk&cost to adopt outweighs the reward.
  - Our time would be better spent separating input handling from rendering. Using the same element for both is a dead end.

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
