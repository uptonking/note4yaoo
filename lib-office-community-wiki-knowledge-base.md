---
title: lib-office-community-wiki-knowledge-base
tags: [community, knowledge-base, office, wiki]
created: 2023-09-21T17:20:07.550Z
modified: 2023-09-21T17:32:15.618Z
---

# lib-office-community-wiki-knowledge-base

# guide

- 尝试将知识库与book/dict/mdx结合的产品

- https://github.com/brettkromkamp/awesome-knowledge-management
  - A curated list of amazingly awesome articles, people, applications, software libraries and projects related to the knowledge management space
# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## [GitLab Wiki or Other self-hosted wiki for Documentation : r/selfhosted _202208](https://www.reddit.com/r/selfhosted/comments/wdjeo8/gitlab_wiki_or_other_selfhosted_wiki_for/)
- I use MediaWiki (the same software that powers Wikipedia).

- I'm currently moving from DokuWiki to Joplin for all my personal notes. The primary reason to move is that Joplin can provide offline access via mobile app. In a team/collaborative environment I would still continue to use DokuWiki.

- ## [Silver Bullet: Markdown-based extensible open source personal knowledge platform | Hacker News_202212](https://news.ycombinator.com/item?id=33843009)
- I'm a huge fan of how Obsidian approaches it- previewing each token if you're not actively editing it. This is always how I use it.
  - I never use split-screen view for Markdown. Split-screen makes sense for something more abstract like latex or html. But I do not see the benefit for Markdown. I would much rather have 50% of my screen.
- My biggest frustration with Obsidian is that it doesn't follow any spec when it comes to raw HTML. They seem to have fixed inline raw HTML at some point but HTML blocks are still broken. They know it and they explicitly will not fix it.

- It says it is inspired by obsidian (and roam). It is also keen on "end-user Programming", so the org-mode (and org-roam) comparison is inevitable on HN

- ## [Managing my personal knowledge base | Hacker News_202001](https://news.ycombinator.com/item?id=22000791)

- I can’t help but wonder why it isn’t more common to see people using a local SQLite database, or any other self hosted database, to serve as a personal knowledge base management system. A lot of the paid solutions I’ve seen seem to bend over backwards to offer a limited subset of the features that are trivially available in an actual database.
- This reminds me of SQLite's own Fossil-SCM product. It's a source control manager with wiki and built-in web interface all stored within one SQLite file. They use it to manage the source of SQLite itself.
  - It's definitely not geared towards note taking the way other apps in this thread are, but it could have value as a self-contained and portable wiki/kb. I'd be interested to hear of people's experience with this, either for its main purpose or even just as a note taking system.
- Yes, but there are no good tool to do it. In my case i need to store a a lot of structured data and files. So i need a Document manager / Database. It's hard...
  - I started with excel a lot of year ago, migrated to access and now i'm trying nixoxdb for android
  - The main problem is the ease to use, you need to create a table for everything you want to store, and nothing support an hybrid free-form AND structured data(while also been able to store files), so the solutions with good text editing are terrible at structured data and viceversa.
  - Other problem are the ability to sync or even open the database in more than a couple of platform and the ability to access the file embedded in the database from other application
  - I'm also evaluating notion, but i really don't want a cloud service since i store basically everything inside my main database and the ability to access years from now is a MUST.
  - Also i still not have a good solution for my email that are stored mostly in thunderbird and only some message are "exported" to my main database.

- I use airtable now when I need to have structured data. I use tiddly for note taking and enhanced bookmark management.

- ## [Kb: A minimalist hacker-oriented knowledge base manager | Hacker News_202009](https://news.ycombinator.com/item?id=24506280)
- I much prefer separate text files for any minimal notes solution, since that plays well with nvAlt, Obsidian, 1Writer, etc, and is the safest sync in every file syncing service (they pretty much all know how to deal with text conflicts). It also lets me write side tooling to crawl and process notes much more easily than if I had to hit a database.
  - it is non-transparent and can’t be edited with a text editor, without being unpacked and repacked like Fossil. Yet another layer of indirection is the last thing I want when I’m in a hurry to write down a thought before I forget it. Of course that can be overcome with practicing the tooling, but that’s also a non-negligible transition cost.

- because the database is the custom schema + the data being managed by the library, not the library itself.

- ## [Ever wonder what the Wikipedia database schema looks like? | Hacker News_200901](https://news.ycombinator.com/item?id=441892)
- I'm amazed how simple it is.
  - I'll second that. I always like pouring over schemas that have been tested by heavy use - and wikimedia sure has.

- Question to those who assumed the schema would be more complicated: Why? Maybe I'm not as good with DB design as I should be, but what parts of Wikipedia did you assume would garner more complexity? Their data layout is pretty flat and I'd actually be surprised if it was more complex than this diagram.
  - Often, simple growth in a company will create a messy schema. Version 1 is often clean, but as you iterate and more functionality is added, the schema often undergoes a hideous transformation from museum-piece to something not that.

- Why do they refer to the table name in every fieldname?
  - May be it exists in their coding guidelines? Although `tablename.tablename_columnname` sounds repetitive and verbose, it might in some cases be of help when one deals with too many tables and too many keys with the same name across tables.
  - in many RDBMS's, you can omit the "tablename." part if columnname is unique in the DB

- ## [JSON for Linking Data | Hacker News_202303](https://news.ycombinator.com/item?id=35321493)
- JSON-LD is an open standard for expressing RDF data as JSON. 
  - RDF is the most fundamental part of the W3C's Semantic Web and Linked Data projects, which began at the end of the 1990s to make the Web more machine-readable
- JSON-LD is just a different serialization format for RDF.
  - For anyone looking for a solution to the link rot problem (as well as versioning and dependency management), they might be interested in [Plow: The ontology package manager](https://plow.pm/).

- It’s a standard in search of anyone who wants to implement it.
  - wikidata
- I want to live in an alternative timeline where RDF was never adopted by wikidata but instead created something that solved its specific problems in a human friendly manner. 
  - People always point to wikidata as a successful semantic web project but fail to imagine how much more awesome it could have been. 
  - First off, wikidata has little use for ontologies outside of its own domain because all the types are modeled as dynamic second order concepts. 
  - Meaning, people organise knowledge using web pages and those webpages are used to structure other knowledge.
- Wikidata was consciously designed without consideration for the semantic web/rdf. I remember being dismayed by this, but they added some facilities later. It is designed around a purpose built data model
- Wikidata builds on RDF at its core (the data model behind JSON-LD), and also supports queries with responses in JSON-LD format.

- I used JSON-LD spec because it is preferred by Google, but it requires a lot of duplicate effort of the actual page content. Its almost as if it is designed for sites that use heavy JavaScript frameworks and not for HTML/CSS sites.
  - Usually the dynamic data would be generated by the server. eg. if you have an eCommerce site, it might update prices, stock remaining, applicable regions, etc. That would then be pulled into Google Shopping or whatever other service might consume it.

- JSON-LD is the reason ActivityPub hasn’t taken off even more. It’s just such a pain to deal with variables that could be URLs or entire object trees. Especially for strongly typed languages, it’s a nightmare.
  - serializing/de-serializing the data not being difficult, but the problem lies more in how you handle that data down the pipeline after you deserialized it.
  - after about 4-5 years of trying to implement a clean Go API for processing ActivityPub payloads that the complexity is quite high, at least if you want to build something that can work with more than one client/service.

- 🤔 Why isn’t semantic web more popular inside companies?
- Because SemWeb doesn't solve any real problem while create a ton of new ones and uses a complex data model. Any company that would benefit from using graphs will be better served using a simpler and more general graph model and database.
  - SemWeb is nothing more than stringly typed data with an URI fetish.
- Because it offers no protection against some team inside the company breaking the whole web by moving to a different URI or refactoring their domain model in incompatible ways. A department pays for some subgraph tailored to their needs and they are not interested in financing this for the whole org.
  - Industrial companies use master data management systems, they are centralized and are considered the single source of truth, everyone else builds on them.

- I think a big reason for lack of popularity is familiarity of graphs in general. Most people wouldn't know of a good graph editor I would guess. Everyone knows documents and spreadsheets/tables/lists/folders, but it's rare to see a graph anywhere.
  - I think part of this is that graphs always appear like a complicated mess, and we prefer hierarchies and categories.
  - I would really like a tool like Airtable for graphs. You start with spreadsheets with columns relating to other columns, and then you view the graph next to it as you go. I don't know of a popular tool that does this. It's funny because behind-the-scenes of spreadsheets there is always big dependency graph that updates cells as changes come through.
  - All the specs feel overly-complex too. Like a relic from the XML/SOAP days. For such a simple base concept (subject-predicate-object / entity-attribute-value) it feels like overkill. It's interesting though thinking about how JSON won, while being extremely inferior to XML. Although I think this ability to move fast has left us with a ton of untyped data lying around, and plenty of ad-hoc data transformations.

- Because it's not what you thing and doesn't solve the problems most companies have.
  - Firstly jsonld is only a format for serializing semantic metadata, nothing more, so it only specifies how you can attach that metadata, but not what exctly can be attached in what way with what subtle meanings.
  - Secondly it's one of this very generic tools which "can solve everything" but in practice often only make things more complicated as long as you don't have enough very complicated (and matrue!) tooling around it.

- 👉🏻 same reason wikis arent, it takes too much effort to maintain and keep it semantic instead of copypasted pile of text
  - you'd need CMS, CRM, knowledge base, documentation, source control, chat/forum, inventory, point of sale, customer support channels, issues ticketing system, and every other thing interconnected to with each other
  - do you know of anyone offering this as a complex turn-key integrated solution at a reasonable price?
- Sounds like an opportunity. In every category you mentioned there are new products released and widely adopted all the time. 
  - Look at the rise of ClickUp for example in such a crowded space as project management. 
  - I don't think its too farfetched to one day see a new entrant offering as a key selling point that their api is just a big interoperable graph that you can easily plug your company into...and that's not just GraphQL.

- Every time I get to work with JSON-LD (and json-schema and so on) I keep asking myself: how is this better than XML? (I am convinced it isn't).

- ## [Show HN: BookStack – An open source wiki platform and alternative to Confluence | Hacker News_202201](https://news.ycombinator.com/item?id=29851834)
- I remember considering BookStack while looking for a (surprise) replacement for Confluence.
  - The main thing that led me to stop considering it pretty quickly is precisely the concept of books - I find it both unnecessarily complicated and unnecessarily limiting.
  - My Org now uses DokuWiki. It has a lot of issues (the prosemirror visual editor is a good start, but in beta and out of development, for example). But it's also the least sucking option I've found. 
  - Most Wiki software severely screws up the editing experience, which may not be such a good idea when you want to get people to document things. I'm glad Bookstack does this right.

- As a former DokuWiki user (both pro and privately) the biggest issue is when you want to migrate from DokuWiki.

- Mediawiki is page focused, needing a lot of tweaking to make it act like something other than a completely open public page editor. Trying to collect pages is annoying ugly; about the best you can do is with "categories." Mediawiki tries to do too much with document metatags and whatnot. Mediawiki is ugly/outdated looking (IMHO) and requires lots of php config file editing.

- Bookstack has a lot more inherent document organization stuff (ie: books>chapters>pages etc), it's easy as hell to administer, and it looks gorgeous out of the box.
- On Bookstack you click a link and get a new page instantly. This is nothing like Confluence where you need to wait 5-8 seconds for each page. And no, I will never not shit in Atlassian products until they fix performance.
