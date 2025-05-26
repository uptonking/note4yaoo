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

- ## [Optimize the rendering by using a diffing algorithm _202103](https://github.com/codex-team/editor.js/pull/1606)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## [React/ReactNative in the scope _202006](https://github.com/codex-team/editor.js/discussions/1883)
  - If anyone cares, I'm porting editorJS to React Native without using WebViews (so no, it doesn't use any code from editorJS, it only shares the syntax of blocks). It's all native and performs fast even if there's thousands of blocks to render. It uses a virtualized view.
  - Don't take it as an advertise; I'm struggling with TextInput (set bold, italic, inline toolbar), and any help it's highly appreciate.
  - Well, I actually ended up writing everything native, because I couldn't load the editor in the WebView.

- Editor.js is strongly relying on browser JS APIs and DOM model.
# discuss-collaboration
- ## 

- ## 

- ## [🚨 Real-time collaborative editing with editor.js](https://github.com/codex-team/editor.js/discussions/1874)
- 蓝湖: we have implemented collaborative documentation (including collaborative cursors) using editor.js + yjs and we are now live.
- https://github.com/hughfenghen/y-editorjs /202005/ts/inactive
  - Editorjs binding for yjs

- 💡 Recently(202303), I tried to make a binding between the YJS and EditorJS. I think the EditorJS(v2.x) has some issues with compatibility design for the collaboration scenarios.
  - **Absent the reactive & incremental state of EditorJS**. updates from other remote clients to local will only use the update method of the block’ API (EditorJS v2.x doesn’t have the update method of the block’ API). 
  - **Too many unnecessary DOM mutations in the EditorJS’s internal**.
- Thank you for your research! We were discussing exactly the same problems internally. Therefore **we are working on the architecture redesign to enable reactive data-first approach**.
  - That is a challenging problem as existing solutions usually work with known in advance set of content blocks. Whereas Editor.js core doesn't know much about connected Tools. We are on the research stage now

- ## [Collaborative editing based on yjs](https://github.com/codex-team/editor.js/discussions/1892)
- yjs

# discuss
- ## 

- ## 

- ## [[Bug] Editor.js bundle size is very large _202009](https://github.com/codex-team/editor.js/issues/1321)
- 108.41 KB gzipped is "very large"? it's 2020. This is negligible for today's internet speed. It makes no sense to complicate the structure with lazy loading.

- ## [How to update some blocks, not all _202003](https://github.com/codex-team/editor.js/issues/1074)
  - i know `editor.render()` can update all blocks, Is there any way to update only a certain block?
  - I see from the source that `BlockMananger` may be able to do it, but it is not a public API.
  - If editor.js can get or update specific blocks, it may be beneficial for collaborative editing and performance.

- 202003: at the moment we can't provide a method to update a certain block, as data passed to the Tool constructor. So to update it, we need to construct the new Block with updated data and replace the old one. I don't think this approach is the best one, so we need to design a block update flow and describe it with APIs and docs.

- If you update all the blocks, the page will jump, so the user experience is very bad

- I approach to use the diff library: kpdecker/jsdiff

- ## [[Feature Request] Apply granular updates without recreating all blocks _202307](https://github.com/codex-team/editor.js/discussions/2427)
  - Look at ChatGPT and how it writes answers letter by letter. It does so by using Server-sent events (SSE) where small text parts are transmitted one by one.
  - Current APIs: Calling `editor.render({ blocks: [..] })` results in recreating all blocks in the editor, so calling it over and over again lets the editor flicker where the contents of the editor become invisible because of too much rerendering.
  - Trying to only update or insert blocks that have changed
- I was trying to accomplish this using editor.js but inthe end I couldn't get it stable enough for production. I had to overwrite almost all block tools but then I run into problems with editor undo history and lots of other difficulties
  - In the end I went to an alternative editor. 
  - By the time now I use quill, because its data model allows diffing new content to the current content and applying only chances, although its abstract model "delta" is terrible.
  - In future I will migrate to slate, because all big apps use it under the hood and it seems to be the best choice.

- I managed to get the openai api text streaming into the editor without any flickering based on your code, but have found myself exactly where you were prior to moving on - non-stop problems/bugs with editor.js, resulting in tons of additional code/plugins attempting to get the editor to work as production ready
  - While researching alternative solutions - Tiptap, Novel (based on Tiptap), Plate all look promising, and now based on your recommendation, I'll explore Slate too. 

- ## [Undo operations by Ctrl+Z _201811](https://github.com/codex-team/editor.js/discussions/1868)

- I've been using immer for a project recently and adding in my own undo/redo functionality was trivial. It is a great library because it offers the ability to use "patches", which are records of the individual pieces of your JSON tree that you have changed on your object.

- The performance for editorjs-undo is unbearable. I've had to fork the undo plugin to support slices of what's changed. However, I have had no luck in getting what has changed from editorjs 
  - We just released a beta version of editorjs-undo (v2.0.0-rc.0) that improve the unexpected behavior. _202201

- ## [CRUD via block ID](https://github.com/codex-team/editor.js/issues/1684)
  - I'm interested in having the opportunity to perform CRUD operations based on ID. 
  - This is vital(必不可少的，极重要的), as the ID is the key in the YMap data structure shared across various clients. So, on the update triggered remotely, I have to propagate this update to the editor.js instance and, specifically, swap the block content.
  - the Blocks Core API lacks the BlockManager.insert() invocation with id (and replace boolean - ideally used to signify replacement by id and not by index) - for the creation (and update).
