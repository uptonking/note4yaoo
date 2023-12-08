---
title: pattern-local-first-community-db
tags: [community, database, local-first]
created: 2023-12-01T09:08:04.006Z
modified: 2023-12-01T09:08:18.316Z
---

# pattern-local-first-community-db

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 🚀 Meet SQLSync: Application development is a lot easier when you're building on top of a frontend-optimized database stack. _20231201
- https://twitter.com/carlsverre/status/1730288131419861420
  - I’m building SQLSync because I want to make client-side applications easier to build without us having to reinvent the wheel each time.
- How do you think about:
  - a) Changing a row's visibility per user (e.g. more granular  RBAC than segmenting access to sync'd databases per org)
  - b) State that a user could see that's too large to fit in the browser
- Good questions!
  - a) I think any sub-db segmentation will have to wait for partial two-way replication, have some ideas but nothing in code yet
  - b) partial replication; or lazy sync: retrieve pages lazily, sync invalidation sets

- Currently SQLSync moves the entire database to every client and keeps them all in sync. This means that it's suited for smallish sets of relational data - ideally per-user or per-document. This is made easier as each db is very cheap to create.
  - this model works very well with @tursodatabase , since we can offer 10k databases for $29 - and more on enterprise plans. We are drooling for an integration here!

- ## [ObjectBox: Fast object-oriented database for Go | Hacker News_201811](https://news.ycombinator.com/item?id=18568029)
- SQLite is a very nice embedded DB indeed. If you like SQL. ObjectBox enables you to work with Go structs and gives you additional performance.

- It's ACID compliant, and thus not not in-memory. https://golang.objectbox.io/faq covers that in detail. In the FAQ, there is a section on comparing to JSON; I guess the same would hold true for CSV.
