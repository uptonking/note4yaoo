---
title: lib-editor-codemirror-community-perf-optimization
tags: [codemirror, community, performance]
created: 2024-08-11T03:32:03.006Z
modified: 2024-08-11T03:39:54.012Z
---

# lib-editor-codemirror-community-perf-optimization


# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🤔🫧 [CodeMirror 6: Web-Worker-isolated state? _202012](https://discuss.codemirror.net/t/codemirror-6-web-worker-isolated-state/2788)
- Considering V6’s singleton and isolated state, I think it’s possible to ‘decouple’ the EditorView instance from it’s state and instead dispatch updates through some asynchronous helper functions. 
  - I wish to do this because, well, it’s fun, and also because I’m doing some fairly heavy lifting on the DOM on the main thread (very, very fast Markdown live-preview, which itself is already heavily web-workerized and asynchronous) and I would like to isolate the potentially parse-heavy operations into a web-worker.
  - I know that monaco-editor already does this, so it would be a ‘competitive’ feature to have or have easily supported.
- 👷 Not doing this is a conscious(清醒地；有意的) decision in this project—serializing/deserializing on worker boundaries is very limiting in the kind of data structures you can (effectively) use, 
  - and asynchronicity everywhere makes code a lot more complex, expensive, and error-prone. 
  - So I went with a synchronous single-heap approach that takes care not to do too much work during updates.

# discuss-batch
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Replace the entire doc performance - v6 - discuss. CodeMirror _202211](https://discuss.codemirror.net/t/replace-the-entire-doc-performance/5289)
  - when I use the dispatch function to insert a huge text, codemirror will create ten-thousands of dom nodes in the background and freeze the page for a while.