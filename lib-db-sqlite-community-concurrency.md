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

- ## Is SQLite threadsafe?
- Threads are evil. Avoid them.
- SQLite is threadsafe. We make this concession(让步，许可) since many users choose to ignore the advice given in the previous paragraph. 
- But in order to be thread-safe, SQLite must be compiled with the `SQLITE_THREADSAFE` preprocessor macro set to `1` . 
  - Both the Windows and Linux precompiled binaries in the distribution are compiled this way. 
- SQLite is threadsafe because it uses mutexes(互斥锁) to serialize access to common data structures. 
  - However, the work of acquiring and releasing these mutexes will slow SQLite down slightly. 
  - Hence, if you do not need SQLite to be threadsafe, you should disable the mutexes for maximum performance.
- Under Unix, you should not carry an open SQLite database across a fork() system call into the child process.
