---
title: pm-office-notion-community
tags: [community, notion-like]
created: 2022-11-25T10:08:57.343Z
modified: 2023-11-28T14:48:45.910Z
---

# pm-office-notion-community

# guide

- resources
  - [Notion. Work](https://notion.work/)
  - [Notion 中文社区导航](https://cnotion.notion.site/Notion-e18268991cd14de89b1cad0de60baa91)
  - [NotionChina 用户手册](https://notionchina.co/)
  - https://news.ycombinator.com/threads?id=jitl
  - https://lobste.rs/~jitl/threads
# changelog-notion
- v202201
  - select text in multiple blocks 
  - https://twitter.com/jitl/status/1483918085384028163

- v202007
  - We recently made our Personal Plan free and removed the block limit
# discuss-author
- ## 

- ## [Faster CRDTs (2021) | Hacker News _202408](https://news.ycombinator.com/item?id=41372833)

- 👷🏻 jitl: Today(202408) Notion is a last-write-wins system with limited intention-preserving operations for list data (like block ordering). Text is last-write-wins, each block text or property is a last-write-wins register. We're working on a new CRDT format for block text.
- Do you use last-write-wins using the received order of operations on the server or using a logical clock?
  - No clocks on the write side

- ## 🔀 [You Might Not Need a CRDT: Document Sync in the Wild [video] | Hacker News _202403](https://news.ycombinator.com/item?id=39615987)
- 👷🏻 jitl: Maybe you don’t need it for shapes and what not, but for collaborative text documents it’s really hard to have a good experience without convergent intention preserving async merges on text - you’re gonna want OT or CRDT for collaborative text editing eventually.
  - I work on Notion, a collaborate editor that (famously?) doesn’t merge text updates. 
  - Our editor predates the popular CRDT libraries. We’ve taken the last write wins optimistic model about as far as it will go, 
  - and now we’re building CRDT text as the basis for a bunch of new features. It’s challenging to integrate with our existing model but I think the end result will be well worth it.

- ## notion: Earlier this year(2023), our infra team 3×-ed our backend database capacity (AKA “sharding”) to support Notion’s growing userbase — all without any app downtime!
- https://twitter.com/NotionHQ/status/1681364115309334530
  - [The Great Re-shard: adding Postgres capacity (again) with zero downtime](https://www.notion.so/blog/the-great-re-shard)

# discuss-stars
- ## 

- ## 🛢️ Notion uses SQLite compiled to WASM in browsers. 
- https://x.com/iavins/status/1855088684850151844
  - LocalStorage: 10MB limit, lost writes
  - IndexedDB: Performance issues, reliability bugs hard to debug
  - Notion also wrote a blog explaining how they implemented this, but it is not heavy on the details about why
  - 📝 [How we sped up Notion in the browser with WASM SQLite _202407](https://www.notion.so/blog/how-we-sped-up-notion-in-the-browser-with-wasm-sqlite)

- where does sqlite persists its data in the browser? Doesnt it have to use indexeddb/localstorsge at the end?
  - In OPFS
- is there a way to use thus without the browser prompting the user to allow file system access?
  - yes it does! It goes into very nice detail of the challenges they faced and how they implemented it

- I’ve implemented OPFS based caching using SQLite WASM and writing raw json strings and it’s like an additional super power in the browser. This is where the web is heading. It will be really interesting to see how this plays out in the coming years.
  - I’ve implemented OPFS based SQLite wasm and writing raw json strings storing upwards of 8 gigs of data in the browser. This type of caching is like an additional super power. Will be very interesting to see where this goes in the future

- ## How Notion uses Sqlite WASM.
- https://x.com/evoluhq/status/1813874658619601205
  - Evolu do that without Shared Workers which are not supported on Android.

- ## [How Notion pulled itself back from the brink of failure (2019) | Hacker News_202106](https://news.ycombinator.com/item?id=27540471)
- 

- I joined Notion two years ago, so this era predates me, but I can shed a little bit of light:
  1. The web UI used Polymer/Web Components. Simon (CTO/cofounder) described this as building on shifting sand as browsers and poly fills changed the standards and things never seemed to work well for long.
  2. There was a lot of Redis with Lua action, using Redis instances as a distributed system for some purpose I don’t understand. This never worked well.
  3. There was experimentation with graph database like Neo4J which turned out to be slow for the kinds of queries Notion needed to do. 
  - Because of all that, they completely rebuilt the product using the most boring/normal technology possible. Today we run on Postgres/Memcached for data, a Redis for rate limit and queueing, and a Typescript/React front-end

- 
- 
- 
- ## [The data model behind Notion's flexibility | Lobsters _202105](https://lobste.rs/s/y11kqf/data_model_behind_notion_s_flexibility)
- So what’s the backend database? Is it an “real” graph database (like Neo4J)?
  - We actually tried Neo4J in an early version of Notion (before my time) but it was very slow for the kinds of access Notion does.
  - We try to use very boring technology. Our source-of-truth data store is Postgres, with a Memcached cache on top. Most of our queries are “pointer chasing” - we follow a reference from one record in memory to fetch another record from the data store. To optimize recursive pointer-chasing queries, we cache the set of visited pointers in Memcached.
- If could view your data structures as trees, rather than graphs, Postgres has ltree module, I use it for taxonomies, works very well (our performance loads are not very big, so cannot comment on very large deployments experience). Some times ago, I traced inner joins operations of regular tables of JSONB fields with our taxonomy trees, and works well. Postgres looks at indices as appropriate.
- I looked at ltree a few years ago when I joined Notion. When I first saw the DB access pattern I asked, “O(n) queries for a page?!? What! This should be O(1)!”. 
  - But I believe for ltree, to move a parent node, we’d need to rewrite the path on all descendants, so we get O(1) queries for page reads, but moving a block becomes an O(n) rows updated. That kind of write amplification fanout isn’t worth the more efficient read path. 
  - I think this kind of shock is common for relational database users coming from small data apps to much bigger data apps — when your data is big enough, you also have to give up JOIN and FK constraints. It’s just not worth the database resources at a certain scale.
- Yes, makes sense. In my case taxonomy trees are static data (changed rarely), so there are no writes into them. And they are negligible in size, compared to operational data that uses them. I can see that your system uses trees or graphs for operational data, so writing performance is a key criteria.

- I assume you have many graphs, that aren’t particularly deep? From my understanding of what blocks are used for, it seems like you’d have graphs that are wider than they are deep, and … hundreds of nodes in total? A few thousand? Any idea what the average and largest number of nodes in a graph is? I am assuming there’s one graph per document?
  - It’s more like a tree descending from the root of a workspace, and a workspace can have 1000+ users in it collaborating on shared pages or working in private. But pages are just a type of block, and like other blocks, can be nested infinitely. To render a page, we crawl recursively down from the “page” block, and we stop at page boundaries, which are just other page blocks below in the tree. (There is a cursor system for doing this incrementally and prioritizing the blocks at the “beginning” of a page that the user needs to see first.).
  - So, spaces are quite a broad and deep graph, but the scope is about what you estimate for an individual page. I don’t have estimate numbers on hand for depth or block count within a space.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

- ## 📈🛢️ [The data model behind Notion's flexibility_202105](https://news.ycombinator.com/item?id=27200177)

- I think it makes us unique among the popular editors of today, but we're very aware that the block model isn't original. Execution matters much more than innovation.
  - Pretty sure Athens & Workflowy (both YC companies) use blocks.

- Not sure how "unique" this model is; for example Claris Works was built out of an even more powerful block model (they called them frames) back in the late 1980s

- Notion clicked for me when I realised that everything is a "page with some attributes". Blocks are interesting at the engineering level, but as a user I found I was normally thinking at the level of pages.
  - Each page is some content (optional) with a set of arbitrary attributes of different types, e.g. date, string, number etc. 
  - When you create a table and populate it, you are creating a set of pages all of whom have the same attributes and the table is just a view of those pages. 
  - You can then create a calendar that's a different way of presenting those same pages
  - It's a really simple data model, and it's pretty flexible. We built all our processes on Notion initially and then moved them off when they got to an appropriate scale. 
- The design decision to feel "default-text" is awesome - text is a great foundation for a "custom workspace" product. But, it's only when the bulk of content is in Tables that things get extremely powerful.
  - Once Notion has in-line text references, ala Coda, the sky is really the limit. I think Notion nailed the UX and speed/performance.
  - Even if it's slow compared to Apple Notes, it's lightning fast compared to Coda, where "Documents" are extremely heavy, and relatively isolated.
  - Notion has a clean route towards eating Coda's most powerful functionality ([an incredible charting and formula](https://coda.io/formulas))
  - Coda, on the other hand, started from an "easier application builder" approach, like Retool for Excel experts

- 🎮 At http://story.ai the editor makes use of an ECS (Shipyard Crate in WASM). The flexibility it affords us has been super powerful particularly in support of constructs that are close to a programming language (values in and out of scope, suggestions and autocompletions, determining whether a "skill" is fully formed for publishing etc)
  - 👷🏻 jitl: In a previous iteration of Notion used a kind of model kinda like ECS, where each block was represented by multiple records called "reference" and "composite", so a block could have different type depending on context. From an internal doc on history: > We later decided this wasn't useful or necessary and collapsed them into one thing. WTF was I thinking??

- I'm actually building a Confluence/Notion competitor, and it is document based. Being block-based makes a lot of things much more complex

- 🌰 Salesforce and JIRA both did something similar: their underlying database schema is very generic, basically keys and values, allowing arbitrary logical schemas to be defined at runtime. 
  - Yet in both cases, they ended up not really taking advantage of this flexibility. 
  - The logical schema of both systems is a very ordinary relational schema that could have been implemented directly on the database, with much better performance. 
  - I wonder if the Notion developers made a serious attempt to build on top of a more conventional structured schema, and found it really was unworkable?
- 👷🏻 jitl: I actually think Notion's data model is much more conventional than the data stores behind document editors like Google Docs or Figma. Blocks are "just" rows in Postgres.
  - We **use JSON for properties for flexibility and for user-defined property schemas**.
  - We could use an `entity-attribute-value` table as you describe for that, but such a table would complicate our caching techniques. It would also be enormous, but, it might be time for another think about that since we finished sharding.
- I was thinking more along the lines of, specific tables for different classes of entity, with a schema that’s as fixed as possible, so you get the most compact and indexable representation.
- I'm curious if Notion has any plans to make the "type" property user-extensible. Given the current data-structure, which decouples the block data from the way its rendered through the type property, a user has to define only one template for rendering arrangements of UI components (boxes, bullets, etc), titles and children. 
  - This sounds a bit like customized structured data types with style inheritance, à la DITA.
- How do you store, query, and search across documents?
  - Our source-of-truth data store is Postgres, with a Memcached cache on top.
  - Most of our queries are "pointer chasing" - we follow a reference from one record in memory to fetch another record from the data store. To optimize recursive pointer-chasing queries, we cache the set of visited pointers in Memcached.
  - We use Elasticsearch for search features like QuickFind.

- Been working with multiple document API's recently for my start-up. It's been a real challenge to understand how different document stores compare -- 
  - **Confluence uses undocumented XML markup** that "mostly" mirrors HTML, Google Docs gives you sometimes semantically-incorrect HTML with lots of inline styles, Slack has its own funny Markdown, etc. Then there's Notion blocks. 
  - I had to write my own HTML-to-Notion block parser, but I think I prefer working with it over everything else because structured data is just easier. 
  - One interesting gotcha: if you want to completely overwrite a page you currently have to remove every content block one at a time, and then add each new line one at a time. This is using their undocumented API, but the new API doesn't even offer deleting content yet. I'm eager to switch over but it may be a while...

- As author of a Notion browser extension, "everything is block" concept made it significantly easy to understand the notion doc structure and tweak the UI to add multiple customisations on top of it. For instance showing a fixed static ToC, etc.

- I think the power of Notion became apparent to me when I created a Page, accidentally changed it to some other type, then ctrl+z-ed it back to a Page, with all its contents intact. Seriously impressive. I wish search wasn't so crap though.

- when a user requests a page which will have a full hierarchy of blocks, how are the db queries done.
  - It appears that Notion uses Postgres, which supports the recursive/hierarchical queries that are part of standard SQL. While I don't know for sure that Notion uses this, it seems likely.

- Really interessing. This seem to be a really good use case for a NoSQL database. Am I wrong ?
  - PostgreSQL has Ltree
  - 👉🏻 **Ltree is interesting, but if I understand correctly, to move a parent block, I'd also need to update the path column in all the child blocks** -- at our scale such write amplification is a non-starter.
- Yes, you're wrong. You're wrong because you need to JOIN a massive tree of blocks, to form the graph the author is referring to. You can break out the "block" model into several tables and represent it in a relational database that way.
  - NoSQL = NO JOIN?
  - Hope that helps.
- I don’t actually see a graph represented anywhere in the article; the author references wanting a graph at the start, but the only thing I’m seeing described are trees of nested blocks. Even the properties list seems to be a grab-bag of KV pairs that gets permanently attached to a block once initialized, to support roundtripping.
  - Which is pretty much the ideal scenario for a document store. 
  - The article describes Notion as being very strictly hierarchal
- A block has many properties. A property has a name, and a value.
  - The underlying persisted data doesn't necessarily have to be a bag of KV pairs.
  - A block is related to its parent and descendant blocks.
  - These relations are suitably represented in a relational database, not a document store.
  - EDIT: In graph theory, a tree is an undirected, connected and acyclic graph.
- A document store is basically optimized for specifically hierarchal data situations — a tree. The data structure you’re describing, and what the article describes, is precisely that: a tree.
  - A database can encode a tree just fine, but that doesn’t mean it’s the best tool to do so.
  - There are other properties to a document store I don’t care for, and I don’t like them in general (like the implicit schema, and total lack of data consistency validation by the data store, and the fact that you often don’t truly have a tree), but representing a tree is what’s been described, and it’s exactly what they’re specialized for.

- jitl: We don't use JOIN for the content tree; I don't think I've seen one in any of our queries.
  - We don't use an ORM. Notion's codebase on the back-end is much more functional than object-oriented, in the sense that we have many more code that looks like `transformTheData(theData, theChangeToMake): ResultingData` than we have classes or methods.
  - We do lean very heavily on the TypeScript type system and try to make invalid states unrepresentable.

- 🆚️ Am I the only one who thinks the data model is very complex? How does it compare to a document based data model? What are the pros and cons of each?
- The **major issue with the document model is storage**. 
  - How big can a document grow? How do you persist it, and make small changes inside it? How do you handle "hot" documents that are very popular? 
  - Moving data between documents or having part of a document reference part of another document are complex. Complexity comes from building derived data that looks at slices of a document.
  - With a block-oriented model, your records are much more manageably sized. It's easier to reference or move data between documents, but in turn, you need to do these kinds of recursive shenanigans because your individual records are smaller in scope. Complexity comes from derived data that composes blocks together into a document.

- 🆚️ Is there a reason why you did not use rdf for representation and some rdf aware encoding like jsonld for serialization? Would be significantly easier for others to work with, could easily query it with SPARQL.
  - jitl: An **early version of Notion (before my time) used Neo4j, but it turned out to be very slow** for the kinds of data access Notion does.
- You don't have to use neo4j or any graph database to use RDF. It is just your current model seems very graph based and actually not that difficult to map to RDF, it would likely be possible to do with a jsonld context, and if you provided such a context then it would make your data a lot easier for others to consume.

- I have a requirement to allow users to create adhoc tables within a web application. I was wohoe beat to represent this on database. Any thoughts?
  - Tables (ad-hoc ones) are a beast. Code that aspires to do tame them, looks simple at first then evolve into crazy monsters that die at the altar of excel.

- A graph is so natural for pages, web pages are graphs too. So they choose a well fitting model for the problem, congrats

- ## ✨🔥🔥 [Notion – All-in-one workspace for notes, tasks, wikis, and databases | Hacker News_201901](https://news.ycombinator.com/item?id=18904648)
- 
- 
- 

# discuss
- ## 

- ## 

- ##  If we have 5 employees in the agency, and for example we want two to see all the data in Notion, and the others to have access only to tasks and projects, what is the safest way to do it?
- https://x.com/typeoneerror/status/1834260004414644558

- ## Notion and Slack have so many rough edges in terms of UX.
- https://twitter.com/tantaman/status/1764647109897154815
  - Code blocks that become inescapable
  - Inconsistent shift+enter behavior
  - Lists responding to delete incorrectly when things like mentions are in them
  - vs Obsidian & Discord where everything works as expected.

- ## Databases are available! 这对Atlassian来说是个大动作啊。这是向Notion宣战吗？ _202402
- https://twitter.com/PenngXiao/status/1753369373253996757
- 事实证明这功能很重要，很多时候人们被迫使用 Excel 就是因为少个轻量的 database
- 但是事实上，我们team的table才是notion没有的功能哈哈，因为我们可以merge cells，而且database这个是收购来的，之前是个插件，所以加油啊
  - 而且从内容上来说，现在我们完全可以实现table和database两个不同维度的table，table更偏向于展示而database更偏向于数据和简单计算，我们两个team各自都用同样的核心库来实现，目前应该是我们进度一致。上个半年发了两个feature分别是resizable table和drag and drop。
- 被迫宣战, 否则confluence就完了

- ## The more I think about notebooks & Notion, the more I think that their blocks should be embedded into places like Discord, Slack, instant messengers, etc.
- https://twitter.com/JungleSilicon/status/1748547626818302113
  - Interactive knowledge-bases through conversation that can be promoted into more formal structure.
- I have talked about this before -- but it would be so awesome if their blocks were embeddable in tldraw! unfortunately that doesn't seem to be in their plans at all, unlike @MicrosoftLoop which does go in that direction (kinda, locked into microsoft universe)
  - I can see why they wouldn’t. I can imagine a messenger app built from the ground up for this kind of workflow too.

- read-only embeddable, or read + write?
  - I feel like a message history is inherently an append only log - it makes the medium a bit messy for interactive elements like charts, etc. not sure.

- ## [People who use Notion to plan their whole lives | Hacker News_202304](https://news.ycombinator.com/item?id=35698521)
- I went from Zim to Dokuwiki to Bookstack (where I've been for the past 3 years). The former is an offline app and the latter two are self hosted. All three are FOSS.
  - Edit: after reading some other comments, one thing I really appreciate about Bookstack is that its opinionated and batteries included -> no falling into the "waste all your time customizing and perfecting your workflow" trap.

- https://news.ycombinator.com/item?id=35705195
- (I work for Notion). Notion is also "basically just a bunch of lists", plus titles. Pages in Notion are a title, and a list of blocks. Text blocks are a title (the text of the block) and a list, it's indented children.
  - Semantically our data model is an infinitely nested hierarchical tree of lists, although the UI might not look or feel like "just a list".
  - Our editor is more like an "outliner" than a traditional word processor, and before January 2022, you could't even select text across multiple blocks. We rebuilt the editor to work like both an outliner and a traditional word processor at the same time. You can still "feel" the tree/list structure when you select and drag multiple blocks around, or use indent/dedent - you can't indent a block multiple times within another block because that doesn't make sense in the tree structure.

- I just don't like recreating a kanban board in Notion, it just seems too complex and cluttered, I don't care about all the other stuff, I love trello for how simple it is, but I keep finding different ways to use it, the simplicity is the key as it allows me just to dump what I want into it and use it however I wish, Notion is just overwhelming for me.

- ## 倍速重听了 21 年这期访谈 Logseq 的播客。 
- https://twitter.com/mr_easonyang/status/1642902992683950080
  - 两年过后，当时聊到的「移动版本」、「付费方案」和「同步和加密」等计划都实现了，团队执行力还是很强的。 
  - 虽然现在实时协作方向似乎暂停了，但我不觉得这是件坏事，CRDT 这东西想做得完美成本不低。 
  - 友情提示，录音质量有些差。

- ## support SELECT TEXT ACROSS MULTIPLE BLOCKS!_202201
- https://twitter.com/NotionHQ/status/1483884489235255297
  - https://twitter.com/jitl/status/1483918085384028163
- This is what I've been building since June 2021. It took ~100+ pull requests with 26247 added lines, 11078 removed lines. 
  - It might seem like a small thing - to let you select text in multiple blocks at once - but we had to upgrade nearly every one of Notion's features to understand the new selection model.

- ## Notion will not have #offline mode.
- https://twitter.com/ianberdin/status/1592848167632244736
  - @NotionHQ has Postgres based backend with deep tree structure. 
  - There are no available technologies to sync such structure with a relational database. 
  - And yes, Notion can not rewrite their logic using OT, CRDT. It won't work.

- ## no user wants to fiddle with a merge UI or picking versions like with iCloud.
- https://news.ycombinator.com/item?id=28717848
  - For prose text, what do you think about combining a document-scale CRDT, with fine-grained locking — e.g. splitting the document into a "list of lines/sentences", where lines have identity, and then only allowing one person to be modifying a given line at a time?
- I almost thought Notion would be a good example of this, but apparently not — they actually do allow multiple users to be editing the same leaf-node content block at the same time, and so have taken on the full scope of the CRDT problem.

- ## 💡 Notion’s selection and undo/redo with multiplayer are pretty potato._202209
- https://news.ycombinator.com/item?id=32991105
  - Notion stores selection as grapheme indexes in a text property, so while it won’t lose selection if someone adds/removed characters from a text, your selection won’t make as much sense as one in Google Docs. 
  - 🔀 Likewise with undo/redo or regular typing into the same field - it’s all last-write-wins updates.
- On the other hand, Notion’s editor does a much better job with CJK input, Android, etc compared to Slate. Slate has a beautiful API design but its implementation suffers outside of ideal conditions.
- ProseMirror did the best the last time I tested these libraries. TipTap (a competitor of yours?) provides an API layer on top, which I haven’t spent much time investigating. For my purpose I don’t want intermediary abstractions - but might be useful for your context depending on how much you want to specialize in rich text.

- ## 🔀 [Peritext: A CRDT for Rich-Text Collaboration_202111](https://www.inkandswitch.com/peritext/)
- Notion allows users to edit their notes offline, but if two users concurrently edit the same paragraph (called “block” in Notion), then only one of those edits is preserved, and the other is discarded. The Peritext algorithm would allow them to merge those edits instead.

- ## So much CRDT literature seems to focus on collaborative text, but it feels like a pretty niche(针对特定小群体的) problem to me._202210
- https://twitter.com/gaforres/status/1584909330859671553
  - Block editors like Notion are good enough for most cases. 
  - Editing the same sentence or even paragraph as someone else doesn't really seem like a common user need.
  - But I guess if you're aiming to build perfectly general abstractions you're forced to target the hardest niche case. In my experience making systems, trying to universalize to that extent can become the enemy of progress and usability.
- Collab text feels like a product black hole. If you did it perfectly, the UX would still be bad. It has no tactility(有触觉的；能触知的). People don't co-work that closely in real life. It would be rude. IMO the value of collaboration is a sense of togetherness, but with personal space.
- After having worked on manuscripts with 4+ participants for 6 years or so, I have come to think exactly this. I don't know how we've managed to come to this point; it's like a dance where we all have to step on each others' toes to participate.
  - On the other hand, it does relieve the team of the burden of appointing a merge gatekeeper of changes. In which case, simultaneous editing helps.
- I would assume that when writing async, the merging and keeping the history is more important to not cause any unexpected overwrites when you have been writing offline for some time and sync your changes back
  - I suspected there might be a blind spot in my reasoning while writing those tweets, and this very well may be it! Offline-first text could totally be difficult at block level.
  - Still feels like it would be very difficult to solve with a generalized system, though. Like the final paragraph would diverge inline as changes come in with no respect for meaning. Manual merge at the block level might still be a better UX.
- Is there a tool/library that can handle ordered trees out of the box that you know of? Thx
  - Depends on how you want to query it... The framework I'm building uses schema based data which doesn't handle recursive nesting, but could represent a graph by ID references and query each level iteratively. Not ideal. Classics like YJS probably better. Check GUN too.
- collaborative text is good because its a list type that people are already familiar with! turns out we can build arbitrary JSON out of lists (like what Automerge and Yjs have done) which allow you to synchronize state of entire applications

- ## 🔀 Muse using last-write-wins for merging text blocks._202205
- https://twitter.com/gordonbrander/status/1524885567686660096
  - “Notably, [Figma, @actualbudget ] independently arrived at this notion of having a bunch of last-write-wins registers as the CRDTs. 
  - So these are very small, simple, almost degenerate(退化的；简并的) CRDTs”
- It’s interesting how important this choice is for UX. Eg: big difference between Notion (LWW at block level) and Google Docs (whole doc merges text edits). I find Notion irritating for certain kinds of parallel editing, like taking notes together in a meeting

- ## for notion staff_202207
- https://twitter.com/jitl/status/1550140132891791360
- March 2019:
  - total engineering team of 4
  - React Native to render a webview
- July 2022:
  - total engineering team of ~100
  - 3 iOS eng, 4 android eng
  - SwiftUI/Jetpack Compose renders home tab
  - Everything else is still a webview
- Web is the slowest option but the most cross platform. Native is the fastest option but the least cross platform. RN + react-native-web somewhere in the middle. Chose the right tradeoffs for your team, your users, your project, your market. 

- ## Someone DM'd me to ask what tech we use in the Notion iOS/Android apps._202205
- https://twitter.com/jitl/status/1530326516013342723
  - They're hybrid native apps – idiomatic Kotlin/Swift + a webview running our web app.
  - We used React Native back in the day, but removed it by early 2020.
  - SQLite.
- Our strategy is to progressively nativeify more parts of our app as we grow the team.
  - 👉🏻 However, the editor will probably remain a webview for the foreseeable future, because of complexity tradeoff. 
  - Google Docs, Quip, Dropbox Paper, Coda - all use native shell, webview editor.

- It’s not so much SQLite that makes the desktop app fast — it’s more that the network makes web apps slow…
  - Just as a rough estimate, it takes about 15ms for light to travel from west coast to the east coast…
- It(react-native) added a ton of overhead to the app while providing no value in our hybrid app architecture. It made sense for bootstrapping when we had <5 engineers. 
- The editor has always been web on every platform. React Native drew two screens: (1) the webview, (2) the share sheet, shown when you share to Notion from a browser.
  - The advantage of React Native is allowing web developers to build phone app. If we already have webview for that, React Native does not add value.
- iOS & Android engineers chose Compose / SwiftUI for this and regretted it because not enough control over optimization. Yet another lesson to be conservative about tech adoption.

- ## 🆚️💡 [Choosing DB model for an app similar to Notion, Block-based ("paragraphs") or document-based?](https://stackoverflow.com/questions/71024175)
- 比较项目
  - Fetch the contents of a page
  - Render the content of a page**
  - Update the content of a paragraph in the DB
  - Alternatives for rendering very large documents *
  - Import or paste content
  - Copy content**
  - Real-Time Collaboration
- Our conclusions
  - The problem with those tests is that it is difficult to draw an accurate conclusion about the goodness of both models. Obsidian uses documents locally, so you don't have to sync notes. Roam Research is a very new and poorly optimized app. Standard Notes encrypts notes locally. In other words, it's not always apples to apples.
  - So, we tried to push our doubt as far as we could, but we are still not sure of the answer Which of the two models do you think would offer better performance for our app and why?

- ## [Anyone now what database architecture is Notion using?](https://www.reddit.com/r/Notion/comments/lxhxwi/anyone_now_what_database_architecture_is_notion/)
- We use Postgres. 
- [I'm the first engineering hire at Notion. AMA!](https://www.reddit.com/r/Notion/comments/fi45dc/im_the_first_engineering_hire_at_notion_ama/)

- ## [⚖️ The Block Protocol _202201](https://news.ycombinator.com/item?id=30105510)
- I work on Notion. I think the challenging part of this project will be building intuitive and collaborative interfaces on top of the bare-bones data model. 
- The challenge comes with two parts: 
  - (1) allowing blocks to compose, so I can nest a "task block" inside a "paragraph block", 
  - and (2) figuring out the collaboration model so multiple users can manipulate blocks at the same time, eg by typing characters. 
  - Both of these aspects are un(der)specified in the Block Protocol spec.
- For an example of a challenge building composable blocks, consider the suggested architecture - the project imagines different block types implemented as sandboxed iframes, orchestrated by some editor that stitches them together into a document or dashboard. This would make certain interactions difficult/impossible to implement in the browser. For example, you can't start a text selection in one iframe, and end the text selection in the next iframe. This means that each layer will need to implement many of the standard blocks, just to provide tools that operate on the contents of more than one block at a time.
- I'm left wondering if there will ever be "block protocol native" apps, or if this will be more of an interoperability/import/export format between otherwise monolithic platforms that have their own much richer internal data format.

- ## [A Graph-Based Firebase | Hacker News_202208](https://news.ycombinator.com/item?id=32595895)
- I have built my own similar reactive in-memory triple store with typescripts type safety, but then I realized I still need transactions which are a bit of a pain, because transactions are bundling the otherwise separete triplets, so the atomic, independent logic of triplets and related effects breaks a bit. (I am sure it's solvable.)
  - The example code uses a `transact` function. But it really depends on what you mean by “transaction”. 
  - 👉🏻 We don’t use a triple store at Notion, but we do use an abstraction that ensures a collection of operations either all succeed or all fail. 
  - We don’t support “interactive” transaction, where you can read, modify, write as an atomic group. 
  - This just isn’t desirable in a multiplayer or offline system - in cases we need that kind of consistency we use a normal HTTP API which is online-only.

# discuss-roam-like
- ## 

- ## 

- ## Travel back to any previous version of your Roam with Graph History to access previous states of your notes or recover accidentally deleted data
- https://x.com/RoamResearch/status/1841715046767890511
  - Settings➡️ Graph➡️ Graph History: pick date+time➡️ Go!

- Datomic ftw
# discuss-notion-like
- ## 

- ## 

- ## 

- ## What @NotionHQ feature should we un-ship? _202410
- https://x.com/akothari/status/1843512114612449483
- The AI suggest feature that activates when pressing tab is annoying. It gets in the way of writing
- Everything “AI”

- Mandatory name column in tables
  - Or at least allow us to switch it / combine it with the Auto ID column type Often, I want the page name to be the Auto ID, like in a database of RFCs

- 

- ## ✨ Anything goes edition: What Notion feature SHOULD we ship? _202410
- https://x.com/NotionHQ/status/1844099360671531383
- 

- ## 📈 [Show HN: Eidos – Offline alternative to Notion | Hacker News _202406](https://news.ycombinator.com/item?id=40746773)

- A key idea of Eidos is to make each table a real SQLite table, so users can view and modify it through other software or visualize it with tools like Metabase

- I feel like the sqlite-based thing is, if anything, kind of a downside. Use it for caching and calculation, sure, but I want the source of truth to be just plain markdown files I can take into other apps in 5 years when whatever I'm using now inevitably dies.
  - I think plain text has its limitations. There are many other types of structured data in life. Just like Word and Excel, they have different responsibilities. No one worries that Excel will not work in a few decades because it's just an offline software. Similarly, no one worries that SQLite will be unable to open or view because it has already been running with billions of instances, becoming part of the infrastructure.

- My general answer to this is to make sure whatever thing I'm building understands Pg COPY TSV syntax - specified by https://www.postgresql.org/docs/current/sql-copy.html under 'text format' - and export to/import from that. It's nice to have something that plays nicely with awk/cut/diff/etc. and can be committed into a git (or elsevcs) repo. (I'm not specifically wed to COPY as the form, but given it's well known and documented I've found it a good default)

- What logseq is going to do is just dump documents to markdown (right now they use markdown), I think something along these lines is the way to go, store in sqlite and have a constant background process creating markdown files for everything
- good idea. all documents are currently stored in the eidos__docs table. The `content` field is used to store the state of lexical documents in JSON format. Additionally, there is also a `markdown` field. This can be viewed by any sqlite software. Every time a document is updated, both fields are updated simultaneously, making it easy to convert to a file.

- SQLite won't stop working but your format is proprietary. A markdown can be understood even without rendering to HTML but your tables are useless for an user without your app.
  - This is why I use RTF. It is considerably more flexible than Markdown (which can't do basic stuff like making text red), but not a proprietary format. The application I use (DEVONthink) supports a number of formats including Markdown, HTML and RTF, and documents how to get at the raw files if the application ever becomes unavailable. No use of a proprietary database format. This is for my 30-year files.
  - I also use RTFD in the same application. This is a variant of RTF which can have embedded images. It's not universally supported like RTF, but there are sufficient third-party editors to leave me confident that I will be able to get at the information. This is for my 5-year files.

- I have tried quite many such apps and keep returning to Tiddlywiki (https://tiddlywiki.com/). It is not perfect, and the lack of hierarchy can be both a blessing and a curse. It uses flat-files which can impact performance and be more cumbersome than a database. Also, the integration with external files is a bit clumsy.
  - However, the main strength is customizability. Various data is best presented in various ways, and separating data/content and presentation/template/layout while keeping them tightly integrated is incredibly powerful.

- You can make some adjustments in the settings to store data in a local folder. Then, use iCloud, Git, or your preferred service to back up your data. Just like the web version of VSCode, it can handle local files. The web is just an app and doesn't hold any data.

- How do you deal with iOS deleting PWA data when unused? I'm building an app that relies on indexedDB, which afaik is the only persistent storage a PWA can access.
  - Currently, it can only run on high-version chromium-based browsers, and it's compatible with Android, but not iOS. Apple is killing web apps.

- The lack of note linking is a deal breaker for me. Also when it comes to LLM stuff, I would like to hook up AI's via a OpenAI Compatible LLM such as LiteLLM and Ollama
  - I'm not a fan of 2-way links, but this is on the roadmap and can be easily added . It can work with Ollama.

- Eidos has an Airtable-like table, but Obsidian does not. 
  - Eidos and Obsidian are both file-based. 
  - Eidos is based on SQLite, and Obsidian is based on Markdown.

- Please provide a feature to load data from notion export
  - I developed an extension to implement the import function, it's still in development and lacking documentation. 

- Apple Notes has sync issues with large collections, and backing up to anything except iCloud is a pain.

- ## [decipad: Show HN: A Notion-like platform for building interactive models | Hacker News _202307](https://news.ycombinator.com/item?id=36940514)
- Not sure if this was the feedback you were looking for but I spent about a year in a similar field trying to build out a product before we successfully pivoted. The product was very similar to grid.is
  - Ours was really tough sell as a product because it wasn't really a product. It was kind of a no code platform that worked with excel models. 
  - It was technically very capable and cool, converting excel logic to run in browser but no one really cares about the tech, but what are you supposed to do with it.
  - And you can use it for a lot of things, like someone can embed it into an existing website to serve as a calculator (eg. Mortgage calculator), you can run Monte Carlo on workbooks easier or a solver
  - 💡 But it wasn't a product. Every one of those problems (are they problems?) Could have been solved in a better way
  - No code space is also very competitive and we knew we couldn't keep up with the high bar of generalized no code platforms and the sell wasn't big enough. It was classic solution looking for a problem

- ## [Notion.clone: open-source notes editor like in Notion | Hacker News_202011](https://news.ycombinator.com/item?id=25063122)
- A library that does half of the stuff that notion does and manages to create some sort of consistent markdown output would be amazing. This is amazing work and I think the main thing I see missing is navigation.
  - I couldn’t agree more with this. It would be nice to have an open source text editor with markdown shortcuts and auto-formatting. Bear.app, Typora and outline’s rich text formatter are close but the first two are closed and the latter I find clunky and hard to build on top of. I am excited to see this clone and where it goes

- One of the really great parts of Notion is that you can view your data in multiple ways (table, schedule, timeline view, etc.); 
  - You can configure views, filtering, sorting, summary’s, and foreign keys with roll ups....

- Does it work offline?
  - No, not yet - but that what be interesting to add!

- ## [Big fan of notion. Not a fan of the data lock-in or haphazard security. | Hacker News](https://news.ycombinator.com/item?id=27145970)
- I think Roam has been fully collaborative since the launch. The browser keeps the whole database in IndexedDB and syncs it continuously with a WebSocket streaming Datomic-style transactions.
  - Roam uses Datomic under the hood

- ## [The Fall of Roam | Hacker News_202202](https://news.ycombinator.com/item?id=30320977)
- This is not the fall of Roam. It is just the usual cycle of note taking apps. 
  - There was Evernote before, and there was probably even others before. 
  - And the current trending app is Notion, which will fall at one point too.
  - The particularity of Roam, is that it was designed for developers, product managers and execs in the tech industry. So its market is pretty small

- ## [为什么现在流行的笔记软件喜欢用clojure来编写？ - 知乎](https://www.zhihu.com/question/469287561)
- Roam Research 用了 Clojure

- ## [Logseq 为什么用 clojure 写? - 知乎](https://www.zhihu.com/question/610034256)
- 作者的高度决定了项目语言的选择。工程师选clojure没毛病

# discuss-news-linear
- ## 

- ## 

- ## 

- ## New: Parent & sub-issue automations _202409
- https://x.com/linear/status/1832093481088815493
  - parent issue auto close

- ## Introducing the next evolution of projects in Linear. Close the gap between planning and building. _202405
- https://twitter.com/linear/status/1786059513235177480
- New in Linear Projects:
  › New Project Overview page
  › Collaborative, rich-text project descriptions
  › Milestones with descriptions
  › Turn text into issues and documents
  › Attached views

# discuss-news-notion
- ## 

- ## Take collaboration up a notch with new suggested edits _202407
- https://x.com/NotionHQ/status/1807819016729460894
  - Switch to suggestion mode to effortlessly co-create and refine content with your team.  

- ## Introducing Notion Sites—the easiest way to make a website _202406
- https://x.com/NotionHQ/status/1805619535330132425
- Its $10 per month for plus plan and $10 per month for supporting one custom domain as an add on. So basically $20 per month for having custom domain on notion. charging monthly price for custom domain feels like charging per sms.

- ## Notion 2.39: Getting back to the basics _202405
- https://twitter.com/NotionHQ/status/1786157773673415061
  - Many of you love Notion because of our rich feature set. But we've also heard your feedback. So, we did a little spring cleaning and tidied up the most used parts of the product

- ## A story in 2 parts: Crop image, Mask image _202403
- https://twitter.com/NotionHQ/status/1773739884077105516
  - 用了一张经典搞笑图

- ## Acquired by Notion _202402
- https://twitter.com/FrancescoD_Ales/status/1757067738084717054
  - skiff-email, calendar-cal, Automate.io

- ## ✨ Say hello to buttons in databases _202402
- https://twitter.com/NotionHQ/status/1752728459913400702
- Automate common workflows like:
  • approving proposals
  • upvoting ideas
  • escalating issues
- I love buttons. But what I love more is forms. Create a way to build a form that populates a database and you might just go next level.
- The only missing feature now is: connect Notion to external databases (read and write).
# discuss-like-eidos
- ## 

- ## 代理模式太好用了，深刻理解了依赖抽象而不是实现。
- https://x.com/mayneyao/status/1822712428133785875
  - 最开始把服务端代码搬到 web worker 实现，client-server 一体放在 web 中，实现了离线可用。
  - 现在把 web worker 的代码复用，port 到边缘环境（Cloudflare worker/ Deno deploy ）公网可访问，实现发布服务，只需要少量的适配就行了。 设计模式真伟大

# discuss-showcase
- ## 

- ## 

- ## 

- ## 

- ## New Notion AI template! I've built an open-source editor using @vercel AI SDK + Liveblocks, Lexical, and Next.js.
- https://x.com/ctnicholasdev/status/1836783322103763011
  - [Liveblocks Notion-like AI Editor – Vercel](https://vercel.com/templates/next.js/liveblocks-notion-like-ai-editor)
  - you can select text and ask AI to simplify, add detail, translate, change style. 
  - You can also chat to AI and ask it to generate a new document.
  - It generates markdown, and allows you to create a new @liveblocks text editor document from it, which is powering the collaboration.

- ## 🌰 I've created a new, simple Personal Notion Dashboard using the GTD method (Get Things Done).
- https://x.com/soltwagner/status/1792404905384382933
  - Hey everyone, you can download the GTD Notion template for free here
  - [Notion Get Things Done (GTD) Dashboard for Free by Solt Wagner](https://www.solt.ws/template/notion-get-things-done-dashboard)

- ## [Notion API – public beta | Hacker News_202105](https://news.ycombinator.com/item?id=27144566)
- 
- 
- 

- ## @jkosoy ’s first month as a new Notion employee (AKA Newtino), in his own kanban
- https://twitter.com/NotionHQ/status/1697660535704322514
  - 页面渲染多个分类，效果类似看板
- How does Notion at Notion deal with unbearable database speeds once you have too many relations  and rollups? Notion is a dream of a software and one of the most important in my life, but the performance is just so annoying
  - I just had a conversation with our infra team about it yesterday. It can be a little annoying, but rest assured they are thinking about this *all the time*. 
