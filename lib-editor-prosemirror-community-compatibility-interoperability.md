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

- ## Hooking into other content-editables
- https://discuss.prosemirror.net/t/hooking-into-other-content-editables/4893
  - I am looking for creating a browser extension that checks for grammar in real-time (similar to Grammarly extension). That requires to draw rectangles on a virtual layer and keeping them up-to-date, which is basically handled in vanilla JS. 
- You could create a view and not add it to the DOM. But it’s probably more practical to leave out the view and just work with an editor state if you don’t want to display the editor.

- ## ProseMirror as a client for editing Google Docs
- https://discuss.prosemirror.net/t/prosemirror-as-a-client-for-editing-google-docs/3665

- https://github.com/Financial-Times/structured-google-docs-client
