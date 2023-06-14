---
title: lib-editorjs-issues
tags: [editorjs, issues]
created: 2020-11-17T09:38:33.792Z
modified: 2020-11-17T09:39:37.776Z
---

# lib-editorjs-issues

# faq-not-yet

# faq
- ## [Is there a "view" mode vs "edit" mode?](https://github.com/codex-team/editor.js/issues/914)
- read-only mode is published with v2.19(202011)
- Looks like we need to render the HTML ourselves with the clean data, which editor js provides. 
- [JSON to back to html, How?](https://github.com/codex-team/editor.js/issues/676)
  - I've created a editorjs-parser package for this purpose. 

- ## [Paste from Microsoft Word](https://github.com/codex-team/editor.js/issues/729)
- The problem is that Editor.js is not actually WYSIWYG.
- Surely some plugins might look like WYSIWYG components 
  - but the way of rendering is up to you 
  - and HTML output (or any other) might look completely different from how it looks in the editor.
- I've tried to handle paste from MS Word, 
  - the data from Word comes in RTF format (text/rtf). 
  - It can be parsed, converted and passed to the plugins on the client 
  - but there is too much data, browser just can't process it and gets crushed.
- I've made a few observations trying to get Copy + Paste from MS Word into Chrome on MacOS, and here's what I've found. 
  - My only goal has been to support bold, italic and anchor tags with href property. 
  - I do not want to copy in any other markup or images.
  - When I copy + pasted from MS Word into Chrome, nothing would happen. 
  - However it works properly in both FireFox and Safari without any intervention from me. So I did a little digging.
# issues-not-yet
- ## [[Suggestions for collaborative editing scenario] Reconstruct read-only mode logic](https://github.com/codex-team/editor.js/issues/2265)

- ## [Optimize the rendering by using a diffing algorithm](https://github.com/codex-team/editor.js/pull/1606)
# discuss-collaboration
- ## 

- ## 

- ## [💡 Real-time collaborative editing with editor.js](https://github.com/codex-team/editor.js/discussions/1874)
- 蓝湖: we have implemented collaborative documentation (including collaborative cursors) using editor.js + yjs and we are now live.
  - https://github.com/hughfenghen/y-editorjs

- Recently(202303), I tried to make a binding between the YJS and EditorJS. I think the EditorJS(v2.x) has some issues with compatibility design for the collaboration scenarios.
  - **Absent the reactive & incremental state of EditorJS**. updates from other remote clients to local will only use the update method of the block’ API. 
  - **Too many unnecessary DOM mutations in the EditorJS’s internal**.
- Thank you for your research! We were discussing exactly the same problems internally. Therefore we are working on the architecture redesign to enable reactive data-first approach.
  - That is a challenging problem as existing solutions usually work with known in advance set of content blocks. Whereas Editor.js core doesn't know much about connected Tools. We are on the research stage now

- ## [Collaborative editing based on yjs](https://github.com/codex-team/editor.js/discussions/1892)
- yjs

# discuss
- ## 

- ## [Undo operations by Ctrl+Z](https://github.com/codex-team/editor.js/discussions/1868)

- I've been using immer for a project recently and adding in my own undo / redo functionality was trivial. It is a great library because it offers the ability to use "patches", which are records of the individual pieces of your JSON tree that you have changed on your object.

- The performance for editorjs-undo is unbearable. I've had to fork the undo plugin to support slices of what's changed. However, I have had no luck in getting what has changed from editorjs 

- ## [CRUD via block ID](https://github.com/codex-team/editor.js/issues/1684)
  - I'm interested in having the opportunity to perform CRUD operations based on ID. 
  - This is vital(必不可少的，极重要的), as the ID is the key in the YMap data structure shared across various clients. So, on the update triggered remotely, I have to propagate this update to the editor.js instance and, specifically, swap the block content.
  - the Blocks Core API lacks the BlockManager.insert() invocation with id (and replace boolean - ideally used to signify replacement by id and not by index) - for the creation (and update).
