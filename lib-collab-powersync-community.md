---
title: lib-collab-powersync-community
tags: [collaboration, community, powersync]
created: 2024-02-12T03:22:48.188Z
modified: 2024-02-12T03:23:17.007Z
---

# lib-collab-powersync-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## If you're curious about building local-first, YSK about dynamic data partitioning.
- https://twitter.com/powersync_/status/1763579694220259533
  - Unless all data should be shared across all users, you need a system that controls which data gets replicated to which users' local databases.
  - For this we have Sync Rules, a system that creates "data buckets" (akin to live views) of exactly the data that each app user should have access to, at any point in time. Put differently, Sync Rules create dynamic data partitions.
  - For example, if a user creates a new record, their data bucket dynamically grows to include that record. If that record should be shared with any other users, their data buckets will dynamically adjust as well.
