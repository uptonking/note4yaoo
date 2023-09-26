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

- ## 🤔 [Ask HN: Has anybody shipped a web app at scale with 1 DB per account? | Hacker News_202005](https://news.ycombinator.com/item?id=23305111)
- My startup currently does just this 'at scale', which is for us ~150 b2b customers with a total database footprint of ~500 GB. We are using Rails and the Apartment gem to do mutli-tenancy via unique databases per account with a single master database holding some top-level tables.
  - This architecture decisions is one of my biggest regrets, and we are currently in the process of rebuilding into a single database model.
  - However as we have grown this has become a huge headache. It is blocking major feature refactors and improvements. It restricts our data flexibility a lot. Operationally there are some killers. Data migrations take a long time, and if they fail you are left with multiple databases in different states and no clear sense of where the break occurred.
  - Lastly, if you use the Apartment gem, you are at the mercy of a poorly supported library that has deep ties into ActiveRecord. The company behind it abandoned this approach as described here

- Echoing this as well, I worked for Influitive and was one of the original authours of apartment (sorry!)
- There are **a lot of headaches involved with the "tenant per schema" approach**. Certainly it was nice to never have to worry about the "customer is seeing data from another customer" bug (a death knell if you're in enterprisish B2B software), but it added so many problems:
  - Migrations become a very expensive and time-consuming process, and potentially fraught with errors. Doing continious-deployment style development that involves database schema changes is close to impossible without putting a LOT of effort into having super-safe migrations.
  - You'll run into weird edge cases due to the fact that you have an absolutely massive schema (since every table you have is multiplied by your number of tenants). We had to patch Rails to get around some column caching it was doing.
  - Cloud DB hosting often doesn't play nice with this solution. We continually saw weird performance issues on Heroku Postgres, particularly with backup / restores (Heroku now has warnings against this approach in their docs)
  - It doesn't get you any closer to horizontal scalability, since connecting to a different server is significantly different than connecting to another schema.
  - It will probably push the need for a dedicated BI / DW environment earlier than you would otherwise need it, due to the inability to analyze data cross-schema.
- I still think there's maybe an interesting approach using partioning rather than schemas that eliminates a lot of these problems, but apartment probably isn't the library to do it (for starters, migrations would be entirely different if partioning is used over schemas)

- Can confirm, here be dragons. I did a DB per tenant for a local franchise retailer and it was the worst design mistake I ever made, which of course seemed justified at the time (different tax rules, what not), but we never managed to get off it and I spent a significant amount of time working around it, building ETL sync processes to suck everything into one big DB, and so on.
  - **Instead of a DB per tenant, or a table per tenant, just add a TenantId column on every table from day 1**.

- 
- 
- 

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
