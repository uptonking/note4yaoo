---
title: lib-db-postgresql-community-datatype
tags: [community, datatype, postgresql]
created: 2025-02-28T16:09:31.951Z
modified: 2025-02-28T16:10:09.331Z
---

# lib-db-postgresql-community-datatype

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## In PostgreSQL, inserting "hello" into char(10) and varchar(10) columns will store them differently: 
- https://x.com/andrii_sherman/status/1895472710785875990
  - char(10) -> "hello     " (padded with spaces)
  - varchar(10) -> "hello"
  - "If the string to be stored is shorter than the declared length, values of type character will be space-padded; values of type character varying will simply store the shorter string."

- not if there is a unique constraint and there is already a hello in the the column
