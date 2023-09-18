---
title: lib-db-app-community-query-engine
tags: [community, database, query-engine]
created: 2023-09-17T17:41:27.117Z
modified: 2023-09-17T17:41:51.689Z
---

# lib-db-app-community-query-engine

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-view
- ## 

- ## 

- ## [Practical advice for creating (and updating) materialized views? : PostgreSQL](https://www.reddit.com/r/PostgreSQL/comments/hvysvi/practical_advice_for_creating_and_updating/)
- Dimtri Fontaine recommends using the publish / subscribe messaging queue feature, ON UPDATE and have a listener that consumes the message and triggers the refresh

- ## [Materialized Views vs Views](https://www.reddit.com/r/SQL/comments/158498q/materialized_views_vs_views/)
- I could be wrong, but the way I view (ha) this is:
  - A View is a dynamic query. It is a table that is not stored, but rather it is a select query that is executed every time you query that view.
  - A materialized view seems to be the result of a query that is stored on disk, meaning it is not dynamic and does not change unless you refresh it or overwrite it somehow.
  - So if your original table is updated somehow, the view will also bring that new information while the materialized view won't change.
- If your view is joining a lot of tables or is doing something complicated/not optimized very well and is slow to load. It may be better to create a materialized view so that the result is stored to disk

- to the end-user, a View is basically just a table. It has a query which produces the view, but when you work with a view, you treat it like a table.
  - A Materialized View simply caches the result (on disk) such that the underlying query doesn't need to be run each time. You might use something like this to set up some historical sales data for an analyst. 

- There’s a difference between materialized views in Oracle and SQL Server though.
  - In Oracle it’s as you describe: a view stored on disk that is refreshed periodically to increase performance of slow running views.
  - In SQL Server, a materialized view is created when you add an index to the view. SQL Server will keep the MV current without having to schedule periodic refreshes.
# discuss
- ## 

- ## 

- ## 

- ## [How Query Engines Work | Hacker News](https://news.ycombinator.com/item?id=37415494)
