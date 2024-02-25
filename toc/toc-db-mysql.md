---
title: toc-db-mysql
tags: [db, mysql, toc]
created: 2024-02-25T15:17:13.153Z
modified: 2024-02-25T15:17:25.833Z
---

# toc-db-mysql

# guide

# popular

# extensions

# utils

# devops
- https://github.com/facebookincubator/OnlineSchemaChange /BSD/202402/python
  - A tool for performing online schema changes on MySQL.
  - a tool for making schema changes for MySQL tables in a non-blocking way
  - OSC must be run on the same host as MySQL server.
  - OSC works outside of replication, all the statements are issued under `sql_log_bin=0`. It can be run on either replica or master at your demand. This means you can issue a schema change on one replica first for prove of concept and then roll out to master when you're sure about the change
# more
