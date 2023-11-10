---
title: lib-db-postgresql-blog-dev-blob-binary
tags: [binary, blob, blog, postgresql]
created: 2023-11-10T18:34:16.778Z
modified: 2023-11-10T18:34:45.317Z
---

# lib-db-postgresql-blog-dev-blob-binary

# guide

# blogs

## [BinaryFilesInDB - PostgreSQL wiki](https://wiki.postgresql.org/wiki/BinaryFilesInDB)

- New users to PostgreSQL often ask on the PostgreSQL mailing lists how/if to store binary files like images, Word documents, spreadsheets, HTML, PDF, compressed archives, or even code in the database. 
- There are two prevailing(普遍的；流行的) schools of thought on that, each having pluses and minus

### 1️⃣ Store the large binary file of unstructured data directly in a database field

- pros
  - ACID
  - Files saved into a primary database will stream to standby replicas automatically
  - Backups are easier there is no need to track external files
  - Security and access control are simplified
  - Version controlling is easier

- cons
  - Performance hit storing files in database.
  - Memory requirements higher, for Database
  - Backups can take significantly longer
  - Access to files to external applications is complicated. Normally a temporary file is copied to the client to access and modify the file and then needs to be copied back.

- Storing binary data using bytea or text data types
- pros
  - Storing and Accessing entry utilizes the same interface when accessing any other data type or record.
  - No need to track OID of a "large object" you create
- cons
  - bytea and text data types both use TOAST, limited to 1GB per entry
  - Need to escape/encode binary data before sending to DB then do the reverse after retrieving the data
  - Memory requirements on the server can be steep even on a small record set.

- BLOB binary large object see Large Object Support
- pros
  - limited 4TB (PostgreSQL 9.3+) per entry, & 4 Billion per database
  - Can stream, and seek over entries (can reduce memory requirements on DB server and client)
  - No encoding or escaping required.
- cons
  - Must use different interface from what is normally used to access BLOBs.
  - Need to track OID. Normally a separate table with additional meta data is used to describe what each OID is.
  - Sometimes advised against (basically you only need them if your entry is so large you need/want to seek and read bits and pieces of it at a time).

### 2️⃣ Save the binary file to the regular filesystem, then write metadata and some sort of symbolic link in the database to its location.

- pros
  - Performance accessing binary file skips DB access layer.
  - Number of files limited only by file system
  - Size limited by file system

- cons
  - The database user needs permissions to write outside of the database. That's not normally an option in hosted PostgreSQL environments.
  - Need to develop an interface to keep track of externally attached files
  - External files and database can get out of sync
  - Security settings between file system and database are independent from each other. 
  - Multiple points of failure depending on complexity of the network.

### tips

- When should files be stored in the database?
  - The common suggestion here is when the files have to be ACID.
  - When storing the photos outside the database, there is no easy way to guarantee atomicity, consistency, isolation and durability of the photos. Storing the photos in the database is the only practical solution where the programmer can guarantee rules are followed in the future. The file data will automatically replicate and flow to database backups. 
  - And since writing to arbitrary files on the database server requires extra trust, saving to the database may be the only option available or considered safe by your PostgreSQL administrator.

- When is it bad idea to store binary files in the database?
  - Very large files (100MB+), where performance is critical to the application. The database layer adds a lot of overhead and complexity that may not be required.
# more
