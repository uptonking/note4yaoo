---
title: toc-lib-search-autocomplete
tags: [autocomplete, lib, search, toc]
created: 2020-09-25T09:10:00.530Z
modified: 2023-01-01T13:24:35.994Z
---

# toc-lib-search-autocomplete

# guide
- features
  - chinese
  - persistence

- ref
  - database search solutions
# popular
- elasticsearch /62.3kStar/ElasticLic/202301/java
  - https://github.com/elastic/elasticsearch
  - https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html
  - Open Source, Distributed, RESTful Search Engine
  - elasticsearch-6.7.0-java11-201903
  - elasticsearch-6.7.1-java12
- OpenSearch /6.2kStar/apache2/202301/java
  - https://github.com/opensearch-project/OpenSearch
  - a community-driven, open source fork of Elasticsearch 

- lucene-solr /3.8kStar/Apache2/202009
  - https://github.com/apache/lucene-solr
  - https://lucene.apache.org/
  - Apache Lucene is a high-performance, full featured text search engine library written in Java.
  - Apache Solr is an enterprise search platform written in Java and using Apache Lucene. 
  - Major features include full-text search, index replication and sharding, and result faceting and highlighting.

- Jhaystack /8Star/MIT/202207/ts
  - https://github.com/fukurosan/Jhaystack
  - https://fukurosan.github.io/Jhaystack/#/index
  - A JavaScript search engine with zero dependencies.
  - Every part of the library is built to be customizable as well as unit testable, with support for a variety addons.
  - 支持配置compare/sort/index/cluster
  - 索引Ranking Strategy支持TFIDF (Default)、BM25
  - Jhaystack allows you to search through not just values but also objects and arrays, dates, regex
  - Jhaystack allows you to create full-text indexes using an index strategy. 
  - Full-text indexes can be used not just for full-text search but also for search filters in queries which works great for larger data sets.
# search-js
- flexsearch /9.4kStar/apache2/202210/js
  - https://github.com/nextapps-de/flexsearch
  - Next-Generation full text search library for Browser and Node.js
  - memory-flexible full-text search library with zero dependencies.
  - 提供了搜索相关库的Performance Benchmark (Ranking)
  - The export primarily exists for the usage in Node.js or to store indexes you want to delegate from a server to the client.
  - 支持 Customizable Charset/Language (Matcher, Encoder, Tokenizer, Stemmer, Filter, Split, RTL)
    - All language-specific definitions has excluded and was optimized for maximum dead-code elimination when using compiler/bundler. 
    - Each language exists of 5 definitions, Charset(Encoder, RTL), Language(Matcher, Stemmer, Filter)
  - [whether this library supports reading from IndexedDb instead of memory](https://github.com/nextapps-de/flexsearch/issues/289)
    - This is actually not supported(202210). Supporting interfaces may be provided in future. Since the "flat index" instance hold the whole data structure of one index, it has a good chance to make interfaces for every database.

- lyra /5.1kStar/apache2/202212/ts
  - https://github.com/LyraSearch/lyra
  - https://docs.lyrasearch.io/
  - Fast, in-memory, typo-tolerant, full-text search engine written in TypeScript.
  - Lyra is an immutable, runtime-agnostic, edge, and in-memory full-text search engine that works both on client and server.
  - Lyra has been developed thinking of a simple way to add new features via a plugin system, leaving the core as small as possible.
  - Lyra will only index string properties, but will allow you to set and store additional data if needed.
- https://github.com/xieyezi/lyra-cn
  - a tool for offline search Chinese.
  - 添加对拼音的支持，如搜索"砍伐"的结果包含"看法"

- lunr.js /8.3kStar/MIT/202008/js/inactive
  - https://github.com/olivernn/lunr.js
  - http://lunrjs.com/
  - A bit like Solr, but much smaller and not as bright.
  - For web applications with all their data already sitting in the client, it makes sense to be able to search that data on the client too. 
  - It saves adding extra, compacted services on the server. 
  - A local search index will be quicker, there is no network overhead, and will remain available and usable even without a network connection.
- https://github.com/MihaiValentin/lunr-languages
  - Lunr Languages is a Lunr addon that helps you search in documents written in the following languages, 支持中文

- elasticlunr.js /1.9kStar/MIT/201904/js
  - https://github.com/weixsong/elasticlunr.js
  - Based on lunr.js, but more flexible and customized.
  - Elasticlunr.js is a lightweight full-text search engine developed in JavaScript for browser search and offline search.
  - Elasticlunr.js provides Query-Time boosting, field search, more rational scoring/ranking methodology
  - Elasticlunr.js is a bit like Solr, but much smaller 

- js-search /2.1kStar/MIT/202007/js/NoDeps/lunr/inactive
  - https://github.com/bvaughn/js-search
  - Js Search began as a lightweight implementation of Lunr JS, offering runtime performance improvements and a smaller file size. 
  - It has since expanded to include a rich feature set- supporting stemming, stop-words, and TF-IDF ranking.
  - Js Search enables efficient client-side searches of JavaScript and JSON objects

- minisearch /1.9kStar/MIT/202212/ts/NoDeps
  - https://github.com/lucaong/minisearch
  - a tiny but powerful in-memory fulltext search engine written in JavaScript. 
  - It is respectful of resources, and it can comfortably run both in Node and in the browser.
  - MiniSearch addresses use cases where full-text search features are needed (e.g. prefix search, fuzzy search, ranking, boosting of fields…)
  - Memory-efficient index, designed to support memory-constrained use cases like mobile browsers.

- search-index /1.3kStar/MIT/202207/js
  - https://github.com/fergiemcdowall/search-index
  - A persistent, network resilient, full text search library for the browser and Node.js
  - 依赖level8、fergies-inverted-index、term-vector、lru-cache、p-queue
  - built on top of levelup, its possible to use another backend by passing the appropriate `abstract-leveldown`.
  - [How to search in other languages, except English](https://github.com/fergiemcdowall/search-index/issues/440)
    - I think most languages are straight forward. You add documents, and choose which stopword-language to use. 
    - But when you don't have space between the characters, you need to tokenize the text before adding it. At least to remove stopwords. 

- levi /374Star/MIT/201901/js
  - https://github.com/cshum/levi
  - Stream based full-text search for Node.js and browsers. Using LevelDB as storage backend.
  - 依赖levelup、cosine-similarity、stemmer
  - Full-text search using TF-IDF and cosine similarity plus query-time field boost options. 
  - Levi is built on LevelUP. By default, it uses LevelDB on Node.js and IndexedDB on browser. 
  - Using stream based query mechanism with Highland.js, Levi is designed to be memory efficient

- level-min /4Star/MIT/202208/ts
  - https://github.com/heyauri/level-min
  - 一个支持中文的轻量级全文搜索库，基于Node与LevelDB。
  - 依赖segmentit、natural、stopword、level8、franc
  - TF-IDF Similarity based full text search

- https://github.com/fergiemcdowall/fergies-inverted-index /202212/js
  - Throw JavaScript objects at the index and they will become retrievable by their properties using promises and map-reduce
  - This lib will work in node and also in the browser
  - This is an inverted index library.
  - creates a DB called "myDB" using levelDB (node.js), or indexedDB (browser)

- https://github.com/dominictarr/level-inverted-index /201602/js
  - Inverted Index for levelup.

- libsearch /114Star/MIT/202207/js/单文件
  - https://github.com/thesephist/libsearch
  - https://thesephist.github.io/libsearch/
  - Simple, index-free text search for JavaScript, used across my personal projects

- Fuse /15.2kStar/apache2/202208/js
  - https://github.com/krisk/Fuse
  - https://fusejs.io/
  - a lightweight fuzzy-search, in JS, with zero dependencies.

- https://github.com/superhuman/command-score
  - Yet another javascript fuzzy string matching library!
  - We use this in email client in autocompletion contexts where the set of results is relatively bounded

- wink-bm25-text-search /43Star/MIT/202110/js
  - https://github.com/winkjs/wink-bm25-text-search
  - Fast Full Text Search based on BM25
  - [BM25: The Next Generation of Lucene Relevance_201510](https://opensourceconnections.com/blog/2015/10/16/bm25-the-next-generation-of-lucene-relevation/)
  - Instead of the traditional “TF*IDF”, Lucene just switched to something called BM25 in trunk. 
  - That means a new scoring formula for Solr 6 and Elasticsearch down the line.
- https://github.com/ndx-search/ndx-query /201906/ts
  - Free text search query that is using BM25 ranking function

- https://github.com/leeoniya/uFuzzy /202212/js
  - a fuzzy search library designed to match a relatively short search phrase (needle) against a large list of short-to-medium phrases (haystack
- https://github.com/farzher/fuzzysort /202211/js
  - Fast SublimeText-like fuzzy search for JavaScript.

- https://github.com/karussell/jsii /201304/js
  - Full Text Search Prototype in 100% JavaScript
  - 100% in-memory
  - Solr compatible JSON
  - Queryable via HTTP
  - pagable, filterable and sortable results
  - Real time BUT: jsii is not transaction safe, because there is no 'commit'

- itemsjs /274Star/apache2/202208/js/NoDeps
  - https://github.com/itemsapi/itemsjs
  - Full text, faceted, (almost) dependency free search engine in javascript
  - Created to perform fast search on json dataset (up to 100K items).
  - working on backend and frontend
  - If native full text search is not enough then you can integrate with external full text search, like minisearch/lunr.js
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
- https://github.com/tj/reds
  - simple full text search module for node.js - backed by Redis
  - Version 1.0.0 is syntactically compatible with previous versions of reds (0.2.5).

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

- bibliothecula /152Star/GPLv3/202107/rust/archived
  - https://github.com/epilys/bibliothecula
  - https://epilys.github.io/bibliothecula/
  - document organizer with tags and full-text-search, in a simple and clean sqlite3 schema
  - Store plain text notes with automatic full-text search and back-reference indexing
  - a virtual FUSE filesystem written in Rust.
  - an HTTP GUI written in python3 using django.
  - a GTK3 UI in Rust that was written early and isn't functional.
  - an interactive python shell, bibl-shell.py, with convenient types and methods for working with your database:

- https://github.com/zinclabs/zinc /202211/go
  - a search engine that does full text indexing
  - lightweight alternative to elasticsearch that requires minimal resources, written in Go.

- https://github.com/typesense/typesense /202211/cpp
  - Open Source alternative to Algolia and an Easier-to-Use alternative to ElasticSearch

- https://github.com/manticoresoftware/manticoresearch /202211/cpp
  - an easy to use open source fast database for search. 
  - Good alternative for Elasticsearch. 
# search-ui-examples
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

- https://github.com/hemantwasthere/GitHub-Clone
  - search any github authorized user in this app and checkout there profile

- https://github.com/mohamedbenattia99/Github-repositories-clone
  - a Github repositories clone with search functionality. The project uses THE GITHUB API.

- https://github.com/varianter/handbook
  - https://handbook.variant.no/
  - 依赖mdx2, instantsearch.js, algoliasearch, swr
# search-solutions
- pagefind /677Star/MIT/202301/rust
  - https://github.com/CloudCannon/pagefind
  - https://pagefind.app/
  - Pagefind is a fully static search library that aims to perform well on large sites
  - Pagefind runs after Hugo, Eleventy, Jekyll, Next, Astro, SvelteKit, or any other SSG. 
  - The installation process is always the same: Pagefind only requires a folder containing the built static files of your website
  - After indexing, Pagefind adds a static search bundle to your built files, which exposes a JavaScript search API that can be used anywhere on your site. 
# full-text-search-solutions
- pouchdb-quick-search /370Star/apache2/201702/js/lunr/inactive
  - https://github.com/pouchdb-community/pouchdb-quick-search
  - Full-text search engine on top of PouchDB
  - This is a local plugin, so it is not designed to work against CouchDB/Cloudant/etc. 
  - If you'd like to search against the server, use the CouchDB Lucene plugin, Cloudant's search indexes, or something similar.
  - This plugin uses the classic search technique of TF-IDF

- https://github.com/doriandrn/rxdb-search /202101/ts
  - Search plugin for RxDB based on search-index

- https://github.com/scambier/obsidian-omnisearch
  - A search engine that "just works" for Obsidian. 
  - Includes OCR and PDF indexing. Images OCR and PDF indexing are only available on desktop
  - it uses the excellent MiniSearch library.
  - Automatic document scoring using the BM25 algorithm
  - Note: support of Chinese, Japanese, Korean, etc. depends on https://github.com/aidenlx/cm-chs-patch

- mani /12Star/MIT/201606/js/lunr
  - https://github.com/glennjones/mani
  - Mani provides a document based search tool in javascript, for browser and node.js 
  - 依赖nedb、localForage、lunr.js、geolib
  - It merges together free text search, mongodb type queries, geo search and facets from other projects into one library.
  - Serialize data and indexes to and from a JSON file

- https://github.com/mongoosejs/mongoose-text-search /152Star/MIT/201311/js
  - Provides MongoDB 2.4 text search support for mongoose.

- feathers-nedb-fuzzy-search /11Str/MIT/202012/js
  - https://github.com/FossPrime/feathers-nedb-fuzzy-search
  - NeDB adapter for fuzzy search, api compatible with the MongoDB version
  - Add fuzzy `$search` to NeDB `service.find` queries.
  - 依赖 @seald-io/nedb
  - https://github.com/trinly01/feathers-nedb-puzzy-search

- https://github.com/LokiJS-Forge/LokiDB/tree/master/packages/full-text-search
  - A full-text search engine.
  - lokiDb is blazing fast, feature-rich in-memory database written in TypeScript

- https://github.com/frankred/node-full-text-search-light
  - Full Text Search Light is a pure JS full text search engine with an ultrafast search 

- https://github.com/eugeneware/fulltext-engine /32Star/BSD/201405/js
  - Query your levelup/leveldb engine using full text search phrases with INDEXES.
  - This is a plugin for level-queryengine.
- https://github.com/eugeneware/level-queryengine /63Star/BSD/201405/js
  - A generic pluggable query-engine system (that supports indexes) for levelup/leveldb databases.
  - Using this architecture you can query your levelup database using your own query langauge with full index support.
  - forks
    - https://github.com/mvayngrib/level-queryengine
# more-search
- https://github.com/algolia/docsearch
  - The easiest way to add search to your documentation

- https://github.com/typicode/json-server
  - Get a full fake REST API with zero coding
  - support Full-text search `GET /posts?q=internet`