---
title: lib-db-sqlite-community-internals
tags: [codebase, community, database, internals, sqlite]
created: 2023-10-28T13:44:08.751Z
modified: 2023-10-28T13:45:16.973Z
---

# lib-db-sqlite-community-internals

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🪶⚖️🔥 [The SQLite Database File Format | Hacker News_201409](https://news.ycombinator.com/item?id=8385259)
- The problem with SQLite is that there's no official RFC, it's a pseudo database. When you're weighing up what to implement, it certainly helps when there is an agreed upon technical specification.
- On thing that caught my eye here was the section on the B-tree in the sqlite file format. I've written these, they are hard to get right. But the section here is an english description of a very complex data structure, and if this appeared in an RFC and you asked ten different developers to reimplement it then you'd wind up with wildy different interpretations of the text, all non-interoperable until the world finally decided to have some kind of "interop fest".
  - So I'm happy that SQLite already has a publically available b-tree implementation. Because you won't have a "standard" without that code, and QED.
  - Complex standards need reference implementations. Just calling something an RFC doesn't make it more useful. 

- ## [The lack of proper “alter table” support in SQLite | Hacker News_201306](https://news.ycombinator.com/item?id=5886898)
- I am very familiar with SQLite internals. The answer is already in there. 
  - SQLite stores each row as each column value encoded sequentially corresponding to the declared order of the columns. Changing column order or deletions/inserts require a rewrite of every row. The one special case that is allowed is adding a column on the end of the schema providing it has a default value.
  - A SQLite provided ALTER TABLE implementation would do exactly what was stated - start a transaction, rename the existing table to a temporary name, create a new one with the desired schema, and copy data across mangling as appropriate before deleting the old table and finishing the transaction. 
  - For plain tables this is no big deal, but for more complicated ones there are a lot of issues such as foreign key references, constraints, indices. The majority of the code would be dealing with all these conditions and interactions.
  - SQLite does have several things to help. There is a user_version pragma you can use to keep track of the schema version and use for upgrading. You can temporarily disable foreign key and constraint enforcing. There are numerous pragmas to get table metadata. The table definitions are stored as SQL strings in a sqlite master table, and a pragma allows you to make that writeable.

- ALTER is in itself an odd command, useful only in development, never in production, and bringin with it deep architectural implications and an endless list of problems in basically all SQL systems today.

- The H2 open source java database implements "alter table" exactly as per the description of sql alchemy: create a new table with the new structure, copy all the data across, delete the original table, rename the new table to the origina name. This could perhaps be acceptable for sqlite.
# discuss
- ## 

- ## 

- ## 🪶🌲 [B-Trees: More Than I Thought I'd Want to Know | Hacker News_202108](https://news.ycombinator.com/item?id=28221612)
- The best B-tree resource is SQLite3's documentation of its B-tree on-disk format.
- Postgres has great documentation for their concurrent btree algorithm based on the Lehman Yao paper
  - Just FYI, adding right-sibling pointers to a B-tree makes it impossible to implement a COW B-tree. Kinda like COW semantics makes it impossible to have doubly-linked lists. But if you're not going to COW, then right-sibling pointers are probably a good idea.

- B+Trees minimize the maximum depth of the lookup. All the values have exactly the same cost. In all honesty, I don't care about the lookup cost of the values I never need.
  - Sounds like you are looking for a Splay Tree implementation. Their dynamic optimality properties ensure your most popular data lives right at the root.

- ## 🔥 [VFS shim that allows a SQLite database to be appended to another file | Hacker News_201806](https://news.ycombinator.com/item?id=17264629)
- 
- 
- 

- ## [sqlite rowid after deleting rows](https://stackoverflow.com/questions/35876171)
  - I delete rows with id 3 and 4 and run above query again.
  - Now my problem is rowid not getting reset and holes.
  - 在删除某些行后，其他所有行的rowid不变，不受影响，就会形成断断续续的rowid
- rowid is really special. So special that if you have an `INTEGER PRIMARY KEY` , it becomes an alias for the rowid column. 
  - when your primary key is an alias for rowid, it would be terribly inconvenient if this could change. 
  - Since rowid is now aliased to your application data, it would not be acceptable for sqlite to change it.
- If you really really really absolutely need the rowid to change on a VACUUM, you can avoid this aliasing behavior. Note that it will decrease the performance of any table lookups using your primary key.
  - To avoid the aliasing, and degrade your performance, you can use `INT` instead of `INTEGER` when defining your key

## 🤔🧲 [Why Is SQLite Coded in C (2017) | Hacker News](https://news.ycombinator.com/item?id=28278859)

- But it's still a database, a low level, high performance software system. 
  - Even if you write it in rust, some percentage of the code will be unsafe rust or rust that calls a library written in C. 
  - It will be safer, but still not a panacea. 
  - It would be more viable in my opinion to improve the safety of the C code that currently makes up sqlite.
