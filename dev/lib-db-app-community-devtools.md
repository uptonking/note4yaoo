---
title: lib-db-app-community-devtools
tags: [community, database, devops, devtools]
created: 2023-09-17T17:38:35.970Z
modified: 2023-10-27T09:12:16.163Z
---

# lib-db-app-community-devtools

# guide

# products-db
- [dbdiagram.io - Database Relationship Diagrams Design Tool](https://dbdiagram.io/home)
  - simple tool to draw ER diagrams by just writing code
  - Designed for developers and data analysts
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-db-designer
- ## 

- ## 

- ## 

- ## With http://database.build, you can create an unlimited number of databases using AI
- https://x.com/dshukertjr/status/1865053120537182246
  - we have added the ability to deploy the database you built on http://database.build to Supabase with a click of a button
- The whole no code community deserves to know about this. Well, and the traditional coding community too lol

- ## 🚀 [Show HN: Outerbase Studio – Open-Source Database GUI | Hacker News _202412](https://news.ycombinator.com/item?id=42320032)
- A good browser based DB GUI might just not exist because the existing desktop ones are so good already.
- No browser based tool is going to come close to the experience of an actual desktop app imo
  - Why? Sandbox constraints. Windowing. Browser compatibility issues. Plugins and Integration compatibility.

- I think it's because there's no business model in the pure "DB browser" product. 
  - People don't seem willing to pay enough for it to build a good business around it. 
  - Everyone I've seen either pivots to a Retool competitor or a BI tool. Source: I've tried it twice.
- I think DB Browser is not a product but a feature. It is fairly challenging to monetize it. It can be an entry point for a developer's workflow, and then you can upsell something else.

- Jetbrains Datagrip has been around for a decade and has connectors for most database archetypes (mongo, sql, redis, duckdb, etc). Biggest limitation right now is its lack of support for vector style databases like Lance, qdrant, etc.

- The electron app and running it locally allows you to use TCP protocol which isn't available directly in the browser.

- What I found invaluable is the use of Kate (yes the editor) SQL plugin. It can connect to MySQL/MariaDB, Postgres and others.
  - The main benefit is that you can organize your SQLs in files or even better in markdown files.
  - God knows how many times I had to retype the same or a very similar SQL in the past.

- Databases are B2B products, not consumer products. They are commercially useful only when placed in the context of some larger business process (e.g. tracking customers/orders/goods/users/batches/events/patients/filings etc.).

- For similar projects, check out:
  - Supabase Studio (open source, Postgres only) https://github.com/supabase/supabase/tree/master/apps/studio
  - Prisma Studio (closed source, supporting most popular databases) https://www.prisma.io/studio
  - Drizzle Studio (closed source, supporting most popular databases)

- Could you please add an option to enforce the use of transactions within the SQL input?

- 🐛 All of the browser based database UI's I've tried have a lot of issues when it comes to binary data and very large int's in ways that will corrupt your data.
  - The large ints thing is because people forget that numerics in Javascript are all officially floating point. The optimisers might often see that they can use real integers for performance, but you can't depend on that so have to assume it isn't happening.
  - Integer numbers are accurate up to 2^53-1 (and down to -2^53) as the IEEE754 double precision type is used, which is sufficient for a majority of tasks, but obviously not all.
  - Native BigInt is widely supported these days (has been since late 2020 IIRC, or early 2023 if you waited for LTS releases without the feature to reach EOL) but is not yet widely used 
  - Performance isn't usually bad (about 60% or the basis Number type last time I compared) but there are other issues with JSON or with many libraries only supporting Number not BigInt.

- More of the collaboration features and team features have been or are being built into the Outerbase cloud offering. You can already invite teammates, share resources, see whose looking at what databases, and more there.

- Our goal is to have all of our data sources across all Outerbase products powered by our SDK - https://github.com/outerbase/sdk. Currently the Studio product is not powered by it but our cloud and other offerings are.

- working with Turso / Cloudflare D1 databases etc.

- ## 🚀 [Show HN: DbGate – open-source, cross-platform SQL+noSQL database client | Hacker News _202104](https://news.ycombinator.com/item?id=26899100)
  - this is my passion project. I was unable to find nice SQL client for Linux, so I created it on myself. 
  - It's built on Electron using Svelte
  - It's open source (MIT), cross-platform (Linux, Mac, Windows), or can be run as web-based application in browser.

- Could you please include filters within the database. (Databas filters)

- ## [DBeaver – open-source database client | Hacker News _202403](https://news.ycombinator.com/item?id=39660592)
- I personally like the ER diagram viewer in DBeaver. 

- one of my favorite things about DBeaver is that because it is implemented on Eclipse you can install nearly any Eclipse plugin and they work.

- Also they made a browser database client (cloudbeaver) which is much better than pgdamin IMO. 

- Does DBeaver have a feature similar to PGAdmin's schema diff
  - Yes but not in the community version: https://github.com/dbeaver/dbeaver/wiki/Schema-compare

- The viewer for geospatial data is much better than most other GUI clients (and CLI clients are often not very useful for geospatial data).

- ## [Dbeaver – Multi-platform database tool | Hacker News _201901](https://news.ycombinator.com/item?id=18935138)
- Absolutely. I only work in MySQL and dbeaver was the only tool that worked without a huge headache in Linux.

- I use DBeaver to connect to Oracle SQL (among other things) and it works well for this purpose. I tried other alternatives too but DBeaver felt the best among them (layout, options, and general speed).
- I use DBeaver to connect to Oracle SQL (among other things) and it works well for this purpose. I tried other alternatives too but DBeaver felt the best among them (layout, options, and general speed).
# discuss
- ## 

- ## 

- ## 

- ## [Beekeeper Studio SQL editor 4.0 – Import. backup, restore, and bigquery | Hacker News _202310](https://news.ycombinator.com/item?id=37732329)
- Been using this for a year or so as my daily basic DB client. Really like it for what it is and can definitely recommend it for quick and simple DB operations.
  - I put it in the same category as tableplus - its a nice simple db client when all you need to do is browse some data, edit a row or two, etc. The community edition of beekeeper, however, has less annoyances than tableplus's free version imo.
  - For more advanced use-cases, it doesn't come close to dbeaver or tools like that, but it also isn't designed to imo.

- Does anyone know how this compares to DBeaver?
  - Smoother to use and simpler, but it's missing features when it comes to running long queries where you want to break it up into several so it does not timeout.

- I made Beekeeper Studio because the lack of a good SQL editor on Linux drove me crazy. TablePlus is great on MacOS, but when I started it didn't even have a Linux version.
  - I have full feature parity across all OSes, which I'm pretty proud of as a one-man team (although I do have some AMAZING part time help)

- Almost all Electron-based software has a guilt(有罪; 过失) of shortcuts. By either not having them at all, or by using the scheme alien to a particular OS. Obsidian is my personal pit peeve - it still has a spotty support of F2 (rename) shortcut on Windows. Previously, it hadn't it at all.

- It's a similar value proposition as VSCode/Sublime Text vs IntelliJ. If you are in a database all day and need a big beefy IDE, Beekeeper Studio isn't for you.
  - I built Beekeeper Studio because I wanted an easy to use and intuitive GUI. I'm not a DBA, so using DBeaver or DataGrip required me to basically re-learn the whole app every time I used it, which I didn't have the patience for.

- See also: DBeaver, pgadmin, MySQL workbench, Navicat, MS Access, ... 
  - These graphical database clients mostly end up looking the same in the end

- ## 🔥 [Show HN: Data Diff – compare tables of any size across databases | Hacker News_202206](https://news.ycombinator.com/item?id=31837307)
- 
- 
- 

- ## 🔥 [Show HN: A tool to seed your dev database with real data | Hacker News](https://news.ycombinator.com/item?id=31165538)
- 
- 
- 

- ## 🔥 [Exploring Databases Visually | Hacker News_202104](https://news.ycombinator.com/item?id=26693705)
- 
- 
- 

- ## 🔥 [Dbeaver – Multi-platform database tool | Hacker News_201901](https://news.ycombinator.com/item?id=18935138)
- 
- 
- 
