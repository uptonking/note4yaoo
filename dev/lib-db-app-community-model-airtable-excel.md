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

- ## 

- ## 🧮 [Realtime Editing of Ordered Sequences | Figma Blog _201703](https://www.figma.com/blog/realtime-editing-of-ordered-sequences/)

- 💡💡 Instead of OT, Figma uses a trick that’s often used to implement reordering on top of a database. 
  - Every object has a real number as an index and the order of the children for an element of the tree is determined by sorting all children by their index.
  - To insert between two objects, just set the index for the new object to the average index of the two objects on either side. 
  - We use arbitrary-precision fractions instead of 64-bit doubles so that we can’t run out of precision after lots of edits.
- In our implementation, every index is a fraction between 0 and 1 exclusive. 
  - Being exclusive is important; it ensures we can always generate an index before or after an existing index by averaging with 0 or 1, respectively. 
  - Each index is stored as a string and averaging is done using string manipulation to retain precision. 
  - For compactness, we omit the leading “0.” from the fraction and we use the entire ASCII range instead of just the numbers 0–9 (base 95 instead of base 10).

- Benefits:
  - Easy to understand and implement
  - Reordering an object only involves editing a single value
- Drawbacks:
  - Index length can grow over time
  - Merging new elements from multiple clients may interleave them
  - Averaging between two identical indices doesn’t work

- We’ve been using fractional indexing for multiplayer editing in Figma from the beginning and it’s worked out really well for us. 
  - Even though OT provides some additional benefits around performance and interleaving, it’s much more beneficial for the Figma platform to use simple algorithms that are easy to understand and implement than to use the most advanced algorithms out there. 
  - It means more people can work on Figma, the implementation is more stable, and we can develop and ship features faster.

- ## 🔢🔀 [The surprisingly difficult problem of user-defined order in SQL | Hacker News _202101](https://news.ycombinator.com/item?id=25797674)
- Using this integer strategy also lends itself to easy reindexing

- ✏️🌲 This is the same problem seen in algorithms for concurrent remote document editing, and the author seems to have re-invented some of the same solutions. 
  - This belongs to the class of problems involving trying to represent a tree in a relational database. There are many solutions, all with some problem.

- 🧮 I've been reviewing this problem lately for a project, and I've settled on a solution that feels elegant and versatile which this article doesn't cover: lexicographical sort.
  - I'm using Mudder.js to do it, but the algorithm is straightforward. Define an alphabet (e.g., A-Z). Every time an item is inserted/repositioned, its sort order is given the midpoint between the sort values of its two neighbors. So the first item is given the sort value M (midpoint between A and Z). Inserting before that item gets G (between A and M). Inserting between these two items gets J (between G and M).
  - Once you run out of letters between two sort values, the algorithm tacks a digit onto the sort value of the item ahead of it. So inserting between M and N yields MM. 
  - If you do this enough times in a pathological pattern and wind up with some long string of characters, you can reflow your list and rebalance everything out evenly (though that's strictly an optimization for storage space/bandwidth, and not a requirement for the algorithm to function).
  - This all sorts perfectly with `ORDER BY` etc., supports an number of repositions bounded only by your storage space, and doesn't require arbitrary-precision decimal datatypes or fraction handling.
- Isn't this just a less efficient version of the "arbitrary precision" variant of approach 2 from the article?
  - It applies the same philosophy but doesn't require special data types. Not all data stores support decimal numbers, and every programming language I've used uses floating point numbers my default. JS doesn't seem to even have a native decimal implementation at all.
  - 💡 Strings work everywhere, and are first-class data types it most systems/languages. They take more bits per digit than numbers (though you can choose a wider alphabet to mitigate that, such as ASCII 33 '!' through 126 '~'), but I'm happy to trade the storage away for using a first-class data types.
- Floating point numbers aren't special data types either. You don't need decimal. It works fine with binary floating point. The reason they don't call it robust is that it requires re-balancing, but so does your proposal.
  - float/double data types have a hard requirement of periodic rebalancing to support unbounded repositions. Lexicographical sorting does not require rebalancing ever, though it may be performed as an optional storage/bandwidth optimization. That is a very meaningful distinction in my book.
- I would use byte array instead of strings, as they should be supported by everything and they are more compact. But I'm crazy guy who wants to optimize everything, I think that in reality string will work just as well and probably easier to debug when you need to deal with it (also easier to serialize if you need to pass it around).
  - Since your alphabet is composed of 8-bit words, you'd get more mileage out of each byte by using 256 symbols in your alphabet, one for each binary value. And by using binary as your alphabet makes things conceptually simpler (even if the values are stored as 8-bit words).

- 🌲 String used for indexing can be further used for sorting not only a flat list, but whole trees of nodes. Similar technique was used before (at least in 1997) to answer queries about the order at a particular time in the past.
- I've looked into string-based tree sorting before, but the only answers I can come up with involve recursive queries, or encoding the entire tree path into each item, which means updating many records if an item with many descendants gets repositioned.
  - Updating many records might be necessary, agree, but for balanced trees the number of records to update could likely be logarithmic. No recursive queries was used (e.g., no Oracle's "CONNECT BY").

- There are CRDT algorithms that are similar to this. Some pick from the middle, some from one end or the other and some randomize the choice. It's the solution I'd probably go with for this specific problem (maybe with a bigger alphabet, although some DBMSs are case-insensitive).

- I actually solved this exact problem recently (who is NOT trying to recreate Roam Research amirite?) And surprised no one else suggested the solution I came up with: just use a text column? When a new list is created the items get incrementing chars as text. If a user reorders an item, the items new sort order value is the value of the item above it concatenated to an "a". This is infinitely extensible, it's only slightly a drag on storage, and very trivial to clean up with some periodic code if storage is actually getting to e a problem. Works like a charm and Dont need to modify postgres itself for this!

- I find similar issues with z-index in CSS.

- 🤔 Why not (assuming that every entry has a unique ID) add a “next_id” field, and treat it like a linked list?
  - That was my thought, but the query is not simple to get the list in order. Plus inserts also require an update.
- I used this approach as part of a personal learning project. It ended up working very well because I was using Mongo, so I could just use $graphLookup with an index on the next ID.
- How do you get the list back in order if there are thousands of entries?
  - It seems like you're in one of two situations: (1) you want the entire list, or (2) you want a small "page" of entries in the list, starting from a known point. For (1), you can fetch all of the entries in table order, whatever that may be, and then figure out the list order after you have the entries. For (2), you make the database do seeks for you in a loop, but it's not such a big deal because it's a small number of them.

- Any of these methods can be combined with a process that re-indexes the order column once things get too pathological, or even does it on a schedule.

- For me the final solution is the Left, right and depth approach Ex https://github.com/collectiveidea/awesome_nested_set

- There are two problems here:
  1. The position of an element in an array is not a property of the element but of the array.
  2. Don't use sorted sets when you need the properties of an array / linked list.
- Modern SQL has CTEs, functions, and arrays. They are very elegant when solving the problem of arrays in SQL.
- 💡 This is a much more practical answer. Point #1 seems exactly right. Even without modern SQL arrays one could even keep references to place, per user, in a simple comma separated text field and munge it in code. Elegant? Probably not. But perhaps more practical then some of the approaches presented. But modern SQL does have arrays.

- IMO the first approach is the best, unless there's a very high number of items (which usually in these scenarios, there's not, even a couple thousand wouldn't be catastrophically bad to update if it's not a common operation). they all kind of suck but everything else seems worse.
- A basic ordered list of integers can cause a lot more problems than I would have expected at first glance.
  - Updating dozens/hundreds/thousands of records at once is obviously unnecessarily heavy to process. But depending on your storage layer's locking model, it could cause high lock contention if concurrent actors are updating the same list and fight over large fractions of the dataset with every update.
  - If you're working in a networked scenario, naïve implementations can turn into transmitting a lot of data across the wire for every single reposition.
  - It's also algorithmically challenging in concurrent scenarios. If I update my local state rearrange items, and you update your local state to rearrange items in an overlapping range, when they have to sync up this quickly turns into the developer having to learn to implement CRDTs or Operational Transforms. You could implement optimistic or pessimistic locking, but you have to lock such a large fraction of the dataset that it's easy to limit throughput.
  - Distributed/eventual-consistency problems are particularly challenging with ordering solutions of this variety, but the difference between one operation updating a wide swath of values vs just the single updated value can make a difference in how primitive a reconciliation algorithm the develop can bring to bear.

- 
- 
- 

- ## 🔢 [User-defined Order in SQL | Hacker News _201803](https://news.ycombinator.com/item?id=16635440)
- My immediate thought was to store the information in a doubly-linked list type structure in SQL. Obviously the space efficiency is not optimal, but I am surprised that the article didn't even point this out.
  - The table could be designed with a unique PK, the todo item, and some binary or bool field to determine first (head) and last (tail). You would then add 'previous' and 'next' fields that would be updated for insert/delete/updates.
- This is probably decently efficient if you use recursive CTE's to traverse it, and use keyset pagination rather than limit/offset.

- why not use a linked list made of self references? For the use case of rearranging and inserting at arbitrary positions, wouldn't a linked list be ideal?
  - The table you show is not actually a linked list. Traversing a table with self references in order requires a recursive query, and doesn’t benefit from indexes for ordering.
  - There is also the issue of how many writes you do: finding a fraction between two others let’s you do just one INSERT or UPDATE (effectively the same thing in MVCC); but rewiring a linked list implies altering two rows. That may be okay but it’s not ideal.

- For most practical uses, something like the transaction described in Approach 1 should be good enough.
  - It has no limit imposed by precision, the benefit of a compact and well-supported storage format (just one BIGINT) will probably compensate for any inefficiency caused by updating several rows, and the multiple steps are not fragile at all if you trust PostgreSQL to handle trasactions properly. If you're really worried, just increment the sequence before you update a bunch of rows, not afterward.
  - But what if you have millions of users reordering billions of todo items?
  - Well, change the uniqueness constraint to (user_id, list_id, pos) or something composite like that. Only reorder items belonging to the same list owned by the same user. If a person is manually reordering items, there can't be too many items in any given list in the first place. There's no need to touch billions of other items belonging to other lists and other users.

- Simple solution: Don't use unique.
  - Yes! I'm reading through all this discussion and thinking "why are these people so bent on overthinking such a simple concept"? Also using text as the sort order solves most of the issues people are bringing up.
- Pretty much every implementation of arbitrary sort order I have seen uses varchar for this very reason, and requires none of the cleverness in the article.

- Related is modeling trees in SQL

- Why not strings? For two different strings A and B it's trivial to build one that is between them in alphabetic order.
  - That is equivalent to the "Arbitrary Precision" section under Approach 2.

- While it's vendor-specific, SQL Server has a built-in solution for it

- I must admit, I don't like the the use of floats/decimals/rationals in this way. They are unfit for sorting.
  - Floats only solve two issues: Making inserting easier while still being able to use order by. But reasoning about your data becomes a lot harder.
- They are fine for sorting! You just need to think about things differently. 
  - This option works for unlimited top-n without creating a bunch of unnecessary columns in the response.
- Would you elaborate on why you consider these types unfit for sorting? Their orderings are deterministic, and efficiency depends on the implementation of the indexes for those specific types, not inherent in the data types themselves.
  - I should have changed that language, what I meant was that they were unfit for reasoning about your data from an isolated point of view, i.e. standing with just one row. To understand an item's position using floats, you must know the entire context.

- Another approach is that users often want the newest items listed first, but occasionally want exceptions. Thus, have a "sort date" with a time portion that governs the order. The sort-date defaults to the data entry (add) date/time. The display date and sort-date may differ, if present. A sort-date doesn't work for everything, but is simple, intuitive, and effective for news- or blog-like content.

- Honestly I don't think there is a "best" solution here. Even in a "regular" programming language where you can easily use any data structure, it's not obvious which is best for maintaining the order.
  - Updating the order "value" of all the rows = moving a value around in an array (causing you to also shift a bunch of other values around).
  - Storing the ID of the row that should show up next in the list (not mentioned in the article, but mentioned in the comments below) = moving nodes around in a linked list.
  - It is a little bit trickier in a database, just because, no matter what you do, you also have to pay the price of putting something into a tree as well. Still... I can think of situations where I'd use any of these techniques. In general, this is not a problem with a clean solution for every use case.

- At Pinterest, we expanded the precision of our existing timestamp-based sequence column to accommodate reordering
  - 🌰 [How we built rearranging Pins | Pinterest Engineering Blog | Medium _201802](https://medium.com/pinterest-engineering/how-we-built-rearranging-pins-b11052e95c8b)

- I implemented something like this in a naive way. 
  - I took the modified date (previous default sort order) and stored the unix timestamp * 100 in a 64 bit indexed SortVal column. 
  - Drag-n-drop sets the SortVal +/-1 relative to the item it is being dropped against. There's only ~30 items per page so I figure it won't break except in the pathological case.
  - Curious if there is some obvious flaw with this plan or if I really need the power of true fractions.
- How do you handle situations where two items (lets call them A and B) are both moved before a third item C? Then wouldn't A and B both have a "SortVal" that's 1 less than C's SortVal? That would make your SortVals non-unique and order arbitrary.
  - Well, only if your UI allows dragging two items at once. If you reorder multiple items, well, I suppose you can resolve it by passing some relative position. If you want to squeeze something in-between reordered items, then -1 probably is not a good choice, but more like calculating some middle value between previous and next item.

- You can also use ORDPATH, which is built for tree structures but should work just as well for a flat list as it does support "in-between inserts."

- There are a lot of solutions to this problem, each with their own merits. Personally, I'd probably add a second table with FKs to the todos table PK. That allows you to remove the calls to nexval. It doesn't remove the need for a processing language, but it's a much cleaner solution, I think.

- with a graph database this would be trivial.

- 
- 
- 

- ## [How can I reorder rows in sql database - Stack Overflow](https://stackoverflow.com/questions/812630/how-can-i-reorder-rows-in-sql-database)
- As others have mentioned, it's not a good idea to depend on the physical order of the database table. Relational tables are conceptually more like unordered sets than ordered lists. Assuming a certain physical order may lead to unpredictable results.
  - Sounds like what you need is a separate column that stores the user's preferred sort order. But you'll still need to do something in your query to display the results in that order.
  - It is possible to specify the physical order of records in a database by creating a clustered index, but that is not something you'd want to do on an arbitrary user-specified basis. And it may still lead to unexpected results.

- anyone still looking for an answer to this problem, you need to use the Stern-Brocot technique.
  - For each item you need to store a numerator and denominator. Then you can also add a computed column which is the division of both. Each time you move an item inbetween 2 others, the item's numerator becomes the sum of both neighboring numerators, and the item's denominator becomes the sum of both neighboring denominators.
  - https://github.com/PieterjanDeClippel/DragDropOrderingDatabase /202111/csharp/inactive
    - How to reorder items at database level using the Stern-Brocot technique
  - Up to a certain point. If the user manages to choose the right order of reordering, he can manage to screw things up after 50 swaps. In the demo, you need to let the numbers grow as fast as possible. Thus, the reliability of this method depends on the number of items in the list...

- ## 🔢🔀 [Reorder a selected row in a table · pawelsalawa/sqlitestudio _202105](https://github.com/pawelsalawa/sqlitestudio/issues/4099)
  - Ability to order (move up and down) the selected row in a table.

- This would be against how data is stored in the database. 
  - Order is dictated by the query that you execute. 
  - If you need to modify order of query that shows you a table data, you can click on header of the column or right-click and define more complex sorting order from there.
  - Drag&drop of a row (or few rows) would have no result in the actual order in database, because - as I said above - row order is not a stored property(*), but rather property of SQL query. If such D&D would be allowed, it would give users wrong idea that rows were actually reordered and they would expect the same order after refreshing data view - which it would not be and they would come here and report bugs.
  - (*) - to be more precise, the default order IS property of stored data, but the thing is that it is insertion order and you cannot change insertion order, because - well - it is order in which you inserted data and that's it.

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
# discuss-pm-airtable
- ## 

- ## [It's time to add Databases now that Tables are fully supported - Time to overthrow Notion! - Help - Obsidian Forum _202403](https://forum.obsidian.md/t/its-time-to-add-databases-now-that-tables-are-fully-supported-time-to-overthrow-notion/78428)
- 202403: Recently, SiYuan launched this database feature which I think is the ultimate replacement for Notion. It is fully open source and also supports PDF annotation, one of the most requested features in Obsidian
- you’re talking about ~siyuan~ being very slow with 50 row tables?
- Siyuan notes are JSON, so that’s a massive drawback, in my opinion.

- the dataview/datacore effort is well thought out. Nobody else is as knowledgeable or fluent about doing sql like querying of markdown data using the Obsidian api.
- the dynamic view is developed by the Obsidian team, and Datacore by the author of the Dataview plugin.

- ## [Docmost is one of the best open source notion alternative out there : r/selfhosted _202502](https://www.reddit.com/r/selfhosted/comments/1iyfig5/docmost_is_one_of_the_best_open_source_notion/)
- No, it's absolutely not a Notion alternative. It's a good note taking app and wiki, but it has nothing of what makes Notion special. It doesn't even have databases, which is one of the major features of Notion.

- SiYuan doesn’t have a traditional “database” that is used to store data which is served to its clients. Everything is stored locally in plaintext json files with .sy extension and each SiYuan instance is basically identical in functionality and complete in itself. So the docker version isn’t some special “server” version that other instances can connect to.

- ## [What is the best Notion alternative? (really) : r/selfhosted _202410](https://www.reddit.com/r/selfhosted/comments/1g144di/what_is_the_best_notion_alternative_really/)
- Team collaboration is quite impossible in Obsidian. Yes, you can use Sync but that doesn't provide you with permission scopes.
- Take a look at the Obsidian. You need just a git server to synchronize it.

- I would recommend Affine. They are adding new features every month and in my opinion it is the platform that comes closest to Notion.
  - Free edition supporting three users and devices per workspace. Low storage limits. Upgraded plans reasonably priced.
- The license defines limitations for the hosted version, not the self hosted version. From their site: "This EE License applies only to the part of this Software that is not distributed as part of AFFiNE Community Edition."
- Affine fake open source as well
  - All content that resides under the "packages/backend/server" directory of this repository, if that directory exists, is licensed under the license defined in "packages/backend/server/LICENSE".
- Not open source, 3 members max on self host (without breaking the license).
  - This is actually just a bug they haven't gotten around to fixing. Since you're self hosted, the self hosted limits are set in your own database and you can switch it yourself. And the license for self hosting is different.

- If you like Notion database better, maybe you can try APITable?
  - But unfortunately it is a database based product. Although it has docs feature but it is a "database field" call "docs field", which means "docs" is inside the database.

- Using Huly extensively for local project management and some client work, and it's great, but it's really the best Asana alternative, rather than a full Notion competitor.

- 
- 
- 

- ## [Show HN: Linkidex – save and sort the URLs you care about | Hacker News _202210](https://news.ycombinator.com/item?id=33153866)
- I’ve been using a Notion database for exactly this problem. The only feature I can see from a quick glance that this has and Notion doesn’t is quickly exporting to browser bookmark format.

- Notion is an interesting tool because it’s so general-purpose and flexible. In the past I used different tools for bookmarks, notetaking, project organization, recipes, reading lists, etc. I got tired of everything having different UI and features and ended up moving all of that to Notion.
- I think the main features that led me to choose Notion were:
  - Fully cross-platform (web, desktop, mobile)
  - Browser extension (PC & Mobile) to quickly save pages to any database
  - Ability to create searchable databases with custom fields, tags, multiple views, and other advanced features
  - Ability to easily move an item from one database to another, for example moving an article from “Reading List” to “Saved Articles”
  - Every database entry is also a page, so an entry in “Saved Articles” can have notes or links to other similar articles
  - Very easy to share a database or page, similar to Google Drive
- Yeah full text search, saving an archived text based version of the page behind the link and local storage (export) would make it interesting for me.
# discuss
- ## 

- ## 

- ## 🚀 [Show HN: Teable – Open-Source No-Code Database Fusion of Postgres and Airtable | Hacker News _202403](https://news.ycombinator.com/item?id=39666865)
- When non-technical/semi-technical people are exposed to the database, the biggest issues come from two areas
  * their lack of grasp on data models, and modeling in general. This stumps them every time they see bridge tables, many-to-ones, and joins. Or when they need to answer a question, and the answer is not obvious from the base tables
  * databases in general are very normalized, cryptically named (tables and columns) and have too much evolutionary baggage (both from a schema and data point of view) - except for in new/small systems.

- 👷 Our team consists of 5 freelance programmers without any designers on board, and without any funding, so we had to tackle the design aspect ourselves. Initially, we planned to use a colorful gradient theme, but found the UI coordination too challenging for us. It was then that we came across the beautiful simplicity of shadcn, and decided to go with a black and white theme.

- 🆚 What are the differences to Glide's data-grid?
  - GlideGrid is an outstanding canvas grid component (interestingly, it was initially used by us before we decided to create our own version to enhance the user experience). 
  - Teable, on the other hand, is a fully-featured no-code platform aimed at empowering those without technical backgrounds to efficiently work with Postgres (a relational database).
- Grist's Pro Plan offers up to 100k rows, indicating that queries and calculations are processed on the frontend or in memory, which typically makes it challenging to scale data rows further. This is a problem that Airtable also faces.
- Baserow initially had a limit on the number of rows, but this year's updates seem to have significantly increased its data capacity. Notably, Baserow does not support Bring Your Own Database or query by SQL, but it offers a seamless scrolling table interface, unlike NocoDB, which requires pagination. In terms of other functionalities, both have their strengths. My assessment aligns with what I found on Baserow's official forum and comparisons with NocoDB.
- ✨ Teable Compared to similar products, Teable invests heavily in its table format UI, striving for seamless scrolling, copy-pasting, batch editing, and other quick table operations, which we believe are key to saving users' time. 
  - Therefore, we developed our Canvas table rendering component to achieve perfection. 
  - Meanwhile, batch operations pose a significant challenge for database compatibility, but we see this as a necessary investment.
  - Additionally, Teable supports developers by offering open database connections and database permission management, a concept inspired by Supabase. This allows both developers and users to create on the same platform.

- Can you join data from various tables and build a view? Also - my team prefers airtable because of the calendar view.... would be great to see.
  - There is currently no "join" capability, but there is a "Link Field" to handle table relationships.

- Can you build a SQL VIEW and access that from teable?
  - We have a plan to do it, we have a lot of user feedback, and we find it very useful

- ✨ In fact, Teable has no limit on the number of rows; you can always trust Postgres . Here's a table with 1 million rows, where you can experience the response speed as well as the feedback from filtering and sorting.

- 🤔🤔🤔 How do you handle schema changes like adding columns or changing the type of columns? Is the schema fixed at design time by a database admin, or can the end-user add/remove columns, create tables, and introduce relationships?
  - That is what I want to share. When users create fields in the visible table, it directly creates columns in the corresponding Postgres table. There's a mapping between the fields on the UI and the physical columns. 
  - At the same time, relationships are a major highlight; the "link field" of the Teable will create logical foreign keys or junction tables between physical tables to maintain the relationship.

- 
- 
- 
- 
- 

- ## [What is the database schema of note-taking apps such as Notion with 'database' feature? : r/Database _202405](https://www.reddit.com/r/Database/comments/1d3vdpt/what_is_the_database_schema_of_notetaking_apps/)
- actually they use postgresql JSONB to store each block.

- You can get stern looks from some for mentioning it, but have a look into EAV (Entity-Attribute-Value) tables. You flip the table on its side and use rows for columns, allowing you to have a flexible schema. Lookups and joins can be a pain, and maintenance is harder but can be overcome with some discipline. Something to have a play with and see if it suits your use case.

- A couple days old but I'll share what I do with SQLite since this shares a lot of similarities to a CMS. (I'm making a website builder w/ CMS)

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
