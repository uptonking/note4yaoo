---
title: lib-search-index-dev
tags: [search, search-index]
created: 2023-01-05T09:35:38.731Z
modified: 2023-01-05T10:20:29.496Z
---

# lib-search-index-dev

# guide

- roadmap
  - 合并search-index和linvodb的存储层

- features
  - 支持import/export index

- tips
  - 传统全文搜索的效果不如llm，因为llm可以用英文数据训练，然后用中文搜索
# discuss
- ## [Geohash: Sort on other things than tf-idf?](https://github.com/fergiemcdowall/search-index/issues/476)
- Yes sorting is much better in v1.0.x, and a geohash example would be really cool.
# faq
- Can I use another backend like MySQL or Redis?
  - Yes you can! Because search-index is built on top of levelup its possible to use another backend by passing the appropriate abstract-leveldown when initialising.

- How do I make a simple typeahead / autosuggest / matcher
  - if you just want a simple "begins with" autosuggest, then you can simply use the `DICTIONARY` function
# docs
- `const idx = await si(options);`
- 支持配置
  - db
    - When instantiated in a browser, it will use indexedDB as a keystore by default; 
    - when instantiated in node.js, it will use levelDB. 
  - caseSensitive
  - cacheLength for LRU
  - name for index storage
  - tokenAppend: to separate language tokens from scores in the underlying index.
  - stopwords: words to be ignored when indexing and querying

- `PUT_RAW` writes raw documents to the index. 
  - Raw documents are the documents that the index returns. 
  - Use raw documents when the documents that are indexed are not the same as the ones that you want the index to return.
  - This can be useful if you want documents to be retrievable for terms that dont appear in the actual document. 
  - It can also be useful if you want to store stripped down versions of the document in the index in order to save space.
