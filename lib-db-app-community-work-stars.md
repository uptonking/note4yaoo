---
title: lib-db-app-community-work-stars
tags: [community, database]
created: 2021-08-30T15:51:01.157Z
modified: 2023-10-27T06:54:20.487Z
---

# lib-db-app-community-work-stars

# guide

# discuss-stars
- ## 

- ## 💡 Most databases were built when data was static and queries were dynamic. 
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

- ## 🕛🔥 [Big problems at the timezone database | Hacker News_202109](https://news.ycombinator.com/item?id=28650019)
- 
- 
- 

- ## 🛢️🔥 [The Next 50 Years of Databases (2015) | Hacker News_201911](https://news.ycombinator.com/item?id=21508210)
- 
- 
- 

- ## this isn’t to say that every application should have its own totally bespoke(定制的) database. most of them probably shouldn’t. 
- https://twitter.com/aboodman/status/1708208649984950515
  - but these things are not magical and we should remember that they’re just code, too. code we can understand and debug and modify as needed.
- That’s not to say you shouldn’t write your own database, or web server, or compiler. Just don’t do it because your app is somehow magical and unique. Your app is variables and for loops inside, too
- There is no magic. It’s just variables, if statements, and loops, arranged cleverly. Every time - every single time - I’ve looked inside a web server, database, browser, or whatever my reaction has been the same.
- I remember very clearly the first time I got to look at gws -- google web server. Just given the name and aurora of the company, I was expecting something grand, inscrutable, insanely complex. Instead, I got an event loop and some very nicely structured event registration code.
  - Also usually a bunch of FIXME comments, comments explaining weird code choices, and sometimes even comments expressing frustration. I.e. just the same as in any codebase that you’d work on yourself.
- This is actually a nice corollary(必然结果): making things simple and easy to understand is the real art of software engineering.
- Also often the simplest code is the easiest for the computer to run. a compiler from the 2000s will happy unroll normal for loops. Code that stacks abstractions 10 layers deep - probably not
  - unfortunately I’m addicted to complicated abstractions like incremental programming
- 
- 
- 

- ## 🤔 [Skip the API, ship your database | Hacker News](https://news.ycombinator.com/item?id=37497345)
- If you give access to your DB directly, your API effectively becomes your API with all the contract obligations of the API. Suddenly you don't completely control your schema: you can't freely change it, you need to add things there for your clients only. 👉🏻 I've seen it done multiple times and it always end up poorly. You save some time now by removing the need to build API, but later you end up spending much more time trying to decouple your internal representation from schema you made public.
- The system that I'm currently responsible for made this exact decision. The database is the API, and all the consuming services dip(浸；泡) directly into each other's data. This is all within one system with one organisation in charge, and it's an unmanageable mess. The pattern suggested here is exactly the same, but with each of the consuming services owned by different organisations, so it will only be worse.
- Versioned views, materialized views or procedures are the solution to this. It is frequent that even internally, companies don't give access to their raw data but rather to a restricted schema containing a formated subset of it.
  - Views will severely restrict the kinds of changes you might want to do in the future.
  - Stored procedures technically can do anything, I guess, but at that point you would be better with traditional services which will give you more flexibility.
- Of course it’s possible, but now you need more people with DB and SQL knowledge. Also, using views and stored procedures with source control is a pain. Deploying these into prod is also much more cumbersome than just normal backend code. Accessing a view will also be slower than accessing an “original” table since the view needs to be aggregated.

- A downside I didn't see mentioned (it was gestured at with contracts and the mention of backwards compatible schema changes, but not addressed directly) was **tight coupling**. 
  - When you link services with APIs, the downstream changes of a schema migration end at the API boundary. 
  - If you are connecting services directly at the database level, the changes will propagate into different services.

- A very interesting idea to be sure, but IME the biggest downside (which tbf is mentioned in the article) is the contract. If you have clients with knowledge of and dependency on the schema, you can't change it in a breaking way unless you update all the client's code.
  - I've tried various patterns in the past like one that just exposes database columns as an API, and this pain point always comes calling and it hurts. 
- I've freelanced with several teams, primarily comprised of front-end devs, who decided to use Firebase for their product. When they first told me they query the database directly from both their website and their mobile app, I immediately was like "so...what happens if you need to change the structure of the database"?

- The solution to this is the same as with APIs: versioning. Instead of naming your table "my_foo", you name it "my_foo_v1". Then, when you want to make a breaking change to the schema, you: 
  1. Create a new table "my_foo_v2" with your desired schema
  2. Modify write queries for "my_foo_v1" so that they also write to "my_foo_v2"
  3. Copy over existing data in "my_foo_v1" to "my_foo_v2" with a migration script
  4. Modify read queries for "my_foo_v1" so that they read from "my_foo_v2" instead
  5. Remove all write queries to "my_foo_v1"
  6. Drop the "my_foo_v1" table

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
