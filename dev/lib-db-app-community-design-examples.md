---
title: lib-db-app-community-design-examples
tags: [community, database, database-design, dataseed, examples]
created: 2023-10-27T09:13:44.575Z
modified: 2023-10-27T09:14:12.088Z
---

# lib-db-app-community-design-examples

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🌰 [database - Alternatives to Northwind - Stack Overflow](https://stackoverflow.com/questions/2100982/alternatives-to-northwind)
- How about Chinook Database

- Microsoft do another set of sample databases called AdventureWorks (these are often used in MS courses).

- [Want to download Northwinds sample database, but confused : SQL](https://www.reddit.com/r/SQL/comments/v3bd5e/want_to_download_northwinds_sample_database_but/)
  - Don't use Northwind, grab Wide World Importers or AdventureWorks. They're more modern and have more complete instructions for setting up.

- [Northwind or AdventureWorks – SQLServerCentral Forums](https://www.sqlservercentral.com/forums/topic/northwind-or-adventureworks)
  - AdventureWorks is the better choice in my opinion. It's more complex than Northwind but it covers much more features of SQL Server 2005 and many samples in BOL (Books On Line) work with AdventureWorks

- ## 💡🔥 [Old, Good Database Design | Hacker News_202009](https://news.ycombinator.com/item?id=24467136)
- 
- 

- ## 🌰🔥 [Gallery of database schema diagrams of open-source packages | Hacker News_202004](https://news.ycombinator.com/item?id=23006159)
- 
- 
- 

- ## 🌰🔥 [Ask HN: What are some examples of good database schema designs? | Hacker News_202002](https://news.ycombinator.com/item?id=22324691)

- Northwind Traders
- That made me laugh. My 2 cents after doing this long enough to recognise it
  - Aim for 3NF but not religiously. Still, if you need a flat table try a view.
  - Any ternary relationship can be modeled as a pair of binary relations (you'll never regret keeping it simpler)
  - You don't need EAV (Magento is a good example of why you shouldn't)
  - On the other hand don't serialize data (looking at you WordPress)
  - XML and JSON data types though are perfectly fine when you need to store an object
  - Every table should have a primary key (preferably an integer)
  - If you really want a string for your primary key make it a candidate key (why, because someone will insist on changing it)
  - E/R diagrams are your friend
  - So are Venn diagrams for visualizing a complex select
# discuss
- ## 

- ## 

- ## [The Evolution of Reddit’s Architecture (2017) | Hacker News_201809](https://news.ycombinator.com/item?id=18013727)
