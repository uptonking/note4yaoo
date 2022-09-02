---
title: lib-editor-prosemirror-community-plugin-extension-command-utils
tags: [community, extensions, plugin-system, prosemirror, utils]
created: 2022-08-30T22:05:05.301Z
modified: 2022-08-30T22:07:26.164Z
---

# lib-editor-prosemirror-community-plugin-extension-command-utils

# guide

# discuss
- ## 

- ## props to plugin views
- https://discuss.prosemirror.net/t/props-to-plugin-views/4672
  - What’s the best way to pass props into plugin views so that they update when props change (not only when state changes)?

- This is Prosemirror tied into a bigger system, and the problem I’m having. 
  - I can’t pass props i.e. app state (or app services, but I didn’t show them here) into editor plugin views.
  - Like state about the theme colors, or global user font preference, etc.
- Here are four possible options to fix the problem.
- You can use a “props” plugin which goes into the editor state, and you just have to make sure to update it every time the app state changes.
- The second option is to just lift plugin views out of prosemirror and just make it your app view’s responsibility. 
  - Now you just read the plugin state through the editor state and use whatever services you need. 
  - Basically you make it the App’s responsibility to render the plugin views.
  - This is, imo, the “right” approach. 
  - In an ideal world, you shouldn’t even need the EditorView component when integrating Prosemirror into a bigger system. 
  - It gets replaced by the App view and EditorState gets rendered as part of it.
- The third approach is using observables/subscriptions like cole suggested or in my initial post. 
  - I didn’t bother to figure out how to draw this, but in mount you pass in those subscriptions as the “initial” props to the Editor View.
- The fourth approach is inventing some new concept in Prosemirror to support this. I’m not really sure what it would look like; Maybe the EditorView becomes a function of state and props where props is any object.

- Plugin views have their update method called as normal when the editor’s props change. Except when the state is reconfigured—then they are destroyed and recreated entirely.
- That sounds like a concept entirely outside ProseMirror. Put it in a state field and update it when it changes using a transaction, if you want to tie it into ProseMirror’s update cycle.

- ## state and view plugins

 - [Separating state and view plugins](https://discuss.prosemirror.net/t/separating-state-and-view-plugins/3970)

- [Generalized State Architecture](https://discuss.prosemirror.net/t/generalized-state-architecture/3908)
