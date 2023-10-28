---
title: lib-db-sqlite-community-examples
tags: [community, examples, sqlite]
created: 2022-11-27T18:05:24.364Z
modified: 2022-11-27T18:06:10.599Z
---

# lib-db-sqlite-community-examples

# guide

# discuss
- ## 

- ## 

- ## 🔥 [The Winamp Skin Museum is powered by a SQLite3 database with 1.2GB of metadata | Hacker News_202206](https://news.ycombinator.com/item?id=31703874)
- 
- 
- 
- 

- ## 🤔🔥 [Ask HN: Have you used SQLite as a primary database? | Hacker News_202204](https://news.ycombinator.com/item?id=31152490)

- Pros:
  - A single API server, no separate database to worry about, configure, and update.
  - Backups are as simple as backing up one file every so often. SQLite even has an API to do this from a live connection.
  - Handles way more concurrent users than we’ve ever needed.
  - Dev and test environments are trivial and fast.
  - Plenty of tools for inspecting and analysing the data.

- Cons:
  - There are certainly use cases it won’t scale to, or at least not without a bunch of work, but in my experience those are less than 1% of projects. YMMV.
  - The type system (even with the newish stricter option) has nothing on Postgres. I realise this is basically a non-goal but I’d seriously love to somehow combine the two and get PG’s typing in a fast, single file embedded DB library.
  - Postgres JSON support is also better/nicer IMO.

- 👉🏻 For me, SQLite's lack of online schema changes seems like perhaps the biggest blocker to actual production. I've never had a production project where the schema didn't change a lot.
  - I have this beef too. Tooling for dumping and restoring into a new schema are easy/simple/fast. So, these schema migrations can happen w/o issue. Some tricks with the `PRAGMA` directive in SQLite so you can roll out changes (eg: code supports old/new schema while migrating)
  - I'm just using shell scripts and the SQLite CLI. I dump/restore files to the same FS so I can mv into place when ready. Checkout the PRAGMA `user_version`, I just modify on schema change, so app knows where stuff is.
- We also used SQLite and leverage PRAGMA `user_version` to do the trick. But **decided to move to PostgreSQL mainly due to the schema migration constraints**. Our experience is SQLite is OK for small to medium projects, but when the business logic/data model becomes more complex, SQLite is not sufficient.

- What is the point of using SQLite under a web service?
  - SQLite is far faster than Postgres or MySQL, however, the price you pay for this is having a single writer thread, and it's a library incorporated into your process, not a shared DB. It's faster because those other features of a server have a cost as well, particularly the cost of write arbitration.
  - SQLite is fine when all your load can be served by a single backend process on a single machine. The moment you need multiple backends to handle more load, or the moment you need high availability, you can't do it with SQLite. **SQLite has very limited DDL operations**, so you also can't evolve your schema over time without downtime. Now, for streaming backups - how do you come back from node failure? You're going to incur downtime downloading your DB.
  - I love SQLite, and use it regularly, just not for production web services.
- 👉🏻 SQLite has write ahead logging as well
  - It doesn't let you run an active replica from WAL.
- your app has full access to the SQLite file. MySQL/PostgreSQL have users and permissions. Security is about layers, and SQLite is removing one layer of security. You can, for example, put DELETEs or access to certain tables on a separate user that your web app has no access to. With SQLite, if your app gets hacked then they can do anything with the whole DB they want to. In addition, with a separate DB process you get audit logs. If someone hacks your SQLite app they may have access for months before you realize it, if you ever do. Especially if they are doing something subtle like UPDATEs on specific tables/fields that may go unnoticed but provide the hacker some benefit. This is why you can't simply rely on the idea of using a backup. That's only going to help if the hacker totally trashes your DB.
- Take a look at the Consider SQLite post I linked. They address your performance questions too.

- The reason I decided against it is that it doesn’t have proper stored procedures. I use them a lot in PGSQL. They result in far fewer lines of code.

- I switched from Postgres to SQLite for a couple of versions, put mainly because Postgres wasn't "supported" I called SQLite an "internal database thing".

- https://internetdb.shodan.io is powered by a SQLite database and gets millions of requests a month. It does require a different workflow and custom synchronization scripts but otherwise it's performed well.

- VATcomply.com has been using SQLite as a primary database for 2 years and is serving ~70 requests per second without an issue.
  - https://github.com/madisvain/vatcomply

- ## [SQLite as an Application File Format (2014) | Hacker News_202006](https://news.ycombinator.com/item?id=23508923)
- The great thing about applications that use sqlite as their application file format is that you can write secondary apps and utilities to supplement the applications themselves.
  - For example, Adobe's Lightroom uses sqlite as their application file format, which means that it's almost trivial to write an application to help it do things it's either really bad/exceedingly slow at (like removing images from a catalogue that no longer exist on disk) or literally can't do (like generating a playlist of files-on-disk for a specific collection or tag), without being locked into whatever janky scripting solution exists in-app. 
- All you need is a programming language with a sqlite connector, and you're in the driving seat. And sure, you'll need to figure out the table schemas you need to care about, but sqlite comes with sqldiff so it's really easy to figure out which operations hit which tables with only a few minutes of work.

- SQLite vs json vs xml

1. SQLite database files are self descriptive, which JSON and XML are not.
2. SQLite is a compressed binary format. JSON and XML are plain text.
3. building on that, SQLite files were designed to contain arbitrary data, and you can store whatever you want using the BLOB datatype. JSON and XML can't, they have no notion of types, everything has to be syntax-compliant strings.
4. SQLite files can be encrypted. JSON and XML can't.
5. SQLite files were designed to be queried. JSON and XML are not.

- And I already hear you try to object, so let's expand:
1. JSON and XML cannot describe their own structure, their syntax is prescribed, but any schema has to come from either external files, like XML's DTD, or from literally nothing because JSON has no official schema language. Yes, https://json-schema.org/ exists, but it's certainly not an official spec - maybe "yet", maybe just "full stop".
2. Yes, you can compress JSON/XML using zip/etc but now it's no longer JSON/XML. Now it's an archive file like any other archive file, and it's "nothing" you can work with until you unpack it, incurring delays, and then repack it once you're done, incurring even more delays (because packing is far more work than unpacking), and worse: the bigger the file gets, the longer the delay becomes.
3. Sure, you can convert binary to a text format and then put that in JSON/XML too, but there no types: you have no way of universally indicating which field is plain text, and which field is binary-as-text nor a way to universally indicate which encoding you've used.
4. Same as (2): sure, you can encrypt the data yourself, but there is no universal spec for indicating what encryption you used for which fields, or parts of the file, or the entire file, in JSON or XML.
5. JSON and XML are data serialization formats: they are perfect for transport, but they are not data repositories and even at the spec level make zero affordances towards efficient data retrieval, storage, and representation. Which for an application file format is critical.

- Can you use JSON/XML as application file formats? No, not really. They're terrible for that purpose. They might work for configs (as you point out), and they are fantastic for moving small quantities of data from one system to another (for large quantities, they make no sense: even something as dumb as CSV becomes more efficient when dealing with lots of data) but they are absolutely unsuitable for storing arbitrary application data, because they are horrendously inefficient for almost everything an application needs out of a good file format, without rolling your own standards, for which there is no enforcement tooling unless you write that yourself, too. And then get others to adopt it as well. And now you're started down the path of replicating what SQLite already does, and doing so poorly.

- ## [What If OpenDocument Used SQLite? (2014) | Hacker News_202012](https://news.ycombinator.com/item?id=25462814)
- I'd say better to export tables to CSV files, and dump the schema to an SQL file.
- 👉🏻 Standards like OpenDocument are expected to have multiple independent implementations. I'm not sure such a thing is feasible with SQLite (this is why WebSQL was rejected).

- The only application/document file format I know that uses sqlite is [cherrytree – giuspen](https://www.giuspen.com/cherrytree/)
- I am the developer of a platform that hosts documents in a NoSQL (MongoDB) so that every paragraph of text is a 'record' in MongoDB and there's a 'path' property which is what builds out a 'tree' structure to give the documents a hierarchy. You guys might be interested if you're interested in new kinds of document/wiki innovations.
  - https://quanta.wiki/

- All I would like from OpenDocument, and LibreOffice, is an ASCII storage format that is not specifically designed to be incompatible with revision control systems.
  - As it is, they have an almost-serviceable format that fails only by having each line start with a random number that differs from the number on the corresponding line that was originally read in.
  - Fixing it would not even be an incompatible change! They could just remember the number that was there, and write it back out, next time.
  - There is a report for this in their bug tracker that me
- Microsoft more or less does this already with their Office Open XML file format in SharePoint Online/OneDrive. Small changes are read/written as users edit the doc. Real-time co-authoring locks on a per-paragraph basis.
