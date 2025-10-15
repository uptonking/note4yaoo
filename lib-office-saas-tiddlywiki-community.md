---
title: lib-office-saas-tiddlywiki-community
tags: [cms, community, tiddlywiki, wiki]
created: 2023-11-14T16:09:12.446Z
modified: 2023-12-15T17:50:49.509Z
---

# lib-office-saas-tiddlywiki-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Diff-match-patch. Feature Bloat? - Discussion - Talk TW _202412](https://talk.tiddlywiki.org/t/diff-match-patch-feature-bloat/11477)
  - I’m working with the later versions of TiddlyWiki, and I’m seeing that there are filters to making and applying patches. These rely on a minified utility module of not-small size.

- I do think that the diff match patch library is unnecessary for the core, since it doesn’t have much use case in the core (We already have the `difftextwidget` for comparing, while applying diff files to tiddlers isn’t widely used ). Perhaps making them independent as a plugin and add some more features (like registering `text/x-diff` as a tiddler type) is better.

- The diff-match-patch library was added 6 years ago, to be able to identify changes with the $:/Import dialogue. It is possible to show the difference between an existing and a new plugin or tiddler.

- The difftext-widget uses the diff-match-patch library. So without the library, there would be no widget.

- ## 🤝🏻 [Multi User Alternative to TiddlyWiki - Discussion - Talk TW _202203](https://talk.tiddlywiki.org/t/multi-user-alternative-to-tiddlywiki/2899)
- TiddlyWiki needs an auth system to enable a real multi-user experience. We can store username and salted password in a tiddler that only the admin can see and modify.

- 
- 
- 

- ## 💡 [Taking Node Server to the next level_201911](https://groups.google.com/g/TiddlyWiki/c/BtmLkx1mwtU)
  - I have a radical proposal which would take data folders to the next level. What if instead of the file system adapter we would write a new adapter to use a database. We could use PouchDB, but I would vote for something much more widespread like SQLite.

- 🆚️ A while ago I made a syncer that used sqlite and from that I wouldn't suggest a relational database, SQL seems like it would be almost perfect for storing tiddlers but I immediately ran into problems with the database schema because aside from text, title, tags, created, type and modified you have on way of knowing what fields are going to be used so everything else just gets thrown into an otherfields column and you lose the desirable features of a relational database.
  - I found pouchdb to work much better because you can have arbitrary structures in the documents and implement the tiddlywiki filters pretty exactly in calls to `allDocs` and as a document store it can store single file wikis without any trouble at all.
  - I have been considering skipping pouchdb and just using leveldb directly on the back-end but I don't know if the performance improvements are worth the extra hassle.
  - Also in pouchdb you just make a new database for each wiki and never run into problems of scale except in the most extreme cases. I have had pouchdb databases that were close to a gig without any real performance hit, I think that wikis anywhere near that size are going to be rare.
  - I have looked into other nosql databases and none of them look like they would be any better than pouchdb or using leveldb with some basic namespaced storage setup.
  - also in my experience database maintenance is much easier in pouchdb and leveldb than in MySQL/MariaDB. You don't have the same problems of having database files taking up 100gigs when you only have 4 gigs of data that changes often. I am sure that problem can be solved by having an experienced database maintenance person, but I think that with one of the nosql databases you could skip that completely.

- The problem with solutions like PouchDb is that there are no turn-key installations. You have to pretty much do everything yourself down to the bare metal.
  - SQL, on the other hand, is supported almost everywhere.
  - The workaround re fields is to specify the fields you want in advance. Rebuild the database when you need to add fields.
  - Or to have a dozen fields with generic names in the database, but then map them with a configuration file.
  - Mostly, I'm saying that a solution that is for everyone needs to based on technology that's commonly available.
- The benefit of PouchDB is that it can be installed using NPM, or packaged into something like BobEXE without having to do a system-wide installation. For a local installation PouchDB is much easier to set up than MySQL/MariaDb

- There have been quite a few experimental syncadaptors over the years. Some of them come back from a simple GitHub search
  - Another syncadaptor that I'd love to see is one that stores tiddlers in an online Google Sheet. Done right, one would be able to seamlessly switch between editing the same data within TiddlyWiki and via the Google Sheet user interface.
  - Another interesting sync adaptor would be one that retrieved and stored tiddlers via the Wordpress API. The attraction is that WordPress hosting is highly commoditised, being readily available and cheap. It should be possible to store tiddlers as “Pages”, and to inherit WordPress’s very smooth handling for media and attachments.

- ## 🛋️ [TW 5.2.0 + CouchDB ?_202111](https://groups.google.com/g/TiddlyWiki/c/jKYp7GIm1o8)
- I have been following the TW project for years and I am still very surprised that the community continues to actively support super strange, inconvenient and limited ways of saving and synchronizing – but at the same time all developments using normal technologies on which synchronization could be easy, seamless and safe, such as CouchDB, are not supported in official release and abandoned by community.
  - Especially considering the new data storage format in JSON, with which synchronization with object databases has never been easier. It's even easier than maintaining the current server solution on files, which in principle cannot work offline, unlike a solution based on IndexedDB+PouchDB→CouchDB or IndexedDB→Mongo/Postgres.
  - I have used PouchDB adapter from NoteSelf, but it's outdated and contains a lot of bugs. Other solutions were outdated even earlier.

- I was quite keen(热心的) on noteself, had it set up and everything but then after the takeover, Couch DB moved past my tolerance for banging my head against software and it killed it for me.  I suspect that was true for others.

- I think there were a few reasons that I didn't personally take CouchDB further in TiddlyWiki 5:
  * TiddlyWiki's internal store needs to offer a synchronous API, but CouchDB offers only async APIs. That means there would always be a requirement for a sync process between TWs synchronous DB and the CouchDB API, which means that TW still has to handle synchronisation
  * The difficulties of setting up and running a server of my own
  * The lack of CouchDB online services
- I was delighted to see Danielo's work with NoteSelf, and it deservedly attracted a lot of interest. It demonstrated that CouchDB can be retrofitted onto TW5 just like any other database with an async API.

- ## [TiddlyPWA: putting TiddlyWiki on modern web app steroids | Hacker News_202307](https://news.ycombinator.com/item?id=36885753)
- Tiddlywiki was great because it was a single file, the whole point of tiddlywiki was being a single self-modifying html file. No app needed.

- This effort is remarkable as the mobile side of saving is not as robust as on the desktop side of things and there is a scaling limit on performance as the number of tiddlers grows. Also the syncing between tw documents between different desktop/mobile clients can be a challenge with diffing.

- One of the main reasons I switched away from tiddly wiki was I needed better mobile support and syncing was always a monumental pain. Not to mention saving the HTML file was fundamentally broken in modern browsers at the time.

- I'd like to see a proper tiddlywiki in an Electron application. The one that exists now is quite ugly and annoying to use. Maybe what I really want is someone to re-imagine TW as something similar to Obsidian (or Obsidian->TW?)

- If you're on windows, you can give the tiddlywiki file an . HTA extension and it will behave like an HTML app. It does double the filesize due to encoding changes if I'm not mistaken but it works

- ## [TiddlyWiki 5.1.23 | Hacker News_202012](https://news.ycombinator.com/item?id=25527581)
- TiddlyWiki 5 has no feature or plugin to have revision history integrated into the UI, although one might come in the future
  - There is a plug-in for revisions, but it may be too simple for your needs?

- I'm interested in the idea of dividing information into smaller-than-a-normal-wiki-page 'tiddlers', and I like the UI design. Overall, I can't find any other software that quite matches TiddlyWiki's capabilities.

- It's hard to find a good solution since the main Tiddlywiki is built as a single-user rather than multi-user solution.

- What's the best way to persist state with TiddlyWiki? I really would like to save without any browser extensions.
  - I've found setting up the Git integration to be the best way

- Was a happy user of TiddlyWiki 5+ years ago but eventually left when adding too many pictures made that HTML file so bloated it could barely open.
  - There is lazy-loading now you can use with the server edition, but I don't like either that they're still served out as base64 embedded content. I suspect the most elegant solution is to have your images live hosted somewhere else, and just add references to them.

- ## [Tiddlywiki – A non-linear personal web notebook | Hacker News_201809](https://news.ycombinator.com/item?id=18107271)
- I personally think Tiddlywiki is a fascinating project and I even used it professionally for a few years. But, these days, I think you likely do better with either a Dropbox directory full of Markdown files or installing the free tool Simplenote everywhere (mobile/desktop) and using its support for notes/Markdown. 
  - It's true that if you go with these simple schemes, you lose wiki-style linking. But, I've found that YAGNI applies here.

- The only annoying thing are:
  - we need to press 2 carriage return to go to the next line
  - the markup languages are never standard. we use redmine with textile which is kinda compatible with TW, but not 100%

- I look at TW every couple of years or so, and there has never been either:
  - a sane way to keep a wiki on something like Dropbox (at the time, the only way to have persistence was to disable browser security and allow JavaScript to write to disk directly) or
  - a service to sync a wiki between machines
  - Has that changed nowadays?

- The most unique thing for me is the fact that it's an .html file that you can just download and run. The data/saving mechanism is completely separate. This "unhosted-ness" seems to be a growing trend.

- ## [TiddlyWiki: a local, single-page wiki | Hacker News_201701](https://news.ycombinator.com/item?id=13523660)
- I built a TiddlyWiki site for an RV park circa 2008. It was easy to do and looked great. It was easy for the non-technical owners to update. But Google completely ignored it, and so the park was invisible to most tourists. It folded a few years back, and I partly blame myself, for picking TiddlyWiki.
  - By now you can export static pages from it

- I am also a TiddlyWiki user. I use it as personal note taking + bookmarking + daily reading log. The best feature it has is a Wiki feature, not any TiddlyWiki feature: backlinks. I could make the backlinks show up in the footer of every page (tiddlers) and this reminds me connections I might have forgot. Tiddlywiki is also a great system for bookmarks. This is different from restrictive categories.
- Couple of problems I face:
  - No converter to convert files to other Wikis or formats
  - Static pages has awful URLS
  - Duplicate titles
  - Data corruption

- I think we still don't have a free opensource version of a personal wiki that supports the following:
  - 1. Easy copy and paste (or import) of Web pages (including embedded images) 
  - 2. Embedding and resizing images 
  - 3. No server requirement. 
  - 4. Cross platform 
  - 5. Extensible
# discuss-altertives-wiki
- ## 

- ## 
