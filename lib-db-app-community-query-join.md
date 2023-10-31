---
title: lib-db-app-community-query-join
tags: [community, db, query]
created: 2023-10-31T11:17:38.308Z
modified: 2023-10-31T11:17:48.697Z
---

# lib-db-app-community-query-join

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## Prisma doesn’t JOIN (related records are fetched as separate requests from the DB) so I think it’d be slow at the edge anyways_202310
- https://twitter.com/jitl/status/1719347464359026862
- Hey Jake! While you are correct, we don't use Joins in every instance. We are currently doing a lot of work to fix this. We pushed out the initial change in 5.4. More to come! Thanks for using Prisma!

- ## [For Want of a JOIN | Hacker News_202212](https://news.ycombinator.com/item?id=34092645)

- With that said, the JOIN is a very powerful concept which, unfortunately, has been given a terrible reputation by the NoSQL community. Moving such logic out of the database and into to DB's client is just a waste of IO and computing bandwidth.
  - SQL has been the ONLY technology/language that has stuck with me for > 25 years. The fact that it is (apparently) not being taught by institutions of higher learning is just a shame.
- I agree. It took me 3 years or so to actually land in a project and learn SQL for the first time. Before it was all with ORMs. I didn't know what a join was for the first couple of years of my career. Understanding SQL and being able to work with data interactively has made me a better software engineer. This tech is important enough that it should be taught in university/coding camps.

- I often wonder how often this exact problem happens, but where A and B are [micro]services owned by two different teams, one is required by company policy to use their APIs not their raw databases, and escalation of each of these issues e.g. query size/rate limiting runs the risk of burning political capital on top of everything else.

- ## 🔥 [Joining CSV and JSON data with an in-memory SQLite database | Hacker News_202106](https://news.ycombinator.com/item?id=27565482)
- 
- 
- 

- ## 🔥 [Doing a database join with CSV files | Hacker News_201912](https://news.ycombinator.com/item?id=21923911)
- 
- 
- 

- ## 🔥 [Show HN: OctoSQL – Query and join multiple databases and files, written in Go | Hacker News_201907](https://news.ycombinator.com/item?id=20449610)
- 
- 
- 
