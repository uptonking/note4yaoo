---
title: lib-db-app-community-model-airtable-excel
tags: [airtable, community, database-design, excel, notion-database, spreadsheet]
created: 2023-09-26T20:06:23.313Z
modified: 2023-10-26T21:54:54.201Z
---

# lib-db-app-community-model-airtable-excel

# guide

# discuss-stars
- ## 

- ## [A Gentle Introduction to Ted Nelson's ZigZag Structure (2002) | Hacker News_202105](https://news.ycombinator.com/item?id=27210008)
- Happily, Nelson's patent has finally expired.

- In its simplest form, a ZigZag structure can be an n-dimensional grid, where each node is connected to its direct neighbors in the grid. In 2D, that would give you a spreadsheet. However, ZigZag can do more: you can have loops along any axis, e.g. a spreadsheet where the columns "wrap around". Furthermore, ZigZag supports looping the columns of only one particular row: a normal 2D spreadsheet, except that row 13 only has 4 columns, and those columns are wrapped up in a loop. You could also have sparse grids - where nodes are missing, and the edges skip over the missing node.
  - The idea is to have something that locally, if you look only at the surrounding nodes, always looks like a neat n-dimensional grid. But the global topology can be totally whacky.

- To put it coarsely, outside ZigZag there are three different kinds of structures in computers today: linear lists (and grids i.e.~lists of lists), hierarchical trees and messes. That is really messes, not meshes. By a mess, I mean any complicated data structure, usually with one-directional links to make things even more unmanageable.
  - That's not a mess, that's a graph.
# discuss-dataframe/tabular/excel
- ## 

- ## 

- ## 🔥 [Excel as a database | Hacker News_201304](https://news.ycombinator.com/item?id=5515290)
- 
- 
- 

- ## [Why isn’t there a decent file format for tabular data? | Hacker News_202205](https://news.ycombinator.com/item?id=31220841)
- several high quality and well-developed formats
  - csv/tsv -- Simple for simple use cases, text-based, however many edge cases, feature lacking etc
  - xlsx -- Works in excel, ubiquitous format with a standard, however complicated and missing scientific features
  - sqlite -- Designed for relational data, somewhat ubiquitous, types defined but not enforced
  - parquet / hdf5 / apache feather / etc -- Designed for scientific use cases, robust, efficient, less ubiquitous
  - capn proto, prototype buffers, avro, thrift -- Has specific features for data communication between systems
  - xml -- Useful if you are programming in early 2000s
  - GDBM, Kyoto Cabinet, etc -- Useful if you are programming in late 1990s

- The latest version of SQLite has a STRICT command to enforce the data types. 
  - This option is set per table, but **even in a STRICT table you can specify the type of some columns as ANY** if you want to allow any type of data in that column (this is not the same meaning of ANY in non-strict tables).

- One major limitation with quoted values that can this contain record delimiters (as opposed to escaping the delimiters) is that it stops systems from being able to load records in parallel.
  - Some systems ban embedded record delimiters, for this reason.

- Parquet is a wonderful file format and is a dream to work with compared to CSV. 
  - Parquet embeds the schema in the footer metadata, so the query engines don't need to guess what the column names / data types are.
- Parquet is still relatively poorly supported in the JVM world 
- The other problem with Parquet is that it's overly flexible/supports application-specific metadata. 
  - It's all fine when you use a single tool/library for reading and writing files but cross-platform is problematic. 
  - Saving a Pandas dataframe to parquet, for example, will include a bunch of Pandas-specific metadata which is ignored or skipped by other libraries.
- I've been pretty impressed with parquet lately. One thing I've missed is a way to group tables. Is there a standard for that? While parquet is generally column oriented it has support for metadata about tables of multiple columns. However, I'm not aware of any format that groups the tables, short of just zipping a bunch of files.

- It's it possible to diff a parquet file?
  - Its possible but you can't just diff the file bytes. Because you will get spurious differences due to metadata, etc.

- There is a decent file format for tabular data, and the author dismisses it: parquet.
# discuss
- ## 

- ## 

- ## 

- ## 🔥 [Show HN: Plato – Airtable for your SQL database | Hacker News_202303](https://news.ycombinator.com/item?id=35070488)
- 
- 
- 

- ## 🔥 [On Anki's Database | Hacker News_202202](https://news.ycombinator.com/item?id=30427549)
- 
- 
- 

- ## 🔥 [Retool Database | Hacker News_202303](https://news.ycombinator.com/item?id=35369279)
- 
- 
- 

- ## 🔥 [Ask HN: Best low-/no-code solution for simple web-based database frontends | Hacker News_202104](https://news.ycombinator.com/item?id=26657803)
- 
- 
- 

- ## [Excel never dies (2021) | Hacker News](https://news.ycombinator.com/item?id=32346288)

- It's true that Google sheets and LibreOffice don't have Powerquery, and that's a big pain. But the worse thing is that they don't have tables. As in, the "format as table" button in Excel. 
- Maybe it's a problem of naming -- "format" makes people think it's just about aesthetics, but actually it imparts real semantic structure onto a rectangular grid of data.
  - It gives the grid a name that you can refer to in formulae, and the columns are named too, with their names living inside the table namespace ("structured references" is what Microsoft calls it). The table automatically expands its boundaries when you start typing a column header to the right of the current columns, and likewise it expands to comprise the row beneath it if you type values into that row. And it has smart indexing: there's special syntax to refer to "this table" and "this row" in formulae.
- The point is the semantic structure that makes your spreadsheet more than just a rectangular soup of cells, so you don't have to claw through endless cryptic "G70:$K100" cell references. 
  - Think of it like a mutable resizable dataframe. 
  - It's the core data structure of an efficient, scalable, maintainable Excel document

- ## ✨ [Grist – Open core alternative to Airtable and Google Sheets | Hacker News_202202](https://news.ycombinator.com/item?id=30392227)
- 
- 
- 

- ## ✨ [Baserow.io – Self-hosted Airtable alternative | Hacker News_202103](https://news.ycombinator.com/item?id=26448985)
- Airtable and the like strike me as a database tool for dummies who want 'anyone change anything anytime', which is just a recipe for no one knowing who the hell is changing what and when anymore.

- I like notion because it’s a hybrid of wiki, table/database, calendar, kanban. You can do a lot more than just tables.

- ## 🚀🔥 [Undb – Private first, unified, self-hosted no code database | Hacker News_202306](https://news.ycombinator.com/item?id=36404622)
- I love the idea of an Airtable/Notion open source alternative, but I haven't seen any projects yet that look like a solid long-term bet.
  - NocoDB is neat, but looks like it's a single vendor-driven project that could go open core or die altogether if funding dries up.
  - Baserow also looks good, but already appears to be open core and another single-vendor project.
- Single-vendor open core (SVOC) can move quickly but it tends to degrade and disappoint over time. I would love to see a project of this sort that's actually trying to be truly community driven.

- Undb handles reference for you, which is always most hard/difficult part to handle in most lowcode system, so it's not just a database frontend. It's like MS access when you link reference in the access ui, but undb can also handle lookup & rollup in browser

- I'd be much more interested in a clean library that abstracts sqlite data access, but stores it in the same format. That way, I could implement the library in my frontend app to store data, and then use the sqlite files that can be exported to load into your Undb app to inspect them

- ## ✨ [Show HN: NocoDB – Open-Source Airtable Alternative | Hacker News_202105](https://news.ycombinator.com/item?id=27303783)
- 
- 
- 

- ## [Ask HN: How Airtable / Notion's Database is implemented? | Hacker News](https://news.ycombinator.com/item?id=36475866)
- There are some open source competitors to Airtable and Notion that can provide good insight.

- ## [Wildcard: Spreadsheet-Driven Customization of Web Applications | Hacker News_202002](https://news.ycombinator.com/item?id=22439141)
- Wow, I absolutely love this concept.
  - It is messy and overly ambitious, but promises something like a return to the "view source" mindset of the old web - where data was in plain sight and anyone curious and a little tenacious could reshape the web for their own needs.
  - I have gone partway down this path for a related concept, and **browser extensions are really the only way to go**. 
  - The biggest risk and hassle is a reliance on brittle, site-specific logic to make things work well. I haven't dug into this project yet to see how automated any of this is or might become, but if there is an element of community sourcing (like a ruleset for scraping AirBnB effectively) it opens up a potential attack vector like any GreaseMonkey-tyoe script, especially if passed routinely to less technical users. 
  - Not a huge issue on day 1 but not an easily solvable issue.

- This is the most inspiring implementation of live web scraping that I have seen. However, I think it will only work well on semantic HTML. I don't know about AirBnb, used in the paper, but I can say many good words about GitHub. GitHub is an awesome example of a customizable web app thanks to solid, semantic HTML structure. You can see hundreds of web extensions and Tampermonkey user scripts for GitHub that work consistently. I wrote a few of my own.

- I've been following this lab's work for a while and actually suggested to them that the implementation for this be based on an RDF style data model. 
  - Ontology languages are the level of abstraction up from a spreadsheet and are an atomic unit in semantic web technologies. 
  - It looks like the way this fits in to the existing architecture is that the site adapters would extract data as RDF triples.
- **Please don't bring RDF out of its coffin. It has been tried and failed because it's overly complex and verbose**. It's terrible, and technologies which still use it are terrible to interact with to this day.
- Interestingly enough I think that the core of rdf (the subject predicate object triple) is a quite elegant abstraction for knowledge graph representation.
  - I do agree that the layered system of different ontology languages as present in current semantic web standards is not beginner friendly, but it doesn’t mean they can’t be improved on.

- I've said it a few times here on HN that I think the best UX for many web apps (particularly business apps) would be a spreadsheet connected to an API (or better yet, multiple APIs). Of course most web apps don't expose an API, so here we are.
- Spreadsheet-Driven Customization is a great way to enable non-technical users to customize and configure software.

- Obviously **the main challenge, is that not all of the data is present on the frontend**. Also, user cannot permanently change the app, **since just the DOM is changed and that is not persisted anywhere**, am I right?
  - But the whole idea to be able to peek "under the hood" of an app and customise/edit it sounds very appealing to me! I am actually working on the open source project that has that aim, to "understand" the web app from within.

- Seems like you'd want to look into eavt databases for a universal schema, Datomic has a lot of resources explaining it's schema

- ## [Excel 2.0 – Is there a better visual data model than a grid of cells? | Hacker News_202203](https://news.ycombinator.com/item?id=30868696)
- UltOrg is roughly "spreadsheets re-built atop the RDBMS datamodel". The UI supports nested joins, aggregations, filtering, for both display and data update.

- Airtable really ought to be killing Excel, but the SaaS model combined with a stupidly low artificial row count limit (over 50000 rows is listed as "contact us for pricing") means that it will never achieve penetration into weird and wonderful use cases like Excel has.

- I liked the way Apple did it in their Numbers clone of Excel - you can have multiple grids on a single page. It makes it a lot easier to have related data on the same page without fiddling with the row/column sizes to suite multiple types of data.
- Many things that Numbers seems to me to be better than Excel from a formatting perspective:
  * Freeze header rows & columns.
  * Naming header rows & columns.
  * Graphs that don't overlap the sheet.
- Things that I find Excel does better than Numbers from a data perspective:
  * Data validation
  * Large tables
  * Formula Error checking

- ## [Airtable raises $100M at a $1.1B valuation | Hacker News_201811](https://news.ycombinator.com/item?id=18460902)

- I wonder the database structure behind airtable-like flexible data apps. I suppose they would create databases and tables on the fly to increase performance - or maybe they just use unstructured (or flexibly structured) databases like mongodb?
- Maybe something similar to a triple store.

- I use Airtable for my job, mostly as a project management application. This may be an unusual use case, but I find myself limited at many times.
  - It's almost like nobody at Airtable pays attention to the design of features. Everything is so limited. Blocks are an incredibly useful idea, but in practice uncustomizable and not something I find helpful.

- There is one lurking competitor to Airtable that no one knows: Notion.
  - Except Notion is far more capable than Airtable. You can do all these table joins across pages but in Notion everything is a page whereas in Airtable it's just a form. That is the ultimate flexibility which makes it exceptionally well suited for any kind planning effort. And it's a great canvas for creative projects.
  - Plus Notion has some of the best customer service around. Half the company are there for support!

- Coda is more capable in other ways - I can summon up chats of my data and define new formulas. I love that buttons let me effectively create a little webapp that also works beautifully on mobile.

- It's a database primarily operated upon using a spreadsheet interface. You can create different representations (literally Views) of your data / rows. You can add custom logic "blocks" to rows / entries / tables that, for example, send a text message to a customer in the table.
  - You're not going to build a brand new consumer app on Airtable, but all of the backoffice and internal crap we write over and over and over again... it's a really good option for simplifying those processes and is accessible to non-developers.

- ## 🔥 [Show HN: We made a real-time editor for web database apps | Hacker News_201810](https://news.ycombinator.com/item?id=18113779)
- 
- 
- 

- ## 🔥 [Show HN: SpreadsheetDB – A database that you can query with spreadsheets | Hacker News_201703](https://news.ycombinator.com/item?id=13978271)
- 
- 
- 

- ## 🔥 [Dropplets - A simple database-less CMS | Hacker News_201310](https://news.ycombinator.com/item?id=6508043)
- 
- 
- 

- ## 🚀🔥 [Show HN: Airtable, a real-time spreadsheet-database hybrid | Hacker News_201409](https://news.ycombinator.com/item?id=8373914)
- Airtable is fantastic. My only wish is that they formalize a “Airtable open format specification”. 
  - At the moment, in spite of all its shortcomings, an excel file is far more portable than an Airtable doc. 
  - We need the Airtable data structure to become an open standard.
  
- ## 🔥 [A web-based Excel/database hybrid | Hacker News_201205](https://news.ycombinator.com/item?id=3959486)
- 
- 
- 
