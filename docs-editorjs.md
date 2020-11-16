---
title: docs-editorjs
tags: [docs, editorjs]
created: '2020-11-16T13:20:14.528Z'
modified: '2020-11-16T13:20:48.869Z'
---

# docs-editorjs

## editorjs-intro

- features
  - block-styled editor
  - clean data output in JSON
  - API designed to be extendable and pluggable

- resources
  - [awesome-editorjs](https://github.com/editor-js/awesome-editorjs)
  - [editor-config.d.ts](https://github.com/codex-team/editor.js/blob/master/types/configs/editor-config.d.ts)

- Editor.js is a block-styled editor for rich media stories. 
  - It outputs clean data in JSON instead of heavy HTML-markup. 
  - And more important thing is that Editor.js is designed to be API extendable and pluggable.

- In other classic editors, the workspace is provided by single `contenteditable` element in where you can create different HTML markup. 
  - All of us saw permanent bugs with moving text fragments or scaling images, while page parts are jumping and twitches. 
  - Or highlighting big parts of the text in the case when you just want to make few words to be a heading or bold.
  - The Editor.js workspace consists of separate Blocks: paragraphs, headings, images, lists, quotes, etc. 
  - Each of them is an independent contenteditable element (or more complex structure) provided by Plugin and united by Editor's Core.

- Classic WYSIWYG-editors produce raw HTML-markup with both content data and content appearance. 
  - On the contrary, Editor.js outputs JSON object with data of each Block.
  - You can use this data to easily render in Web, native mobile/desktop application, pass to Audio Readers, create templates for Facebook Instant Articles, AMP, RSS, create chat-bots, and many others.
  - Also, the clean data can be useful for backend processing: sanitizing, validation, injecting an advertising or other stuff, extracting Headings, make covers for social networks from Image Blocks, and other.

- API is the feature.
  - Each Block is provided by a plugin.
  - It's easy to create your own.
  - All main functional units of the editor — Blocks, Inline Formatting Tools, Block Tunes — are provided by external plugins that use Editor's API.
  - Any challenges and tasks you are facing can be implemented by your own plugins using the API. 

## Creating a Block Tool

## Creating an Inline Tool
