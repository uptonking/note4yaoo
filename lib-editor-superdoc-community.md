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

- ## 

- ## Recommended pattern for applying SuperDoc edits into a doc open in the Word desktop app (Office.js)
- https://discord.com/channels/1299087524056010902/1526547357984882719
  - We use SuperDoc's engine server-side to apply agent-generated tracked-change edits to .docx (great for our web editor). We also ship a Microsoft Word desktop add-in (Office.js task pane) where customers work in Word's own canvas on live documents.
  - Our understanding: SuperDoc owns the document model (OOXML/ProseMirror), so it can't drive a document that's open in the Word application — the only way to inject edits into live Word is Office.js's granular API. We confirmed that whole-doc bridges ( `compareFromBase64 / insertFileFromBase64` of a SuperDoc-redlined docx) corrupt iterative redlining — Word's Compare treats pre-existing tracked changes (ours and the counterparty's) as accepted, destroying them on the second turn.
  - Is there any supported way to use SuperDoc to apply tracked-change edits into a document that's open in the Word desktop app, or is SuperDoc fundamentally a Word replacement (you own the doc) with no live-Word-injection path? For teams that must keep users in Microsoft Word, do you have a recommended architecture?
- Currently, SuperDoc cannot directly modify a document that is open in Word (with the exception of when the file is on the same machine as opposed to via a live session), but it can modify a document externally and send that document back to Word, which sounds like what you're currently doing with insertFileFromBase64.
  - For your architecture, to avoid a wholesale document replacement, I would recommend having the backend return an operation (or list of operations) that your add-in can ingest and then execute via Office.js.
  - While Office.js and SuperDoc aren't one-to-one in this aspect, there's fairly good alignment between their CRUD operations. For a non-exhaustive list of SuperDoc operations and their closest Office.js equivalents, the attached reference may prove useful.
  - we've worked with Word add-ins before, although our implementation has generally used `insertFileFromBase64` , which it sounds like you've already ruled out for this particular workflow.

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
- 👷 We found the issue - the editor sometimes drops or reverts Chinese characters mid-input. The root cause is a limitation in the editing engine we use today, which we're replacing as part of a bigger upgrade already underway.
  - This update is part of the top priority Core Editor v2 project at SuperDoc, which includes significant performance improvements on large documents and overall rendering improvements.
- 👷 202607: Core Editor V2 is still actively in progress, and it includes the editing-engine changes needed to address this Chinese IME input issue. V2 also includes major improvements to document loading, rendering, selection, editing interactions, tracked changes, and overall performance, especially for larger and more complex DOCX files.

- [Support CellSelection/TableSelection in editor.doc.selection.current() and context menu APIs  _202607](https://github.com/superdoc-dev/superdoc/issues/3806)
  - We’re currently working on a V2 version of SuperDoc that does not use ProseMirror at all, and instead uses our Document API for this kind of interaction. 

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
