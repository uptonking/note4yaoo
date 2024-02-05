---
title: lib-saas-nocodb-community
tags: [community, nocodb]
created: 2023-01-22T18:46:57.384Z
modified: 2023-12-15T17:04:24.911Z
---

# lib-saas-nocodb-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Feature : Support Kanban view](https://github.com/nocodb/nocodb/issues/140)
- You need to create a `SingleSelect` column in your table. Other column types are not supported to be a grouping field.

- ## [Nocodb: Turns Any MySQL, Postgres, SQLite into a Spreadsheet with REST APIs | Hacker News _202210](https://news.ycombinator.com/item?id=33078798)

- Unfortunately, these tools only provide basic record listings with form views. Except for being able to render images, they don't do much more that database browsing tools.

- ## [NocoDB – Turn your SQL database into a Nocode platform | Hacker News _202111](https://news.ycombinator.com/item?id=29176436)
- This, for me, was easiest to try out. And quite impressive, honestly. The key point was that in each table, the 'title' column (created by default) has a special meaning as they show up in the join columns cleanly.
  - This has been my experience with internal tool builders too. The barrier to entry is quite high to try most of them and it's really hard to have a whole team test them out. This adoption issue was part of the inspiration for Wax which lets you build internal tools on top of Google Sheets. If your team is already using Sheets, it's much easier to add the missing pieces there vs. pushing people to an entirely separate platform.
- In noco we've the concept of primary-value (like primary key) and that shows up automatically when you join with other tables (defaults to 'title'). However the primary value column can be changed to any other column too (by hovering on the column name). Other tools in the list do not give the smart-spreadsheet automatically when you connect to databases. And frankly, these are two different tools we are comparing.

- I could also see this being used as somewhat as an "Admin UI" for SaaS software administrators.
  - Yes, it could be easily used as Admin UI. We create a virtual schema for every database that we connect to. If there are schema changes done outside noco GUI - then noco has a sync option that does automatically sync the changes.

- We support Forms. By page designer - its about custom reports from the data.

- What exactly is it good for?
  - Spreadsheets has limits to number of rows/cells. And they tend to corrupt after certain limit easily. 
  - Then things like creating relation between sheets or deriving different views are not possible/easier in spreadsheet. 
  - This is when teams using spreadsheets start to move to databases. But it involves a lot of effort to build a spreadsheet like product on databases. This is where noco helps.

- ## 🚀 [Show HN: NocoDB – Open-Source Airtable Alternative | Hacker News _202105](https://news.ycombinator.com/item?id=27303783)
- NocoDB works by connecting to any relational database and transforming them into a smart spreadsheet interface!
  - NocoDB currently works with MySQL, PostgreSQL, Microsoft SQL Server, SQLite, Amazon Aurora & MariaDB databases.
  - Also NocoDB's app store allows you to build business workflows on views with combination of Slack, Microsoft Teams, Discord, Twilio, Whatsapp, Email & any 3rd party APIs too

- Would it be possible to use planetscale as db?
  - Yes, in our earlier version we could connect to Planetscale and create tables (this was at inception stage). With recent Planetscale release DDL are no longer supported and branching is the way. We would love to support if anything changes.

- The free limit is 1200 rows per DB now. The paid plans are expensive though. Cheapest is $120/year
- Looks good - for monetization you should make the integrations paid and the core thing free.
  - Or build consulting, management and integration partners. Strategic use of tools/trainings, etc. are really important. See how Oracle grows with consulting teams.

- It looks pretty, but has some fairly substantial problems.
  - Data collection: Generally feels nasty these days, especially on something self-hosted. The opt-in-by-default newsletter checkbox might even be illegal in Europe. 
  - Deceptive(欺骗性的；骗人的) data collection: The HotJar survey popping up starts making you think maybe it needs to know where you host images so that it can handle image uploads... but no, it just wants to collect data and dial home
  - Couldn't work out how to connect from one docker instance to a second docker instance mysql database. Might need some kind of docker-compose setup though, I didn't look that long
  - And that's kinda where I gave up.

- I love the audit table, that's a nice touch.

- 🆚️ This looks a lot like baserow.io too; nice to see more projects like this opening up spreadsheet/db alternatives.
  - Although there is similarity, we are radically different.
  - 💡 We transform any existing databases MySQL, Postgres, SQL Server & SQLite databases into a spreadsheet. This is a _massive_ difference to begin with. 
  - And the ability to invite team to collaborate and build business workflow automations with Slack, Twilio is available for everybody. 
  - Since the launch today, I have already have close to 25+ plugin requests which sounds reasonable for NocoDB to have! 
  - We believe for a horizontal product like NocoDB - developing every app, connector and plugins is just beyond the ability of single team in open source. It is community driven approach that eases this possibility.
- What would you say is the current upper bound on the number of records in a table that you support ?
  - There is no limit on upperbound - spreadsheet fetches data from your table in database.
- Does it updates them in the database?
  - Yes it does which is what it makes it interesting.
- Are there any schema assumptions, like numeric primary/foreign/surrogate keys?
  - We automatically identify all PKs & FKs

- Interested that the project started as a REST API generator for any MySQL database, and then in a year was transformed to what can be seen today from what I gather following the git log.
  - Yes, Xmysql was a hobby project originally submitted on HN. Below is the gist of it.
  - We open sourced two API solutions before NocoDB : 
  - A no-code REST APIs generator for any MySQL DB. ~200, 000 Docker pulls. This was a hobby project & had no GUI. 
  - A low-code REST-GraphQL APIs generator for any database with GUI. Used by 100s of companies. Including fortune 500s & publicly trading companies.
  - The thing that surprised us the most was that even non-developers started using our API products & rooting for us. Whilst everybody loved instant API access to databases, it was slow-and-painful for them to build UI and collaborate with their teams. This made us to radically recombine the power of our 2 API products then transform them into something better.

- I believe NocoDB can be used as admin apps in most backends. We've audit mechanism to track every single action from all our users. And the access control is really fine grained till column level.

- I'd like to try using this at work for an internal tool but AGPL is a no go.
  - All of the AGPL bits are inside that docker container. You don't need to worry about AGPL contamination unless you're modifying the contents of the container.

- Given that the project is AGPL without any CLA, how do you plan on doing that, if you don't mind me asking? Some sort of portal in front that does this on your behalf? Asking since I've considered AGPL for my own projects and wanted to monetize via making SAML/SSO "premium" and found that I could not do this easily without CLA
  - We're using developer certificate of origin. Used by nextcloud and likes.
