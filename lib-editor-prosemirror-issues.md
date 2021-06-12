---
title: lib-editor-prosemirror-issues
tags: [editor, issues, prosemirror]
created: '2021-06-12T02:40:02.657Z'
modified: '2021-06-12T02:40:42.535Z'
---

# lib-editor-prosemirror-issues

# issues

- ## 

- ## 

- ## 

- ## 

- ## prosemirror and mermaid
- https://gitter.im/ProseMirror/prosemirror?at=59c2cbef614889d47520666a
- There are some filters for tools like pandoc that can also render them to different image formats, and the images can be embedded into transformed document formats (like PDF/DocX). 
  - Mermaid itself is a combination of a set of DSLs for different diagram types and and engine that renders the diagrams with D3.js to a SVG canvas. 
  - There's also a Markdown-previewer extension for Visual Studio Code that lets you preview the rendered markdown + diagrams on the fly, 
- Now, to my question; I've looked at the Prosemirror example where there's an option to switch between WYSIWYG and markdown. 
  - Now, is it doable to create a plugin for Prosemirror that could inline HTML canvas'es inside a contenteditable element? 
  - My goal would be that the dev could create/edit the diagrams in plain mermaid-DSL embeded in fenced code sections in Markdown, and switch over to WYSIWYG and see the diagrams inlined (but readonly).
- so it is technically feasible to have a canvas element floating inside a contenteditable element?
  - I can’t think of any reason why not.

- ## How to create a nodetype consist of an image and text with inline editing experience?
- https://discuss.prosemirror.net/t/how-to-create-a-nodetype-consist-of-an-image-and-text-with-inline-editing-experience/1326
- ProseMirror needs to be able to ‘fix’ documents to conform to the schema, for example if editing somehow yields an image wrapper node with only a paragraph inside of it, it must generate an image to satisfy the schema constraint. 
  - But because images contain attributes without a default value, it can’t.
  - One solution would be to model the node as a captioned image instead of a wrapper, with its own image src (an possibly alt etc) attribute, and inline* content, rendering as something like ["div", ["img", {....}], ["p", 0]]. 
  - That way, the node can’t get in a state where the image is missing, since it’s not part of its editable content.
  - Alternatively, use 'image? p' as content expression, so that the image isn’t required and doesn’t ever need to be generated.

- ## Block structure editor by prosemirror
- https://discuss.prosemirror.net/t/block-structure-editor-by-prosemirror/2620
- notion’s block is an independent contenteditable dom, which only has an independent node (table/calendar or other nodeType)
  - I am wandering if separate all my schema into each mini-prosemirror editor and have a doc container that holds all the mini-prosemirror, can i achieve the block structure style new editor as notion.
- You can, but I don’t see why you’d want that. **Separating your document into multiple editors breaks things like cross-block selections**. This type of setup complicates user interaction, and I never really understood what advantage it brings.
  - in my opinion, notion block structure makes it flexible to save the data, cus doc can be described as two part: block-id-list, block-content-data-hashmap
  - besides, each block has it's own menubar popover, so user don't need move mouse up to top menubar and down to editor frequently, make user experience better.
  - in my project, i want treat table as database to make table data accessable and sharable between different user's docs, maybe block style can be a little bit easier.
  - Notion’s solution to this is quite nice: dragging a selection across two blocks creates a selection containing the whole of both blocks.

- ## ProseMirror for editing page layout
- https://discuss.prosemirror.net/t/prosemirror-for-editing-page-layout/1045
  - I’m thinking about using ProseMirror for editing the layout of a blog post or similar. 
- This is probably possible — ProseMirror isn’t really written for showing content precisely as it will appear in some final output, since we take the approach that during editing you’re more interested in semantic information than in layout, but I expect it’s flexible enough to get something like this working.
- I guess dragging blocks into the editor could be made to trigger structural changes to the document. So yes, I think this’ll work well with ProseMirror. Embedding things that aren’t editable is definitely supported.
  - Depending on what your HTML looks like, contentEditable may misbehave for some complex things like having things positioned in fancy ways. You’ll have to experiment and see.

- ## Multi-column layouts
- https://discuss.prosemirror.net/t/multi-column-layouts/44
- if it is possible to have multi-column/grid layouts (not tables!) inside a contenteditable. All of them told me: nope, very messy with contenteditable.
- ProseMirror’s approach is to mostly limit the editing view to a semantic representation of the document, and leave the presentation to other parts of the pipeline.
- Using the `column-count` CSS property on the editor view works just fine.
  - 此属性大约100%的浏览器支持
  - 但给的示例大多是用来自动拆分文本，不清楚对图文混排的支持
