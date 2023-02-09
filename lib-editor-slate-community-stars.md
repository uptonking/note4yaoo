---
title: lib-editor-slate-community-stars
tags: [community, slate-editor]
created: 2022-05-15T18:41:58.641Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-community-stars

# guide

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
  - defer render
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Modeling RichText with Automerge](https://github.com/automerge/automerge/issues/193)
- I have spent a while thinking about this too, and I also think that a single document sequence with marker characters is the way to go. 
  - If you represent a document as a tree, there are a lot of operations that require deleting and re-inserting nodes (e.g. hitting enter in the middle of a paragraph, causing it to split into two paragraphs), which don't merge well in a concurrent setting. 
  - If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence.
- My intention was that Automerge. Text should be usable for this purpose. That is, I want Automerge. Text to be able to contain marker objects as well as characters from the text
- Maybe I am overlooking something, but "If a document is just a flat sequence, hitting enter in the middle of a paragraph just means inserting a '\n' element into that sequence." means we can not express tree structures. I can not imagine WYSIWYG without at least an anchor which has to be split as well.

- there is new development going on: next month, @geoffreylitt and @sliminality will be kicking off a research project to figure out the best way of handling rich text in CRDTs such as Automerge, with the support of the @inkandswitch research lab. 
  - https://www.inkandswitch.com/peritext/

- ## Dynamic Rendering Feature (performance improvement); only render visible blocks and not render blocks hidden within the y-overflow.__201705
- https://github.com/ianstormtaylor/slate/issues/790
- The Ace Editor: ajaxorg/ace does this by rendering two divs: 
  - a full height "scroller" div and then a "content" div that dynamic adjusts based on scrolls while updating it's content (removing hidden dom nodes and adding newly shown dom nodes).
  - https://github.com/ajaxorg/ace/blob/master/src/virtual_renderer.js
  - https://github.com/clauderic/react-tiny-virtual-list

- I don't think it's possible to arbitrarily render any part of a Slate Document at a given scroll position because it is difficult, possibly impossible, to tell how much space a Slate block will take until after it is rendered. 
  - Ace editor is an editor for monospace text so it is easy to predict how much space text will take before we render it.
- That said, what could work and could improve performance, is to render the visible portion of the page first before giving control back to the user. The rest of the content could fill in afterwards.
  - I think this might be a good low hanging fruit. Just render up to the visible portion, then use setTimeout to render a few blocks at a time for the rest without blocking the UI.

- For anyone needing this, I would highly recommend looking into other performance improvements in the general rendering case first, because they are probably much lower-hanging fruit.

- Rendering is very fast, almost instantly, with or without react-window, and deserializeHugeText is also fast. But before rendering, loading it to slate is slow.

- Interested to know everyones thoughts on a deferred rendering method (Such as described in this article on Twitter Lite)
