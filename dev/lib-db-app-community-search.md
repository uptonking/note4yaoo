---
title: lib-db-app-community-search
tags: [community, database, search]
created: 2023-10-26T19:55:59.634Z
modified: 2023-10-26T19:56:12.974Z
---

# lib-db-app-community-search

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## What is the sqlite equivalent for document search? 
- https://twitter.com/squarecog/status/1768773259653533755
  - Like if I have a few doc files and I want to create a tiny index and query it from my code, with no other infra to run?
- doesn't really exist unfortunately. sqlite has an FTS module but it's not very good.
- Tantivy came closest 
- Depending on the size, you could use FAISS to embed and index your dataset. Then run similarity search, vector clustering and more as if you had an in memory DB.

# discuss-text-search
- ## 

- ## 

- ## 

- ## If you have a text search feature in your product, how do you implement it?
- https://twitter.com/aboodman/status/1760036352220143772
  - db-fts vs lucene vs ilike

- People underestimate what can be done with client side searching. 9/10 it can, in my experience, be implemented fully client side.
- dataset is small enough that loading everything on the frontend, with fuse.js and periodic indexing works surprisingly well.

- we are making this decision right now. probably going with postgres fts and expecting to replace it in a year when it inevitably gets slow / isn't good enough. or when @paradedb is usable on @render and we can have the best of both worlds.
- Couchbase has an FTS engine that works along the query engine. It’s really convenient because I can filter the documents upstream within an SQL-like query.

- pinecone hybrid + elastic
- Semantic search with Pinecone, Google’s Multimodal embeddings, and Firebase cloud functions

- Text search is effectively my entire product, so not typical or representative. But I use Vespa. Would switch to any search product that nicely implemented end to end retrieval with Colbert though.

- Actually building my own right now. wouldn’t recommend it for most people, inverse indexes are a bitch to work with
# discuss-pm-search
- ## 

- ## 

- ## 

- ## 11 种语言，700GB 数据，1.44 亿个向量，索引整个维基百科
- https://x.com/tuturetom/status/1824265560483570115
  - @upstash 开源 「Semantic Search on Wikipedia」并提供在线体验地址
- https://github.com/upstash/wikipedia-semantic-search /MIT/202408/ts
  - https://wikipedia-semantic-search.vercel.app/
  - Semantic Search on Wikipedia with Upstash Vector
- 这类的数据和embedding开源意义更大. 看了下是bge-m3的embedding model (看重多语言) 具体chunk是用的自然段, 然后过滤掉过短的.

# discuss-recsys
- ## 

- ## 

- ## 

- ## TikTok just open-sourced their recommender system framework (Monolith) -- and it uses Keras _20241220
- https://x.com/fchollet/status/1869949776764252328
  - This means that nearly all the major recommender systems in the industry are built on Keras -- YouTube, TikTok, Spotify, Snap, X/Twitter, and many more (Grubhub...)

- wild how Keras became the unofficial standard for big tech recommenders... feels like Python/PyTorch vs TensorFlow wars are settling

- X/Twitter doesn’t use Keras
# discuss
- ## 

- ## 搜索引擎&爬虫工程师的工具链感觉现在全面面临洗牌了。
- https://x.com/karminski3/status/1879333078558179725
  - 以前靠SVM来分类，靠 TF-IDF 来抽关键词，trie-tree 来过滤敏感词，基于文本密度算法来抽正文，靠余弦相似度等相似度算法来消重。
  - 现在，大模型能全面取代这些传统NLP做法了。
- 不仅仅是这个层面，传统NLP的很多方向都会面临问题。我们原来七八个算法(有教授、博士、大厂经历)建立的产品，现在准备用大模型重构，发现可以没有算法或者只需要一个了解算法基本概念的工程也可以做到。

- 目前 RAG 领域，感觉还是需要结合传统的搜索那套。

- 垂域对精确度有要求的，还是bert和传统方法好用，llm只是泛化强。但从科研角度传统nlp确实没必要做了
  - 是的，不过我觉得垂搜现在面临的新挑战不光是精度，而是多种媒体类型，现在大多数垂直社区都是短视频+图了。对这些内容进行索引也不是传统NLP能很好解决的了
- 图片, 视频内容的文字化, 对于LLM模型吃算力, 不是一般公司能养的起来的. 模型是开源, 但是养不起.

- ## [Elasticsearch SQL | Hacker News_202210](https://news.ycombinator.com/item?id=33320477)
- MongoDB has an SQL interface these days if you need it
- Seems like all the NoSQL databases eventually implement SQL, maybe we should use EventuallySQL instead NoSQL
- Even DynamoDb has one
- Microsoft's CosmosDB (their DocumentDB clone) has a SQL-like (yes) interface.
- Cassandra added CQL which is very similar to but not exactly SQL.
- Hadoop (and any other Spark data source) via SparkSQL

- I would like SQL better if jOOQ-style libraries were common across every major language. A standardized query language is good, but passing in queries as strings will never not feel wrong to me.
# discuss-code-search
- ## 

- ## 

- ## 🌰 The code search on GitHub is a great tool. But how does it work?
- https://twitter.com/Franc0Fernand0/status/1762094007348306234
  - You can search over 200M+ public repositories in seconds with it. 

- The code search problem is not the same as the normal full-text search.
- Full text lets you look through all the words in a file to find a search term. 
  - This is a well-known problem that systems like Lucene and Elasticsearch handle.
- Code search is different and has its own rules:
  - there is no stemming(词干)
  - punctuations are ignored
  - words from queries are left intact
- GitHub uses Blackbird: a Rust-based search engine tailored to search through programming languages.
- All text search engines use a data structure called Inverted Index. 
- An inverted index resembles an index section of a textbook:
  - all words are ordered alphabetically
  - each word is followed by page numbers where the word is found
- Blackbird uses a particular type of inverted index called an n-gram index. 
  - Building such a data structure at the GitHub scale was quite challenging. 
- The collection of documents was too large for a single inverted index. 
  - How to deal with this? By sharding.
  - Documents are partitioned across shards based on blob object IDs. This ID is given by the SHA-1 hash of the file contents; thus, identical files always share the same ID. 

- Architectures for crawling and indexing are generally stream processing flows that transform and augment the data as it is collected. Not surprising that Kafka plays a big role there.
