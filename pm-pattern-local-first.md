---
title: pm-pattern-local-first
tags: [local-first, pattern, pm]
created: '2021-08-22T08:05:15.252Z'
modified: '2021-08-22T08:05:39.413Z'
---

# pm-pattern-local-first

# guide

- 本地文件格式的设计
  - 完全自定义，类似pdf、xls、doc、dwg
  - 多层级文件夹，类似git
  - 被封装的多层级，类似epub、odt
  - sqlite
  - 可以结合多种方案，将适合用户读写的数据以纯文本格式暴露，不合适读写的数据放在其他格式甚至数据库

- why local
  - 平台封号
  - 百度网盘后期限速，就算开了超级会员仍然可能因为带宽流量消耗过多而被系统限制
  - 腾讯起诉DD373交易平台，庭审时腾讯代表称「账号主人不可转卖自己的手机游戏账号」
# examples-local-first
- https://github.com/jaredly/local-first
  - This aims to eventually be a fully-featured solution for managing, syncing, and storing application data, in a way that works offline, and collaboratively.

- https://github.com/local-first-web/state
  - A Redux-based state container for local-first software, offering seamless synchronization using Automerge CRDTs. (Formerly known as fish Cevitxe).
  - @localfirst/state is an automatically replicated Redux store that gives your app offline capabilities and secure peer-to-peer synchronization superpowers.
# [Local-first software__201910](https://www.inkandswitch.com/local-first.html)
- Cloud apps like Google Docs and Trello are popular because they enable real-time collaboration with colleagues, and they make it easy for us to access our work ~~from all of our devices~~ anytime anywhere. 
  - However, by centralizing data storage on servers, cloud apps also take away ownership and agency from users. 
  - If a service shuts down, the software stops functioning, and data created with that software is lost.
- In this article we propose “local-first software”: a set of principles for software that enables both collaboration and ownership for users. 
  - Local-first ideals include the ability to work offline and collaborate across multiple devices, while also improving the security, privacy, long-term preservation, and user control of data.
- We survey existing approaches to data storage and sharing, ranging from email attachments to web apps to Firebase-backed mobile apps, and we examine the trade-offs of each. 
  - We look at Conflict-free Replicated Data Types (CRDTs): data structures that are multi-user from the ground up while also being fundamentally local and private. 
  - CRDTs have the potential to be a foundational technology for realizing local-first software.

- Motivation: collaboration and ownership

## Seven ideals for local-first software

- Fast; No spinners: your work at your fingertips
- Offline-able; The network is optional
- Longevity; The Long Now(accessing the data for a long time in the future)
- User control; You retain ultimate ownership and control
- Privacy; Security and privacy by default

- Collaborative; Seamless collaboration with your colleagues
- Multi devices; Your work is not trapped on one device

## Existing data storage and sharing models

- How application architecture affects user experience
  - Files and email attachments
  - Web apps: Google Docs, Trello, Figma
  - Dropbox, Google Drive, Box, OneDrive, etc.
  - Git and GitHub
- Developer infrastructure for building apps
  - Web app (thin client)
  - Mobile app with local storage (thick client)
  - Backend-as-a-Service: Firebase, CloudKit, Realm
  - CouchDB

## Towards a better future

- CRDTs as a foundational technology
- Ink & Switch prototypes
  - Trello clone
  - Collaborative drawing
  - Media canvas
  - Findings

- Ink & Switch has developed an open-source, JavaScript CRDT implementation called `Automerge`. 
  - It is based on our earlier research on JSON CRDTs. 
  - We have then combined Automerge with the Dat networking stack to form Hypermerge. 
  - We do not claim that these libraries fully realize local-first ideals — more work is still required.
- However, based on our experience with them, we believe that CRDTs have the potential to be a foundation for a new generation of software. 
  - Just as packet switching was an enabling technology for the Internet and the web, or as capacitive touchscreens were an enabling technology for smartphones, so we think **CRDTs may be the foundation for collaborative software that gives users full ownership of their data**.

- We built three prototypes
- Trellis
  - https://github.com/automerge/trellis
  - Trello clone/sample app for Automerge persistence library
  - take a look at PushPin, a much more complete & robust implementation of this approach to software development.
- pixelpusher
  - https://github.com/automerge/pixelpusher
  - bringing a Figma-like real-time experience to Javier Valencia’s Pixel Art to CSS.
- PushPin
  - https://github.com/automerge/pushpin
  - a mixed media canvas workspace similar to Miro or Milanote.
  - A local-first collaborative corkboard app. 

- Our goal in developing the three prototypes Trellis, PixelPusher and PushPin was to evaluate the technology viability, user experience, and developer experience of local-first software and CRDTs. 
  - CRDT technology works.
  - The user experience with offline work is splendid.
  - Developer experience is viable when combined with Functional Reactive Programming (FRP).
    - The FRP model of React fits well with CRDTs. 
    - A data layer based on CRDTs means the user’s document is simultaneously getting updates from the local user (e.g. as they type into a text document) but also from the network (as other users and other devices make changes to the document).
  - Conflicts are not as significant a problem as we feared.
  - Visualizing document history is important.
  - URLs are a good mechanism for sharing.
  - CRDTs accumulate a large change history, which creates performance problems.
    - Performance and memory/disk usage quickly became a problem because CRDTs store all history, including character-by-character text edits. 
    - These pile up, but can’t easily be truncated because it’s impossible to know when someone might reconnect to your shared document after six months away and need to merge changes from that point forward.
    - We continue to optimize Automerge, but this is a major area of ongoing work.
  - Network communication remains an unsolved problem.
  - Cloud servers still have their place for discovery, backup, and burst compute.

- Then some strategies for improving each area:
- Fast. 
  - Aggressive caching and downloading resources ahead of time can be a way to prevent the user from seeing spinners when they open your app or a document they previously had open. 
  - Trust the local cache by default instead of making the user wait for a network fetch.
- Offline. 
  - In the web world, Progressive Web Apps offer features like Service Workers and app manifests that can help. 
  - In the mobile world, be aware of WebKit frames and other network-dependent components. 
  - Test your app by turning off your WiFi, or using traffic shapers such as the Chrome Dev Tools network condition simulator or the iOS network link conditioner.
- Longevity. 
  - Make sure your software can easily export to flattened, standard formats like JSON or PDF. 
  - For example: 
    - mass export such as Google Takeout; 
    - continuous backup into stable file formats such as in GoodNotes; 
    - and JSON download of documents such as in Trello.
- User control. 
  - Can users easily back up, duplicate, or delete some or all of their documents within your application? 
  - Often this involves re-implementing all the basic filesystem operations, as Google Docs has done with Google Drive.
- Privacy. 
  - Cloud apps are fundamentally non-private, with employees of the company and governments able to peek at user data at any time. 
  - But for mobile or desktop applications, try to make clear to users when the data is stored only on their device versus being transmitted to a backend.

- Collaboration. 
  - Besides CRDTs, the more established technology for real-time collaboration is Operational Transformation (OT), as implemented e.g. in ShareDB.
- Multi-device. 
  - Syncing infrastructure like Firebase and iCloud make multi-device support relatively painless, although they do introduce longevity and privacy concerns. 
  - Self-hosted infrastructure like Realm Object Server provides an alternative trade-off.

- If you are an entrepreneur interested in building developer infrastructure, all of the above suggests an interesting market opportunity: “Firebase for CRDTs.”
  - Such a startup would need to offer a great developer experience and a local persistence library (something like SQLite or Realm). 
  - It would need to be available for mobile platforms (iOS, Android), native desktop (Windows, Mac, Linux), and web technologies (Electron, Progressive Web Apps).
  - User control, privacy, multi-device support, and collaboration would all be baked in. 
  - Application developers could focus on building their app, knowing that the easiest implementation path would also given them top marks on the local-first scorecard. 

## Conclusions

- In the pursuit of better tools we moved many applications to the cloud. 
  - Cloud software is in many regards superior to “old-fashioned” software
  - it offers collaborative, always-up-to-date applications, accessible from anywhere
- However, in the cloud, ownership of data is vested(合法的归属于) in the servers, not the users, and so we became borrowers of our own data. 
  - The documents created in cloud apps are destined to disappear when the creators of those services cease to maintain them. 
  - Cloud services defy(不可能；反抗) long-term preservation. 
  - No Wayback Machine can restore a sunsetted web application. 
  - The Internet Archive cannot preserve your Google Docs.
- But more work is needed to realize the local-first approach in practice.
  - Application developers can take incremental steps, such as improving offline support and making better use of on-device storage. 
  - Researchers can continue improving the algorithms, programming models, and user interfaces for local-first software. 
  - Entrepreneurs can develop foundational technologies such as CRDTs and peer-to-peer networking into mature products able to power the next generation of applications.
# [SQLite As An Application File Format](https://www.sqlite.org/appfileformat.html)
- An SQLite database file with a defined schema often makes an excellent application file format. 
  - Here are a dozen reasons why this is so:
  - Simplified Application Development
  - Single-File Documents
  - High-Level Query Language
  - Accessible Content
  - Cross-Platform
  - Atomic Transactions
  - Incremental And Continuous Updates
  - Easily Extensible
  - Performance
  - Concurrent Use By Multiple Processes
  - Multiple Programming Languages
  - Better Applications

- An "application file format" is the file format used to persist application state to disk or to exchange information between programs. 
  - There are thousands of application file formats in use today, like doc/xls/pdf/dwg/epub/git/...
- We make a distinction between a "file format" and an "application format". 
  - A file format is used to store a single object. 
    - So, for example, a GIF or JPEG file stores a single image
  - An EPUB file, in contrast, stores both text and images (as contained XHTML and GIF/JPEG files) and so it is considered an "application format". 
  - The boundary between a file format and an application format is fuzzy. 
  - This article is about "application formats".
  - For this article, let us say that a file format stores a single object and an application format stores many different objects and their relationships to one another.

- Most application formats fit into one of these three categories:
- Fully Custom Formats. 大多单文件、大多二进制、读写需要专用软件
  - Custom formats are specifically designed for a single application. 
  - DOC, XLS, DWG, PDF, and PPT are examples of custom formats. 
  - Custom formats are usually contained within a single file, for ease of transport. 
  - They are also usually binary, though the DWG format is a notable exception.
  - Custom file formats require specialized application code to read and write and are not normally accessible from commonly available tools such as unix command-line programs and text editors.
  - In other words, custom formats are usually "opaque blobs". 
  - To access the content of a custom application file format, one needs a tool specifically engineered to read and/or write that format.
- Pile-of-Files Formats. 通常多级文件夹、部分可读写、移动或引用不便
  - A pile-of-files format essentially uses the filesystem as a key/value database, storing small chunks of information into separate files. 
  - Git is a prime example of this, though the phenomenon occurs frequently in one-off and bespoke applications. 
  - This gives the advantage of making the content more accessible to common utility programs such as text editors or "awk" or "grep". 
  - But even if many of the files in a pile-of-files format are easily readable, there are usually some files that have their own custom format (example: Git "Packfiles") and are hence "opaque blobs" that are not readable or writable without specialized tools. 
  - It is also much less convenient to move
  - Finally, a pile-of-files format breaks the "document metaphor": there is no one file that a user can point to that is "the document".
- Wrapped Pile-of-Files Formats. 
  - Some applications use a Pile-of-Files that is then encapsulated into some kind of single-file container, usually a ZIP archive. 
  - EPUB, ODT, and ODP are examples of this approach.
  - OpenOffice documents (ODT and ODP) are also ZIP archives containing XML and images that represent their content as well as "catalog" files that show the interrelationships between the component parts.
  - A wrapped pile-of-files format is a compromise between a full custom file format and a pure pile-of-files format. 
  - A wrapped pile-of-files format is not an opaque blob in the same sense as a custom format, since the component parts can still be accessed using any common ZIP archiver, but the format is not quite as accessible as a pure pile-of-files format because one does still need the ZIP archiver
  - As with custom file formats, and unlike pure pile-of-file formats, a wrapped pile-of-files format is not as easy to edit, since usually the entire file must be rewritten in order to change any component part.

- The purpose of this document is to argue **in favor of a fourth new category of application file format: An SQLite database file**.

- Any application state that can be recorded in a pile-of-files can also be recorded in an SQLite database with a simple key/value schema 
  - CREATE TABLE files(filename TEXT PRIMARY KEY, content BLOB); 
  - it has the advantage of being able to **update individual "files" without rewriting the entire document**.
- An SQLite database can have dozens or hundreds or thousands of different tables, with dozens or hundreds or thousands of fields per table
  - An SQLite database is a more versatile container than key/value filesystem or a ZIP archive. 
- The power of an SQLite database could, in theory, be achieved using a custom file format. 
  - But any custom file format that is as expressive as a relational database would likely require an enormous design specification and many tens or hundreds of thousands of lines of code to implement. 
  - And the end result would be an "opaque blob" that is inaccessible without specialized tools.

- SQLite database as an application file format has compelling advantages
- Simplified Application Development
- Single-File Documents
  - An SQLite database is contained in a single file, which is easily copied or moved or attached. 
  - SQLite does not have any file naming requirements and so the application can use any custom file suffix that it wants to help identify the file as "belonging" to the application.
- High-Level Query Language
- Accessible Content
  - Information held in an SQLite database file is accessible using commonly available open-source command-line tools 
  - It is true that command-line tools such as text editors or "grep" or "awk" are not useful on an SQLite database, 
  - but the SQL query language is a much more powerful and convenient way for examining the content
  - An SQLite database is a well-defined and well-documented file format that is in widespread use
  - The longevity of SQLite database files is particularly important to bespoke(定制的) applications, since it allows the document content to be accessed far in the future
  - Data lives longer than code.
- Cross-Platform
- Atomic Transactions
  - Writes to an SQLite database are atomic.
  - They either happen completely or not at all, even during system crashes or power failures. 
  - So there is no danger of corrupting a document just because the power happened to go out at the same instant that a change was being written to disk.
  - SQLite is transactional, meaning that multiple changes can be grouped together such that either all or none of them occur, and so that the changes can be rolled back if a problem is found prior to commit. 
  - This allows an application to make a change incrementally, then run various sanity and consistency checks on the resulting data prior to committing the changes to disk. 
- Incremental And Continuous Updates
- Easily Extensible
- Performance
  - In addition to being faster for raw read and writes, SQLite can often dramatically improves start-up times because instead of having to read and parse the entire document into memory, the application can do queries to extract only the information needed for the initial screen.
  - As the application progresses, it only needs to load as much material as is needed to draw the next screen
  - This helps keep the memory footprint of the application under control.
  - A pile-of-files format can be read incrementally just like SQLite. 
  - But many developers are surprised to learn that SQLite can read and write smaller BLOBs (less than about 100KB in size) from its database faster than those same blobs can be read or written as separate files from the filesystem.
  - There is overhead associated with operating a relational database engine, however one should not assume that direct file I/O is faster than SQLite database I/O, as often it is not.
  - In either case, if performance problems do arise in an SQLite application those problems can often be resolved by adding one or two `CREATE INDEX` statements to the schema or perhaps running `ANALYZE` one time and without having to touch a single line of application code. 
- Concurrent Use By Multiple Processes
  - SQLite automatically coordinates concurrent access to the same document from multiple threads and/or processes. 
  - Two or more applications can connect and read from the same document at the same time. 
  - SQLite automatically ensures that the low-level format of the document is uncorrupted. 
  - Accomplishing the same with a custom or pile-of-files format, in contrast, requires extensive support in the application. 
  - And the application logic needed to support concurrency is a notorious bug-magnet.
- Multiple Programming Languages
- Better Applications

- Conclusion
  - in many cases, SQLite is a far better choice than either a custom file format, a pile-of-files, or a wrapped pile-of-files. 
  - SQLite is a high-level, stable, reliable, cross-platform, widely-deployed, extensible, performant, accessible, concurrent file format. 
  - It deserves your consideration as the standard file format on your next application design.
# discuss
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
