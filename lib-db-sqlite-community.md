---
title: lib-db-sqlite-community
tags: [community, sqlite]
created: 2021-08-30T17:33:26.516Z
modified: 2021-08-30T17:33:46.086Z
---

# lib-db-sqlite-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [sqlite rowid after deleting rows](https://stackoverflow.com/questions/35876171)
  - I delete rows with id 3 and 4 and run above query again.
  - Now my problem is rowid not getting reset and holes.
  - 在删除某些行后，其他所有行的rowid不变，不受影响，就会形成断断续续的rowid
- rowid is really special. So special that if you have an `INTEGER PRIMARY KEY` , it becomes an alias for the rowid column. 
  - when your primary key is an alias for rowid, it would be terribly inconvenient if this could change. 
  - Since rowid is now aliased to your application data, it would not be acceptable for sqlite to change it.
- If you really really really absolutely need the rowid to change on a VACUUM, you can avoid this aliasing behavior. Note that it will decrease the performance of any table lookups using your primary key.
  - To avoid the aliasing, and degrade your performance, you can use `INT` instead of `INTEGER` when defining your key
