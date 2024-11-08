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

- usecase
  - 针对ssg/blog的搜索，类似algolia-docsearch/autocomplete-renderer, hacker-news-search
  - 针对列表项的搜索，类似searchkit, es-search-ui

- resources
  - database search solutions
  - [Various search databases and backends as alternatives to Elasticsearch](https://gist.github.com/manigandham/58320ddb24fed654b57b4ba22aceae25)
  - [Tips for a good search | DocSearch by Algolia](https://docsearch.algolia.com/docs/tips)
# popular
- https://github.com/algolia/hn-search /MIT/202403/ruby/ts/可参考搜索ui
  - https://hn.algolia.com/api
  - the widely known Hacker News API 
  - This API is built on top of Algolia Search's API. 
  - It enables developers to access HN data programmatically using a REST API. 
  - This documentation describes how to request data from the API and how to interpret the response.
  - https://github.com/HackerNews/API
    - Documentation and Samples for the Official HN API
    - In partnership with Firebase, we're making the public Hacker News data available in near real time

- OpenSearch protocol
  - https://github.com/dewitt/opensearch
  - OpenSearch is a collection of simple formats for the sharing of search results.
  - launched in 2005 by A9.com, an Amazon subsidiary, as a means for sharing search queries and search results in a standardized format.
  - The specification has been unchanged and stable for over a decade
  - The OpenSearch protocol lets you describe a search engine for your website, so that browsers or other search clients can use that search engine.

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

- https://github.com/jameslittle230/stork /apache2/202307/rust/ts/inactive
  - fast web search, made for static sites.
  - Stork is built with Rust, and the Javascript library uses WebAssembly behind the scenes.
  - [I'm winding down my work with Stork_202306](https://github.com/jameslittle230/stork/discussions/360)
    - Tinysearch and PageFind are, philosophically, the most similar alternatives to Stork. 
    - 💡 Lunr, Fuse.js, and Minisearch are similar, but are Javascript-only (no WASM). 
    - Meilisearch, EdgeSearch, and Tantivy are all server-hosted search engines written in Rust. 
# search-js
- flexsearch /11.3kStar/apache2/202401/js
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
  - https://github.com/beekeeper-studio/flexsearch
    - FlexSearch v0.7.0 is a modern re-implementation and was newly developed from the ground up

- orama/lyra /5.1kStar/apache2/202311/ts
  - https://github.com/oramasearch/orama
  - https://github.com/LyraSearch/lyra
  - https://docs.lyrasearch.io/
  - https://docs.oramasearch.com/
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
  - [Still maintained?](https://github.com/olivernn/lunr.js/issues/504)
    - lunr is meant for browser use and as such it's very small in size compared to Lyra Search
  - https://github.com/MihaiValentin/lunr-languages
    - Lunr Languages is a Lunr addon that helps you search in documents written in the following languages, 支持中文
  - https://github.com/olivernn/lunr.rs /201710/rust
    - A Lunr backend implemented in Rust.
    - The current implementation is able to generate an index that is readable and searchable by lunr.js, but that is about it. 
    - Currently there is no pipeline and no ability to associate metadata with a token.
  - 🍴 forks
  - https://github.com/CrazyFork/lunr.js

- elasticlunr.js /1.9kStar/MIT/201904/js
  - https://github.com/weixsong/elasticlunr.js
  - Based on lunr.js, but more flexible and customized.
  - Elasticlunr.js is a lightweight full-text search engine developed in JavaScript for browser search and offline search.
  - Elasticlunr.js provides Query-Time boosting, field search, more rational scoring/ranking methodology
  - Elasticlunr.js is a bit like Solr, but much smaller 

- js-search /2.1kStar/MIT/202003/js/NoDeps/lunr/inactive
  - https://github.com/bvaughn/js-search
  - Js Search began as a lightweight implementation of Lunr JS, offering runtime performance improvements and a smaller file size. 
  - It has since expanded to include a rich feature set- supporting stemming, stop-words, and TF-IDF ranking.
  - Js Search enables efficient client-side searches of JavaScript and JSON objects
- https://github.com/bvaughn/js-worker-search
  - Full text client-side search based on js-search but with added web-worker support for better performance.

- minisearch /1.9kStar/MIT/202311/ts/NoDeps
  - https://github.com/lucaong/minisearch
  - a tiny but powerful in-memory fulltext search engine written in JavaScript. 
  - It is respectful of resources, and it can comfortably run both in Node and in the browser.
  - MiniSearch addresses use cases where full-text search features are needed (e.g. prefix search, fuzzy search, ranking, boosting of fields…)
  - Memory-efficient index, designed to support memory-constrained use cases like mobile browsers.
  - 支持中文
  - forks
  - https://github.com/Mister-Hope/slimsearch /202402/ts

- itemsjs /274Star/apache2/202409/js/NoDeps
  - https://github.com/itemsapi/itemsjs
  - https://github.com/itemsapi/itemsjs/blob/master/docs/demo.md
  - Full text, faceted, (almost) dependency free search engine in javascript
  - **Created to perform fast search on json dataset (up to 100K items)**.
  - working on backend and frontend
  - If native full text search is not enough then you can integrate with external full text search, like `minisearch/lunr.js`.
  - Facet filtering and sorting: Filter and order results by various facets.
  - pagination
  - https://github.com/unplatform-io/instantsearch-itemsjs-adapter /202203/ts
    - an adapter that connects the search engine ItemsJS with the opensource tool Instantsearch
  - https://github.com/unplatform-io/clientside-instantsearch-demo

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

- https://github.com/gajus/liqe /BSD/202210/ts
  - Lightweight and performant Lucene-like parser, serializer and search engine.
  - 依赖nearley

- https://github.com/dominictarr/level-inverted-index /201602/js
  - Inverted Index for levelup.

- libsearch /114Star/MIT/202207/js/单文件
  - https://github.com/thesephist/libsearch
  - https://thesephist.github.io/libsearch/
  - Simple, index-free text search for JavaScript, used across my personal projects

- Fuse /15.2kStar/apache2/202310/js/NoDeps
  - https://github.com/krisk/Fuse
  - https://fusejs.io/
  - https://www.fusejs.io/demo.html
  - lightweight fuzzy-search library, with zero dependencies.
  - fuzzy searching (more formally known as approximate string matching) is the technique of finding strings that are approximately equal to a given pattern (rather than exactly).
  - [a lightweight fuzzy-search, in JS, with zero dependencies.](https://gist.github.com/ericyd/fe4ce86a1143e86b821e0d12d5daf236)
    - 实现很简单
    - an example of how to implement fuse.js with a web worker

- https://github.com/askorama/orama /apache2/202402/ts
  - https://docs.oramasearch.com/
  - Fast, dependency-free, full-text and vector search engine with typo tolerance, filters, facets, stemming, and more. 
  - Works with any JavaScript runtime, browser, server, service
  - Orama is a full-text and vector search engine. This allows you to adopt different kinds of search paradigms depending on your specific use case.

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
  - a fuzzy search library designed to match a relatively short search phrase (needle) against a large list of short-to-medium phrases (haystack)
  - It might be best described as a more forgiving String.indexOf().
  - ufuzzy.js 能在手机上 9ms 内模糊搜索 16 万单词和短语，搞不懂为什么需要关系数据库
- https://github.com/farzher/fuzzysort /202211/js
  - Fast SublimeText-like fuzzy search for JavaScript.

- https://github.com/karussell/jsii /201304/js
  - Full Text Search Prototype in 100% JavaScript
  - 100% in-memory
  - Solr compatible JSON
  - Queryable via HTTP
  - pagable, filterable and sortable results
  - Real time BUT: jsii is not transaction safe, because there is no 'commit'
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
  - [Support for hugo](https://github.com/algolia/autocomplete/discussions/999)
    - There's nothing specific about the backend or static site generation that would make autocomplete not work. Can you clarify where you are stuck?
    - There's also examples here: /examples
  - [Autocomplete – A JavaScript library for building autocomplete experiences | Hacker News _202306](https://news.ycombinator.com/item?id=36236578)

- autoComplete.js /3.7kStar/apache2/202206/js/NoDeps
  - https://github.com/TarekRaafat/autoComplete.js
  - https://tarekraafat.github.io/autoComplete.js
  - Simple autocomplete pure vanilla Javascript library.
  - Powerful Search Engine with two different modes: strict/loose
  - Works on anything (<`input>`,  `<textarea>` and `contentEditable` elements)

- https://github.com/webscopeio/react-textarea-autocomplete /202210/js
  - React component implements configurable GitHub's like textarea autocomplete.
  - It can be used for example for emoji autocomplete or for @mentions.
# search-data
- https://github.com/searchkit/searchkit/tree/main/sample-data
  - movies, electronics-ecommerce
# search-wasm
- https://github.com/kbumsik/blogsearch /202007/ts
  - a pure client-side, full-text search engine for static websites, powered by SQLite compiled to WebAssembly.
  - The search engine basically is SQLite with the FTS5 extension, compiled to WebAssembly. 
  - The SQLite FTS5 offers the built-in BM25 ranking algorithm for the search functionality.
# search-non-js
- https://github.com/tj/reds
  - simple full text search module for node.js - backed by Redis

- https://github.com/meilisearch/meilisearch /40.2kStar/MIT/202402/rust
  - https://www.meilisearch.com/
  - fast search engine that fits effortlessly into your apps, websites, and workflow.
  - [Elasticsearch like alternative · Issue · mastodon/mastodon](https://github.com/mastodon/mastodon/issues/20743)
  - https://github.com/meilisearch/arroy /MIT/202312/rust
    - a Rust library with the interface of the Annoy Python library to search for vectors in space that are close to a given query vector.
    - It is based on LMDB, a memory-mapped key-value store, so many processes may share the same data and atomically modify the vectors.
    - There are some other libraries to do nearest neighbor search. However, most of them are memory-bound, and none use LMDB for their storage
  - [Scalability _202203](https://github.com/meilisearch/meilisearch/discussions/2240)
    - 202404: We don't have horizontal scaling yet on the open-source side. However, we will put it on our Cloud offering
    - Note that we already have high availability by using high disk availability from our current provider and leveraging the quick boot time of Meilisearch (<100ms).
    - What will happen if we try to enable HPA on K8s and supply AWS EFS as a shared file system via Persistent Volume Claim to all Meilisearch replicas?
      - Highly unrecommended. Meilisearch uses LMDB internally, our ACID and transactional memory-mapped key-value store. It relies on filesystem principals such as locks to maintain the integrity of the data. Using multiple engines on the same database works but not particularly well on network file systems. You can do that at your own risk. 
- https://github.com/riccox/meilisearch-ui /apache2/202401/ts
  - https://meilisearch-ui.riccox.com/
  - fast meilisearch admin dashboard UI for managing your meilisearch instances

- https://github.com/paradedb/paradedb /AGPLv3/202402/rust/c
  - https://paradedb.com/
  - an ElasticSearch alternative built on PostgreSQL, engineered for lightning-fast full text, similarity, and hybrid search.
  - It offers the most comprehensive, Postgres-native search features of any Postgres database, so you don't need to glue cumbersome services like a search engine or vector database on top.
  - built in Rust on top of PostgreSQL and Tantivy, a Rust-based implementation of Apache Lucene
  - Consolidate your database and search engine into a single system, so you don't need to worry about keeping separate services in sync.
  - Write search queries in SQL with ACID transactions.
  - Scale to millions of rows with support for distributed search, high availability, backups, and point-in-time-recovery.

- https://github.com/valeriansaliou/sonic /18.9kStar/MPLv2/202312/rust
  - lightweight & schema-less search backend. 
  - An alternative to Elasticsearch that runs on a few MBs of RAM.

- https://github.com/toshi-search/Toshi /MIT/202310/rust
  - a full-text search engine similar to Elasticsearch
  - Toshi strives to be to Elasticsearch what Tantivy is to Lucene.

- https://github.com/quickwit-oss/tantivy /MIT/202401/rust
  - Tantivy is a full-text search engine library inspired by Apache Lucene and written in Rust
  - If you are looking for an alternative to Elasticsearch or Apache Solr, check out `Quickwit`, our distributed search engine built on top of `Tantivy`.
- https://github.com/quickwit-oss/quickwit /AGPLv3/202403/rust
  - https://quickwit.io/
  - Cloud-native search engine for observability. 
  - An open-source alternative to Datadog, Elasticsearch, Loki, and Tempo.
  - Elasticsearch-compatible API, use Quickwit with any Elasticsearch or OpenSearch client

- bibliothecula /152Star/GPLv3/202107/rust/archived
  - https://github.com/epilys/bibliothecula
  - https://epilys.github.io/bibliothecula/
  - document organizer with tags and full-text-search, in a simple and clean sqlite3 schema
  - Store plain text notes with automatic full-text search and back-reference indexing
  - a virtual FUSE filesystem written in Rust.
  - an HTTP GUI written in python3 using django.
  - a GTK3 UI in Rust that was written early and isn't functional.
  - an interactive python shell, bibl-shell.py, with convenient types and methods for working with your database:

- https://github.com/slackhq/kaldb /MIT/202401/java/仅搜索不修改
  - a cloud-native search and analytics engine for log, trace, and audit data
  - designed to be easy to operate, cost-effective, and scale to petabytes of data.
  - Non-Goals
    - Document mutability - records are expected to be append only.
    - Additional storage engines other than Lucene.

- https://github.com/zinclabs/zinc /202211/go
  - a search engine that does full text indexing
  - lightweight alternative to elasticsearch that requires minimal resources, written in Go.

- https://github.com/typesense/typesense /202211/cpp
  - Open Source alternative to Algolia and an Easier-to-Use alternative to ElasticSearch

- https://github.com/manticoresoftware/manticoresearch /202211/cpp
  - an easy to use open source fast database for search. 
  - Good alternative for Elasticsearch.

- https://github.com/leontoeides/indicium /apache2/202310/rust
  - simple in-memory search for collections (Vec, HashMap, BTreeMap, etc) and key-value stores. Features autocompletion.
  - Indicium easily can handle millions of records without breaking a sweat thanks to Rust's BTreeMap. 

- https://github.com/cloudant-labs/clouseau /apache2/202401/scala
  - Expose Lucene features as an erlang-like node
# search-ui
- Faceted Search ui
  - [Tailwind CSS Faceted Search Drawers](https://flowbite.com/blocks/application/faceted-search-drawers/)

- elastic-search-ui /1.8kStar/apache2/202212/ts/vanillajs/headless
  - https://github.com/elastic/search-ui
  - https://docs.elastic.co/search-ui/overview
  - https://docs.elastic.co/search-ui/solutions/ecommerce
  - [Customizing Styles and Components](https://codesandbox.io/s/github/elastic/search-ui/tree/main/examples/sandbox?from-embed=&initialpath=/customizing-styles-and-html)
  - Search UI. Libraries for the fast development of modern, engaging search experiences.
  - Flexible front-end - Not just for React. Use with any JavaScript library, even vanilla JavaScript.
  - Flexible back-end - Use it with Elasticsearch, Elastic Enterprise Search, or any other search API.
  - The core is a separate, headless vanilla JS library
    - It provides the underlying "state" and "actions" associated with that view
  - build a custom connector so you can use Search UI with your own API.
  - [A non-react guide to Search UI](https://github.com/elastic/search-ui/issues/332)
  - https://github.com/iMicknl/search-ui-azure-connector
  - [What are you building with Search UI?](https://github.com/elastic/search-ui/issues/793)

- https://github.com/algolia/instantsearch
  - https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/
  - https://codesandbox.io/embed/github/algolia/instantsearch/tree/master/examples/js/getting-started
  - Libraries for building performant and instant search experiences with Algolia. 
  - Compatible with JavaScript, TypeScript, React and Vue.
  - https://github.com/meilisearch/instant-meilisearch
  - https://github.com/typesense/typesense-instantsearch-adapter
    - https://github.com/typesense/typesense-instantsearch-demo
    - https://typesense.org/docs/overview/demos.html
  - https://github.com/unplatform-io/instantsearch-itemsjs-adapter
    - https://github.com/unplatform-io/clientside-instantsearch-demo
    - https://clientside-instantsearch-demo.vercel.app/

- https://github.com/searchkit/searchkit /4.7kStar/apache2/202403/ts
  - http://www.searchkit.co/docs
  - https://www.searchkit.co/demos
  - Search UI for Elasticsearch & Opensearch. 
  - Compatible with Algolia's Instantsearch and Autocomplete components. 
  - core几乎无依赖
  - Works with Javascript, React, Vue, Angular, and more.
  - Searchkit Node API proxies Elasticsearch requests from the browser.
  - https://github.com/searchkit/searchkit-starter-app

- https://github.com/appbaseio/dejavu /8.3kStar/MIT/202301/js/inactive
  - https://dejavu.reactivesearch.io/
  - The Missing Web UI for Elasticsearch: Import, browse and edit data with rich filters
- https://github.com/appbaseio/reactivesearch /apache2/202401/js
  - https://opensource.appbase.io/reactivesearch
  - Search UI components for React and Vue: powered by appbase.io / Elasticsearch

- https://github.com/aralroca/search-engine-wc /MIT/202409/ts
  - https://search-engine-wc.vercel.app/
  - This Web Component allows you to have a search engine similar to Vitepress easily in any framework (React, Brisa, Vue, Solid.js, Svelte, Vanilla JS, etc).
  - MiniSearch, Mark.js, Signals, Declarative Shadow DOM
  - [Brisa Framework](https://brisa.build/)

- https://github.com/hemantwasthere/GitHub-Clone
  - search any github authorized user in this app and checkout there profile

- https://github.com/mohamedbenattia99/Github-repositories-clone
  - a Github repositories clone with search functionality. The project uses THE GITHUB API.

- https://github.com/varianter/handbook
  - https://handbook.variant.no/
  - 依赖mdx2, instantsearch.js, algoliasearch, swr

- https://github.com/tinper-acs/ac-search-panel /202303/js
  - https://tinper-acs.github.io/ac-search-panel/
  - 查询面板 SearchPanel
  - 基于 bee-search-panel 进一步封装，主要将表单元素样式封装进组件内部
# search-solutions
- https://github.com/duolingo/metasearch /apache2/202311/ts
  - Metasearch is a tool for searching many other tools in parallel
  - Search aggregator for Slack, Google Docs, GitHub, and more
  - 支持 Google Drive docs, spreadsheets; Confluence pages; Figma files, projects, and teams; 

- pagefind /2.8kStar/MIT/202402/rust
  - https://github.com/CloudCannon/pagefind
  - https://pagefind.app/
  - Pagefind is a fully static search library that aims to perform well on large sites
  - Pagefind runs after any static site generator and automatically indexes the built static files. 
    - Pagefind runs after Hugo, Eleventy, Jekyll, Next, Astro, SvelteKit, or any other SSG. 
    - Pagefind then outputs a static search bundle to your website, and exposes a JavaScript search API that can be used anywhere on your site.
  - The installation process is always the same: Pagefind only requires a folder containing the built static files of your website
  - After indexing, Pagefind adds a static search bundle to your built files, which exposes a JavaScript search API that can be used anywhere on your site. 
  - [Using Pagefind with a specific SSG](https://pagefind.app/docs/resources/)
    - 支持hugo,hexo,Eleventy,Astro

- https://github.com/dosyago/DiskerNet /AGPLv3/202312/js
  - https://github.com/dosyago/DownloadNet
  - An internet on yer disk. Full text search archive from your browsing and bookmarks.

- https://github.com/answeroverflow/answeroverflow /FSL-1.1-MIT/202406/ts
  - https://www.answeroverflow.com/
  - Indexing Discord Help Channel Questions into Google
  - Powerful analytics - Learn what questions are asked the most, who is most helpful, and other community insights
# full-text-search
- pouchdb-quick-search /370Star/apache2/201702/js/lunr/inactive
  - https://github.com/pouchdb-community/pouchdb-quick-search
  - Full-text search engine on top of PouchDB
  - This is a local plugin, so it is not designed to work against CouchDB/Cloudant/etc. 
  - If you'd like to search against the server, use the CouchDB Lucene plugin, Cloudant's search indexes, or something similar.
  - This plugin uses the classic search technique of TF-IDF

- https://github.com/doriandrn/rxdb-search /202101/ts
  - Search plugin for RxDB based on search-index

- https://github.com/scambier/obsidian-omnisearch /GPLv3/202401/ts/svelte
  - A search engine that "just works" for Obsidian. 
  - Includes OCR and PDF indexing. Images OCR and PDF indexing are only available on desktop
  - it uses the excellent `MiniSearch` library.
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
  - 🍴 forks
    - https://github.com/mvayngrib/level-queryengine
# docsearch
- https://github.com/algolia/docsearch
  - The easiest way to add search to your documentation
  - DocSearch crawls your documentation, pushes the content to an Algolia index and provides a dropdown search experience on your website.
  - [Run your own | DocSearch by Algolia](https://docsearch.algolia.com/docs/legacy/run-your-own/)
    - The scraper is a python tool based on scrapy

- https://github.com/typesense/typesense-docsearch-scraper /MIT/202312/python
  - https://typesense.org/docs/guide/docsearch.html
  - A fork of Algolia's awesome DocSearch Scraper, customized to index data in Typesense

- https://github.com/jquery/typesense-minibar /MIT/202312/js/NoDeps
  - a fast 2kB autocomplete search bar for Typesense. 
  - It is an alternative to typesense-docsearch.js, Algolia DocSearch, InstantSearch, autocomplete-js, and typesense-js.
# code-search
- https://github.com/BloopAI/bloop /apache2/202402/rust/ts
  - https://bloop.ai/
  - a fast code search engine written in Rust.

- https://github.com/bytefish/ElasticsearchCodeSearch /csharp
  - This repository is an Elasticsearch experiment to see how to build a code search engine.
# vector-db
- https://github.com/Stevenic/vectra /200Star/MIT/202312/ts
  - Vectra is a local vector database for Node.js with features similar to Pinecone or Qdrant but built using local files. 
  - Each Vectra index is a folder on disk. There's an index.json file in the folder that contains all the vectors for the index along with any indexed metadata.
  - When queryng Vectra you'll be able to use the same subset of Mongo DB query operators that Pinecone supports and the results will be returned sorted by simularity
  - Keep in mind that your entire Vectra index is loaded into memory
  - https://x.com/tuturetom/status/1796168541395194100
    - 开源了 Perplexity 企业版和 Glean 的平替产品
    - 企业级搜索和最近 Perplexity 公布的企业级动作以及 Glean 产品非常像
    - Ocular AI 产品的核心初衷是因为目前各种 SaaS 软件信息查找很困难，这个领域的用户诉求是：
    1. 在工作中快速找到需要的信息：比如任务、文档、Slack threads
    2. 管理复杂的工程工具：比如很多软件、程序的使用文档、日志等
# search-ai-gpt
- https://github.com/OcularEngineering/ocular /Elastic/202406/ts
  - https://www.useocular.com/
  - AI Powered Search and Chat for Orgs - Think ChatGpt meets Google Search but powered by your data.
  - Ocular is a set of modules and tools that allow you to build rich, reliable, and performant Generative AI-Powered Search Platforms without the need to reinvent Search Architecture.
  - Google Like Search Interface - Find what you need
  - App MarketPlace - Connect to all of your favorite Apps
  - Custom Connectors - Build your own connectors to proprietary data sources.
  - Customizable Modular Infrastructure - Bring your own custom LLM's, Vector DB and more into Ocular
  - Governance Engine - Role Based Access Control, Audit Logs etc.

- https://github.com/leptonai/search_with_lepton /apache2/202401/python/ts
  - https://search.lepton.run/
  - Build your own conversational search engine using less than 500 lines of code.
  - Built-in support for LLM
  - Shareable, cached search results

- https://github.com/Nutlope/turboseek /202406/ts
  - https://www.turboseek.io/
  - AI search engine inspired by Perplexity
  - An open source AI search engine. Powered by Together.ai.
# more-search
- https://github.com/typicode/json-server
  - Get a full fake REST API with zero coding
  - support Full-text search `GET /posts?q=internet`
