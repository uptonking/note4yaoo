---
title: lib-editor-app-community-styling-formats
tags: [community, editor, styling]
created: 2023-11-01T12:32:22.724Z
modified: 2023-11-01T12:33:20.763Z
---

# lib-editor-app-community-styling-formats

# guide

# discuss-formats-comments
- ## 

- ## 浏览器已经支持通过 JavaScript 对内容进行高亮操作了，从此网页上可以告别使用 mark/span 作为搜索高亮标签了。
- https://twitter.com/Barret_China/status/1719891344259485792
  - 1）定义一个 ::highlight 的 CSS 样式，当前仅支持 background 和 color
  - 2）使用 Range API 获取到文本的起始位置
  - 3）通过 CSS.highlights 将高亮样式赋值给（多个）选中的文本

- ## new API is starting to hit browsers! The CSS Custom Highlight API. 
- https://twitter.com/wesbos/status/1719367659119079492
  - Highlight text on the page without having to wrap in a `<mark>` or `<span>` .
  - [How to Use Text Fragments to Highlight Searched Text - YouTube](https://www.youtube.com/watch?v=JmsSfmXiWbk)
- The spec is still in Draft, but it recently Hit Chrome, Edge and Firefox nightly. 
  - You can currently only style the `background-color` and `color` in CSS. 
  - Would be nice to have a tad(少量；一点儿) more control over border-radius, bg image, borders and gradients - squiggly lines is a use case
  - Also interesting to note, this is one of the first browser APIs that use a Map as the basis for it's API. The get/set/clear/delete API you already know works on setting custom highlights
- Text decorations, filters and background-images definitely. And I can imagine outline should be possible in ::highlight() as well. But not border, unless it will be changed in some strange way so it would not affect the layout.
- Little pain it doesn't inherit custom properties defined on `:root`

- does it support regex?
  - it supports start and stop numbers, how you find those numbers if up to you. Here I wrote a little loop that used `string.indexOf` to find them all
- Do you know if it's related to text fragments?
  - I had not seen that API - but thats exactly what we need for the podcast transcripts. It is related to the clipboard/selection API which also use the Range constructor as a basis
- I will admit that this is cool. However, I wonder how this will be handled in terms of accessibility.  Granted this style of feature always seems to be difficult to handle in an accessible manner.  Let alone make the regions actionable.

- This will be specifically useful for js based ebook readers. By any chance, does it support click event on these highlights?
  - Neat use case, but unlikely since at a minimum you need an Element to add a listener, this is 2 steps deeper because it needs a Text node, and then a range of that.

- Nice, can we do CSS-only syntax highlighting of source code with this?
  - Well you still need JS to make the ranges, so not really

- that's a great solution! I used to use `mark.js` and I'll continue to use it, but as soon as Safari adds support, I'll definitely move to the built-in JavaScript features.

- I wonder if this would help with http://pelicanizer.com... it might save me the trouble of span-wrapping everything.
# discuss-highlighting
- ## 

- ## Highlight.js makes per-line highlighting really challenging without recursing through every node which is just gonna be a no from me.
- https://twitter.com/RogersKonnor/status/1726112759518024188
  - PrismJS being a global UMD is gross. 
  - Are there any other syntax highlighting libraries I'm missing?
- Rouge. It's Ruby only tho.
- He made Torchlight. https://torchlight.dev Making HTTP requests to highlight on every keystroke probably isn't a good idea either.

# discuss
- ## 

- ## 

- ## 

- ## 
