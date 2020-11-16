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

- each Block in Editor.js is provided by a Plugin. 
  - There are simple external scripts with their own logic.
  - There is the only Paragraph block already included in Editor.js. 
  - Probably you want to use several Block Tools that should be installed and connected.
  - [Link Tool for Editor.js](https://github.com/editor-js/link)

- Editor.js needs a bit time to initialize. 
  - It is an asynchronous action so it won't block execution of your main script.
  - If you need to know when editor instance is ready, you can pass `onReady` property to the configuration object
  - Similar to onReady callback, you can use the `onChange` callback to handle any modifications inside the Editor
  - Since the 2.19.0 version, Editor.js can be initialized in the read-only mode. 
    - That means that users won't have the ability to change the document content.

- You can specify the common order of Inline tools using the `inlineToolbar` property.

- A blocks property contains an array of objects with `type` and `data` of Editor Blocks. 
  - The values of this fields are depend on the Tools you use
  - Note that `type` field in Block data is the key of object of Editor config's `tools` property. 
  - In other words, it can be changed by you own.

## Creating a Block Tool

- In this series of articles, we will learn how to create a full-featured Block Tool step-by-step.
- We need at least of two methods to create a Block Tool for Editor.js — `render` and `save`.
- The first method,    `render`, will create a UI of a Block that will be appended when our Tool will be selected from the Toolbox. 
- The second method,  `save` — will extract the Block's data from that UI.
- Our Block Plugin is almost done. To make that appear at the Toolbox, we should provide an icon and a title with a static getter toolbox.

## Creating an Inline Tool

- Inline Tools allow you to make your text more informative. 
- The simplest examples of them are bold, italic, and underline modifiers which are commonly used.
- Every Inline Tool must provide a button — HTML element with icon or some layout — for Inline Toolbar of the Editor. 
  - When button is pressed Inline Tool receives selected text range as JavaScript Range object references to TextNode on the page. 
  - Some Tools may also provide actions for additional interactions with the user.
