---
title: lib-editor-prosemirror-community-perf-optimization
tags: [community, optimization, perf, prosemirror]
created: 2022-08-31T00:21:43.729Z
modified: 2022-08-31T00:23:09.227Z
---

# lib-editor-prosemirror-community-perf-optimization

# guide

# discuss
- ## 

- ## 

- ## Optimize prosemirror-view with intersection observer api?_202103
- https://discuss.prosemirror.net/t/optimize-prosemirror-view-with-intersection-observer-api/3580
  - I find that one hot spot is iterDeco(…) in prosemirror-view. 
  - In iterDeco() the code seems have to iterate over the whole list of contents to find matching ones. 
  - I was wondering is it possible to optimize this procedure with intersection observer api? so that we can limit the iteration range down to leaf nodes being shown in the viewport and selection.

- Viewport-based drawing is out of scope for ProseMirror. 
  - It’s just too much extra complexity and failure modes. (It might be possible to rig something up with an external plugin, but it’s not going to be easy.)
  - That being said, the expected bottleneck for huge documents is the DOM. iterDeco being the slow part isn’t expected. 

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

- ## Single step with too large data
- https://discuss.prosemirror.net/t/single-step-with-too-large-data/3234
- This isn’t something the library will do for you. You could try to do something in dispatchTransaction that, if a large insertion has multiple nodes at its top level, splits it into smaller insertions, but that wouldn’t always work (say, when pasting a single huge list).

- ## Performance Issues with ProseMirror and Chrome
- https://discuss.prosemirror.net/t/performance-issues-with-prosemirror-and-chrome/2498
- Chrome plugins (e.g. Grammarly or other spell checkers) impact performance because they run in the same browsing context as ProseMirror.
