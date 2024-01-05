---
title: lib-editor-prosemirror-community-compatibility-interoperability
tags: [community, compatibility, interoperability, prosemirror]
created: 2022-08-30T22:02:27.964Z
modified: 2022-11-14T20:12:58.259Z
---

# lib-editor-prosemirror-community-compatibility-interoperability

# guide

# discuss
- ## 

- ## 

- ## 

- ## If there is a common and sane standard of Blocks inside Markdown - many systems will be interoperable. _202310
- https://discord.com/channels/1050770647564943402/1051327545288704130/1161333191135735921
  - GitHub is big, way bigger than Obsidian. So the way they do it - will likely set the standard.
  - I can't see what GitHub is going to do.
  - The way examples presented at https://blockprotocol.org/hub makes me think the readability was not among the goals. It is simply too verbose.
  - If GitHub just slaps JSON with full property names there - everyone including Obsidian would have to follow. This will work in some ways, but will be sub-optimal in others. 

- RIP GitHub Blocks experiment. I really hope they'll give the Block Protocol another chance as it becomes more mature!

- ## Hooking into other content-editables
- https://discuss.prosemirror.net/t/hooking-into-other-content-editables/4893
  - I am looking for creating a browser extension that checks for grammar in real-time (similar to Grammarly extension). That requires to draw rectangles on a virtual layer and keeping them up-to-date, which is basically handled in vanilla JS. 
- You could create a view and not add it to the DOM. But it’s probably more practical to leave out the view and just work with an editor state if you don’t want to display the editor.

- ## ProseMirror as a client for editing Google Docs
- https://discuss.prosemirror.net/t/prosemirror-as-a-client-for-editing-google-docs/3665

- https://github.com/Financial-Times/structured-google-docs-client
