---
title: lib-db-sqlite-docs
tags: [docs, sqlite]
created: 2021-08-30T17:32:48.451Z
modified: 2021-08-30T17:33:20.586Z
---

# lib-db-sqlite-docs

# guide

# [CREATE TABLE](https://www.sqlite.org/lang_createtable.html)
- Each table in SQLite may have at most one PRIMARY KEY. 
  - If the keywords PRIMARY KEY are added to a column definition, then the primary key for the table consists of that single column. 
  - The PRIMARY KEY is optional for ordinary tables
- If a table has a single column primary key and the declared type of that column is "INTEGER" and the table is not a WITHOUT ROWID table, then the column is known as an `INTEGER PRIMARY KEY`. 
  - According to the SQL standard, PRIMARY KEY should always imply NOT NULL. Unfortunately, due to a bug in some early versions, this is not the case in SQLite. 
- Except for `WITHOUT ROWID` tables, all rows within SQLite tables have a 64-bit signed integer key that uniquely identifies the row within its table. 
  - This integer is usually called the `rowid`. 
  - The `rowid` value can be accessed using one of the special case-independent names "rowid", "oid", or "_rowid_" in place of a column name.
  - If a table contains a user defined column named "rowid", "oid" or "_rowid_", then that name always refers the explicitly declared column and cannot be used to retrieve the integer rowid value.
- The data for rowid tables is stored as a B-Tree structure containing one entry for each table row, using the rowid value as the key. 
  - This means that retrieving or sorting records by rowid is fast. 
- if a rowid table has a primary key that consists of a single column and the declared type of that column is "INTEGER" in any mixture of upper and lower case, then the column becomes an alias for the rowid. Such a column is usually referred to as an `integer primary key`.
- Rowid values may be modified using an UPDATE statement in the same way as any other column value can, either using one of the built-in aliases ("rowid", "oid" or "_rowid_") or by using an alias created by an integer primary key. 
- If an INSERT statement attempts to insert a NULL value into a rowid or integer primary key column, the system chooses an integer value to use as the rowid automatically. 
# [SQLite Autoincrement](https://www.sqlite.org/autoinc.html)
- summary
  - The AUTOINCREMENT keyword imposes extra CPU, memory, disk space, and disk I/O overhead and **should be avoided** if not strictly needed. It is usually not needed.
  - In SQLite, a column with type `INTEGER PRIMARY KEY` is an alias for the `ROWID` (except in WITHOUT ROWID tables) which is always a 64-bit signed integer.
  - On an INSERT, if the ROWID or INTEGER PRIMARY KEY column is not explicitly given a value, then it will be filled automatically with an unused integer, usually one more than the largest ROWID currently in use. This is true regardless of whether or not the AUTOINCREMENT keyword is used.
  - If the AUTOINCREMENT keyword appears after INTEGER PRIMARY KEY, that changes the automatic ROWID assignment algorithm to prevent the reuse of ROWIDs over the lifetime of the database. In other words, the purpose of AUTOINCREMENT is to prevent the reuse of ROWIDs from previously deleted rows.

- If no ROWID is specified on the insert, or if the specified ROWID has a value of NULL, then an appropriate ROWID is created automatically. 
  - The usual algorithm is to give the newly created row a ROWID that is one larger than the largest ROWID in the table prior to the insert. 
# [Clustered Indexes and the WITHOUT ROWID Optimization](https://www.sqlite.org/withoutrowid.html)
- A WITHOUT ROWID table is a table that uses a Clustered Index as the primary key.
- The WITHOUT ROWID syntax is an optimization. It provides no new capabilities. 
  - Anything that can be done using a WITHOUT ROWID table can also be done in exactly the same way, and exactly the same syntax, using an ordinary rowid table. 
  - The only advantage of a WITHOUT ROWID table is that it can sometimes use less disk space and/or perform a little faster than an ordinary rowid table.
