---
title: pm-office-notion-community
tags: [community, notion]
created: 2022-11-25T10:08:57.343Z
modified: 2023-03-29T17:23:37.126Z
---

# pm-office-notion-community

# guide

- notion社区-中文
  - [Notion. Work](https://notion.work/)
  - [Notion 中文社区导航](https://cnotion.notion.site/Notion-e18268991cd14de89b1cad0de60baa91)
  - [NotionChina 用户手册](https://notionchina.co/)
# changelog
- We recently made our Personal Plan free and removed the block limit!_202007
# discuss-author
- ## 

- ## 

- ## notion: Earlier this year(2023), our infra team 3×-ed our backend database capacity (AKA “sharding”) to support Notion’s growing userbase — all without any app downtime!
- https://twitter.com/NotionHQ/status/1681364115309334530
  - [The Great Re-shard: adding Postgres capacity (again) with zero downtime](https://www.notion.so/blog/the-great-re-shard)

# discuss-stars
- ## 

- ## 

- ## [How Notion pulled itself back from the brink of failure (2019) | Hacker News_202106](https://news.ycombinator.com/item?id=27540471)
- 
- 

- I joined Notion two years ago, so this era predates me, but I can shed a little bit of light:
  1. The web UI used Polymer/Web Components. Simon (CTO/cofounder) described this as building on shifting sand as browsers and poly fills changed the standards and things never seemed to work well for long.
  2. There was a lot of Redis with Lua action, using Redis instances as a distributed system for some purpose I don’t understand. This never worked well.
  3. There was experimentation with graph database like Neo4J which turned out to be slow for the kinds of queries Notion needed to do. 
  - Because of all that, they completely rebuilt the product using the most boring/normal technology possible. Today we run on Postgres/Memcached for data, a Redis for rate limit and queueing, and a Typescript/React front-end

- 
- 

- ## 💡 [The data model behind Notion's flexibility_202105](https://news.ycombinator.com/item?id=27200177)

- I think it makes us unique among the popular editors of today, but we're very aware that the block model isn't original. Execution matters much more than innovation.

- Not sure how "unique" this model is; for example Claris Works was built out of an even more powerful block model (they called them frames) back in the late 1980s

- Notion clicked for me when I realised that everything is a "page with some attributes". Blocks are interesting at the engineering level, but as a user I found I was normally thinking at the level of pages.
- The design decision to feel "default-text" is awesome - text is a great foundation for a "custom workspace" product. But, it's only when the bulk of content is in Tables that things get extremely powerful.
  - Once Notion has in-line text references, ala Coda, the sky is really the limit. I think Notion nailed the UX and speed / performance.
  - Even if it's slow compared to Apple Notes, it's lightning fast compared to Coda, where "Documents" are extremely heavy, and relatively isolated.
  - Notion has a clean route towards eating Coda's most powerful functionality ([an incredible charting and formula](https://coda.io/formulas))

- I'm actually building a Confluence/Notion competitor, and it is document based. Being block-based makes a lot of things much more complex

- Salesforce and JIRA both did something similar: their underlying database schema is very generic, basically keys and values, allowing arbitrary logical schemas to be defined at runtime. Yet in both cases, they ended up not really taking advantage of this flexibility. The logical schema of both systems is a very ordinary relational schema that could have been implemented directly on the database, with much better performance. I wonder if the Notion developers made a serious attempt to build on top of a more conventional structured schema, and found it really was unworkable?
- 👉🏻 I actually think Notion's data model is much more conventional than the data stores behind document editors like Google Docs or Figma. Blocks are "just" rows in Postgres.
  - We **use JSON for properties for flexibility and for user-defined property schemas**.
  - We could use an entity-attribute-value table as you describe for that, but such a table would complicate our caching techniques. It would also be enormous, but, it might be time for another think about that since we finished sharding.

- Been working with multiple document API's recently for my start-up. 
  - It's been a real challenge to understand how different document stores compare -- **Confluence uses undocumented XML markup** that "mostly" mirrors HTML, Google Docs gives you sometimes semantically-incorrect HTML with lots of inline styles, Slack has its own funny Markdown, etc. 
  - Then there's Notion blocks. I had to write my own HTML-to-Notion block parser, but I think I prefer working with it over everything else because structured data is just easier. 
  - One interesting gotcha: if you want to completely overwrite a page you currently have to remove every content block one at a time, and then add each new line one at a time. This is using their undocumented API, but the new API doesn't even offer deleting content yet. I'm eager to switch over but it may be a while...

- As author of a Notion browser extension, "everything is block" concept made it significantly easy to understand the notion doc structure and tweak the UI to add multiple customisations on top of it. For instance showing a fixed static ToC, etc.

- I think the power of Notion became apparent to me when I created a Page, accidentally changed it to some other type, then ctrl+z-ed it back to a Page, with all its contents intact. Seriously impressive. I wish search wasn't so crap though.

- I'm curious if Notion has any plans to make the "type" property user-extensible. Given the current data-structure, which decouples the block data from the way its rendered through the type property, a user has to define only one template for rendering arrangements of UI components (boxes, bullets, etc), titles and children. 
  - This sounds a bit like customized structured data types with style inheritance, à la DITA.

- I'm wondering ... so when a user requests a page which will have a full hierarchy of blocks, how are the db queries done.
  - It appears that Notion uses Postgres, which supports the recursive/hierarchical queries that are part of standard SQL. While I don't know for sure that Notion uses this, it seems likely.

- 🤔 How do you store, query, and search across documents?
  - Our source-of-truth data store is Postgres, with a Memcached cache on top.
  - **Most of our queries are "pointer chasing"** - we follow a reference from one record in memory to fetch another record from the data store. To optimize recursive pointer-chasing queries, we cache the set of visited pointers in Memcached.
  - We use Elasticsearch for search features like QuickFind.

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

- We don't use JOIN for the content tree; I don't think I've seen one in any of our queries.
  - We don't use an ORM. Notion's codebase on the back-end is much more functional than object-oriented, in the sense that we have many more code that looks like `transformTheData(theData, theChangeToMake): ResultingData` than we have classes or methods.
  - We do lean very heavily on the TypeScript type system and try to make invalid states unrepresentable.

- 🤔 Am I the only one who thinks the data model is very complex? How does it compare to a document based data model? What are the pros and cons of each?
- The **major issue with the document model is storage**. How big can a document grow? How do you persist it, and make small changes inside it? How do you handle "hot" documents that are very popular? Moving data between documents or having part of a document reference part of another document are complex. Complexity comes from building derived data that looks at slices of a document.
  - With a block-oriented model, your records are much more manageably sized. It's easier to reference or move data between documents, but in turn, you need to do these kinds of recursive shenanigans because your individual records are smaller in scope. Complexity comes from derived data that composes blocks together into a document.

- Is there a reason why you did not use rdf for representation and some rdf aware encoding like jsonld for serialization? Would be significantly easier for others to work with, could easily query it with SPARQL.
  - An **early version of Notion (before my time) used Neo4j, but it turned out to be very slow** for the kinds of data access Notion does.
- You don't have to use neo4j or any graph database to use RDF. It is just your current model seems very graph based and actually not that difficult to map to RDF, it would likely be possible to do with a jsonld context, and if you provided such a context then it would make your data a lot easier for others to consume.

- I have a requirement to allow users to create adhoc tables within a web application. I was wohoe beat to represent this on database. Any thoughts?
  - Tables (ad-hoc ones) are a beast. Code that aspires to do tame them, looks simple at first then evolve into crazy monsters that die at the altar of excel.

- A graph is so natural for pages, web pages are graphs too. So they choose a well fitting model for the problem, congrats

- ## 🚀🔥 [Notion – All-in-one workspace for notes, tasks, wikis, and databases | Hacker News_201901](https://news.ycombinator.com/item?id=18904648)
- 
- 
- 

# discuss
- ## 

- ## [People who use Notion to plan their whole lives | Hacker News_202304](https://news.ycombinator.com/item?id=35698521)
- I went from Zim to Dokuwiki to Bookstack (where I've been for the past 3 years). The former is an offline app and the latter two are self hosted. All three are FOSS.
  - Edit: after reading some other comments, one thing I really appreciate about Bookstack is that its opinionated and batteries included -> no falling into the "waste all your time customizing and perfecting your workflow" trap.

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

- ## Notion’s selection and undo/redo with multiplayer are pretty potato._202209
- https://news.ycombinator.com/item?id=32991105
  - Notion stores selection as grapheme indexes in a text property, so while it won’t lose selection if someone adds/removed characters from a text, your selection won’t make as much sense as one in Google Docs. 
  - Likewise with undo/redo or regular typing into the same field - it’s all last-write-wins updates.
- On the other hand, Notion’s editor does a much better job with CJK input, Android, etc compared to Slate. Slate has a beautiful API design but its implementation suffers outside of ideal conditions.
- ProseMirror did the best the last time I tested these libraries. TipTap (a competitor of yours?) provides an API layer on top, which I haven’t spent much time investigating. For my purpose I don’t want intermediary abstractions - but might be useful for your context depending on how much you want to specialize in rich text.

- ## [Peritext: A CRDT for Rich-Text Collaboration_202111](https://www.inkandswitch.com/peritext/)
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

- ## Muse using last-write-wins for merging text blocks._202205
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

- ## [Choosing DB model for an app similar to Notion, Block-based ("paragraphs") or document-based?](https://stackoverflow.com/questions/71024175)
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

- ## The Block Protocol
- https://news.ycombinator.com/item?id=30105510
- I think the challenging part of this project will be building intuitive and collaborative interfaces on top of the bare-bones data model. 
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

# discuss-notion-like
- ## 

- ## 

- ## [Notion.clone: open-source notes editor like in Notion | Hacker News_202011](https://news.ycombinator.com/item?id=25063122)
- A library that does half of the stuff that notion does and manages to create some sort of consistent markdown output would be amazing. This is amazing work and I think the main thing I see missing is navigation.
  - I couldn’t agree more with this. It would be nice to have an open source text editor with markdown shortcuts and auto-formatting. Bear.app, Typora and outline’s rich text formatter are close but the first two are closed and the latter I find clunky and hard to build on top of. I am excited to see this clone and where it goes

- One of the really great parts of Notion is that you can view your data in multiple ways (table, schedule, timeline view, etc.); 
  - You can configure views, filtering, sorting, summary’s, and foreign keys with roll ups....

- Does it work offline?
  - No, not yet - but that what be interesting to add!

- ## ✨ [BlockSuite: An open-source Notion-like editor with multiplayer support | Hacker News_202306](https://news.ycombinator.com/item?id=36505318)
- I want to be able to open a document in read-only mode. Otherwise, while just navigating through pages or reading content, it's far too easy to accidentally add text
  - First time I had a job that used Confluence as an idle tick i would just tick-untick-tick-untick the checkboxes on documents. I never realised that a) i was actually editing and saving the page, and b) it would send an email to the owner for every single tick/untick edit.
  - No, it's an editor, not a immutable website for consumption. The whole goal of them is that you can switch fast between editing and the rendered result. In that sense they are like word processors.

- It seems like there's a lot of recent interest and effort in open-source or self-hosted Notion-like/markdown-with-widgets applications and platforms.
  - To assuage my internal conflict I remind myself that I think plaintext is fundamentally the right choice for much knowledge collection, and I'm proud to say that if the internet shut down, I'd retain a significant growing fraction of my personal data.

- The approach here is a bit novel i.e treat each block as a separate editor instance (contenteditable) and somehow wire-up cursor movements to behave as if it's one big editable area.
  - But it comes with its downsides as well. For example cross block selection doesn't work.
  - If the entire page is one big editable area, then it becomes difficult to embed complex blocks like "kanban views" and calendar.
  - I guess we should think beyond contenteditable at this point and separate rendering layer from input layer - sort of like how Google Docs has built its editor.
  - But writing a rich text editor is not just a text-editing problem. It essentially needs you to build a layout engine itself (like webkit) that knows how/when to recalculate and draw the affected parts (render objects) when the rich-text changes. Why? because baking in tables and image-wraps and other complex resizable blocks affect other elements around/after it.
  - Bottomline: we need a custom built layout engine + text renderer + input handler(that respects accessiblity) + selection handler to build an absolutely powerful rich-text editor. I'd like to start a open source project in this direction.
- 👉🏻 Notion used this strategy until January 2021, when we rolled over to **one-big-ContentEditable**. I actually tried the tactic Affine is using, that is implementing drag-to-select gesture yourself and forcing that selection on the browser, but I hit a bunch of roadblocks on iOS and Android that made me abandon it and go with big-ContentEditable.
- Curious about the issues you faced on mobile! At Slite I was part of the mobile team, and the editor is using Slate. So to make it work in React Native we had to go for a WebView (similar to what Notion uses), with all the downside it can bring.. I tickled with the possibilty to do a native adapter of Slate, but the fact that it's based on a content editable, makes it complicated to adapt in React Native.. I have the feeling that block approach might fit better a more native integration on mobile. It seems similar to what Craft does, isn't it ?
  - Mostly Android input being a hellscape, and wrangling React inside ContentEditable posing weird synchronization challenges with input method editors.
- Fyi, I'm building an open source block-based editor @ https://www.blocknotejs.org that uses **one large contenteditable** and doesn't have those downsides you mention. It's built on top of Prosemirror.

- On the flip side, with individual contenteditables, you can be more confident you're not accidentally editing a block you didn't mean to.

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

# discuss-showcase
- ## 

- ## 

- ## 

- ## 

- ## 

- ## @jkosoy ’s first month as a new Notion employee (AKA Newtino), in his own kanban
- https://twitter.com/NotionHQ/status/1697660535704322514
  - 页面渲染多个分类，效果类似看板
- How does Notion at Notion deal with unbearable database speeds once you have too many relations  and rollups? Notion is a dream of a software and one of the most important in my life, but the performance is just sooooo annoying
  - I just had a conversation with our infra team about it yesterday. It can be a little annoying, but rest assured they are thinking about this *all the time*. 
