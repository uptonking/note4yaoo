---
title: pm-pattern-local-first-community
tags: [community, local-first, pattern]
created: '2022-03-03T18:19:36.049Z'
modified: '2022-03-03T18:20:12.075Z'
---

# pm-pattern-local-first-community

# guide

# discuss
- ## 

- ## 

- ## Downsides of Offline First__202110
- https://news.ycombinator.com/item?id=28717848
  - https://news.ycombinator.com/from?site=rxdb.info
- I’m a “true believer” in CRDTs, which I have some experience in. 
  - You can implement a useful CRDT for simple applications in under 100 lines if all you care about are standard database objects - like maps, sets and values. 
  - List CRDTs are where they get complicated, but most applications aren’t collaborative text editors.
  - The promise of CRDTs is that unlike most conflict resolution systems, you can layer over a crdt library and basically ignore all the implantation details. 
  - Applications should (can) mostly ignore how a CRDT works when building up the stack.
- The biggest roadblock to their use is that they’re poorly understood. Well, that and implementation maturity. 
  - Automerge-rs merged a PR the other day which brought a 5 minute benchmark run down to 2 seconds. But by bit we’re getting there.

- My biggest open question is how to design my centralized server side storage system for CRDT data. 
  - To service writes from old clients I need to retain a total history of a document, but I don’t want to force new clients to download the entire history nor do I want these big histories in my cache, so I end up wanting a hot/cold system; 
  - and building that kind of thing and dealing with the edge cases seems like more than 100 lines of code.
- It seems like the Yjs authors also recognize that CRDT storage on the server is an area to address, there was some work on a custom database in 2018, although my thinking is more about how to retrofit(改进，翻新) text CRDTs into my existing very conservative production cloud software stack than about writing to block storage.

- For prose text, what do you think about combining a document-scale CRDT, with fine-grained locking — e.g. splitting the document into a "list of lines/sentences", where lines have identity, and then only allowing one person to be modifying a given line at a time?
  - I almost thought Notion would be a good example of this, but apparently not — they actually do allow multiple users to be editing the same leaf-node content block at the same time, and so have taken on the full scope of the CRDT problem.


- ## My goal is to build a database that makes it easier to build local-first software.
- https://twitter.com/ccorcos/status/1532185301438738433
  - Embedded, reactive, schemaless, and transactional read/write directly to indexes (inspired by FoundationDb)
- SQLite is great, but it leaves much to be desired. It's mostly just a problem with SQL. 
  - Queries aren't reactive, no multi-valued columns, no indexes across tables for relational queries... All of these currently require bespoke(定制的) solutions.
- Segment trees/ interval trees are cool, I implemented one once for keeping track of register liveness in a compiler code generator
- Interesting idea to have cross-table indexes; is any RDBMS supporting that?
  - I think many databases avoid it because of arbitrarily expensive write time complexity. 
  - For example, one tweet = one row per follower. 
  - In a large multi-tenant(租户) system, companies end up with event-sourced architecture like Twitter with eventual consistency.
  - But for personal tools and fully distributed local-first p2p apps, that shouldn’t be as much of an issue. Worst case scenario, your computer is slow, but you aren’t going to break the app for everyone else.
- Write amplification can be a problem in these scenarios as well.
  - True. But if someone tweets and it needs to end up in 100M feeds, then thats just the nature of the problem… Not allowing indexes for this scenario doesn’t solve the problem.
- https://github.com/ccorcos/tuple-database
  - The local-first, "end-user database" database.
- https://github.com/ccorcos/game-counter
  - TupleDatabase as a UI state management system.
  - External effects interface through services defined on the Environment.

- ## The idea of persisting UI state to a database has me thinking of tons of possibilities. 
- https://twitter.com/devongovett/status/1526227167952117761
  - Not only a super nice user feature, also great for development. You could reload and be right where you left off with no Fast Refresh needed. Or debug state using database tools. So cool!
  - According to the article, sqlite is fast enough to store the scroll position and re-query data in a virtualized table in real time
- Yes, that is how our app works for 7 years now ; -) we syns whole sate (localStorage then and idb now) and react to changes. All UI is built in browser. No hot reloads  needed.
- I remember reading an article quite a while ago about how FB built their iOS app where everything was driven from SQLite tables - everything. It’s a pattern I’ve been interested in applying for a while. We already do it with business logic loaded + cached in client driving ui
- There's a ClojureScript project that explores similar ideas: https://github.com/fulcrologic/fulcro. It changed my perspective on UI development

- ## In Riffle we avoid manual network by optimistically loading all data onto the client and doing queries locally. 
- https://twitter.com/geoffreylitt/status/1505932761453977606
  - HF / DIEL take a diff approach: keep some computation server-side, but help schedule across the boundary
  - Interesting tradeoffs there. Having all data local seems simpler when it's possible. eg: 0 net latency enables new patterns like storing UI state in the DB.
  - OTOH, def some benefits to putting data/compute off-device. Access control, avoid huge data / queries on device...

- ## Wrote an essay about Riffle, a new project I've been working on. Guiding question: could we simplify app dev w/ a new kind of reactive local-first database?
- https://twitter.com/geoffreylitt/status/1499083601387864069
- I imagined: what if you could customize any web app in a spreadsheet view?
  - Apps today aren't _actually_ built on spreadsheets.
  - OK then, so what would it look like to build apps w/ spreadsheets?
  - There've been some great answers to this in prior work, but they often have a low complexity ceiling--good for building TodoMVC, but hard to scale up.
- w/ Riffle we're trying something ambitious: simplify app dev for both experts building "real apps", and novices.
  - Focused on providing an awesome foundation for state management, inspired by good ideas from databases research, spreadsheets, incremental computation, and more.

- ## I'm having trouble reconciling an offline-first app with online SaaS sync. 
- https://twitter.com/_paulshen/status/1431745519873781765
  - How do you handle auth while offline? 
  - What happens to your offline documents/changes when you reconnect logged out or as a different user?
- files backed by git provide some inspiration. you own the files on your disk. but the manual push/pull and resolution steps don't translate directly to "apps"
- Maybe figma can help you with some ideas of how to handle it
  - [Can I work offline with Figma?](https://help.figma.com/hc/en-us/articles/360040328553-Can-I-work-offline-with-Figma-)
  - Figma is probably the gold standard here. this doc is very thorough. thanks!
  - I tried making some Figma changes offline and deleted my session cookie. It silently lost the changes but Figma doesn't claim to be an offline tool. The save to `.fig` file is nice.
- Understood. The feature to save the document to .fig file is neat, as that's the only guaranteed way to avoid losing data.
- Brainstorm: it could be split into different layers:
  - give the user a way to export the docs to a file (avoid user losing offline data if they want to, ex, uninstall the browser)
  - when reconnecting, if session is ok + user still has same access to the docs, sync the changes*
- I think it’s ok to disallow switching accounts when you’re offline.
- agreed but things can change on the server side while you're offline. maybe you lose permissions to the file or you triggered an action to log out of all your clients.
  - What should happen in those cases isn’t technically hard, but more of a problem of designing a UI that informs and sets expectations effectively. I do understand designing such a UI isn’t trivial.
- Offline data sync is complicated with web browsers. User might have a few tabs opened, so you need to sync between them.
  - You probably don't want to sync the same changes from all tabs. 
  - Only Chrome has a way to sync data in background I think. 
  - Other browser quirks like IndexedDB not working in FF private tabs and Safari had some problems. So it gets complicated quickly

- ## It’s quite rare for software to offer both a real local file format and also substantial(大量的，重大的) cloud/SaaS behavior (ie other than syncing). 
- https://twitter.com/andy_matuschak/status/1428777459235782660
  - Usually it’s one or the other
  - if the cloud has active behavior, apps are thin clients which don’t expose an accessible on-disk format (eg Notion).
  - I recently finished re-architecting @withorbit to expose an on-disk format, thought I’d write a bit about what I learned.
- Orbit的解决方案小结
  - 存储层基于SQLite
  - 协作/同步层基于比CRDT更简单的events log
- It’s hard to pull this off, as I&S describe. 
  - You need to design a file format which syncs efficiently and reliably, which is already tough. 
  - Gets tougher when your SaaS is an active replica with its own public API, and when you layer on indexing/querying, migration, sparsity.
- There are enterprise solutions which solve these problems (Realm, CouchDB), 
  - but one consistent limitation is that they “own” the file format, and often the server component as well. 
  - I don’t feel good exposing my on-disk format to local clients if it’s tied to a specific backend.
- CRDTs are a useful piece of the puzzle, but they don’t solve the problem as fully as people often imagine. 
  - The I&S folks are working diligently on many of these. 
  - But **one problem I don’t know how to solve** is the complexity of the resulting opaque file formats.
- In an ideal world, everything’s just plaintext, so you can modify it with whatever tool you like. No libraries needed. 
  - Problems with this include semantic sync, indexing, structured data, etc. 
  - SQLite is almost as good, if the schema is well-defined
  - [SQLite As An Application File Format](https://www.sqlite.org/appfileformat.html)
- Maybe someday automerge’s serialization format will be as durable and universal as SQLite’s, but in the meantime, it’s certainly not amenable(易处理的) to casual concurrent local access in some user script.
- Of course, **SQLite leaves you to solve syncing**. 
  - The typical approach is a write-only log of events (CRDT mutations or otherwise) which can be replayed across replicas. 
  - Snapshots of entity states are computed from queries across these events.
- That’s **the approach Orbit takes**: simple event structures (simpler than CRDTs, sacrificing some of their key guarantees to reduce complexity), with well-defined merge operations, in a SQLite db. 
  - Users can write scripts to insert their own events if they like.
- I’m still not satisfied with this. 
  - Reading/writing data yourself requires using Orbit’s libraries or a SQLite library and an understanding of the schema. 
  - I’d like to just expose the data as plaintext, but I’m not yet sure how to achieve that practically.
- One approach is to define Git-style “plumbing” CLI primitives which offer plaintext-like I/O to your data structures. 
- Another is to define a FuseFS layer, @rsnous style.
- Orbit’s cloud server has its own (third, ugh) backend implementation, which it uses to offer APIs, aggregate analytics (for my research), and services like study reminder notifications.
  - I see now why people don’t generally do this. It was a huge amount of work. 
  - As it happens, Orbit’s implementations are quite general (i.e. they have almost no specific knowledge of Orbit’s structures), so perhaps they’ll be of use to others.
  - https://github.com/andymatuschak/orbit

    - Orbit is an experimental platform for publishing and engaging with small tasks repeatedly over time.

- another hard thing about implementing this type of data format is that web browsers demand their own implementation. 
  - @kirkbyo_ kindly implemented an IDB-based Orbit backend. Excited about absurd-sql

- I like what @craftdocsapp does here: for each note, you can choose to persist either to on-disk file or to their realtime cloud. A sensible compromise given there's not a great way (yet!) to get the best of both worlds
  - In your Metamuse interview I really liked when you (or maybe it was @_adamwiggins_ or @mmcgrana ) talked about how code IDEs provide all these features on top of basic data, like “jump to definition”, syntax highlighting etc. Wonder how this can be applied to other data…
  - Another example is Photoshop (or any bitmap image editor); Instead of an array of bytes representing plain text, it operates on an array of bytes representing pixels. Adds computed information like histogram, color replacement, etc.
  - Yeah layering complex interpretations over a simple serialized format seems to work well in those domains. 
  - Note taking seems trickier… eg, Markdown isn’t powerful enough to express Notion documents
  - Maybe Notion documents is not a good benchmark and maybe markdown is not the ideal “elemental material” or perhaps it is. Figma is interesting as its file format is a list of key-value maps. The app then gives special meaning to certain keys and values.
  - Aside: interestingly this is the data format underlying almost everything in Spotify; an ordered dictionary. 
  - Keys and values are just byte strings. Hierarchy and meaning applied computationally. (3-way diff-merge was less hard to implement this way. Etc etc.)
- Ingredients for a future:
  • Elemental material that is absent of meaning (but has some structure)
  • Domain-specific agreements about meaning of data (eg rich text editor, game scene, etc)
  • Synchronization tools that act on the elemental material (w/ optional domain knowledge)
- Elemental material: maybe XML is the closest we've ever gotten? HTML, RSS, SVG are three distinct domains.
  - I had always hoped a file sync service like Dropbox or iCloud could add a developer API and become the last point, but that didn't happen.
- Maybe JSON can be the elemental material? Definitely my default choice moving simple structured data between programs.
  - This is why I find automerge interesting--it provides that sync tool on the structured layer without any domain-specific knowledge
- I think JSON is popular because it is the weakest link. 
  - No integers or pointers, sparse representation (like XML.) 
  - But ultimately I think that story of how PostScript came out of the JaM project as a solution the problem of an evolving data structure is a good lesson.
  - Hmm yeah... maybe this gets at a fundamental tension: weaker, stripped-down formats are easier to make generic across domains + tools? Eg: a huge drawback of plaintext code is the lack of pointers, and yet smart editors can "rename function" just fine by interpreting the text
  - Similarly, newline-delimited text in classic UNIX tools is a very underconstrained/weak format, but simultaneously super versatile and quite useful... maybe two sides of the same coin? idk
- I wonder a lot about relational database as "elemental material"... eg, what if my emails, calendar, photos, contacts, projects, tasks were all just in sqlite? I could routinely use a nice Airtable-style UI to manually edit, and also write scripts against my DB quite easily
  - Very interesting idea. SQLite is very portable and truly open, so that's a good start. 
  - I struggle with one thing with SQLite though and I wonder how you deal with this: How to... look at it, copy paste, massage the structure, etc. (e.g. bitmap = image editor, text = text editor)
  - There are plenty of GUI apps for SQLite of course but they are all MUCH less flexible than say editing a text file in a good text editor with things like Ctrl+A to select all
  - Maybe what we need is a really good editor for whatever a good "elemental material" is for data. I'm thinking something that can make use of the speed of a keyboard but have more dimensions than sequential bytes (i.e. plain text.) Maybe a DOM structure?
- Yeah, agree: the elemental material can only be as good as the best editor for the format. 
  - Fun to imagine the ideal keyboard-driven SQLite viewer/editor for daily usage. Inspirations could be classic iTunes, Airtable, + more powerful visual query UIs
  - It's funny how many apps eventually build a table UI... each one has unique quirks, and usually not extraordinary UI since the team is busy w/ other stuff
  - Like, instead of Github building a table UI for Issues, could I just use familiar Airtable or magic generic table editor ?
- I wonder if better to focus on SQL as the communication protocol, rather than SQLite as an implementation?
  - For example: maybe I would like to use my table editor with a web service exposing a virtual SQL database as just an API; I don't care what lives behind the SQL protocol
- If you use a Mac, there's a decent chance your email, photos, calendar and tasks are already in SQLite
- I tend not to run it directly against the SQLite files in-use by apps though, 
  - since they're not designed with concurrency in mind (they often don't enable WAL mode so you get a lot of locking errors) - my tools tend to create a separate database copy which I update intermittently(间歇的，断断续续的)
- I've not tried applying a write to a file used by some application yet - my worry is that they'd have some weird denormalizations that I wouldn't fulfill and I'd break things
  - Yeah that makes sense. Seems like a general challenge w/ sharing a database across apps... I guess only hope would be to try to encode as many constraints as possible directly in the DB layer
- The other problem with encouraging other apps to access your DB file directly is that it turns your schema into a supported API, which makes schema changes massively harder if you don't want to break things outside your app's control
- I like the idea of defining named SQL views that are the "supported" way to access data - that way you can change the rest of the schema and then modify those views to continue serving the same shape of data against the modified schema
  - Yeah that makes total sense for reads! Writes seem to require more machinery though... I guess you can (1) get fancy and figure out how to send writes backwards through the view query, or (2) treat SQL as just a read interface and have some separate constrained write API
  - I guess writes could be handled by predefined stored procedures in databases that support those, but sadly SQLite doesn't (yet)
- @simonw ‘s blog post about querying photo metadata gives me hope that sqlite are at the heart of other consumer apps even though it’s not advertised widely.
- Another random inspiration is how Automerge assigns unique IDs to every little piece of a JSON blob… hard to make it efficient, but incredibly convenient foundation for having pointers that stably reference anything
  - Re: types, I am enamored by super rich types, things like “phone number”, “email address”, “US State”, etc. Maybe naive to imagine these types can be agreed upon by everyone (I know world is complicated!) but still feel so convenient…

- This was the world people imagined with RDF
  - It's supported today by Google (search engines, Gmail) and other large small companies. JSON-LD, RDFa, microformats.  Works directly with many triple stores with a standard graph query language. Whatever it's flaws nothing is nearly as widely supported.

- Have you looked at Firebird? It's a db that supports ANSI SQL and claims to seamlessly flip between on-disk, in-memory and client/server. I've never tried it beyond v simple local things.

- Didn't consider scuttlebutt but looked at many distributed logs like it. 
  - Two key issues are the need for indexing/querying and an on-disk file format I can expose to local clients, ideally one which is not tied to protocol implementation.

- This is very top of mind for me with http://natto.dev. I've tried representing canvases as text files and using isomorphic git in the browser. The current live version uses yjs, a CRDT, though not syncing. hoping to share the next (final?) iteration soon.

- TabFS is an example of another (perhaps heavier) way to go about it, basically keeping client/server by using a virtual filesystem
  - https://omar.website/tabfs/
  - Technically no cloud, but you are integrating with a foreign and otherwise opaque system
  - TabFS is a browser extension that mounts your browser tabs as a filesystem on your computer. Each of your open tabs is mapped to a folder.

- One observation that @pvh makes is that web browsers aren't a good fit for local-first. They're fundamentally thin clients with throwaway local caches. Maybe that's part of the mismatch for Orbit?
  - Thick clients with a sync-style model like Dropbox, Git, Craft, and Obsidian are easier to fit with this, although often still don't have a user-facing flat file format outside of explicit export.
  - **On CRDTs and merging: I think this is less about realtime collaboration** (although that's important) and more about the fact that once you have multiple sources of truth, there has to be a reliable way to reconcile them.
  - If my phone and my laptop are peers rather than subservient to a central server, it doesn't matter if I'm never "live" editing on both devices. 
  - There will be situations where the changes need to be merged, and Git-style conflict resolution is too heavyweight for many/most apps.

- Currently I’m staying far away from automatic merging of text edits precisely because of the “opaque file format” problem. 
  - But automatic merging of edits made to “conceptually different text chunks” is straightforward in a replicated key/value store & the format is still simple.
- Stopped thinking about storage implementations earlier because I knew that would require another project entirely. Glad someone took a stab at it!

- An in-between solution is to keep source of truth on the server but 
  - (a) guarantee all data can import/export to a simple format like csv, 
  - and (b) periodically export it to user owned place (eg s3, gdrive), so the user doesnt worry that “a” is a fake claim.
