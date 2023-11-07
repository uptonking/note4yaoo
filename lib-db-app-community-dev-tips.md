---
title: lib-db-app-community-dev-tips
tags: [community, database-design]
created: 2023-10-27T09:17:03.711Z
modified: 2023-11-07T16:47:11.499Z
---

# lib-db-app-community-dev-tips

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🔥🔥 [When your data doesn’t fit in memory: the basic techniques | Hacker News_201911](https://news.ycombinator.com/item?id=21508542)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 🔥🔥 [Show HN: I wrote a free eBook about many lesser-known/secret database tricks | Hacker News_202212](https://news.ycombinator.com/item?id=33833836)
- 
- 
- 

- ## 🔥 [Mistakes Beginners Make When Working with Databases | Hacker News_201606](https://news.ycombinator.com/item?id=11862723)
- 
- 

- ## 🔥 [Database development mistakes made by application developers | Hacker News_201012](https://news.ycombinator.com/item?id=1999874)
- 
- 
- 

- ## 🔥 [Three things you should never put in your database | Hacker News_201205](https://news.ycombinator.com/item?id=3916497)
- 
- 
- 

- ## 🔥 [Two common mistakes when using databases | Hacker News_200910](https://news.ycombinator.com/item?id=865695)
- A well thought-out post and a good read, but both of the author's points about the limitations of relational databases are a little misleading.
  - The first, "Every single element in a relation (aka table) has to be exactly the same type" is true in many relational databases, but isn't necessary: SQLite, for example, is implemented with a nice form of dynamic typing where individual columns can take on multiple data types.
  - Second, "SQL isn't even Turing-complete" is sort of a folk theorem in computer science that isn't necessarily true anymore, especially with all of the proprietary SQL dialects in existence: the original standard, SQL92, is basically equivalent to relational algebra, which has the expressive power of first-order logic - it's so weak it can't even express concepts like graph reachability. But constructs like recursive queries have been added to the SQL standard since SQL92 which may make even standard SQL Turing Complete.
- PL/SQL and T-SQL are certainly Turing complete.
  - Oracle's SQL is by itself Turing complete since the introduction of the "Model" clause 

- For beginners, this is definitely good advice. Particularly the first point - if you're using a relational database, and don't structure your data around its strengths, you'll take a profound performance hit. And sure, don't pass around data structures if you don't know what you're doing, and MySQL is a pretty crummy place to put them.
  - However, once you're doing real work, sometimes translating to XML and back is extraordinarily expensive.
  - The best approach is a hybrid. Use the database to store things relationally if possible, and using defined APIs for sure. 
  - And if your translation stage is expensive, use something like memcached to make sure you do that translation as infrequently as possible. _This_ is the layer that it's appropriate to store serialized data structures at. It's not permanent storage, you can blow it away when you change the internal structures, and nobody external is relying on it. 
  - But you end up, in most programs, with even more speed benefits than if you'd stored it in the database like this to begin with - the initial build can be expensive, but then you're reading basically from memory. (Not all data is well suited to this approach, but if your data is read frequently and written to infrequently - there's few things you can do to increase performance more than this.)
