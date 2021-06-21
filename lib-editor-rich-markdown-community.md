---
title: lib-editor-rich-markdown-community
tags: [community, markdown, rich-markdown-editor]
created: '2021-06-02T10:29:05.540Z'
modified: '2021-06-02T10:29:43.088Z'
---

# lib-editor-rich-markdown-community

# pieces

- ## 

- ## 

- ## always copy latest value of node in CodeFence
- https://github.com/outline/rich-markdown-editor/pull/409
  - This change copies the logic of the language toggle such that it gets the position of the node, and then finds the node in the editor view and gets the latest text content.
- but the duplicated logic between `handleCopyToClipboard` and `handleLanguageChange` to find the codeblock node could be removed by allowing for custom nodeviews written with vanilla javascript (in addition to React ).
  - That's because with custom node views, you can easily get access to the current node and its position in the constructor and in the update method.
  - To do that, this library would just need to relax constraints in `createNodeViews` and move `ComponentView` into the `extension.component` method, so individual nodes could choose to use React or plain JS.

- ## Migrate to Prosemirror
- https://github.com/outline/rich-markdown-editor/issues/134
- We're investigating moving a future version of this project to Prosemirror for a couple of reasons:
  - Out of the box collaborative editing support
  - More stable API. Slate's API completely changes several times a year as it is still being refined
  - More performant
  - Improved support for soft keyboards (non-latin languages / mobile)
  - Ideally, if this comes to fruition the external API would remain largely the same, with the exception of losing support for custom Slate plugins.

- ## Has a hard time with larger amounts of data.
- https://github.com/outline/rich-markdown-editor/issues/29
- I've noticed an issue where if I'm testing larger amounts of text data, let's say 100 paragraphs or so, the editor will hang pretty intensely.
- after some more digging I think it's specifically the `Markdown.deserialize(props.defaultValue)` function that causes the hang on initial load. 
  - I wonder if we can make it more async. 
  - It'd be cool to pass the length of content/line count and render a placeholder or at least prevent the component from being blocking.
- I noticed that Paper for example only renders one page worth of stuff on load, and then renders the rest
  - Yea, I think that would be ideal too but more of a Slate concern
- I was thinking it'd be great to chunk or segment the data that the editor was using. My first thought was that it'd be cool to load the first page immediately and then merge in prefetched data as the user went on. It seems like there aren't any performance drags once the editor has mounted and has the data.
