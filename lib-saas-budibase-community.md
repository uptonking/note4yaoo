---
title: lib-saas-budibase-community
tags: [budibase, community, lowcode, saas]
created: 2024-01-11T01:55:24.036Z
modified: 2024-01-11T01:55:59.453Z
---

# lib-saas-budibase-community

# guide

# dev

# discuss-stars

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## there is no native offline sync for something like field management in Budibase, however there are potentially some workarounds. _202303
- https://discord.com/channels/733030666647765003/1080253461179940874/1080424708081733724
  - For example you can use App State (https://docs.budibase.com/docs/app-state) to store some form data in memory until you have an internet connection to submit. 
  - You could also potentially setup a local database on your device to save data to if you are self-hosting. Then have a cron job to push that data to an online database somewhere else, or export a CSV.
- The latter works pretty well. I use MySQL to store my application data, and Budibase and it's database (ultimately CouchDB) store my application structure.

- ## I want to setup BudiBase using docker on my private VPS but want to install PostgreSQL and MariaDB RDBMS also. _202306
- https://discord.com/channels/733030666647765003/1119158384227254303
  - While reading the documents on how to install BudiBase using Docker, I observed that by default only CouchDB is installed.

- you could install Postgres, MariaDB or any other database on your host VPS and connect to them from your BB container. Alternatively you could run these other databases in containers also. 
  - The host address for the data source will vary depending on the DB install method you have chosen. Please also take some time to secure your database from unwanted external connections.
  - If you add a specific network for both containers, then you should be able to connect using the container name as the hostname but I would suggest spending a lot of time learning this for security reasons

- https://discord.com/channels/733030666647765003/1115238016970141746/1115375578300809428
  - In terms of MySQL and PostgreSQL, those are not shipped at all with Budibase.  Budibase uses "CouchDB" as their internal Database, which does not have to be used at all.
  - After Budibase is set up, you are free to set up any SQL server that is supported, and just put the credentials and IP into budibase when choosing data sources.  This can be set up the same way you would set up any database(You can use docker if you want to set them up).

- ## 🛋️ since the budibaseDB is based on CouchDB; I can define relationships in table form _202210
- https://discord.com/channels/733030666647765003/1022503693867823104/1026511148218077284
  - but what does one-to-many mean in JSON format? Will it be an array? Will it auto adjust to one-to-squillions?
- relationships on the internal tables are essentially always many to many - but we flag them so that the one side in a 1:many relationship can only have one relation. 
  - They will always be arrays, with a limit set on how many relations there can be based on the relationship type
- As for scaling - generally we don't recommend the internal tables for heavy relational data as an actual relational database is better at handling this sort of data. 
  - The way we handle relational data is through a joining document and a CouchDB view which creates an index for us to essentially "join" two documents when we retrieve them - in theory this could scale quite well but retrieving all of the related documents would get very slow at a huge number of relationships - they would need to be retrieved in pages.

- CouchDB is a bit of a complicated one - perfect for handling Budibase workloads/apps - its ideal for handling transactional data, simple documents etc
  - the way it handles replication and its protocol can be supported in a few cool ways makes it great for offline first type data

- ## [Budibase - An open-source low code platform for creating business apps (alternative to PowerApps, Mendix, Retool) is now out of beta._202111](https://www.reddit.com/r/kubernetes/comments/qwooi1/budibase_an_opensource_low_code_platform_for/)
- 🆚️ How would you say this compares to Appsmith?
- TLDR; AppSmith and Budibase are quite different platforms, but with significant overlap. 
  - Budibase is meant to be used by IT Professionals (sysadmins, dbas, IT managers, PMs, developers). 
  - AppSmith is more targeted at developers. 
  - Because of this, Budibase has much less of a reliance on code - we like to say “code optional”. But you can write JS in both platforms.
- Another differentiator is that Budibase comes packaged with a database (runs on CouchDB). 
  - This makes creating new applications easy - without having to spin up another DB. We also offer 1st class support for SQL Databases - Budibase will automatically fetch your tables and automate the basic INSERT, UPDATE, SELECT and DELETE statements (like an ORM).

- I'm a co-founder of Appsmith. Excited to know what you think once you try both. We are focused on developers as our target users and our features reflect that. Listing down a few select features of Appsmith from my POV here.
