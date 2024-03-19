---
title: lib-editor-lexical-dev
tags: [lexical-editor]
created: 2022-05-15T18:36:57.252Z
modified: 2022-05-15T18:37:07.368Z
---

# lib-editor-lexical-dev

> An extensible text editor framework that does things differently

# guide
- features
  - Fast
    - Lexical is minimal. 
    - It doesn't directly concern itself with UI components, toolbars or rich-text features and markdown. 
    - The logic for these features can be included via a plugin interface.
    - Lexical exposes a set of individual, modular packages that can be used to add common features like lists, links, and tables.
  - extensible
    - Nodes can be extended to add or change behavior and simple, imperative APIs make it a breeze to build for custom use cases.
  - Reliable
    - Lexical is comprised of editor instances that each attach to a single content editable element. 
    - A set of editor states represent the current and pending states of the editor at any given time.
  - Accessible
    - compatible with screen readers and other assistive technologies.
  - framework agnostic

- who is using #lexical-editor
  - ghost-cms
  - webstudio

- lexical-resources
  - https://lexical.dev/docs/intro
# faq-not-yet
- editor.update(()=>{}) 和 immer 更新的原理相同吗
  - When starting a fresh update, the current editor state is cloned and used as the starting point. 
  - From a technical perspective, this means that Lexical leverages a technique called double-buffering during updates. 
  - There's an editor state to represent what is current on the screen, and another work-in-progress editor state that represents future changes.
  - Creating an update is typically an async process that allows Lexical to batch multiple updates together in a single update – improving performance.
# [Rethinking Rich Text: A Deep Dive Into the Design of Lexical - Acy Watson_202210](https://www.youtube.com/watch?v=EwoS0dIx_OI)
- problems with draftjs
  - code size
  - modularity
  - rendering performance
  - input method/ime
  - accessibility

- design of lexical

- lexical-concepts
  - EditorState
  - Node
  - update
  - transform
  - commands
  - event-listeners

- nodes
  - element has children
  - leaf has no children
  - both element and leaf can be extended
  - decorate node

- updates 
  - pendingState > activeState

- update workflow
  - editorState
  - update1  update2  update3
  - pendingState batched
  - reconciler
  - dom

- transform
  - has access to new state before commit to dom

- listeners
  - connection to update

- dom events usually dispatch commands, internal event system
  - commands support priority
# dev
- ## [Add an experimental Table component in React_202209](https://github.com/facebook/lexical/pull/2929)
  - This PR adds an experimental React-based table implementation to the playground. 
  - It aims to emulate all the existing behavior of the current table implementation – without needing to features in core, and without suffering some of the drawbacks that come from having a pure Lexical implementation ( 💡 lack of sorting, filtering etc). 
  - The only downside is that collaboration's behavior is now slightly less than optimal, as cursors no longer show within the tables.
# more
