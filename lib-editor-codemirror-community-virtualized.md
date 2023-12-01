---
title: lib-editor-codemirror-community-virtualized
tags: [codemirror, community, virtualized]
created: 2023-11-30T06:56:07.608Z
modified: 2023-11-30T06:56:24.809Z
---

# lib-editor-codemirror-community-virtualized

# guide
- pros
  - fast render for large document
  - fast render for mobile

- cons
  - in-page search 不能直接使用浏览器提供的能力
  - scroll into view如锚点滚动需要自定义实现，因为可能不在可见范围
  - 影响现有的第三方组件，如scrollbar、(syntax)highlighting
# discuss-stars
- ## 

- ## 

- ## 
# discuss-codemirror
- ## 

- ## 

- ## 

- ## [Possible performance enhancement for very long rows - v5 - discuss. CodeMirror](https://discuss.codemirror.net/t/possible-performance-enhancement-for-very-long-rows/4897)
- Yes. And it’s not going to be implemented in version 5, since it would be complicated and invasive(侵袭的, 扩散的) to retrofit(更新；改型；改装).

- ## [Overlay scrollbars in CM6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/overlay-scrollbars-in-cm6/4644)
  - Content in CM6 is virtualized so I’m not sure how third party scrollbars libraries would go.

- ## [editor lines out of sync in merge view - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/editor-lines-out-of-sync-in-merge-view/7138)
- Thanks, I managed to reproduce it now (it only showed up for me when I scrolled back up from the bottom). This patch overhauls how spacers are handled, and seems to help

- ## how does codemirror stay so fast even on thousands of lines of code
- https://twitter.com/RogersKonnor/status/1730043499850977383
  - TIL it actually virtualizes the viewable nodes. Well, that makes sense, also not looking forward to virtualized scrolling in `<light-editor>` ...
  - I'll probably have to find a way to virtualize the syntax highlighting for `<light-editor>` to not tank performance

# discuss-virtualized
- ## 

- ## 

- ## 

- ## 📝🏘️ [Slate – A completely customizable framework for building rich text editors | Hacker News_202107](https://news.ycombinator.com/item?id=28000086)
- The recent changes to the API in 0.50 look good. The number of iteration passes really shows. Out of the available open source editor frameworks, 🆚️ Slate is probably most similar to Notion’s internal editor system. If I had to rebuild on a framework tomorrow, it’d be Slate or ProseMirror. Still if I used Slate it would be with the expectation that I’d end up owning an aging fork of a forgotten version at some point.
- I've been using Slate heavily this year. I'm not a Slate developer, but I've read a lot of the source code, follow all the Github issues, etc., and I'm "owning an aging fork".
  - I ended up forking only the React part of Slate, which is officially a plugin, and massively rewriting it to support virtualized windowing, so we can work with very large possibly complicated to render documents. I also added fairly generic realtime collaboration support. This is currently used in https://cocalc.com for WYSIWYG editing of Markdown documents. I also have plans to extend my use of Slate with windowing to Jupyter notebooks and other document types.
  - I chose Slate over Prosemirror because the source code of Slate is Typescript written in a clear modern style, and I was able to start reading any part of it and understand it easily, whereas I find Prosemirror's core source code more difficult (this may just be a reflection of my shortcomings). I spent a lot of time initially just reading Slate PR's claiming to fix bugs, then integrating the PR's into my fork, often in a way that makes sense for my project, but likely wouldn't in general (I left helpful remarks on Github).
  - I have no plans to switch from Slate to Prosemirror. Getting virtualized windowing to work with Slate was quite difficult, but it's really table stakes for what I plan on doing longterm, and I don't even know where to begin to do virtualized windowing in Prosemirror.

- How does virtualization play with text search? Did you end up having to roll your own?
  - Yes, I very much have to implement my own text search. There are many custom elements, so I would have to roll my own anyways at some point.

- What features of Slate put it closest to Notion's editor compared to other frameworks besides the obvious one that Slate's view layer is built on top of React? Is it somehow that Slate is more suitable handling asynchronous data (e.g. server generated uuids for each block, recursively fetching content for each block and its children)?
