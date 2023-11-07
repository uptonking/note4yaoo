---
title: lib-db-sqlite-community-concurrency
tags: [community, concurrency, sqlite]
created: 2022-12-19T00:45:02.786Z
modified: 2022-12-19T01:59:01.628Z
---

# lib-db-sqlite-community-concurrency

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [SQLite B-Tree Module | Hacker News_202204](https://news.ycombinator.com/item?id=30894913)
- This has been shared without context but I guess the SQLite team is starting to modularize the btree code in order to facilitate work like SQLightning: https://github.com/LMDB/sqlightning
  - SQLightning greatly improved SQLite performance but due to LMDB's requirement to have keys fit in 2/3 of a page it wasn't really useful as a general purpose replacement of SQLite's internal b-tree implementation.

- 🤔 Is using SQLite from multiple processes safe? For a long while, either SQLite itself or the Python bindings weren't safe for concurrent access, is this still the case? Can I use SQLite for my Django app? With the backup system on the Tailscale post yesterday, the operational burden is much much lower than Postgres for many use cases.
  - It is always safe, and by "safe" I mean "safe for data". You won't have to deal with data corruption. Precisely, see "How To Corrupt An SQLite Database File"
  - Now concurrent accesses from different processes/connections can lead to runtime errors (SQLITE_BUSY), because the database happens to be locked by one connection.
  - Those errors are greatly reduced by the WAL mode (https://sqlite.org/wal.html) which provides ultra-robust single-writer/multiple-readers semantics
- I think they're safe now. The error message when using the connection from multiple threads is "outdated"
- With WAL it's a generally smooth experience. Really depends on your use case though.
  - The WAL doesn't work with shared directories (NFS/SMB) though. Found this out when I tried to store the Plex data directory on a NSF share in a VM and it had really weird issues. Turned out Plex uses SQLite with WAL enabled.
- This is just what I’ve heard so take with a grain of salt, but as I understand it sqlite is “mostly” safe to use concurrently. There are situations where it doesn’t behave correctly under concurrent load, the one I’ve heard about being when the sqlite is on a network-mounted drive. I’d love to hear from someone who knows more though.
  - That's kind of expected, I think. Due to its design, SQLite relies on filesystem semantics to provide atomicity. If the filesystem doesn't provide the semantics, it makes sense that atomicity will fail. I'm more asking whether it's still unsafe to use in a filesystem that DOES provide those semantics.
- Yeah it's safe. The biggest problem SQLite has is it's size limitations. It can only hold ~281 TB in a database unfortunately. If you need more storage than that - that's the only reason I could endorse someone using a different database.

- ## Can multiple applications or multiple instances of the same application access a single database file at the same time?
- multi
  - Multiple processes can have the same database open at the same time. 
  - Multiple processes can be doing a `SELECT` at the same time. 
  - But only one process can be making changes to the database at any moment in time, however.
- SQLite uses reader/writer locks to control access to the database. 
  - this locking mechanism might not work correctly if the database file is kept on an NFS filesystem. 
  - This is because `fcntl()` file locking is broken on many NFS implementations. 
  - People who have a lot of experience with Windows tell me that file locking of network files is very buggy and is not dependable.
- SQLite allows multiple processes to have the database file open at once, and for multiple processes to read the database at once. 
  - 👉🏻 When any process wants to write, it must lock the entire database file for the duration of its update.
  - Other processes just wait on the writer to finish then continue about their business.
- Other embedded SQL database engines typically only allow a single process to connect to the database at once.
- If your application has a need for a lot of concurrency, then you should consider using a client/server database.
  - This is possible in a client/server database because there is always a single well-controlled server process available to coordinate access. 
  - But experience suggests that most applications need much less concurrency than their designers imagine.
- When SQLite tries to access a file that is locked by another process, the default behavior is to return SQLITE_BUSY. 

- ## 🤔 Is SQLite threadsafe?
- Threads are evil. Avoid them.
- SQLite is threadsafe. We make this concession(让步，许可) since many users choose to ignore the advice given in the previous paragraph. 
- But in order to be thread-safe, SQLite must be compiled with the `SQLITE_THREADSAFE` preprocessor macro set to `1` . 
  - Both the Windows and Linux precompiled binaries in the distribution are compiled this way. 
- SQLite is threadsafe because it uses mutexes(互斥锁) to serialize access to common data structures. 
  - However, the work of acquiring and releasing these mutexes will slow SQLite down slightly. 
  - Hence, if you do not need SQLite to be threadsafe, you should disable the mutexes for maximum performance.
- Under Unix, you should not carry an open SQLite database across a fork() system call into the child process.
