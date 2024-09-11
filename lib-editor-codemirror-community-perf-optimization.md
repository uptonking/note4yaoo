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
# discuss-big-document
- ## 

- ## 

- ## [Text not highlighted after EditorView.scrollIntoView - v6 - discuss. CodeMirror _202309](https://discuss.codemirror.net/t/text-not-highlighted-after-editorview-scrollintoview/7073)
- Parsing work is throttled so as to not slow down the UI and not waste too much cpu/battery/power. That means that if you are way down a big document, it may take a while to catch up, and if the editor isn’t active, it may stop doing work altogether on the assumption that the user isn’t working with it.

- is there an official way to increase the time budget or trigger a refresh programmatically?
  - I think `forceParsing` is what you are looking for.
# discuss
- ## 

- ## 

- ## [Cache objects between Widgets updates - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/cache-objects-between-widgets-updates/6844)
  - In a Widget’s constructor, I’m initializing a class (a UI library) that is slow to compute, so I’d like to cache it between updates. Unfortunately, the Widget’s constructor is called on every update, so that object is disposed, even if the Widget is equal
  - I understand Widgets are supposed to be cheap to create, but is there a proper way to retain data inside a Widget?
- Not really, except closing over it in the code run in toDOM. I don’t know why you need to retain this value, so I can’t really give specific advice from what you’ve shown.

- ## [Replace the entire doc performance - v6 - discuss. CodeMirror _202211](https://discuss.codemirror.net/t/replace-the-entire-doc-performance/5289)
  - when I use the dispatch function to insert a huge text, codemirror will create ten-thousands of dom nodes in the background and freeze the page for a while.
