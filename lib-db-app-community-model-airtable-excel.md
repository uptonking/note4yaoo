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

- ## 

- ## [自定义字段的功能数据库是怎么设计的呢？ - V2EX _202211](https://www.v2ex.com/t/895430)
  - 业务中开发了个设施巡检系统，功能只是记录对种类不同的设备进行记录。
  - 如果描述不清楚，同样的需求在 OA 平台、问卷系统、低代码平台很常有，想了解下一般实现方案。
- mongodb 本身就是 document 数据库，没有 schema ，性能也足够。但是你需要有一套成熟的 ORM 框架。还有如果用 mongodb 你也要考虑到和其他数据表的 relation 。如果你已经很熟悉 mysql 或者 psql 了，用 json 类型其实也可以。
  - 或者就是单独一个表来保存扩展属性（ key/value 的形式），这种就是读取数据时，要 join 联查出来
- postgresql 的表继承方案也可以了解一下， 我们公司用的就是这种方案

- 📝 [MySQL动态存储方案对比「转」 - RoninZc 的个人博客](https://ronin-zc.com/%E5%8A%A8%E6%80%81%E5%AD%98%E5%82%A8%E6%96%B9%E6%A1%88%E5%AF%B9%E6%AF%94%E8%BD%AC%E8%BD%BD/)

- ## 🌰🆚️ Is there some kind of web app or tool that mimics a spreadsheet/excel in UX that directly translates into sql queries?
- https://twitter.com/Captaintobs/status/1761835197459538195
- The closest thing that comes to mind is VSCode Data Wrangler: UI that generates pandas code
- I have built the open source Buckaroo table widget for Jupyter/VSCode.  It has a prototype for a lowcode UI that can emit pandas/polars (IBIS soon) code

- Depends what aspects of spreadsheets you are looking for, but https://tadviewer.com has a spreadsheet-like pivot table UI powered by @duckdb .
- @Ultorg does that; spreadsheet-like UI, generates SQL behind the scenes. It's a desktop app, so you can connect directly to databases on localhost or on a private network if desired.
- jetbrains datagrip has a feature for this! I don't think that part of the code is open source

- @QuadraticHQ is doing spreadsheets with SQL capabilities

- @Tabulaio provides exactly this - it is visual no code step by step transformation builder and compiles into SQL dialect of your database or python code. It can also compile into dbt projects.

- ## 🧮 [A Gentle Introduction to Ted Nelson's ZigZag Structure (2002) | Hacker News_202105](https://news.ycombinator.com/item?id=27210008)
- Happily, Nelson's patent has finally expired.

- In its simplest form, a ZigZag structure can be an n-dimensional grid, where each node is connected to its direct neighbors in the grid. 
  - In 2D, that would give you a spreadsheet. 
  - However, ZigZag can do more: you can have loops along any axis, e.g. a spreadsheet where the columns "wrap around". 
  - Furthermore, ZigZag supports looping the columns of only one particular row: a normal 2D spreadsheet, except that row 13 only has 4 columns, and those columns are wrapped up in a loop. You could also have sparse grids - where nodes are missing, and the edges skip over the missing node.
  - The idea is to have something that locally, if you look only at the surrounding nodes, always looks like a neat n-dimensional grid. But the global topology can be totally whacky.

- To put it coarsely, outside ZigZag there are three different kinds of structures in computers today: linear lists (and grids i.e.~lists of lists), hierarchical trees and messes. That is really messes, not meshes. By a mess, I mean any complicated data structure, usually with one-directional links to make things even more unmanageable.
  - That's not a mess, that's a graph.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Any database engine supports 20-40k column tables? : r/SQL _202210](https://www.reddit.com/r/SQL/comments/xs7dqk/any_database_engine_supports_2040k_column_tables/)
  - The question: does any DB support 40k columns with 100k rows and performs quite fast? Essbase?

- no db engine supports bad design

- ## 🚀 We've created the fastest spreadsheet
- https://twitter.com/ProgRockRec/status/1763337727335125031
- The 8 million row one worked, and it is blazing fast to work with, a sum was instantaneous, however Sort doesn't seem to be implemented yet?
  - If you select the 8M row range, you can right click and select "Sort range" (or Data > Sort). You can also filter, which creates a persistant UI for sorting & filtering.

- https://twitter.com/wesmckinn/status/1763285838673449377
  - I’m thrilled to be an early investor in @GetRowZero and proud that it is built on @ApacheArrow !

- ## [Microsoft announces Lists, a new Airtable-like app | Hacker News_202005](https://news.ycombinator.com/item?id=23236364)
- It's just something with lots of Microsoft's latest software that annoys me. They all feel behind, laggy and lacking features in comparison to their competitor.
  - Slack > Teams
  - Trello > Planner
  - PowerBi > Tableau, Looker, Mode

- ## [Grist is a modern, relational spreadsheet | Hacker News _202311](https://news.ycombinator.com/item?id=38080951)
- it's kinda annoying when people call something spreadsheet, when it's really just a richful WYSIWYG-interface for a relational database. Not that it's bad to have a good Database-Interface, but the flawed communication will make a poor impression with those who really want a real excel-like spreadsheet, and then got something else. This will probably more harmful than beneficial in the long run.
  - The motivation for calling Grist a spreadsheet is that it has formulas, and cell values get updated automatically when something they depend on gets updated

- ## [Show HN: Visual DB – Airtable alternative for your own database | Hacker News _202308](https://news.ycombinator.com/item?id=37223019)
- I've been wanting to build something like this myself, due to the sheer lack of alternatives. Other purported "airtable clones" often lack filtering and grouping, the essence of Airtable.
  - Right, others such as NocoDB, Baserow, Plato and Mathesar don’t support grouping. Even Google Tables has only one level of grouping.

- ## [Rows 2.0: The easiest way to use data on a spreadsheet | Hacker News _202303](https://news.ycombinator.com/item?id=35002720)
- Calling it a spreadsheet and making it look and work like a spreadsheet is a bad idea, because now you're competing against Excel.

- ## [Rows.com – Spreadsheet that supports external API integration and collaboration | Hacker News _202111](https://news.ycombinator.com/item?id=29171490)
- rows.com seems more focused on external integrations; 
  - Grist has API but is more focused on powerful formulas and layouts for working within the data.

- ## [Show HN: I made an app that consolidated 18 apps (doc, sheet, form, site, chat…) | Hacker News_202401](https://news.ycombinator.com/item?id=38901504)
- Single biggest thing you need to nail down fast: the data model. It is extremely hard to shift as things grow, and without careful thought, it’ll turn into a horrifying miasma of JSONB columns, duplicated data, orphaned rows, and garbage performance.
  - Customers are going to store surprisingly large items in Docs, where you’d be tempted to inline them instead of offloading to S3 et al.
  - Chat practically needs to be its own DB. Discord runs on Scylla, Slack runs on Vitess over MySQL. The needs of chat access are wildly different from other types of storage.
  - If you’re doing any kind of active-active, have a plan for how to move off of that, because it does not scale (at least, not without breath-takingly expensive hardware).

- Single biggest technical thing, anyway. IMO, the single biggest thing is focus and clarity in their communication. If people without a working mental model of software development can’t instantly understand the tangible problem it solves in their existing business process, they won’t even scroll past the break, let alone pay for it
  - The second biggest problem is having an interface design team that makes all of those disparate apps consistent enough to be more usable than individual solutions.
  - The fact that nearly no popular user-facing applications are developer-managed FOSS (as opposed to Firefox/blender/signal/et al which are managed by a company that hires professional designers) despite being free, tells you everything you need to know about dev-driven UI/UX. 
  - Nailed the real important part, the product marketing

- He's most likely using SQLite per account, because that's the easiest way to have an offline DB and sync it, which will most likely scale perfectly fine with appropriate indexes as long as you are careful about the feature set.
  - That introduces a new problem when it syncs to others in the same workspace, if it’s large.
- Nice thing about SQLite is you can “clone” the repository by copying a single file. And in cases where you need incremental sync, you can use an SQLite of diff’s as a single packfile (similar to git).
  - Things like cr-SQLite also have a lot of potential to make single SQLite per client a lot more viable. But I’m interested to see what you think the problems are? Have you found a solution or alternative?

- No one cares about that. Export to open document format or microsoft. You are living in a bubble of “hackers”. You are not your average user. Case in point of “engineers are not product people”

- If your selling point is consolidating apps, you absolutely have to get the data model right, else you don't solve the problem. Just because you don't go in and sell it that way, doesn't mean it's not important as hell. The very reason it's hard to get apps to interoperate is that each one has it's own data model. If they used one giant data model... it wouldn't be a problem.

- Notion might have written something about their journey in this regard?
  - They have, yes, but they also mention learning that skipping building indices during a DB copy (doing so instead after the new instance is built) is much faster, which is pretty basic RDBMS knowledge. It’s great to be learning, and even better to be sharing that knowledge, but it gives me pause about accepting much of what they’ve written as expertise.
  - IME, many SaaS companies have eschewed the idea of having any DB experts, and this inevitably leads to pain down the road.

- As a business user it's not clear how I would use it, and why I would care.
  - A good comparison against your front page would be against monday.com or Asana who start with use-cases and practical application. 

- I built something similar many years back.
  - I should have found a handful of customers who needed tight integration among these use cases and let their needs drive the implementation.
  - Why? There are already plenty of applications that do the same functions. (MS Office, Google Drive, ect, ect.) These applications are mature, and well-understood by the whole market.

- I personally prefer apps that do one thing well. I don't like "super" apps that does everything. I like separate tools, and not a Swiss army knife.

- One of the most important features to get right for tools like this is collaborative editing. It's incredibly difficult to get this right (live preview, conflict resolution, history management, etc), especially given how the vast majority of users are non-technical folks (which aren't used to tools like git). 
  - I actually think this hyper-granular realtime collaboration like in Google docs is slightly overrated.
  - All I’m saying is this CRDT craze isn’t always necessary or even appropriate for many products. It adds a lot of technical complexity, especially for a small shop.
- 🔀 jitl/notion: Realtime collab apps tend to kill their competitors without realtime collab. 
  - See Figma: slightly worse UX and performance compared to Sketch, easily killed Sketch. 
  - How did Notion penetrate the competitive docs/wiki market? Much more collaborative than the incumbent Confluence (now confluence is iterating on realtime collab to remain relevant).
  - Realtime is becoming table stakes in any online collab system. I think code is the exception, not the rule, because it’s 100x more brittle(容易损坏的；不安全的) than prose or pixels that need to convey approximate meaning to humans.
  - You can implement realtime without using CRDT/OT, Notion is paragraph-by-paragraph last write wins, no fancy algo, but mostly good enough to remain competitive.

- > I actually think this hyper-granular realtime collaboration like in Google docs is slightly overrated.
  - I have to disagree. It's absolutely necessary for a lot of workflows, especially when people are collaborating on a doc in real time during a meeting (super super common), or when you've got 10 reviewers of a doc all leaving their feedback in comments, and comments responding to comments, over the course of the same hour.
  - The model of clean commits works well for code. It doesn't work well at all for business team documents that are in-progress.

- I would love to know a little more about your tech stack and architecture?
  - It's on GCP and 99% "serverless" with TypeScript + React frontend. Flutter for mobile apps and Electron for desktop apps (planning to switch the desktop apps to Flutter too once their desktop frameworks are more stable)
  - I thought about doing CRDT in the beginning, but because not every block type is text, I simplified the implementation to last write wins. Note that every paragraph is a block, so it's not like the entire page is overwritten. CRDT is still doable though.
  - There are real-time text cursors and block selections, but I intentionally did not implement Figma-style floating cursors that people may expect in certain modules. I thought it looks cool but doesn't offer much value, especially when you can already see what other people selected.
- Interesting you say that because I've always felt like a big drawback of Google Docs is the inability to see the floating cursor. It doesn't feel as immersive as, say, Figma editing. However, I'm just one person and my opinion doesn't speak for them all! It'd be interesting to see an A/B test with this sort of functionality.

- 替代品: google-docs-suite; microsoft-teams; zoho; 飞书

- ## 🔥 [Show HN: Plato – Airtable for your SQL database | Hacker News_202303](https://news.ycombinator.com/item?id=35070488)
- [Plato | Build flexible internal tools](https://www.plato.io/)

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

- ## 📈 [APITable: open-source Airtable alternative | Hacker News_202212](https://news.ycombinator.com/item?id=34127804&ref=upstract.com)
- online demo: https://gitpod.io/#https://github.com/apitable/apitable
  - admin@apitable.com / Apitable2022

- I see some serious red flags on their homepage:
  - "Partners" just seem to be logo-hijacking potential hosting platforms (not actual partnerships)
  - The testimonials use fake names + stock art
- for baserow
  - it’s only open-core: loads of important features locked behind subscription pricing, 
  - You will not lose any features by self-hosting. Quite the opposite, some enterprise features like SSO are only possible for self-hosted instances. Source: I work for Baserow.

- Is there an ongoing trend of sketchy "OSS" product offerings using this same website layout and similar fake quotes from users? I feel like I'm seeing this a lot recently.

- Initial commit was in August and there are only 5 contributors, yet it's calling itself the "the best Airtable alternative" and filled their side with all kind of fancy screenshots? 
  - Unless they ported the whole project from a previous project, there would be no way to barf out a high quality competition in such a short time with such a small team.
  - Without the screenshots and partner-claims I would think they are just overly enthusiastic. But the whole highly professional sales vibes for such a fresh project makes it just untrustable.

- It’s also AGPL licensed but has incompatibly-licensed dependencies.

- Is'nt there some joke that every month a new startup tries to reinvent pivot tables?

- Airtable was so cool when I tried it years ago but it was insufferably slow. Just unusable as are many web apps these days unfortunately

- ## 📈✨ [Grist – Open core alternative to Airtable and Google Sheets | Hacker News_202202](https://news.ycombinator.com/item?id=30392227)
- 
- 
- 

- ## 📈 [Rowy: Open-source Airtable alternative on Google Cloud | Hacker News_202110](https://news.ycombinator.com/item?id=28758598)
- 
- 
- 

- ## 📈✨ [Baserow.io – Self-hosted Airtable alternative | Hacker News_202103](https://news.ycombinator.com/item?id=26448985)
- Airtable and the like strike me as a database tool for dummies who want 'anyone change anything anytime', which is just a recipe for no one knowing who the hell is changing what and when anymore.

- I like notion because it’s a hybrid of wiki, table/database, calendar, kanban. You can do a lot more than just tables.

- ## 🚀🔥 [Undb – Private first, unified, self-hosted no code database | Hacker News_202306](https://news.ycombinator.com/item?id=36404622)
- I love the idea of an Airtable/Notion open source alternative, but I haven't seen any projects yet that look like a solid long-term bet.
  - NocoDB is neat, but looks like it's a single vendor-driven project that could go open core or die altogether if funding dries up.
  - Baserow also looks good, but already appears to be open core and another single-vendor project.
- Single-vendor open core (SVOC) can move quickly but it tends to degrade and disappoint over time. I would love to see a project of this sort that's actually trying to be truly community driven.

- If you're looking for a performant no-code database, you might want to try Baserow. It's made to scale, and can handle 1M+ rows with 15+ fields. Disclaimer: I'm the founder of Baserow.

- could we call this product somehow differently? I don't feel it's database, it's database frontend or smth.
  - You are right, it's not a database, so I call it undb
  - It seems more along the lines of a "headless CMS", which is basically just extensible CRUD often with API endpoints; compare it to Strapi. This one looks finished enough to play around with at least.

- in my opinion the most value undb provide is to handle the reference part which you always have to impl in code when you use traditional RDBMS. Also it provides typed api, real-time sub and user friendly views
  - Undb handles reference for you, which is always most hard/difficult part to handle in most lowcode system, so it's not just a database frontend. It's like MS access when you link reference in the access ui, but undb can also handle lookup & rollup in browser

- I've been in the midst of developing my own frontend (SPA/PWA) data storage solution, using IndexedDB (and the Dexie library), so I've been watching all of the recent announcements about the wasm-sqlite implementations and wondering if I should probably just switch over to that. If, for nothing else, for the exportable .sqlite file that would be available without having to do a custom "Database Export".
  - 👉🏻 With that in mind, I'd be much more interested in a clean library that abstracts sqlite data access, but stores it in the same format. 
  - That way, I could implement the library in my frontend app to store data, and then use the sqlite files that can be exported to load into your Undb app to inspect them (I'm thinking for, say, error debugging or whatever). Similar to how I might pull a client's db backup and load it into Microsoft's SSMS management app.

- Undb doesn't support MySQL as I see. But it has the feature I'm missing in NocoDB: a Calendar View which funnily NocoDB promoted on their website but doesn't have
  - Noco Founder here. We just managed to handle all date time and timezone issues which is quite complicated and made a release like a month ago. When we started, we could not have anticipated the difficulties surrounding timezone issues. So we will be getting to Calendar view soon.

- ## 📈✨ [Show HN: NocoDB – Open-Source Airtable Alternative | Hacker News_202105](https://news.ycombinator.com/item?id=27303783)
- 
- 
- 

- ## [Ask HN: How Airtable / Notion's Database is implemented? | Hacker News](https://news.ycombinator.com/item?id=36475866)
- There are some open source competitors to Airtable and Notion that can provide good insight. like nocodb

- ## [Microsoft announces Lists, a new Airtable-like app | Hacker News_202005](https://news.ycombinator.com/item?id=23236364)
- 
- 
- 

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

- ## ✨ [subset: Excel 2.0 – Is there a better visual data model than a grid of cells? | Hacker News_202203](https://news.ycombinator.com/item?id=30868696)
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

- ## 📈🚀🔥 [Show HN: Airtable, a real-time spreadsheet-database hybrid | Hacker News_201409](https://news.ycombinator.com/item?id=8373914)
- Airtable is fantastic. My only wish is that they formalize a “Airtable open format specification”. 
  - At the moment, in spite of all its shortcomings, an excel file is far more portable than an Airtable doc. 
  - We need the Airtable data structure to become an open standard.
  
- ## 🔥 [A web-based Excel/database hybrid | Hacker News_201205](https://news.ycombinator.com/item?id=3959486)
- 
- 
- 
