---
title: lib-db-app-community-local-first-offlineable
tags: [community, database, local-first, offlineable]
created: 2023-09-22T19:27:50.280Z
modified: 2023-09-22T20:15:10.616Z
---

# lib-db-app-community-local-first-offlineable

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

- ## 

- ## 

- ## 

- ## [Offline-First Database Comparison | Hacker News_202110](https://news.ycombinator.com/item?id=28995268)

- 
- 
- 

- I had a really great experience building an EAV store with Datalog as the query interface on top of SQLite for embedding in native mobile apps.
  - Pros: querying complex data hierarchies was easy, and was able to skip the pain typically associated with managing a SQL schema.
- What’s the application for this? EAV is often an anti-pattern when a schema could be defined, but I’m actually using it as well. Our application is an end-user-defined database for mobile data collection. The EAV model in SQLite is a bit of a cognitive burden but makes offline sync and conflict resolution pretty straight forward. It’s almost a crude(简陋的；粗糙的) CRDT implementation.
- I wasn't aware that EAV is an anti-pattern in that case. Is it an efficiency thing?
  - For clarity, my design wasn't schemaless, values (can) have defined datatypes and relationships are first-class. I meant that I found adding to or modifying the schema was less cumbersome and error prone than traditional SQL schema additions or changes. I feel like SQL schema management is more suited to server-based dbs where you have tight control over the db lifecycle, which you don't when it lives on a bunch of mobile devices.
  - Totally agree with the ease of sync and conflict resolution, another strong pro.

- Are you able to elaborate on why you chose EAV over using something like the json1 extension of SQLite?
- It was built on a single table that held the entity-attribute-value tuple along with some additional metadata like type information, whether or not the attribute was a pointer to another entity, and the cardinality of that relationship (one or many).
  - Relationships were walked via self joins and the eav columns were all indexed.
- This sounds very similar to what we’re doing and we are in the process of migrating most of the EAV models (other than the relationships) to a json1 column (Which I’d argue is still EAV just in document format). Keeping the relationship foreign keys outside of the json allows the database itself to enforce referential integrity.
  - The **difficulty with having all attributes be EAV** becomes apparent when having to do multiple joins to fetch a single record type (what would be a “table” traditionally). 
  - Although this is manageable, the **bigger difficulty** I’ve found is synchronizing deletions of records, especially if deletions/insertions are done in bulk. 
  - Rather than just 1 transaction you have to do multiple delete/insert queries to also delete/insert the attributes and the values and they should be done in a way that doesn’t break key constraints.

- You might be interested in the now defunct Mentat project from Mozilla. They made an EAV store with syncing on top of sqlite. **It ran datalog queries by translating them into sql**.

- 
- 
- 
- 
