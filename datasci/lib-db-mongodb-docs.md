---
title: lib-db-mongodb-docs
tags: [docs, mongodb]
created: '2022-06-13T02:58:31.397Z'
modified: '2022-06-13T02:58:46.880Z'
---

# lib-db-mongodb-docs

# guide

# overview

# [Embedded Documents](https://www.geeksforgeeks.org/mongodb-embedded-documents/)
- MongoDB provides you a cool feature which is known as Embedded or Nested Document
  - Embedded document or nested documents are those types of documents which contain a document inside another document. 
  - Or in other words, when a collection has a document, this document contains another document, another document contains another sub-document, and so on, then such types of documents are known as embedded/nested documents. 
- In MongoDB, you can only nest document up to 100 levels.
  - The overall document size must not exceed 16 MB.

- To specify a query condition on fields in an embedded/nested document, use dot notation ("field.nestedField").
