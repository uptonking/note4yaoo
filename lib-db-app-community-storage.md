---
title: lib-db-app-community-storage
tags: [community, database, storage]
created: 2023-09-17T17:35:57.181Z
modified: 2023-09-17T17:36:36.118Z
---

# lib-db-app-community-storage

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

- ## [Soft deletion probably isn't worth it | Hacker News_202207](https://news.ycombinator.com/item?id=32156009)
- I've been a software dev since the 90s and at this point, I've learned to basically do things like audit trails and soft deletion by default, unless there's some reason not to.
  - Somebody always wants to undelete something, or examine it to see why it was deleted, or see who changed something, or blah blah blah. It helps the business, it helps you as developer by giving you debug information as well as helping you to cover your ass when you are blamed for some data loss bug that was really user error.
  - **Soft deletion has obvious drawbacks but is usually far less work than implementing equivalent functionality out-of-stream**, with verbose logging or some such.
  - Retrofitting your app and adding soft deletion and audit trails after the fact is usually an order of magnitude more work. Can always add it pre-launch and leave it turned off.
- If performance is a concern, this is usually something that can be mitigated. You can e.g. have a reaper(收割者；收获者) job that runs daily and hard-deletes everything that was soft-deleted more than n days ago, or whatever.

- Views are a simple solution to this problem. Pretty much all moderns RDBMSs support **updatable views**, so creating views over your tables with a simple WHERE deleted_at IS NULL solves the majority of the author's problems, including (IIRC) foreign key issues, assuming the deletes are done appropriately.
  - I feel like a lot of developers underutilize the capabilities of the massively advanced database engines they code against. Sure, concerns about splitting logic between the DB and app layers are valid, but there are fairly well developed techniques for keeping DB and app states, logic and schemas aligned via migrations and partitioning and whatnot.

- Cascaded deletes scare me anyway. It only takes one idiot to implement UPSERT as DELETE+INSERT because it seems easier, and child data is lost. You could always use triggers to cascade you soft-delete flags as an alternative method, though that would be less efficient (and more likely to be buggy) than the built-in solution that cascaded deletes are.
- If you look at how system-versioned (or “temporal”) tables are implemented in some DBMSs, that is a good compromise. The history table is your audit, containing all old versions of rows even deleted ones, and the base table can be really deleted from, so you don't need views or other abstractions away from the base data to avoid accidentally resurrecting data. You

- 
- 
- 
- 
- 
- 
