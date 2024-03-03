---
title: lib-search-lunrjs-community
tags: [community, lucene, lunrjs, search]
created: 2024-03-02T14:59:19.194Z
modified: 2024-03-02T14:59:58.825Z
---

# lib-search-lunrjs-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [Lunr.js as a search for static websites? _202305](https://github.com/olivernn/lunr.js/issues/26)
- It would be super-amazing to have a Lunr.js run with statically generated websites. I can imagine it running effectively in two modes:
  - Server-side mode during static site generation - when it does indexing, similar to how `SASS` precompiler works. That would generate a compressed index.
  - Client side which loads the index and does the search.

- I am missing some of the skills to do that at the moment and my current focus is on Solr
  - Looks like the feature is implemented and maybe it just needs to be advertised more.

- lunr.js is actually the basis of manastech/middleman-search(ruby), a Middleman extension for client-side search. The implementation was pretty much straightforward - it may also help you build your own plugin/extension for any other system you have to deal with.
