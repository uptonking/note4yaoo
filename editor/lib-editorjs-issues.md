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
