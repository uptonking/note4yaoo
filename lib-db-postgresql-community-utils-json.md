---
title: lib-db-postgresql-community-utils-json
tags: [community, hstore, json, jsonb, postgresql]
created: 2024-03-01T09:18:49.953Z
modified: 2024-03-01T09:19:11.669Z
---

# lib-db-postgresql-community-utils-json

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-comparison 🆚️
- ## 

- ## 

- ## 

- ## 🆚️ [hStore Vs. JSONB in postgreSQL | Medium _202310](https://medium.com/@alireza.stack/hstore-vs-jsonb-in-postgresql-c7e772cba6ab)
- In PostgreSQL, both hstore and JSONB are data types that allow you to store semi-structured or key-value data. 

- hstore is a PostgreSQL data type that stores key-value pairs.
  - Keys and values in hstore must be text.
  - hstore is a good choice when you have simple key-value data with textual keys and values.
  - It provides a set of built-in operators and functions for querying and manipulating data.
  - 🐛 It does not support nested structures or complex data types.

- JSONB is a PostgreSQL data type that stores JSON data in a binary format, which provides efficient storage and retrieval.
  - JSONB supports nested structures, arrays, and various data types (text, numbers, booleans, etc.) as values.
  - You can query JSONB data using a wide range of functions and operators for JSON manipulation.
  - JSONB also allows indexing for faster searches on specific keys within the JSON data.
  - JSONB is more flexible and versatile than hstore and is a good choice when dealing with complex or hierarchical data.

- If you need indexing capabilities for specific keys within your JSON data, JSONB is better suited for this purpose.
- If you want to ensure strict data validation and enforcement of data types, JSONB allows you to define JSON schemas to some extent.
# discuss-jsonb
- ## 

- ## 

- ## 

- ## 🆚 [Postgres with large JSONBs vs ElasticSearch : r/PostgreSQL _202601](https://www.reddit.com/r/PostgreSQL/comments/1q5ts8u/postgres_with_large_jsonbs_vs_elasticsearch/)
  - A common scenario in data science is to dump JSON data in ElasticSearch to enable full-text searching/ranking and more. Likewise in Postgres one can use JSONB columns, and pg_search for full-text search, but it's a simpler tool and less feature-rich.
  - However I was curious to learn how both tools compare (PG vs ES) when it comes to full-text search on dumped JSON data in Elastic and Postgres (using GIN index on tsvector of the JSON data). So I've put together a benchmarking suite with a variety of scales (small, medium, large) and different queries. 
  - https://github.com/inevolin/Postgres-FTS-TOASTed-vs-ElasticSearch
  - TL; DR: Postgres and Elastic are both competitive for different query types for small and medium data scales. But in the large scale (+1M rows) Postgres starts losing and struggling. [FYI: 1M rows is still tiny in the real world, but large enough to draw some conclusions from]
  - This benchmark is intentionally designed to keep the PostgreSQL JSONB payload large enough to be TOASTed for most rows (out-of-line storage). That means results reflect “search + fetch document metadata from a TOAST-heavy table”, not a pure inverted-index microbenchmark.
  - A key learning for me was that JSONB fields should ideally remain under 2kB otherwise they get TOASTed with a heavy performance degradation. 

- So basically, postgres is faster than elastic until the jsonb documents become big enough to require toast?
  - Thats the tl; dr more or less. But pg is not faster/better on every metric/query either, and definitely not at larger scales.

- Add a metric for concurrent queries per node, that’s where elastic would crash even on the <16GB shards. You’ll be seeing interesting things when you plot dataset size on one axis, concurrent users on another, and response time in color gradient

- ## Postgres has lots of types, but you really only need 2: id(serial), jsonb
- https://x.com/tomdoes_tech/status/1892675795828801877
- Good but not perfect yet - why do we need bother with multiple tables when we can have a single table with id, table_name and data?
  - At that point, embrace DynamoDB and embrace the single table design pattern using the power of partition and sort key lookups. It can be massively powerful and scalable if done correctly.

# discuss-postgis
- ## 

- ## 

- ## 

- ## Postgres is more than a relational database. The PostGIS extension turns Postgres into a geo database. 
- https://twitter.com/denismagda/status/1783892446050504934
  - @openstreetmap uses Postgres with PostGIS to let you use the map of the entire world for free

# discuss
- ## 

- ## 
