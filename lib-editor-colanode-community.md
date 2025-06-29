---
title: lib-editor-colanode-community
tags: [colanode, community, notion-like]
created: 2025-06-21T19:11:05.576Z
modified: 2025-06-21T19:12:34.201Z
---

# lib-editor-colanode-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-author/internals
- ## 

- ## In @colanode each change is tracked as Yjs (CRDT) transaction and stored locally before eventually synced with the server. _202506
- https://x.com/hakanshehu/status/1937402812255682743
  - The server assigns a sequential number for each transaction to guarantee ordering of changes. 
  - Colanode clients use a cursor based syncing (similar as Kafka) and process/sync all transactions in order locally.
  - For performance reasons these clients do not store all individual transactions locally, but only the final merged state. This approach saved storage for users. Only confirmed transactions from the server are merged in the final state. Pending local transactions are stored in a separate queue before syncing with the server.
  - With undo/redo you basically need to revert a transaction. This gets tricky when you need to send the revert to other clients which did or didn't yet sync that transaction locally. Since the clients merge all transactions in one final state, you can't know which specific transaction to revert.
  - 💡 Given the constrains, undo/redo in Colanode is implemented as a new transaction which makes the necessary changes to bring back the document to a previous state. It uses the `UndoManager` provided by Yjs which tracks only the current user changes but appends the undo/redo operations as a new update for the document.
  - The downside of this approach is that it can create a lot of transactions if the user frequently undos/redos a document (each one is a new transaction that needs to be synced). But, we had this problem before (each small changes creates a new transaction) and we are working on an optimization for this.

- ## @tan_stack/query is not meant to be used only for fetching the data from a server. 
- https://x.com/hakanshehu/status/1935466602998415516
  - At @colanode we use it to perform queries and mutations in a local SQLite database (both in web and electron) and it has been a great developer experience.
  - Since you cannot access the db directly from UI, you need to send a message (query or mutation) to the main process and handle the response. This communication is async, similar to a typical frontend - backend request. It makes perfect sense to use an async state management. 
  - We built a wrapper which contains type safe inputs, automatically generates query keys and handles the communication between processes. It also updates the cache on result changes from the main process. Basically almost all of app state is handled this way
  - By using TanStack/Query we get caching, loading states, retries and many other features out of the box which has been a great help in development of the app.

- ## 🚀🧭 We have build a local-first web client for @colanode . It supports full offline mode _20250618
- https://x.com/hakanshehu/status/1935031919785160973
  - To achieve this we use 🛢️ SQLite with wasm and OPFS (Origin Private File System) in browsers (not supported by all browsers yet). The assets are cached using PWA techniques for offline support. The data you have access to is stored locally and is accessible anytime. New changes are stored locally first and eventually synced with the server.

# discuss
- ## 

- ## 

- ## [Selfhosted colanode setup, but getting error _202504](https://github.com/colanode/colanode/issues/17)
- Running Colanode Server via docker on a linux box on my network @ http://192.168.68.73:3381. Could not fetch server configuration. Please make sure the domain is correct.
  - this happens because the Colanode desktop app currently requires secure connections ( `https` and `wss` ) when connecting to a server, except when the host is `localhost` . That's why it works with http://localhost:3000 but fails when using an IP address without a certificate.
  - For now, you need to use either localhost or a hostname with a valid HTTPS certificate. We're planning to improve this in the future to allow connections to self-hosted servers without HTTPS as well.

- You can add the env variable `DEBUG=colanode:*` which will show more logs and errors

- ## 🚀 [I built Colanode, an open-source & local-first Slack and Notion alternative that you can self-host : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1khpftl/i_built_colanode_an_opensource_localfirst_slack/)

- do you have any plans on making a web client? I think something like this would be great if i could use it in the browser
  - We have it in plan to implement the web client as well, we just need to look into some stuff related with local-first. Just curious, is there any reason you can't install the desktop app?
- I'd prefer using it in the browser since an app like this doesn't really need many system APIs. The browser approach is actually more secure (being sandboxed) and would automatically make it more Linux-compatible too.

- To create a Kanban view you need to have at least one 'select' or 'multi select' field in the database. We will add options for other fields in the future

- Does your databases/tables support relationships? Can I link one table to another one?
  - Yes it does, when you create the database you can add fields with the type 'relation' which lets you connect with other databases (or even with the same database itself)

- Does this support formulas like AirTable? If so, does it support referencing cells that are formulas to expand into another formula? Something similar to vlookup…
  - Not yet, it's part of our roadmap.

- Looks cool. If I can get the attendance and vacation list to work on this, it will be a nice replacement for the odoo.

- ## 🚀💬📄 [Show HN: Colanode, open-source and local-first Slack and Notion alternative | Hacker News _202504](https://news.ycombinator.com/item?id=43780176)
  - 👷 As a heavy Notion user, I often found it tough to get my teams fully onboard since people naturally gravitate toward chat for quick interactions. 🐛 Maintaining context between chat apps like Slack and documentation apps like Notion became increasingly frustrating. Switching contexts, losing track of information, and managing data across multiple tools created unnecessary friction.
  - This frustration led me to build Colanode, a single platform integrating structured notes and knowledge management with real-time chat. After building the first version, early feedback highlighted a critical issue: teams/organizations want full control over sensitive data, especially conversations. That's why I decided to open-source Colanode under an Apache 2.0 license, making it fully self-hostable so you can retain complete ownership and privacy over your data.
  - Colanode is built with simplicity and extensibility in mind, using only open-source tools and avoiding any vendor or cloud lock-in.
  - It features a local-first architecture offering complete offline support. 
  - From a technical perspective, Colanode consists of a Node.js server API and an Electron desktop client, with mobile apps coming soon. 
  - 🏘️ Everything in Colanode is represented as a node (e.g., message, file, folder, chat, channel, database, record), each with specific attributes and permissions. 
  - All reads and writes performed by the desktop client happen locally within a SQLite database, and changes sync seamlessly via a synchronization engine built on top of SQLite, Postgres, and Yjs—a CRDT library for conflict resolution. 
  - The server then propagates these changes to other collaborators. You can self-host the server in any environment using Docker, Postgres, Redis, and any S3-compatible storage, and connect using the official desktop client, which supports simultaneous connections to multiple servers and accounts. 
  - This local-first approach also prepares us for future integrations with fully local LLMs, further enhancing privacy and performance.
- 📱 we do plan to implement mobile apps, but we don't have a concrete timeline yet. It depends on the limitations and challenges we might face when we implement the same local-first approach as we did in desktop (full offline support, background syncing etc).

- Here an example of it taking arbitrary input and blindly casting it to a type; anything after this point can blow up. There seems to be no input validation anywhere.
  - And the database use looks racy(improper or indecent), sometimes not using transactions at all but having a read-modify-write cycle, no GET FOR UPDATE seen anywhere in transactions. Somebody is going to figure out how to do nasty things to the data.

- do real time cross platform notifications work? If yes, how did you solve this for people self hosting?
  - That's a great question! We didn't come to it yet, because we are focused only in desktop app for now. This is definitely one of the challenges we need to solve once we start working on the mobile apps. The self-hosting use case makes it tricky (and probably fun challenge to solve).
- Having used several real time self hostable apps with chat (Nextcloud, Odoo, Rocket chat) this is the hard problem to solve.
  - Rocketchat uses it as a way to funnel you into paying.
  - Nextcloud runs their own server for free, but you have to accept that you'll be sending data via their server. 
  - Odoo, I don't think I ever got notifications working.
  - I have researched other apps: Mattermost does something similar to Rocketchat, using notifications as a sales funnel. Element is similar to Nextcloud, they host their own free server, although I think you can self host that too.
  - From this experience, I would never try a new app until they have this feature solved, clearly documented, and with proof that it works and isn't a sales funnel.
- Can you elaborate on this? I manage a Mattermost instance and there are some features missing from the OSS self-hostable community edition, but notifications seem to mostly work, even on mobile where notification delivery does rely on their gateway
  - When hosting and using their free notifications service, you're basically using their test server with no uptime guarantees. I agree that there's only so much you can expect from a free service, but unreliable notifications make a chat app 100% useless for any serious work.
- https://zulip.com is decent. Self hosted free plan has mobile notifications for organizations with up to 10 users

- Notion is a tragedy when it comes to export or migration. I didn’t see any bragging about the exportability of content from this one, but that’s the main thing I look for now.
  - We don’t have export or migration features in place yet, but we are planning to add them.

- ⛓️ Have you thought about adding programmable logic or automations between nodes?
  - My 2c: A particular thing about notion that bugs me is that hn page content get imported as simple tables and in notion there is no automated way to delete all empty cells of all tables on page, that make it unreadable, or just to convert tables automatically into text

- 🆚 How does this compare to Huly?
  - from a quick look (and a test I did some time ago) it seems to take a more opinionated approach: features such as issues, projects, and overall layout are pre-defined. 
  - Colanode, by contrast, works like Notion, giving you flexible building blocks so you can model your own workflows and knowledge structures. 
  - Another key distinction is tech architecture: Colanode is built around a local-first design, providing full offline support with background syncing. I haven’t found equivalent offline capabilities documented for Huly, even though they may have them.

- 🆚 How does this compare to Notesnook?
  - I haven’t used Notesnook personally, but from their description it focuses mainly on note-taking. 
  - Colanode, by contrast, also includes collaboration features such as chat, file sharing, and databases. 
  - One other difference is that Notesnook offers end-to-end encryption, whereas Colanode does not (at least for now).

- Is there a name for this new-age method of notes/webpage/data productivity genre? They all seem to have "write with /" to insert "block" content.
  - The term I'm familiar with is "outliners", as is used by Logseq
  - Block-based editors maybe?

- Is the Electron app a necessity or is using a browser possible as well?
  - For now, Colanode is available only as a desktop app (Electron). The primary reason is that we wanted to implement some local-first features, which are currently more complex to achieve in the browser.

- ## From thousands of files to two SQLite databases: the story how @Colanode ships 8K emojis and icons that work fully offline. _202501
- https://x.com/hakanshehu/status/1885332261265916131
  - While building it we had an interesting challenge: how do we include over 8, 000 emojis and icons, keep them all fully searchable, and ensure everything works even when users are completely offline?
  - In a local-first app like Colanode, there’s no relying on CDNs or external sources. Every asset: messages, documents, files, and even emojis and icons, needs to be available locally at all times. That way, users can keep collaborating and customizing their experience without the internet. We wanted to offer a rich library of emojis for reactions and icons for pages, but shipping thousands of small image files in our Electron-based desktop app was tricky.
  - Initially, we thought: why not just include all emoji and icon files in the repository? But adding thousands of SVGs directly to Git quickly became cumbersome and wasn’t a pleasant developer experience. Plus, we needed a better way to search through all these assets by keywords and categories.
  - One day I wash watching a talk by the creator of SQLite where one thing he said stood out: “SQLite can be faster than the file system for certain use cases, especially when dealing with many small files.”
  - We built a script to merge different emoji and icon sets into a consistent data model, then load them into two SQLite databases, one for emojis, one for icons. As part of this process, we: generate a unique id for each asset, add metadata such as category, tags, and keywords and index everything for lightning-fast text search
  - When it’s time to package the Colanode desktop app, we simply include these two SQLite databases. In effect, we’ve bundled more than 8, 000 assets in just two files. Although the total size is the same, the experience and performance is much better. It makes even the developer experience easier where we need to keep track of just two files and can easily update the icons and emojis later.
  - Since Colanode is open source, all the scripts for building these databases are up in our public repo. Check it out in Github
