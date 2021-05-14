---
title: lib-editor-community
tags: [community, editor, lib, text-editor]
created: '2021-05-14T12:04:27.547Z'
modified: '2021-05-14T12:04:55.412Z'
---

# lib-editor-community

# guide

# discuss-stars

- ## Which one was the one with the bad performance on long documents? ProseMirror or CodeMirror?
- https://twitter.com/thomasaull/status/1314484953686695936
- CodeMirror is normally much faster for big documents, 
  - but from the context, I suspect that in this case the magic layered on top to make CodeMirror behave like a rich text editor is the source of the slowness.

- ## Why is CodeMirror not based on or replaced by ProseMirror?
- https://twitter.com/tjconceptdk/status/1035585261198041088
- They solve different problems -- `structured rich text with configurable schema` versus `plain text with syntax highlighting and lazy rendering` . 
  - On the web you don't want to ship big, overly general code for a smaller problem

- I was doing some research and I was wondering why you didn't use the same textarea technique in ProseMirror as you did in CodeMirror? Is it planned or impossible to implement in a rich text editor? 😊
  - Because it is a more problematic hack than just using contenteditable. CodeMirror 6 will do the same

# discuss

- ## 

- ## 

- ## Announcing: Work is underway on CodeMirror 6, a full rewrite with accessibility, mobile support, and modularity as design goals. 
- https://twitter.com/teppeis/status/1034581567551631361
- How will this affect ProseMIrror project? What is the difference?
  - ProseMirror is for structured text, CodeMirror for plain text and code. They don't really affect each other
- Will it support the native browser spellchecker?
  - Somewhat. The main issue is that in many browsers, the spell checker gets completely confused (removes most of its underlines) when you programmatically touch the DOM. And in typical situations, CodeMirror will do that to adjust the highlighting.
  - Still, we do take care to only mess with the DOM when necessary, so when in content that doesn't change it highlighting during typing (Markdown without markup, HTML text nodes) it might work pretty well. Haven't done that much testing there yet
- Monaco still doesn't support even arrow keys on iPad/iOS. Ace and codemirror are at least usable.
