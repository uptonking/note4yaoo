---
title: toc-lib-search-autocomplete
tags: [autocomplete, lib, search, toc]
created: 2020-09-25T09:10:00.530Z
modified: 2023-01-01T13:24:35.994Z
---

# toc-lib-search-autocomplete

# popular

- elasticsearch /49.9kStar/Apache2/202007
  - https://github.com/elastic/elasticsearch
  - https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html
  - Open Source, Distributed, RESTful Search Engine
  - elasticsearch-6.7.0-java11-201903
  - elasticsearch-6.7.1-java12

- lucene-solr /3.8kStar/Apache2/202009
  - https://github.com/apache/lucene-solr
  - https://lucene.apache.org/
  - Apache Lucene is a high-performance, full featured text search engine library written in Java.
  - Apache Solr is an enterprise search platform written in Java and using Apache Lucene. 
  - Major features include full-text search, index replication and sharding, and result faceting and highlighting.
# search-ui
- elastic-search-ui /1.8kStar/apache2/202212/ts
  - https://github.com/elastic/search-ui
  - https://www.elastic.co/enterprise-search/search-ui
  - A React library that allows you to quickly implement search experiences without re-inventing the wheel

- https://github.com/searchkit/searchkit
  - /3.9kStar/Apache2/202008
  - a suite of UI components built in react to rapidly create beautiful elasticsearch applications
  - https://github.com/searchkit/searchkit-starter-app

- https://github.com/appbaseio/dejavu
  - /7kStar/MIT/202008
  - The Missing Web UI for Elasticsearch: Import, browse and edit data with rich filters
# search-js
- flexsearch /9.4kStar/apache2/202210/js
  - https://github.com/nextapps-de/flexsearch
  - Next-Generation full text search library for Browser and Node.js

- lunr.js /8.3kStar/MIT/202008/inactive
  - https://github.com/olivernn/lunr.js
  - http://lunrjs.com/
  - A bit like Solr, but much smaller and not as bright.
  - For web applications with all their data already sitting in the client, it makes sense to be able to search that data on the client too. 
  - It saves adding extra, compacted services on the server. 
  - A local search index will be quicker, there is no network overhead, and will remain available and usable even without a network connection.
- elasticlunr.js /1.9kStar/MIT/201904/js
  - https://github.com/weixsong/elasticlunr.js
  - Based on lunr.js, but more flexible and customized.
  - Elasticlunr.js is a lightweight full-text search engine developed in JavaScript for browser search and offline search.
  - Elasticlunr.js provides Query-Time boosting, field search, more rational scoring/ranking methodology
  - Elasticlunr.js is a bit like Solr, but much smaller 

- lyra /5.1kStar/apache2/202212/ts
  - https://github.com/LyraSearch/lyra
  - Fast, in-memory, typo-tolerant, full-text search engine written in TypeScript.

- js-search /1.6kStar/MIT/202007/js/NoDeps/inactive
  - https://github.com/bvaughn/js-search
  - Js Search began as a lightweight implementation of Lunr JS, offering runtime performance improvements and a smaller file size. 
  - It has since expanded to include a rich feature set- supporting stemming, stop-words, and TF-IDF ranking.
  - Js Search enables efficient client-side searches of JavaScript and JSON objects

- libsearch /114Star/MIT/202207/js/单文件
  - https://github.com/thesephist/libsearch
  - https://thesephist.github.io/libsearch/
  - Simple, index-free text search for JavaScript, used across my personal projects

- https://github.com/cshum/levi /201901/js
  - Stream based full-text search for Node.js and browsers. Using LevelDB as storage backend.
  - Full-text search using TF-IDF and cosine similarity plus query-time field boost options. 
  - By default, it uses LevelDB on Node.js and IndexedDB on browser. Also works with a variety of LevelDOWN compatible backends.
  - Using stream based query mechanism with Highland.js, Levi is designed to be memory efficient

- minisearch /1.9kStar/MIT/202212/ts
  - https://github.com/lucaong/minisearch
  - a tiny but powerful in-memory fulltext search engine written in JavaScript. 
  - It is respectful of resources, and it can comfortably run both in Node and in the browser.

- Fuse /15.2kStar/apache2/202208/js
  - https://github.com/krisk/Fuse
  - https://fusejs.io/
  - a lightweight fuzzy-search, in JS, with zero dependencies.

- bibliothecula /152Star/GPLv3/202107/rust/archived
  - https://github.com/epilys/bibliothecula
  - https://epilys.github.io/bibliothecula/
  - document organizer with tags and full-text-search, in a simple and clean sqlite3 schema
  - Store plain text notes with automatic full-text search and back-reference indexing
  - a virtual FUSE filesystem written in Rust.
  - an HTTP GUI written in python3 using django.
  - a GTK3 UI in Rust that was written early and isn't functional.
  - an interactive python shell, bibl-shell.py, with convenient types and methods for working with your database:

- https://github.com/superhuman/command-score
  - Yet another javascript fuzzy string matching library!
  - We use this in email client in autocompletion contexts where the set of results is relatively bounded

- search-index /1.3kStar/MIT/202207/js
  - https://github.com/fergiemcdowall/search-index
  - A persistent, network resilient, full text search library for the browser and Node.js

- https://github.com/fergiemcdowall/fergies-inverted-index /202212/js
  - Throw JavaScript objects at the index and they will become retrievable by their properties using promises and map-reduce
  - This lib will work in node and also in the browser

- https://github.com/leeoniya/uFuzzy /202212/js
  - a fuzzy search library designed to match a relatively short search phrase (needle) against a large list of short-to-medium phrases (haystack
- https://github.com/farzher/fuzzysort /202211/js
  - Fast SublimeText-like fuzzy search for JavaScript.
# search-autocomplete
- tom-select /947Star/apache2/202212/ts
  - https://github.com/orchidjs/tom-select
  - https://tom-select.js.org/examples/
  - Tom Select is a dynamic, framework agnostic, and lightweight (~16kb gzipped) `<select>` UI control.
  - Tom Select was forked from `selectize.js` with the goal of modernizing the code base, decoupling from jQuery, and expanding functionality.
  - Options are efficiently scored and sorted on-the-fly (using sifter). 
  - https://github.com/orchidjs/sifter.js
    - A library for textually searching arrays and hashes of objects by property (or multiple properties). 
    - Designed specifically for autocomplete.

- autocomplete /2.3kStar/MIT/202212/ts
  - https://github.com/algolia/autocomplete
  - https://www.algolia.com/doc/ui-libraries/autocomplete/introduction/what-is-autocomplete/
  - JavaScript library for building autocomplete experiences.
  - The data that populates the autocomplete results are called sources. 
  - You can use whatever you want in your sources: a static set of searches terms, search results from an external source like an Algolia index, recent searches, and more.
  - The library creates an input and provides the interactivity and accessibility attributes, but you’re in full control of the DOM elements to output.
  - Unlike InstantSearch, Autocomplete doesn’t provide a library of ready-made UI widgets

- autoComplete.js /3.7kStar/apache2/202206/js/NoDeps
  - https://github.com/TarekRaafat/autoComplete.js
  - https://tarekraafat.github.io/autoComplete.js
  - Simple autocomplete pure vanilla Javascript library.
  - Powerful Search Engine with two different modes: strict/loose
  - Works on anything (<`input>`,  `<textarea>` and `contentEditable` elements)
# search-non-js
- https://github.com/opensearch-project/OpenSearch
  - a community-driven, open source fork of Elasticsearch 

- https://github.com/meilisearch/meilisearch /202211/rust
  - fast search engine that fits effortlessly into your apps, websites, and workflow.
  - [Elasticsearch like alternative · Issue · mastodon/mastodon](https://github.com/mastodon/mastodon/issues/20743)

- https://github.com/valeriansaliou/sonic /202210/rust
  - lightweight & schema-less search backend. 
  - An alternative to Elasticsearch that runs on a few MBs of RAM.

- https://github.com/toshi-search/Toshi /202204/rust
  - Toshi is meant to be a full-text search engine similar to Elasticsearch.
  - https://github.com/quickwit-oss/tantivy
    - Tantivy is a full-text search engine library inspired by Apache Lucene and written in Rust

- https://github.com/zinclabs/zinc /202211/go
  - a search engine that does full text indexing
  - lightweight alternative to elasticsearch that requires minimal resources, written in Go.

- https://github.com/typesense/typesense /202211/cpp
  - Open Source alternative to Algolia and an Easier-to-Use alternative to ElasticSearch

- https://github.com/manticoresoftware/manticoresearch /202211/cpp
  - an easy to use open source fast database for search. 
  - Good alternative for Elasticsearch. 
# search-ui-examples
- https://github.com/hemantwasthere/GitHub-Clone
  - search any github authorized user in this app and checkout there profile

- https://github.com/mohamedbenattia99/Github-repositories-clone
  - a Github repositories clone with search functionality. The project uses THE GITHUB API.
# full-text-search-solutions
- feathers-nedb-fuzzy-search /11Str/MIT/202012/js
  - https://github.com/FossPrime/feathers-nedb-fuzzy-search
  - NeDB adapter for fuzzy search, api compatible with the MongoDB version
  - Add fuzzy `$search` to NeDB `service.find` queries.
  - 依赖 @seald-io/nedb
  - https://github.com/trinly01/feathers-nedb-puzzy-search

- https://github.com/LokiJS-Forge/LokiDB/tree/master/packages/full-text-search
  - A full-text search engine.
# more-search
- https://github.com/algolia/docsearch
  - The easiest way to add search to your documentation

- https://github.com/typicode/json-server
  - Get a full fake REST API with zero coding
  - support Full-text search `GET /posts?q=internet`
