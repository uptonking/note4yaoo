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

- ## 
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
