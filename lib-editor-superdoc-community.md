---
title: lib-editor-superdoc-community
tags: [community, superdoc]
created: 2026-04-20T00:35:30.825Z
modified: 2026-04-20T00:35:49.933Z
---

# lib-editor-superdoc-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [feat(superdoc): deprecate ProseMirror internals and editor commands (SD-2434) by caio-pizzol · Pull Request · superdoc-dev/superdoc _202604](https://github.com/superdoc-dev/superdoc/pull/2674)
  - Adds soft deprecation for ProseMirror internals and editor commands ahead of the planned PM removal, steering consumers toward the Document API (editor.doc).
  - Runtime deprecation Proxy at the consumer boundary (onEditorCreate callback) — logs one-time warnings per deprecated property access
  - Internal code paths unaffected — Proxy only wraps the editor handed to consumer callbacks

- the current editor engine is still ProseMirror-centered for editing, but SuperDoc does not render from ProseMirror DOM. It renders through its own pipeline, with a hidden ProseMirror editor behind the scenes.
  - That split gives SuperDoc strong rendering control, but it also creates a fragile bridge between the visible surface and the hidden editing engine.
  - Remove ProseMirror as the public/editor-core dependency. The docs repeatedly say direct ProseMirror access is deprecated and will be removed. The replacement surface is the engine-agnostic Document API.
  - Improve large-document performance by reducing editing-engine overhead and leaning on the newer layout infrastructure. The repo already has incremental layout, virtualization, debounced passes, and performance budgets, which look like building blocks for a stronger v2.

- IME/composition input is bridged, not native on the visible surface. The visible layout surface forwards keydown, beforeinput, input, and composition* events into a hidden editor DOM via synthetic events. For Chinese/Japanese/Korean IME, that is exactly the sort of setup where composition state can drift and characters can appear, disappear, or get reverted.
- Focus and scrolling fight the hidden editor. The hidden host exists partly to stop the browser from auto-scrolling toward the off-screen contenteditable caret, which would conflict with SuperDoc’s own scrolling/virtualization
# discuss-roadmap
- ## 

- ## 

- ## 

- ## [Chinese IME input intermittently fails _202603](https://github.com/superdoc-dev/superdoc/issues/2581)
- We found the issue - the editor sometimes drops or reverts Chinese characters mid-input. The root cause is a limitation in the editing engine we use today, which we're replacing as part of a bigger upgrade already underway.
  - This update is part of the top priority Core Editor v2 project at SuperDoc, which includes significant performance improvements on large documents and overall rendering improvements.

- ## [SuperDoc Product Roadmap  _202602](https://github.com/superdoc-dev/superdoc/issues/1982)
- Expanded List Styles & Interactions 
- Insert template fields with predefined content like tables and lists.
- 
- 
- 

- ### released
- Expanded Document API + SDK/CLI Capabilities (Alpha)
- Robust CSS Variable & Theming System
- 
- 
- 
- 

# discuss-issues
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
