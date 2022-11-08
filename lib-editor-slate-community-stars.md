---
title: lib-editor-slate-community-stars
tags: [community, slate]
created: 2022-05-15T18:41:58.641Z
modified: 2022-05-15T18:42:42.839Z
---

# lib-editor-slate-community-stars

# guide

- 渲染长文档的思路
  - virtualized render
  - defer render
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

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
