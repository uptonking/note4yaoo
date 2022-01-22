---
title: thread-pm-base-editor-text-code
tags: [code-editor, text-editor, thread]
created: '2021-05-23T10:31:12.011Z'
modified: '2021-08-16T06:56:58.774Z'
---

# thread-pm-base-editor-text-code

# pieces

- ## 

- ## 

- ## 

- ## Ace, CodeMirror, and Monaco: A Comparison of the Code Editors You Use in the Browser
- https://blog.replit.com/code-editors
- In late 2018 Marijn announced a rewrite for CodeMirror to modernize the editor, CodeMirror version 6 with an excellent design doc. 
- **One of the primary motivators for the rewrite was adding support for touch devices**. 
- If you want a code editor that supports mobile, you should use CodeMirror 6. 
  - Ace has not-bad support but does not come close, and Monaco is unusable on mobile.
  - I'd go as far as saying that CodeMirror is probably suitable even for native applications as a webview component. 
  - Most things in CodeMirror are serializable so you can interop with the webview from your native code.

- ## It'd be neat if we could reference other files/lines of code in comments, and tooling would let you jump into and out of those links. Add `#135` at the end of a comment and you could jump to that line
- https://twitter.com/jlongster/status/1437423113139101701
  - I hate jumping around code based on how variables are referenced. Human-level docs have a much higher level of signal to noise, but currently there's no way to construct a walkable knowledge graph
- I think you’d want IDs instead of line numbers.
  - I’d love to be able to mark related code fragments and later retrieve them.
  - yeah, you'd need to resolve the line number into what Roam calls blocks. I'd want this done automatically, so it tracks an expression and knows how to link to it
- In Javadoc you do this via the "link" syntax. But you reference symbol names rather than line numbers, so the that link doesn't break when the target file is edited.
- Yea, the back refs might be too heavy for most big code bases, but would be nice.

- ## VS Code "Comment tagged templates" is sweet, such a clever idea. 
- https://twitter.com/stevage1/status/1427063995903528962
  - Get syntax highlighting for code embedded in strings by putting a comment before it saying what language it is.

- ## Would an auto-indenter that clears space-only lines ever cause problems?
- https://twitter.com/MarijnJH/status/1424650950216650754
- Ah, multiline strings. Damn
  - You probably know this, but SublimeText automatically removes trailing spaces, including in multiline strings. I’ve gotten used to it and like it a lot.
- Any language that allows if conditions without curly braces? Also python?
  - Python works correctly if you have a blank (no whitespace) line in the middle of indented code

- ## People frequently ask us what the difference between Web Sockets and @replicache is. 
- https://twitter.com/aboodman/status/1410441402366922762
  - It's a totally reasonable question if you've never tried to implement something like multiplayer or offline sync before. 
  - Another variant: what's the difference between Replicache and Firebase?
- Simplifying, web sockets (or Firebase) are a way to send data from clients to servers and back fast -- "in realtime".  If what you're trying to build is "realtime collaboration", it's reasonable to wonder if WS gives you everything you need.
  - Spoiler alert: they don't.
  - You need something like Replicache (or alternately a class of data structures called CRDTs) *and* realtime communication.
- To understand why, here's a thought experiment:
  - Imagine you are implementing a multiplayer drawing program like @figmadesign .
  - Round trip to a server - even a fancy edge server - almost always takes dozens of ms. 100ms is more realistic.
  - But if you want an experience with drag and drop manipulation that feels fluid and local, this requires the UI to respond at at least 60fps - that's 16ms per frame.
- it's clear that sending changes over a websocket to server and waiting for confirm isn't going to work.
  - Instead, you're going to have to **keep a cache of the datamodel on the client, allow user to edit the local copy (i.e., "optimistically"), then send the changes to the server (perhaps via socket)** in the background.
  - Now let's imagine that you have several users editing a drawing this way. Each time a user changes something, they send a message to server
  - What happens with this simple drawing app when everyone is doing this in parallel. Does it work? What do users see?
  - Hopefully this thought experiment makes it clear that what you get is... a mess.
  - Clients will frequently recv changes in different orders, resulting in seeing a different drawing. For one user, obj 1 is green, because they changed it to green then recv'd the "change to red" message. For other user it's red because they changed it to red, then recv'd opp msg.
  - These are super simple examples, but this gets complicated fast. 
  - This is an untenable way to build quality software. It just doesn't make sense for users to potentially be editing a copy of state which differs from other users or the server.
- Replicache is a client-side cache that makes it easier to build collaborative apps by making divergence as described above impossible. 
  - **Replicache (and more broadly, all CRDTs) allows you to edit state locally for performance**, but guarantees local state will converge(达成一致；会合；汇聚) with server later.
  - For the special case of building client-server software (aka SaaS or almost all mobile and web apps) Replicache has compelling advantages over classic CRDTs. 
- why do you call it “cache” though? Sounds like it’s not persistent state?
  - It’s persistent. It’s called a cache purposely and this gets to the difference between crdts and Replicache. The server is authoritative.
- If the server is authoritative and the client may have to rebase ops, is the model more like Operational Transforms rather than CRDT?
  - It's similar to operational transform in that the server is authoritative, but the mechanism is different. 
  - OT works by modifying operations to preserve intent when OOO operations are received.
  - Replicache does not ever modify operations server-side. Once an operation executes server-side it is final.(on the client side, one could say the operation is "modified" but a better way to think of it is rebase -- the operation replays and may compute something different).
- OT is still considered the best when it comes to unstructured text editing. And this makes sense given how it works.
  - But the Replicache approach is easier to implement, especially since it places few restrictions on architecture of backend, and works better for structured data.
- from a serious OT dev: [I was wrong. CRDTs are the future](https://josephg.com/blog/crdts-are-the-future/)

- ## If your online SaaS has a quick interaction-feedback loop (eg Figma, Google docs, etc), you still want to consider local-first approaches. 
- https://twitter.com/_paulshen/status/1418294517292175363
  - maybe don't need to go full CRDT but need something where you preserve intention history on the client.
- Interesting to compare approach of Google Docs where the collaboration has a slight delay (I assume due to CRDT syncing) vs Figma which uses (what looks like) real-time connections
  - while not "offline-first", Figma is definitely offline-capable. that combined with having multiple writer clients requires CRDT-adjacent methods. They dive into this here!
  - [How Figma’s multiplayer technology works](https://www.figma.com/blog/how-figmas-multiplayer-technology-works/)
- a devtool i'm excited about is @replicache, which provides a solution similar to figma's where you have a centralized authoritative server.

- ## Are there any great text editor libraries out there that work like GitHub’s? Markdown, with drag and drop upload support, APIs for things like tagging people., etc?
- https://twitter.com/adamwathan/status/1405278574337150977
- The GitHub editor is open source:
  - https://github.com/github/github-elements
  - GitHub's Web Component collection.
- I tried a whole bunch of markdown editors last month and ended up going with tiptap.dev. It was the easiest of all the editors to add custom behavior/config.
- I've built my own editor https://github.com/michelson/dante, it's like a medium editor with pluggable blocks (giphy, vlog, embeds, image, voice recording and more). ( the latest version is on top of @tiptap_editor, previous was written on draftjs ) oh, and I'm using tw for the doc site
- Any side-by-side Markdown editor/preview without scroll synchronization is a pill of poop.

- ## My favorite idea from Helix. Why don't text editors build AST support into text rendering? 
- https://twitter.com/jarredsumner/status/1399891268713422848
  - Remember what JavaScript code formatters were like before Prettier? That's every modern text editor reading your code.
- What do you mean by building in AST support?
  - Like .tmLanguage but it'd emit an AST instead of just tokens
- dependency graph would be cool too, I think there are some cool text editor features that could be built on top of ASTs and dependency graphs

- ## we've been working on a massive project to move the editor from Slate to ProseMirror in order to get everything working well on mobile.
- https://twitter.com/maccaw/status/1395868244876144647
  - I just successfully booted up the mobile app for the first time. Feels good!
- ProseMirror doesn't do weird stuff with preventDefault that stops Slate working on Android.
- I have gone through this exact migration, best of luck! You won't be disappointed with Prosemirror, it's a fantastic piece of software.
