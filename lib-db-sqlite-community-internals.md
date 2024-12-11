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

- ## [Why SQLite Uses Bytecode | Hacker News _202404](https://news.ycombinator.com/item?id=40206752)
- It is difficult to summarize the advantages and disadvantages of byte-code versus AST for SQL 

- The problem of rendering a tree-of-objects as a table is sufficiently difficult that nobody does it, as far as I know. Hence, no tree-of-objects database engine provides the level of detail in their "EXPLAIN" output that SQLite provides.
  - I believe Microsoft SQL Server uses an object tree internally, and yet its query plan output is a table
- It can also execute a query incrementally. In fact, certain features rely on this behavior. “Watch live data” (in SSMS) for extended events is actually an infinite table-valued function. It’s not exactly rocket science to do in a database, you just need to model data sources and operators as iterators.
- Same with PostgreSQL. You can choose between text output (one table row per line), XML or JSON. But none of them are ordered according to a strict execution order like bytecode would be. To me that makes perfect sense though because if represents what can be parallelized in the plan. The bytecode representation in SQLite seems to have the inherent limitation that it is single threaded.

- > "A tree-of-objects representation is more difficult to publish in a human-readable form. The objects that comprise the tree tend to all be very different, and thus it is tricky to come up with a consistent and simple table representation with which to display the objects. Any any such table representation that you do come up with would almost certainly have more than six columns, probably many more. The problem of rendering a tree-of-objects as a table is sufficiently difficult that nobody does it"

- 🤔🤔 What I want to do is represent my tree-structure as a table in a relational database and then be able to efficiently get the tree structure back by transforming the table-representation back into a tree. Further I would like to do that in plain standard SQL. This must be a common problem, any documented solutions out there?
  - Great question - you have touched on the key difference between a labeling scheme and an encoding scheme for tree data structures.
  - To be able to evaluate a expression that processes a tree, one needs a labeling scheme. The purpose of a labeling scheme is to assign unique labels to each node in the tree and these labels must facilitate node ordering, and often (but not always) a labeling scheme will permit the reconstruction of the tree structure.
  - However, no labeling scheme captures the node type, names or the content stored at the nodes. For that we need an encoding scheme. An encoding scheme is constructed upon a labeling scheme and augments it with the information necessary to fully represent the tree in a table-like data structure. In answer to your question, it also permits the full transformation from the table representation to the original tree structure.
  - Thus, it sounds like what you are looking for is an encoding scheme.
  - There are many different labeling schemes out there for tree structure data, and virtually all of them can be augmented with additional information to construct a complete encoding scheme. Concerning documented solutions - I have not been active in this space for a number of years, so off the bat - I don't have a recommended documented solution to point you too.

- Maybe I'm missing something, but the bytecode approach seems really obviously better, just from a memory usage and locality point of view. Scanning an array of bytes or words is obviously going to be faster than traversing a tree of pointers.
  - So I'd be surprised to find a serious language implementation using a pure AST in its interpreter, without at the very least flattening it to an array!
- It’s fine to use an AST interpreter if you pair it with really great JITs.
  - That has its own problems though - using an AST as a shared source of truth for your JIT compilers is cumbersome for implementing stuff like OSR. But from a perf standpoint, it’s probably fine.
  - Also - say you want to optimize just for startup time, like if the code you’re running has minimal looping or reexecution. Then AST is better because you skip a step before first execution.

- SQLite's design docs were the first time I had seen a database use a virtual machine instead of walking a tree. I later noticed VMs in libraries, embedded DSLs, and other applications outside of large general-purpose programming languages. That really drove home for me that VMs could be anywhere and were often a useful step in handling a user's expressions.
- SQLite's VM is register-based, not stack-based.
  - It’s been both - was stack, converted to register
- Stack-based VMs, like SQLite's (I think), ARE trees. A stack based VM's bytecode (without DUP and POP) is just the post-order depth-first traversal of the corresponding expression tree. With DUP you have a connected acyclic DAG. With POP you have an acyclic DAG with one or more components. With loops you have a full graph.

- Does SQLite's VM have an API? I mean, one where I can build and issue opcodes into directly.
  - Not a public one, because they want to have the freedom to change how it works

- Everything is either a compiler or interpreter

- 🤔 Doesn't MS Word internally run a Forth-like VM? I remember reading an article by someone who decompiled an early MS-DOS version of Word only to discover that there was a VM inside.
  - They called it p-code at the time. The purpose was (purported) to simplify the porting between architectures.
- Or indeed any time complexity need to be layered. A VM design doesn't even have to have an explicit bytecode compilation stage -- you can write an interpreter that runs as the instructions are issued.

- I was surprised the text didn’t mention one major difference between the byte code approach vs AST: coupling.
  - When your database engine runs in-process, there is no possibility of the server and the client library having diverging versions. But this is common with traditional databases.
  - Once you bake in the execution steps („how to execute“) instead of describing the query via AST („what to execute“), an important part of the execution logic now lives in the driver.
  - I suspect this complicates version upgrades and bugfixes, because the database is less self-contained.

- MonetDB is another database that uses a VM, using an instruction set called the MonetDB Assembly Language (MAL). I believe it pioneered the technique. The VM is basically designed to express the query as vectorized functions on columns.

- I recently implemented my own expression evaluator in java for in-memory data frames, and once you think about doing that deeply, you very quickly understand the need for bytecode. 
  - If you directly evaluate the expression using a tree representation, you basically have to do a whole lot of branching (either via switch statements or polymorphism) for every single line of useful operation. Yes, the branch predictor kicks in and it means that your code wouldn’t be as slow as if it didn’t, but it is still measurably slower than if you converted the expression into bytecode once and just ran that on all rows instead.
- You should look at https://janino-compiler.github.io/janino/ it can compile Java into class files in memory that can be directly executed.
  - I found this by looking at spark source code to figure out what they were doing under the hood to deal solve this problem.

- Running bytecode is much lower latency than compiling into native code. If you're not bottlenecked by running the bytecode (as opposed to memory or disk speed), you don't really have to JIT it any further into native code.
  - Which is why JavaScript engines (and JIT compilers for other languages) are typically designed to: start interpreting the code once it has been parsed, and start jitting a function being called; 
- Yeah, but nobody is seriously considering that unless maybe for huge prepared statements. The argument is usually bytecode vs parser and associated data structures.
- PostgreSQL is not only considering it, they're doing it! https://www.postgresql.org/docs/current/jit-reason.html
  - I don't have personal experience on it, but I've read that in practice it's not worth the effort—at least not yet. Apparently there are some issues with it and it barely speeds up queries (except perhaps certain ones?). I imagine this could be in big part because LLVM is not really a good fit for JIT where you want to spend very little time to do the compilation itself.
- Yeah my experience of the pg jit is mostly negative, it’s quite slow and it has a hard time estimating the cost of interpreted v compilation + compiled execution so more often than not it’s actively detrimental. It might fare better if you make heavy use of a limited number of prepared statements.

- The reason bytecode is generally faster (not just for SQL, but in most interpreted languages you may use (Python, etc)) is that walking the AST is relatively expensive and doesn't treat caches nicely. Bytecode is generally located next to each other in memory, and you can make the bytecode fetch/dispatch pretty tight, relative to indirect function calls on an object in an AST.
  - Another advantage to that is that it avoids the branching of the while loop in the interpreter that iterates over the AST, providing better instruction pipelining with having all the run code next to each other.
- The downside -- especially for dynamic languages like JavaScript -- is that you need to keep all of the type checks and fast-paths in the code, resulting in larger code blocks. With more type analysis you could group fast-path instructions together (e.g. within a while or for loop) but that takes time, which is typically why a JIT engine uses multiple passes -- generate the slower machine code first, then improve the fast-path blocks for code that is long running.

- You don't need one, Lua is another example where no AST is ever generated. In some sense the resulting bytecode closely corresponds to the AST that would have been generated though.

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
