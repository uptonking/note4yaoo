---
title: lib-editor-prosemirror-community-perf-optimization
tags: [community, optimization, perf, prosemirror]
created: 2022-08-31T00:21:43.729Z
modified: 2022-08-31T00:23:09.227Z
---

# lib-editor-prosemirror-community-perf-optimization

# guide

- 虚拟渲染
  - 思路
    - 将数据block化
    - 可参考表格rows的数据结构和更新
  - 缺点
    - 不能使用浏览器而需要自己实现查找搜索
    - 可能破坏第三方扩展，如toc
# discuss-stars
- ## 

- ## 

- ## 🆚⚡️ [ProseMirror vs Lexical performance test - discuss. ProseMirror _202410](https://discuss.prosemirror.net/t/prosemirror-vs-lexical-performance-test/7681)
  - My conclusion: ProseMirror wins.
  - For me it looks like Lexical has a little bit better performance, worse docs, same bundle size, worse community / tooling.
  - Conclusions : Lexical’s total of script executing time increases faster than ProseMirror’s, which is probably linked to its faster handling of increasing content and more frequent garbage collection.
  - we just got an update for this article and the memory consumption was caused by Lexical’s history plugin. Without that they’re kind of similar, will post an update soon!

- It seems like the only place Lexical surpasses ProseMirror is in LayoutCount. I wonder if, in the long run, ProseMirror could be optimized in this regard.
# discuss
- ## 

- ## 

- ## 

- ## A4 pages conceptual guide
- https://discuss.prosemirror.net/t/a4-pages-conceptual-guide/2901
- have a schema that looks like
- https://github.com/todorstoev/prosemirror-pagination
  - Plugin for ProseMirror emulating A4 pages

- What is done till now
  - correct split for single line paragraphs
- What should be done
  - correct split in tables
  - correct split for multiline paragraphs

```
doc(
   page(
       header(block+)
       body(block+)
       footer(block+)
       pageCounter(paragraph{1})
   )
)
```

- ## [Paging document](https://discuss.prosemirror.net/t/paging-document/1829)
- There’s some related discussion in this thread, but this is definitely not something that ProseMirror supports—
  - it tries to be an editor of semantic content, and paging is very much a presentation issue that, in my opinion, should be separated from the content editing process.
- I do understand that, yet one of the requirements I have is to have a visual page representation, which will be the same as the one to be printed on A4 paper, so we’ve already picked the approach of having pages in the editor schema.
- We’ve done several iterations on pagination at this point. There are some disadvantages to only splitting and joining and one of those is how technically joining and splitting changes the node the subsequent page’s immutable reference. Thus it causes some things to fire differently in the prosemirror logic. For us, I try to move fragments of text between pages, except when there is overflow or underflow, I usually use join and split then. But, if its overflow and underflow between two pages, I try to move fragments around. Its a bit more efficient, a little more complex to do. But yes, there are far less considerations as you said, if you dont have to deal with the attrs on your second page.

- ## Improving performance (loading on scroll)_202210
- https://discuss.prosemirror.net/t/improving-performance-loading-on-scroll/4972
- ProseMirror doesn’t do viewporting. It may be possible to implement something like that on top of it but I’m not aware of anybody who’s doing that.
  - The library puts the entire document in the DOM

- ## Render a virtual section instead of put in the dom_202110
- https://discuss.prosemirror.net/t/render-a-virtual-section-instead-of-put-in-the-dom/4142
- Virtual rendering is not something this library supports, sorry.

- ## Different parsing strategy for large documents_201710
- https://discuss.prosemirror.net/t/different-parsing-strategy-for-large-documents/1017
  - We’d like to support very large documents (500+ pages) in our application. 
  - Therefore we thought it would be a good solution to only parse/render the nodes which are currently displayed in the viewport
  - As far as I understand CodeMirror supports exactly this. Perhaps there is an approach for this already implemented or in planning for ProseMirror?
- Nope, this is considered out of scope for ProseMirror. I don’t have a strategy for this, and I am not planning to incur all the complexity that this entails in the core library. 
  - 👉🏻 Some users have gotten good results from structuring their interface so that each chapter has its own ProseMirror instance. 
  - You can use offset maps to map changes from such sub-editors into a larger document.

- ## Efficient Viewport rendering? (like CodeMirror)_201701
- https://discuss.prosemirror.net/t/efficient-viewport-rendering-like-codemirror/577
- this is intentionally out of scope, because it was already hugely complicated to get right in a plain text editor like CodeMirror, and I don’t want to bloat and complicate this library with this functionality. I know this can be useful to have, but I’m not tackling it.
  - I have no idea how to cleanly do that. And that’s why I didn’t do it.

- ## Optimize prosemirror-view with intersection observer api?_202103
- https://discuss.prosemirror.net/t/optimize-prosemirror-view-with-intersection-observer-api/3580
  - I find that one hot spot is iterDeco(…) in prosemirror-view. 
  - In iterDeco() the code seems have to iterate over the whole list of contents to find matching ones. 
  - I was wondering is it possible to optimize this procedure with intersection observer api? so that we can limit the iteration range down to leaf nodes being shown in the viewport and selection.

- Viewport-based drawing is out of scope for ProseMirror. 
  - It’s just too much extra complexity and failure modes. (It might be possible to rig something up with an external plugin, but it’s not going to be easy.)
  - That being said, the expected bottleneck for huge documents is the DOM. iterDeco being the slow part isn’t expected. 

- ## Single step with too large data
- https://discuss.prosemirror.net/t/single-step-with-too-large-data/3234
- This isn’t something the library will do for you. You could try to do something in dispatchTransaction that, if a large insertion has multiple nodes at its top level, splits it into smaller insertions, but that wouldn’t always work (say, when pasting a single huge list).

- ## Performance Issues with ProseMirror and Chrome
- https://discuss.prosemirror.net/t/performance-issues-with-prosemirror-and-chrome/2498
- Chrome plugins (e.g. Grammarly or other spell checkers) impact performance because they run in the same browsing context as ProseMirror.
