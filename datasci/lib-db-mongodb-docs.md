---
title: lib-db-mongodb-docs
tags: [docs, mongodb]
created: 2022-06-13T02:58:31.397Z
modified: 2022-06-13T02:58:46.880Z
---

# lib-db-mongodb-docs

# guide

# overview

# [MongoDB 极简实践入门](https://github.com/StevenSLXie/Tutorials-for-Web-Developers/blob/master/MongoDB%20%E6%9E%81%E7%AE%80%E5%AE%9E%E8%B7%B5%E5%85%A5%E9%97%A8.md)
- 传统的计算机应用大多使用关系型数据库来存储数据，比如大家可能熟悉的MySql, Sqlite等等，它的特点是数据以表格(table)的形式储存起来的。
  - 涉及到复杂的跨表查询，需要大量使用join语句。这种跨表查询不仅降低了查询速度，而且这些语句写起来也不简单。
- 在MongoDB里，每篇博客文章以一个文档(document)的形式保存起来，而文档内部包含了很多项目，每一个项目都是key-value的形式
  - 重要的是，一个key可以有多个values，他们用[]括起来。
- 这种“宽松”的数据存储形式非常灵活，MongoDB不限制每个key对应的values的数目。
  - 更灵活的是，MongoDB不要求同一个集合(collection，相当于SQL的table)里面的不同document有相同的key
- 这些不同的文档都可以灵活地存储在同一个集合下，而且查询起来也异常简单，因为都在一个文档里，不用进行各种跨文档查询。
- 
- 

# [Embedded Documents](https://www.geeksforgeeks.org/mongodb-embedded-documents/)
- MongoDB provides you a cool feature which is known as Embedded or Nested Document
  - Embedded document or nested documents are those types of documents which contain a document inside another document. 
  - Or in other words, when a collection has a document, this document contains another document, another document contains another sub-document, and so on, then such types of documents are known as embedded/nested documents. 
- In MongoDB, you can only nest document up to 100 levels.
  - The overall document size must not exceed 16 MB.

- To specify a query condition on fields in an embedded/nested document, use dot notation ("field.nestedField").
