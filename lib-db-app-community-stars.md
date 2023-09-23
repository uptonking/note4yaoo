---
title: lib-db-app-community-stars
tags: [community, database]
created: 2021-08-30T15:51:01.157Z
modified: 2023-09-16T17:54:21.231Z
---

# lib-db-app-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## Most databases were built when data was static and queries were dynamic. 
- https://twitter.com/tantaman/status/1699826662408409383
  - For applications, most queries are static and the data is dynamic
- What you really want is a database where a query is the same things as an index, is the same thing as a subscription... These are all the same underlying mechanic.

- ## Myth(神话，想像或虚构的人物): Using UUID as the primary key will slow down inserts. 
- https://twitter.com/gwenshap/status/1686148804821811200
  - Fact: Not in Postgres.
  - I often recommend using UUIDs instead of integer sequences as primary keys. I was surprised to discover that many developers are uncomfortable with them and believe they will slow down inserts. 
  - [UUIDs are Bad for Performance in MySQL - Is Postgres better? Let us Discuss - YouTube](https://www.youtube.com/watch?v=Y5mWz4vK10A)
- It makes the code easier as well because you can generate IDs on the client.
  - Exactly! this also makes the system as a whole more scalable. This is not something you need early on, but changing PKs later is super hard and starting with UUIDs is not.

# discuss
- ## 

- ## 

- ## [Things I wished more developers knew about databases | Hacker News_202004](https://news.ycombinator.com/item?id=22942278)
- 
- 
- 
- 

- ## [Best practices on primary key, auto-increment, and UUID in RDBMs and SQL databases](https://stackoverflow.com/questions/52414414)

- What I always do, even if it's redundant, is I create primary key on auto increment column (I call it `technical key`) to keep it consistent within the database, 
  - allow for "primary key" to change in case something went wrong at design phase 
  - and also allow for less space to be consumed in case that key is being pointed to by foreign key constraint in any other table 
  - and also I make the candidate key unique and not null.
- Technical key is something you don't normally show to end users, unless you decide to. 
  - This can be the same for other technical columns that you're keeping only at database level for any purpose you may need like modify date, create date, version, user who changed the record and more.

```SQL
CREATE TABLE users(
  pk INT NOT NULL AUTO_INCREMENT,
  id UUID NOT NULL,
  PRIMARY KEY(pk),
  UNIQUE(id)
);
```

- This question is quite opinion-based so here's mine.
- My take is use the second one, a separate UUID from the PK. The thing is:
  - The PK is unique and not exposed to the public.
  - The UUID is unique and may get exposed to the public.
- If, for any reason, the UUID gets compromised, you'll need to change it. Changing a PK may be expensive and has a lot of side effects. If the UUID is separate from the PK, then its change (though not trivial) has far less consequences.

- if you make it an increasing number, your competitors will know how many users you have and how fast you are adding new ones.

- I came across a nice article that explains both pros and cons of using UUID as a primary key. 
  - In the end, it suggests using both but **Incremental integer for PK and UUIDs for the outside world**. 
  - Never expose your PK to the outside.
