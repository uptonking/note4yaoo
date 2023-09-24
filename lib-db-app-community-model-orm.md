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

- ## 

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
