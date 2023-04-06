---
title: toc-lib-search-index
tags: [level-like, search-index, toc]
created: 2023-01-03T18:52:59.210Z
modified: 2023-01-03T18:53:16.716Z
---

# toc-lib-search-index

# guide

- tips
  - 传统全文搜索的效果不如llm，因为llm可以用英文数据训练，然后用中文搜索
# search-index
- https://github.com/eklem/search-index-cookbook /201703/js
  - interesting use cases with search-index
  - 不兼容最新版

- https://github.com/eklem/search-index-pwa-basics /202103/js
  - A Service worker and a shared worker to help create PWAs based on search-index
  - https://github.com/eklem/daq-proc
    - Simple document and query processor to makes search running in the browser and node.js a little better. 
    - Removes stopwords (smaller index and less irrelevant hits), extract keywords to filter on and prepares ngrams for auto-complete functionality.
# utils
- https://github.com/myadbox/algolia-mock-server /202112/ts
  - A mock server to mimick Algolia's search index, primarily for e2e testing purposes.

- https://github.com/marconi1992/algolite /201902/js
  - An Implementation of Algolia to emulate its REST API
  - 依赖search-index.v1, express, minimist

- https://github.com/Ruitjes/javascript-search-index-performance
  - 测试json

- https://github.com/fergiemcdowall/norch /201704/js
  - A search server that can be installed with npm
  - 依赖search-index, restify, byline
  - https://github.com/eklem/norch-vue
    - Vue.js frontend to Norch and search-index.
# examples
- https://github.com/yeojongki/electron-excel-seach
  - Electron 实现 Excel 导入提取数据 & 全文检索
  - 搜索依赖通过script标签导入

- https://github.com/jarfile/hadithdb
  - https://hadith.quranunlocked.com/

- https://github.com/MpMeetPatel/coding-diary /202104/js
  - An Offline only and Offline first personal coding-diary for everyone
# more
- https://github.com/eklem/search-index-indexer /201703/js
  - Easy way to test if search-index is buggy or it's your own code that is the problem.
  - search-index must be at least v0.9.x.

- [Building index by calling PUT once for each document does not return all matches in query afterwards · Issue](https://github.com/fergiemcdowall/search-index/issues/537)
  - In the forthcoming search-index@3 it is possible to PUT in parallel.
