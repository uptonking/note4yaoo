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

- lexical-resources
  - https://github.com/facebook/lexical
  - https://lexical.dev/docs/intro
