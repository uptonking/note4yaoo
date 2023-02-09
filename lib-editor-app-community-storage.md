---
title: lib-editor-app-community-storage
tags: [community, data-structure, editor, storage]
created: 2022-08-30T01:17:48.887Z
modified: 2022-08-30T01:18:19.063Z
---

# lib-editor-app-community-storage

# guide

# discuss-stars

## 

## 

# discuss

## 

- ## [What is the recommended way to store data in a database/create a controlled editor component? · Issue #66 · typewriter-editor/typewriter](https://github.com/typewriter-editor/typewriter/issues/66)
- `editor.getHTML() and editor.setHTML(value)` would work better for rich text. 
  - 👉🏻 If you can save JSON to your store, saving `editor.doc` and restoring it with `editor.set(doc)` is even better.

## [Storing JSON in database vs. having a new column for each key](https://stackoverflow.com/questions/15367696)

- the drawback of the approach is exactly what you mentioned :
  - it makes it VERY slow to find things, since each time you need to perform a text-search on it.
  - value per column instead matches the whole string.
  - (JSON based data) is fine for data you don't need to search by, and just need to display along with your normal data.

- Since 5.7, MySQL now supports a JSON data type (in a binary storage format), 
  - and PostgreSQL `JSONB` has matured significantly. 
  - Both products provide performant JSON types that can store arbitrary documents, including support for indexing specific keys of the JSON object.
- However, I still stand by my original statement that your default preference, when using a relational database, should still be column-per-value. 
  - Relational databases are still built on the assumption of that the data within them will be fairly well normalized. 
  - The query planner has better optimization information when looking at columns than when looking at keys in a JSON document.
- That said, few applications are perfectly relational or document-oriented. Most applications have some mix of both. 
- Here are some examples where I personally have found JSON useful in a relational database(json常用于半结构化或非结构化的数据):
  - When storing email addresses and phone numbers for a contact, where storing them as values in a JSON array is much easier to manage than multiple separate tables
  - Saving arbitrary key/value user preferences (where the value can be boolean, textual, or numeric, and you don't want to have separate columns for different data types)
  - Storing configuration data that has no defined schema (if you're building Zapier, or IFTTT and need to store configuration data for each integration)

- Looking back, JSON allowed us to iterate very quickly and get something out the door. It was great. However after we reached a certain team size it's flexibility also allowed us to hang ourselves with a long rope of technical debt which then slowed down subsequent feature evolution progress. Use with caution.

## [What are the known ways to store a tree structure in a relational DB?](https://stackoverflow.com/questions/3362669)

- As always: there is no best solution. 
  - The right solution for you depends on which operation you will do most.

- Naive Approach with parent-id
- Modified Preorder Tree Traversal (saving a start- & end-point) 
  - uses a non-recursive function (usually a single line of SQL) to retrieve trees from the database, at the cost of being a little trickier to update
  - in case not modify the tree structure frequently
- Saving a path in each Node
- Closure table
- Nested sets
