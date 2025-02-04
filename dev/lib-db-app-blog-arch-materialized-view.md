---
title: lib-db-app-blog-arch-materialized-view
tags: [blog, database, materialized-view, query-engine]
created: 2023-12-03T07:38:52.894Z
modified: 2023-12-03T07:39:22.832Z
---

# lib-db-app-blog-arch-materialized-view

# guide

# blogs

## [Incremental View Maintenance - PostgreSQL wiki](https://wiki.postgresql.org/wiki/Incremental_View_Maintenance)

- PostgreSQL has supported materialized views since 9.3. 
  - This feature is used to speed up query evaluation by storing the results of specified queries. 
  - One problem of materialized view is its maintenance. Materialized views have to be brought up to date when the underling base relations are updated.
- Incremental View Maintenance (IVM) is a technique to maintain materialized views which computes and applies only the incremental changes to the materialized views rather than recomputing the contents as the current REFRESH command does. 
  - This feature is not implemented on PostgreSQL yet. 
- IVM computes and applies only the incremental changes to the materialized views. 
  - Suppose that `view V` is defined by `query Q` over a state of base `relations D`.
  - When D changes `D' = D + dD`, we can get the new view state V' by calculating from D' and Q, and this is re-computation performed by `REFRESH MATERIALIZED VIEW` command. 
  - On the other hand, IVM calculates the delta for view (dV) from the base tables delta (dD) and view definition (Q), and applies this to get the new view state `V' = V + dV`.
- In theory, the view definition is described in a relational algebra (or bag algebra) form. For example, a (inner) join view of table R and S is defined as V = R ⨝ S.

- How to extract changes on base tables
  - There are at least two approaches. 
  - One is using AFTER triggers and Transition Tables, which is a feature of AFTER trigger introduced from PostgreSQL 10. This was implemented originally aiming to support IVM, and in fact the proposed patch uses this. This enables collect row sets that include all of the rows inserted, deleted, or modified by the current SQL statement.
  - Another candidate is using logical decoding of WAL.

- How to calculate the delta to be applied to materialized views
  - This is basically based on relational algebra or bag algebra. 
  - In theory, we can handle various view definition. Views can be defined using several operations: selection, projection, join, aggregate, union, difference, intersection, etc. 
  - If we can prepare a module for each operation, there is possibility of extensive implementation of IVM.

- When to maintain materialized views
  - There are two approaches, immediate maintenance and deferred maintenance.
  - In immediate maintenance, views are updated in the same transaction where the base table is updated. The proposed patch implements a kind of immediate maintenance, that is, materialized views are updated immediately in AFTER triggers when a base table is modified. SQL statement modify only one base table and the changes can be extracted by using Transition Tables mentioned above.
  - In deferred maintenance, views are updated after the transaction is committed, for example, when the view is accessed, as a response to user command like REFRESH, or updated periodically, and so on.

- How to identify rows to be modified in materialized views
  - When applying the delta to materialized views, we have to identify which tuple in materialized views is corresponding to a tuple in the delta. 
  - A naive method is matching by using all columns in a tuple, but clearly this is inefficient. If a materialized view has unique index, we can use this. 

## [Caching Partially Materialized Views Consistently](https://blog.the-pans.com/caching-partially-materialized-views-consistently/)

- According to the PostgreSQL wiki
  - A materialized view is a table that actually contains rows, but behaves like a view.
  - That is, the data in the table changes when the data in the underlying tables changes.

- According to Wikipedia
  - a materialized view is a database object that contains the results of a query.
  - For example, it may be a local copy of data located remotely, or may be a subset of the rows and/or columns of a table or join result, or may be a summary using an aggregate function.

- 👉🏻 A materialized view is a cache.
  - Since any data can be described with the relational model, we can also say every cache is a partially materialized view – I mean every cache. 
  - No matter if it is a cpu cacheline, a DNS entry cached in your browser, or some value in memory your application memoized, it can be reasoned about as a partially materialized view. 
  - Even a cached computation result is a partially materialized view; 
- A cache and a partially materialized view are essentially the same thing. In a database (e.g. PostgreSQL, Oracle, etc.), the materialized view is explicitly defined.
# blogs-usecase

## [Support for Materialized Views · crate/cratedb](https://github.com/crate/crate/issues/10661)

# more
