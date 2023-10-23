---
title: lib-db-app-community-model-orm
tags: [community, database, orm]
created: 2023-09-24T19:05:18.256Z
modified: 2023-09-24T19:05:33.866Z
---

# lib-db-app-community-model-orm

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [Is ORM still an anti-pattern? | Hacker News_202306](https://news.ycombinator.com/item?id=36497613&p=2)
- In any sufficiently complex application, something like a query builder that allows different parts of the application to work together to lazily compose queries (vs combining/filtering/sorting the data in memory) will be created at some point.
  - ORM is a tool that can make this easier, it's also a tool that can make it easier to shoot yourself in the foot (ie by making it easy to create N+1 queries without knowing). Like all tools, there are tradeoffs that need to be accounted for together with the actual use case to make a decision. Operating on SQL statement strings is not something I'd recommend in any case.
- LINQ isn’t exactly an ORM. You create strongly typed LINQ statements that are turned into expression trees that are then turned into a query by a query provider.
- Good points! As someone who uses both ORM and raw SQL (I actually really like SQL as language) I sympathize with both sides of this debate. 
  - I prefer the readability of ORM in my models when developing, but closely monitor and optimize for N+1 and other inefficiencies, when needed. "When needed" is never cut-and-dry, but I try not to optimize too early. 
  - I actually tend to start new projects from the database and will scaffold with factories, seeders, and raw SQL queries to get a sense of the data model prior to coding.
  - ORM's such as Eloquent in Laravel also have some nice methods to resolve N+1 and perform lazy loading, but it's always tradeoff.

- the line between an ORM and a query builder is a very blurry one
  - your query builder isn't just string based to avoid a lot of potential bugs which are easy to introduce and miss in tests? It also has a simple way to (de)serialize row from/to POD structs? Now you already have a thin ORM.

- A point I'm missing is: without using an ORM (or however else you're calling your database interface) you will eventually end up writing and maintaining one yourself, at least for CRUD stuff, and it will be filled with weird bugs, edge cases and security holes.

- ## [What ORMs have taught me: just learn SQL (2014) | Hacker News_201909](https://news.ycombinator.com/item?id=21031187&p=2)
- Will tend to agree with the author.
  - Initially ORMs can save time when developing as you get an easy mapping between objects and the database.
  - However in practise ORM tends to give you quite horrible JOINs that quite frankly are hard to understand for humans.
  - Further more I think that **ORM can lead to a bad practice in the sense that you do not need to think about your data layout first**. 
  - But for database performance data layout is of utter most importance. One need to have data in lay out in a form that makes the application run fast. ORMs does not necessarily provide that. One need to normalize the database.

- This topic pops up frequently here on HN and every time I’m shocked at how many people have issues with ORMs! I’ve been using Hibernate/Spring Data for several years now and never ran into any issues. If I need to write a complex query, I can easily write a @Query annotation in HQL and it neatly fits right in to the repository class.

- 
- 
- 
- 
- 
