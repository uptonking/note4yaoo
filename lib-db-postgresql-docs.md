---
title: lib-db-postgresql-docs
tags: [docs, postgresql]
created: 2022-06-13T03:00:31.773Z
modified: 2022-06-13T03:00:51.734Z
---

# lib-db-postgresql-docs

# guide

- [PostgreSQL wiki](https://wiki.postgresql.org/wiki/Main_Page)
  - [A Brief History of PostgreSQL](https://www.postgresql.org/docs/current/history.html)

- cli-pg
  - [psql](https://www.postgresql.org/docs/current/app-psql.html)
  - [PostgreSQL Cheat Sheet - neon](https://neon.tech/postgresql/postgresql-cheat-sheet)
  - [PostgreSQL command line cheatsheet](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546)
# pg-tips
- [Don't Do This - PostgreSQL wiki](https://wiki.postgresql.org/wiki/Don%27t_Do_This)
  - only do it if you know what you are doing

- [PostgresqlCO. NF: PostgreSQL configuration for humans](https://postgresqlco.nf/doc/en/param/)
  - useful reference for all the PG config options, organized by version
# docs

## [16: F.18. hstore — hstore key/value datatype](https://www.postgresql.org/docs/current/hstore.html)

- This module implements the `hstore` data type for storing sets of key/value pairs within a single PostgreSQL value. 
  - This can be useful in various scenarios, such as rows with many attributes that are rarely examined, or semi-structured data. 
  - Keys and values are simply text strings.
- The order of the pairs is not significant (and may not be reproduced on output).

- [18: 65.4. GIN Indexes](https://www.postgresql.org/docs/current/gin.html)
  - GIN stands for Generalized Inverted Index. 
  - GIN is designed for handling cases where the items to be indexed are composite values, and the queries to be handled by the index need to search for element values that appear within the composite items. 
  - For example, the items could be documents, and the queries could be searches for documents containing specific words.
  - We use the word item to refer to a composite value that is to be indexed, and the word key to refer to an element value. GIN always stores and searches for keys, not item values per se.
  - A GIN index stores a set of (key, posting list) pairs, where a posting list is a set of row IDs in which the key occurs. The same row ID can appear in multiple posting lists, since an item can contain more than one key.
  - One advantage of GIN is that it allows the development of custom data types with the appropriate access methods, by an expert in the domain of the data type, rather than a database expert. This is much the same advantage as using GiST.
  - https://x.com/BenjDicken/status/2001296372134527114
    - They’re great for inverting the typical index use case.
    - Instead of mapping “the row with ID 2 contains the value ‘become a database expert’” you flip it to say “The token ‘database’ maps to the rows with IDs 1, 2, and 3 and ‘expert’ maps to the row with ID 2.”
    - GIN indexes are given a set of values for each row you want to index. Each unique value becomes a key in the index, and maps to the set of CTIDs (row tuple identifiers) containing that value.

- 
- 
- 
- 
- 
- 
- 
- 

# more
- [Ubuntu PostgreSQL安装和配置](https://www.cnblogs.com/Siegel/p/6917213.html)
