---
title: lib-db-sqlite-docs
tags: [docs, sqlite]
created: 2021-08-30T17:32:48.451Z
modified: 2021-08-30T17:33:20.586Z
---

# lib-db-sqlite-docs

# guide

- [Database File Format](https://www.sqlite.org/fileformat.html)
# [SQLite As An Application File Format](https://www.sqlite.org/appfileformat.html)

> [Benefits of SQLite As A File Format](https://www.sqlite.org/aff_short.html)

- An SQLite database file with a defined schema often makes an excellent application file format. 
  - Here are a dozen reasons why this is so:
  - Simplified Application Development
  - Single-File Documents
  - High-Level Query Language
  - Accessible Content
  - Cross-Platform
  - Atomic Transactions
  - Incremental And Continuous Updates
  - Easily Extensible
  - Performance
  - Concurrent Use By Multiple Processes
  - Multiple Programming Languages
  - Better Applications

- An "application file format" is the file format used to persist application state to disk or to exchange information between programs. 
  - There are thousands of application file formats in use today, like doc/xls/pdf/dwg/epub/git/...
- We make a distinction between a "file format" and an "application format". 
  - A file format is used to store a single object. 
    - So, for example, a GIF or JPEG file stores a single image
  - An EPUB file, in contrast, stores both text and images (as contained XHTML and GIF/JPEG files) and so it is considered an "application format". 
  - The boundary between a file format and an application format is fuzzy. 
  - This article is about "application formats".
  - For this article, let us say that a file format stores a single object and an application format stores many different objects and their relationships to one another.

- Most application formats fit into one of these three categories:
- Fully Custom Formats. 大多单文件、大多二进制、读写需要专用软件
  - Custom formats are specifically designed for a single application. 
  - DOC, XLS, DWG, PDF, and PPT are examples of custom formats. 
  - Custom formats are usually contained within a single file, for ease of transport. 
  - They are also usually binary, though the DWG format is a notable exception.
  - Custom file formats require specialized application code to read and write and are not normally accessible from commonly available tools such as unix command-line programs and text editors.
  - In other words, custom formats are usually "opaque blobs". 
  - To access the content of a custom application file format, one needs a tool specifically engineered to read and/or write that format.
- Pile-of-Files Formats. 通常多级文件夹、部分可读写、移动或引用不便
  - A pile-of-files format essentially uses the filesystem as a key/value database, storing small chunks of information into separate files. 
  - Git is a prime example of this, though the phenomenon occurs frequently in one-off and bespoke applications. 
  - This gives the advantage of making the content more accessible to common utility programs such as text editors or "awk" or "grep". 
  - But even if many of the files in a pile-of-files format are easily readable, there are usually some files that have their own custom format (example: Git "Packfiles") and are hence "opaque blobs" that are not readable or writable without specialized tools. 
  - It is also much less convenient to move
  - Finally, a pile-of-files format breaks the "document metaphor": there is no one file that a user can point to that is "the document".
- Wrapped Pile-of-Files Formats. 
  - Some applications use a Pile-of-Files that is then encapsulated into some kind of single-file container, usually a ZIP archive. 
  - EPUB, ODT, and ODP are examples of this approach.
  - OpenOffice documents (ODT and ODP) are also ZIP archives containing XML and images that represent their content as well as "catalog" files that show the interrelationships between the component parts.
  - A wrapped pile-of-files format is a compromise between a full custom file format and a pure pile-of-files format. 
  - A wrapped pile-of-files format is not an opaque blob in the same sense as a custom format, since the component parts can still be accessed using any common ZIP archiver, but the format is not quite as accessible as a pure pile-of-files format because one does still need the ZIP archiver
  - As with custom file formats, and unlike pure pile-of-file formats, a wrapped pile-of-files format is not as easy to edit, since usually the entire file must be rewritten in order to change any component part.

- The purpose of this document is to argue **in favor of a fourth new category of application file format: An SQLite database file**.

- Any application state that can be recorded in a pile-of-files can also be recorded in an SQLite database with a simple key/value schema 
  - CREATE TABLE files(filename TEXT PRIMARY KEY, content BLOB); 
  - it has the advantage of being able to **update individual "files" without rewriting the entire document**.
- An SQLite database can have dozens or hundreds or thousands of different tables, with dozens or hundreds or thousands of fields per table
  - An SQLite database is a more versatile container than key/value filesystem or a ZIP archive. 
- The power of an SQLite database could, in theory, be achieved using a custom file format. 
  - But any custom file format that is as expressive as a relational database would likely require an enormous design specification and many tens or hundreds of thousands of lines of code to implement. 
  - And the end result would be an "opaque blob" that is inaccessible without specialized tools.

- SQLite database as an application file format has compelling advantages
- Simplified Application Development
- Single-File Documents
  - An SQLite database is contained in a single file, which is easily copied or moved or attached. 
  - SQLite does not have any file naming requirements and so the application can use any custom file suffix that it wants to help identify the file as "belonging" to the application.
- High-Level Query Language
- Accessible Content
  - Information held in an SQLite database file is accessible using commonly available open-source command-line tools 
  - It is true that command-line tools such as text editors or "grep" or "awk" are not useful on an SQLite database, 
  - but the SQL query language is a much more powerful and convenient way for examining the content
  - An SQLite database is a well-defined and well-documented file format that is in widespread use
  - The longevity of SQLite database files is particularly important to bespoke(定制的) applications, since it allows the document content to be accessed far in the future
  - Data lives longer than code.
- Cross-Platform
- Atomic Transactions
  - Writes to an SQLite database are atomic.
  - They either happen completely or not at all, even during system crashes or power failures. 
  - So there is no danger of corrupting a document just because the power happened to go out at the same instant that a change was being written to disk.
  - SQLite is transactional, meaning that multiple changes can be grouped together such that either all or none of them occur, and so that the changes can be rolled back if a problem is found prior to commit. 
  - This allows an application to make a change incrementally, then run various sanity and consistency checks on the resulting data prior to committing the changes to disk. 
- Incremental And Continuous Updates
- Easily Extensible
- Performance
  - In addition to being faster for raw read and writes, SQLite can often dramatically improves start-up times because instead of having to read and parse the entire document into memory, the application can do queries to extract only the information needed for the initial screen.
  - As the application progresses, it only needs to load as much material as is needed to draw the next screen
  - This helps keep the memory footprint of the application under control.
  - A pile-of-files format can be read incrementally just like SQLite. 
  - But many developers are surprised to learn that SQLite can read and write smaller BLOBs (less than about 100KB in size) from its database faster than those same blobs can be read or written as separate files from the filesystem.
  - There is overhead associated with operating a relational database engine, however one should not assume that direct file I/O is faster than SQLite database I/O, as often it is not.
  - In either case, if performance problems do arise in an SQLite application those problems can often be resolved by adding one or two `CREATE INDEX` statements to the schema or perhaps running `ANALYZE` one time and without having to touch a single line of application code. 
- Concurrent Use By Multiple Processes
  - SQLite automatically coordinates concurrent access to the same document from multiple threads and/or processes. 
  - Two or more applications can connect and read from the same document at the same time. 
  - SQLite automatically ensures that the low-level format of the document is uncorrupted. 
  - Accomplishing the same with a custom or pile-of-files format, in contrast, requires extensive support in the application. 
  - And the application logic needed to support concurrency is a notorious bug-magnet.
- Multiple Programming Languages
- Better Applications

- Conclusion
  - in many cases, SQLite is a far better choice than either a custom file format, a pile-of-files, or a wrapped pile-of-files. 
  - SQLite is a high-level, stable, reliable, cross-platform, widely-deployed, extensible, performant, accessible, concurrent file format. 
  - It deserves your consideration as the standard file format on your next application design.
# sqlite3_vfs

# [Many Small Queries Are Efficient In SQLite](https://www.sqlite.org/np1queryprob.html)
- with SQLite, 200 or more SQL statement per webpage is not a problem.

- N+1 Queries Are Not A Problem With SQLite
  - SQLite is not client/server, however. 
  - The SQLite database runs in the same process address space as the application. 
  - Queries do not involve message round-trips, only a function call. 
  - The latency of a single SQL query is far less in SQLite. 
  - Hence, using a large number of queries with SQLite is not the problem.
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
# [Using the SQLite Online Backup API](https://www.sqlite.org/backup.html)
- **Historically**, backups (copies) of SQLite databases have been created using the following method:
  - Establish a shared lock on the database file using the SQLite API (i.e. the shell tool).
  - Copy the database file using an external tool (for example the unix `cp` utility or the DOS `copy` command).
  - Relinquish(放弃, 让出) the shared lock on the database file obtained in step 1.
- This procedure works well in many scenarios and is usually very fast. 
- However, this technique has the following shortcomings:
  - Any database clients wishing to write to the database file while a backup is being created must wait until the shared lock is relinquished.
  - It cannot be used to copy data to or from in-memory databases.
  - If a power failure or operating system failure occurs while copying the database file, the backup database may be corrupted following system recovery.
- The Online Backup API was created to address these concerns. 
- The **online backup API** allows the contents of one database to be copied into another database file, replacing any original contents of the target database. 
  - The copy operation may be done incrementally, in which case the **source database does not need to be locked for the duration of the copy**, only for the brief periods of time when it is actually being read from  
