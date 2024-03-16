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
# discuss
- ## 

- ## 

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
