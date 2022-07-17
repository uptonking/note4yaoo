---
title: lib-db-indexeddb-collab
tags: [collaboration, indexeddb]
created: 2022-06-13T06:14:03.941Z
modified: 2022-06-13T06:14:26.048Z
---

# lib-db-indexeddb-collab

# guide

- 同步难点
  - 将indexeddb的数据存储转换为mongodb-like结构
  - 如何同步 mongodb-like 的结构，是否用 crdt，还是 http
  - 是否需要中心化服务器
  - 不必过于纠结crdt的集成或三方库，关注于官方同步示例，如block-editor/y-indexeddb/dexie-sync

## Dexie 

### [Is Dexie. Syncable using OT?](https://github.com/dexie/Dexie.js/issues/587)

- Hmm this sounds correct, at least from what I understand by reading a bit about operational transforms. But this only holds true for dexie syncable itself. What the server does with the data is another issue. There are 2 server implementations that I know of that are open source. Both consider the last change when changing the same object from two different clients so data might get lost there. At least this is what I remember about the implementations.

- I haven't worked on the code for quite some time but this is what I remember:
- Dexie-Syncable records every ADD/UPDATE/DELETE operation. 
  - When it is time to send the operations to the server, the operations are firstly merged. 
  - I guess merge could be seen as OT. 
  - For each operation we check the ID and merge all operations which are defined for that ID. 
  - For example for the ID 1 we might have an ADD, UPDATE, UPDATE then those 3 are merged into 1 ADD operation which contains the two UPDATES. 
  - UPDATES are defined on a property level. Changing a property in an object is an UPDATE but we don't record what exactly changed in the property just the the property was changed and the new value.
- Now the server comes in play. 
  - There is an official server in the Dexie examples and one that I wrote. Both basically work the same. 
  - They record all operations those got from the various dexie clients. 
  - Everytime we get a new set of operations, the server tries to merge the operations. 
  - Now if you have for example two UPDATE operations for one ID and both change the same property, then the last change would win. 
  - I'm not sure if this type of conflict resolution is allowed in OT. 
  - After the server is done all the new operations are sent back to the client.
- So this is how dexie syncable + the server implementations which I know of work. Now I well let you decide if this could be considered OT or not.

### [Vision for Dexie](https://github.com/dexie/Dexie.js/issues/427)

- Chained where clauses and orderBy() on collections are something that have been asked for
  - These can be realized using compound indices and cursor joining techniques, and the resulting code does not need to be that complex. 
- The above example will need to be generalized. 
  - The key to make it work would be to build everything on cursors, so that the result of this operation also generates a cursor to call .continue() on etc.

- There's a lot research being done about Conflict-free replication data and CRDT types. 
  - These types are quite complex and require the API user to design their model for it. 
- However, I believe I have a concept for conflict free replication based on isomorphism. The idea is this:
  - Application Developer encapsulates database-facing code in an isomorphic class (a service)
  - Each method can optionally be decorated for conflict-free replication.
  - When called, the decorator generates an entry in the change log about the operation and the parameters given to it. When changes reach the server, it executes the same operation using the same parameters. This is possible only if the server has the same isomorphic service and can lookup the same code to execute.
- However, it is not always that conflict-free is needed. 
  - Most of the times, it is good enough with merging changes as Dexie. Syncable does now. 
  - Typically you would only need certain operations to be conflict free. 
  - Decorator expresses whether a method wants conflict-free operation or not. 
  - If conflict-free, then the method call and its arguments are registered in the change log. 
  - Otherwise, we would do as we do now - just record CREATEs, UPDATEs and DELETEs.
- This requires we have an isomorphic API - a database with dexie API at the server. 
  - For some database engines it is possible to execute javascript within the database engine itself
  - That way, a decorated method may be looked at as a stored procedure written in javascript.
  - 存储过程（Stored Procedure）是一组为了完成特定功能的SQL语句集，经编译后存储在数据库中，用户通过指定存储过程的名字并给定参数（如果该存储过程带有参数）来调用执行它。
  - 减少网络通信次数：将业务逻辑封装在存储过程中，业务逻辑层仅需要一次数据库操作即可；
  - 但不便于开发人员调式；
  - 当从一种数据库迁移到另外一种数据库时，存储过程要进行修改; 
  - 可维护性方面：存储过程一般过于复杂，对于后期的开发维护成本过高；
  - 如果过多的将业务逻辑封装在存储过程中，会延长事务的处理时间，进一步影响数据库并发量；
  - 上层业务很难复用同一个存储过程，因为不同的业务总会存在不同；
  - 更推荐在业务逻辑层通过调用DAO层提供的单一功能，来完成复杂业务逻辑的处理。
