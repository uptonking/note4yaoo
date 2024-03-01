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
# discuss
- ## 

- ## 
