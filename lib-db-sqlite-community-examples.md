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

- ## 🪶📄⚖️ [What if OpenDocument used SQLite? (2014) | Hacker News_202309](https://news.ycombinator.com/item?id=37553574)

- OpenDocument - Initial release: 1 May 2005; 18 years ago
  - SQLite - Initial release: 17 August 2000; 23 years ago
  - OpenDocument traces it's ancestry to OpenOffice XML format, which traces it's ancestry to StarOffice, which was xmlized around the time Sun bought it in 1999
  - Not to be confused with Office Open XML (OOXML), Microsoft's "standard".

- ⚖️ Is SQLite’s disk format an open, versioned standard? Or is it just “however SQLite saves data to disk”?
  - [Database File Format](https://www.sqlite.org/fileformat2.html)
  - Note that there have been no breaking changes since the file format was designed in 2004. 

- The **problem with SQLite** is that it's not a standardized file format. 
  - It's well-documented and pretty well understood for sure, but there's no ISO standard defining how to interpret an SQLite file in excruciating detail. 
  - Same goes for competing implementations, Zip and XML have a much smaller API surface than SQLite, whose API, apart from a bunch of C functions, is the SQL language itself. 
  - Writing an XML parser is not a trivial task, but it's still simpler than writing an SQL parser, query optimizer, compiler, bytecode VM, full-text search engine, and whatever else Sqlite offers, without any data corruption in the process. 
  - If Open Office used SQLite, its programmers would inevitably start using its more esoteric features and writing queries that a less-capable engine wouldn't be able to optimize too well.
- This isn't a concern for most software. If you're writing a domain-specific, closed-source application where interoperability with other apps or ISO standardization isn't a concern, SQLite is a perfectly fine file format, but as far as I understand the situation, those concerns did exist for Open Office.

- Good article. Although one thing I do like about OpenDocument being just a bunch of XML files in a ZIP archive is that it is fairly easy to generate documents like spreadsheets without using a (potentially hefty) library which knows about the document format.
  - Doing this with SQLite would be possible of course, just a tad more complex and with a lower development speed. Being able to fire up the office suite, create a template document, and just dig into its XML files in the saved file is a nice feature (although admittedly of niche interest).

- The advantages of XML, specifically, a human-readable format; really only work for small files when the design of the schema is optimized for readable XML. 
  - Unfortunately, the need to always rewrite the entire XML file, and the "complexities" that come with lots and lots of features will quickly erode XML's biggest advantages.

- I shipped a product that used both SQLite and XML files.
  - One of the improvements that I made was moving a few tables that contained small amounts of data to xml files. Because these files were small and rarely written; it simplified the data access layer, and simplified diagnostics. (I made sure the files were multi-line tabbed xml.)
  - The advantages of XML, specifically, a human-readable format; really only work for small files when the design of the schema is optimized for readable XML. 
  - Unfortunately, the need to **always rewrite the entire XML file**, and the "complexities" that come with lots and lots of features will quickly erode XML's biggest advantages.
- IMO: A "lay" person needing to muck around with the internals of an office document is fringe enough that learning to use a SQLite reader is an acceptable speed bump. The limitations of XML + Zip, when it comes to random writes in the middle of a file, just can't be overcome by Moore's law.

- 👉🏻 Engineering is all about **tradeoffs**: **SQLite is optimized for quick incremental updates where you don't need to rewrite the whole file**. **Zip & xml aren't**. (IE, if you decide to add a letter to a word at the beginning of a document, with zip & XML you have to rewrite the whole document. SQLite can make a minor change without the whole rewrite.)

- > I like taking the approach of CouchDB where the only correct way to close the system is to crash it.
  - The term you're looking for is (aptly named) crash-only software.
  - [Crash-only software - Wikipedia](https://en.wikipedia.org/wiki/Crash-only_software)

- Coupling a file format to SQLite smells wrong.do we need it do a lot? No, not really. We don’t need the full SQL standard, a query optimiser, etc etc for basic (+ safe) transaction semantics and the ability to store data in a basic table structure.
- custom build: Looks like fair amount of functionality can be left out when compiling sqlite and with options to influence/strip down query planner
- "SQLite does not compete with client/server databases. SQLite competes with fopen()"
- The complaint is not “it isn’t good” but rather “it is not replaceable”. Since SQLite is so powerful, once you specify it as a format, you are stuck with SQLite forever.
- Which is also "not a big issue", since it's a recommended Library of Congress storage format, and supported long term
- SQLite is already used for exactly this purpose. It's used as OGC GeoPackage and Mapbox/Maptiler datasets use this.
- Have you checked the Apple apps? Most of them use SQLite as storage format. iMovie, iPhoto, Voice recording…Same with Docker. Can’t be that wrong?
  - The Apple apps are using Core Data, which uses SQLite as its persistent store by default. So Apple could in theory migrate away from SQLite by changing Core Data’s behaviour without any application-level impact. So in a way, these applications are already decoupled from SQLite in the way the parent comment suggests.
- fossil, the versioning system designed by the people of SQLite, and using SQLite, doesn't even use SQLite as a file format. It's all a bunch of blobs, each with its own format, that happen to be stored on SQLite. SQLite offers safe storage and a bunch of helpful indexes and views, but is not necessary for fossil-the-data to work.
  - Looking in sqlite.fossil there are 27 tables in it and most are not used for storing blobs. I know when looking up how to do things in the past the answer has sometimes been "run this SQL query". The event table for instance looks like a list of all commits with dates and comments etc. There is a config table that looks like the kind of stuff git stores in .git/config (URL to upstream repo etc) and so on. Well, yes there are some blobs in it too.
- Efficiently and safely querying and writing data is central to any document format; you'll leverage both the file structure and in-memory structs to do this. SQL would probably work for this, in fact it's especially natural for spreadsheets (rows x cols).
- OpenDocument works just fine without it. You need key/value lookup, a way to list/paginate, and transaction semantics for updates. AKA: a zip file with entries as keys, and XML documents or attachment blobs for values. What’s lacking and causes issues is the update semantics.
- The issue is incremental updates, and this is where things get complex. If you have a file embedded in the middle of a zip file that is 100 bytes, and you want to resize it to 150 bytes, how do you do that? You can’t squeeze it in without moving everything else about, which disrupts other readers. You could append it to the end maybe, but you need to handle concurrent writers. Compression also is an issue here - I expect zip compression is applied to multiple files at once, rather than per file? So now you might need to update multiple seemingly unrelated files. You need to step down from the concept of a whole file as a unit and move towards pages of data that can be incrementally updated/reused/freed, where each page might contain one, many or even only a part of a “unit” (file/row/whatever)
- 👉🏻 So basically ODF loads everything into memory, relies heavily on in-memory structs for quick unsaved updates, and is crash-safe by writing the whole zip to a temp location during saves. Kinda similar to MS Office. The file structure also helps a little. This is good enough for small docs.
  - Many times have I encountered large docs, often spreadsheets, that push the limits here and become noticeably slow. If you want to get more sophisticated with the indexing and paging, SQLite is a very natural path. Anything else would be reinventing the same wheels SQLite has spent decades refining.

- Other example: raster map tiles (basically up to millions of tiny square pictures)
  - Zip vs tar vs filesystem vs sqlite. Tested all these scenarios, and sqlite was the fastest and the smallest, even beating plain archives with no overhead
- Many filesystems have an issue with tens of thousands or more files in a single directory, which is exactly what you can get with map tiles. No wonder sqlite is faster.
  - Yeah, that's why sqlite was adopted for this back then - many devices still used FAT32 on the storage volumes where tiles we often stored/cached and that had horrendous small file performance - a plain white 130 Byte PNG tile could result in 64 kB being used.
- If SQLite is faster, the problem is the zip library you use. 😩 SQLite has a major draw back (and yes, I love SQLite and built a lot of things around it over the years): the blob you get from the DB cannot be mmap and you have to copy it to somewhere else. For zip files, as long as the file is not compressed, you can mmap it (or it is compressed using some exotic encoding such as PVRTC) just fine.

- OpenDocument is zipped images and XML. Implying you parse the entire format and put it in RAM. And frankly I don't see how SQLite can improve this. Well XML isn't ideal, but it's zipped, so there's no huge penalty in size here.
  - All benefits SQLite's article lists (and I love SQLite to death by the way) can be implemented by having SQLite be the runtime model of the document. On disk and in memory. But SQLite doesn't need to be the transport format. In fact SQLite can easily get bigger than the current format, SQLite is full of unused space when you mutate it around, it can get fragmented and sparse. And if you need to optimize it every time, then the "fast save" etc. benefit goes away.
  - There are formats which do need delta updates and quick indexed look-ups without fully loading the file in RAM, and this is why so many apps do use SQLite as a file format. I just feel OpenDocument was a bad pick to use SQLite for in this hypothetical scenario.
- XML and Zip don't really do incremental updates, meaning the whole application file has to be written on save, meaning corruption can occur due to hiccups mid-write. Sqlite as a disk format and the right application implementation means you can't end up in a corrupted state.
  - I think you can achieve the same thing with xml/zip and some rename shenanigans, but sqlite lets you get that in a single file on disk.
  - Also if you are using sqlite as the memory model, why not use it as the disk/transport format? It's basically free at that point.
- ZIP also can be incrementally updated (file by file) by the way, I think MS Word uses this feature in some saves. But that's beside the point. You simply do not need incremental updates in a transport format.
  - There's a reason "serialization" is called that, it's just serial data. No random access structures, no indices, single representation, often text-based. Throughout the decades, we've learned this is the best way to transport data of any kind. The messy/partial/polymorphic/cryptic/hyperoptimized/indexed formats are not for transport. They're intended to do work in, locally.

- Implementing versioning in the file format conflicts with git, because each document is essentially its own little source control system. This can be surprising to users who copy the file and don’t realize that they’ve effectively copied the entire repo. 
  - I wonder how terrible it would be to either use a git repo as your file format, or to build in git compatibility into your app somehow so you could push and pull?
- it's also pretty well-known that people can share more than they intended in a Word document. Perhaps true of Open Office as well? 
  - Don't forget Exif, its thumbnail and even reflections, in photos.

- I don't want people to read my drafts. That could be highly embarassing, and they should not make it into the final saved document. Past version and undo history should be stored separately from the document. They should be stored out of tree where they wont be committed into some git repository or be automatically synced or anything like that.

- sqlite bad sides:
  - Vulnerabilities: not only in SQLite, but also in wrappers 
  - Lack of transparency: zip with xml's contains only xml's; meanwhile SQLite contains by design all kinds of traces with sensitive information or empty blocks. Attempts to fix these issues removes benefits that were mentioned.
  - Lack of implementer support. It was one of the reasons for WebSQL deprecation many years ago.
  - Lack of standardization for file format. SQLite does not even promise forward compatibility, only backward one. Which means that new documents might not open in old software

- Sqlite-based file formats are also very easy to debug, which saves a lot of dev time. After my app writes to a file and loading back doesn't work, I can just open it in Sqlite and inspect it in any way I wish because I have the full power of SQL at my fingertips.

- 😩 BLOBs in sqlite can be up to 2GB or less, depending on the compilation flags. If you store 2GB and the other application uses sqlite compiled with support for less than 2GB BLOB size, good luck on getting them to work... 
  - If you want to store content larger than 2GB in sqlite, you have to chunk them, manage the chunk sequences, etc. And you can't overwrite a fixed size 2KB portion at the specified offset, you'll have to rewrite the entire 2GB chunk.

- I’m curious to know what a gsheet/doc/slide file actually is under the hood. I as the user am only ever presented with a link, there’s no way to download a gsheet in its native format.

- 🤔 sqlite files aren't small. One thing I don't understand is why they don't do string deduplication in sqlite (as in you only store a string once and every other occurence is just a pointer to that string). It seems such an obvious and easy way to reduce file size, memory consumption and therefore increase performance (less I/O). Is there a technical reason why this would not be desirable?
  - If you have the same (long-ish) string repeating many times in a database, it points to a DB schema needing normalization.
- I guess it depends on the use case. If you load a csv file into a sqlite database, normalisation isn't the first thing you do.
- There is nonzero overhead for doing so: optimizing for duplicate strings invariably adds cost to handling unique strings. This sounds like something you could do at the schema and application level.

- AutoCAD uses a database as its file format, it is fairly slow.

- The SQLite format belongs to SQLite, and an ISO standard would result in that standard being rendered irrelevant by the SQLite team, should they wish to make a change for any reason. Also, people would have to pay ISO for access to the specifications. SQLite should be treated as a defacto standard defined by the SQLite project.

- ## 🪶📄 [What If OpenDocument Used SQLite? (2014) | Hacker News_202012](https://news.ycombinator.com/item?id=25462814)
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

- ## [What If OpenDocument Used SQLite? | Hacker News_201711](https://news.ycombinator.com/item?id=15607316)
- Zip files use a well documented, easily-reproducable and widely implemented deflate algorithm. It's reasonable to assume that someone could, 100 years from now, unzip an OpenDocument file. The contents are XML files - basically text - which can be read with any simple text editor and parsed. The XML is also at least somewhat self-documenting regarding the contained document.
- SQLite databases have a binary format which is known to change periodically.

- > The use of a ZIP archive to encapsulate XML files plus resources is an elegant approach to an application file format. It is clearly superior to a custom binary file format.
  - Why would it be superior? The biggest advantage I can think of is code reuse, but what else?
- Because the author ends up duplicating features of the zip format. Think of all the stuff that goes along with a ppt slide. Fonts, images, videos, sounds. You want to embed the original files anyway, because storing the content in your own custom format is pointless extra work. think how complicated a video file format is. It's a good fit for a file archive.
