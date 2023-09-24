---
title: lib-db-app-community-architecture
tags: [architecture, community, database]
created: 2023-09-17T17:37:06.649Z
modified: 2023-09-17T17:37:19.913Z
---

# lib-db-app-community-architecture

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [For Want of a JOIN | Hacker News](https://news.ycombinator.com/item?id=34092645)

- With that said, the JOIN is a very powerful concept which, unfortunately, has been given a terrible reputation by the NoSQL community. Moving such logic out of the database and into to DB's client is just a waste of IO and computing bandwidth.
  - SQL has been the ONLY technology/language that has stuck with me for > 25 years. The fact that it is (apparently) not being taught by institutions of higher learning is just a shame.
- I agree. It took me 3 years or so to actually land in a project and learn SQL for the first time. Before it was all with ORMs. I didn't know what a join was for the first couple of years of my career. Understanding SQL and being able to work with data interactively has made me a better software engineer. This tech is important enough that it should be taught in university/coding camps.

- I often wonder how often this exact problem happens, but where A and B are [micro]services owned by two different teams, one is required by company policy to use their APIs not their raw databases, and escalation of each of these issues e.g. query size/rate limiting runs the risk of burning political capital on top of everything else.

- ## [Ask HN: Is there a way to efficiently subscribe to an SQL query for changes? | Hacker News](https://news.ycombinator.com/item?id=26901352)
- Source: I worked on Google Cloud Firestore from it's launch until 2020 and was the on responsible for the current implementation and data structures of how changes get broadcasted to subscribed queries.
  - Without joins Google Cloud Firestore does exactly what you're describing.
  - With joins (or any data dependant query where you can't tell a row is in the result set without looking at other data) you need to keep the query results materialized otherwise you can't have enough information without going back to disk or keeping everything in memory, which isn't really feasible in most cases.

- I like this idea a lot. In a sense it's thinking of your application as a spreadsheet, where the database is a data tab and the frontend is the summary tabs. If there's a change to the data tab, the "spreadsheet engine" (or "materialized view engine" in your case) walks the dependency graph and updates all the relevant parts of the summary tabs.
  - The closest thing I'm aware of to this is BigQuery's materialized views, which take care of making otherwise expensive queries cheap fast, but they are rather limited (i.e. no subqueries or joins), and don't have the "streaming output of changes" you describe.
- 
- 
- 
