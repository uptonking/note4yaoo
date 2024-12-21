---
title: lib-collab-powersync-community
tags: [collaboration, community, powersync]
created: 2024-02-12T03:22:48.188Z
modified: 2024-02-12T03:23:17.007Z
---

# lib-collab-powersync-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️ How does WatermelonDB compare to PowerSync, based on your experience? _202311
- https://x.com/bndkt/status/1721652131026042893
- They're pretty different in their approaches. 
  - WatermelonDB only handles the part locally on the device, it includes a SQLiteDB and provides changesets to you (and expects changesets back). How to reconcile the changesets with a backend is for you to figure out and implement. 
  - PowerSync goes much further, it includes a server component where you define "Sync Rules" and PowerSync handles all the syncing for you, including the hard parts of figuring out which data has changed and what parts of data to send where.

- ## 🚀 [PowerSync - Show HN: Bi-directional sync between Postgres and SQLite | Hacker News _202311](https://news.ycombinator.com/item?id=38473743)
- PowerSync Service handles the complexities of dynamic partial replication of the database to different users. In our announcement blog post we wrote a bit more about the trade-offs and design considerations
  - see section "A scalable dynamic partial replication system"

- You can try Watermelon DB. It is local first disconnected framework. And it has a sync framework as well, but you have to create your own backend (using any DB) for syncing.
- 🆚️ Watermelon has its limitations for an offline applicationFirst, if you really want to make use of the application completely offline, you will have to build a synchronizer like CRDT by hand and manage the request queues. 
  - With powersync all of this is managed by them, and with a simple code I can choose which information from the database I will sync for each user. 
  - In my first tests with WatermelonDB, synchronization proved to be unfeasible due to the amount of synchronized data. 
  - In short, Powersync has proven to be a wonderful tool that has allowed my company to move forward with offline services.
# discuss-news
- ## 

- ## 🎯 v1.0.0 of our Docker image for self-hosted PowerSync _20241128
- https://x.com/powersync_/status/1862131536293757243
  - This release introduces a major refactor of the PowerSync Service to support modular replication, along with initial alpha support for MongoDB and MySQL source databases.

- ## PowerSync joins @getsentry @gitbutler @convex_dev and others in adopting the FSL for our Open Edition. _20240606
- https://x.com/powersync_/status/1798702381967806523
  - FSL gives freedom to copy, modify and redistribute. 
  - It disallows providing a paid competitive offering. It also converts to permissive open-source in 2 yrs.

- ## 🚀 Announced at @localfirstconf : PowerSync Open Edition: __20240531
- https://x.com/powersync_/status/1796462870340714871
  - a free, self-hosted, source-available version of PowerSync that contains all the same core functionality as PowerSync Cloud and Enterprise Self-hosted. 
  - Does not include the PowerSync Dashboard.

- Key features of PowerSync's design and architecture:
  - https://x.com/powersync_/status/1798339236665413879
  • Dynamic partial replication, deduplicated for high scalability.
  • Checkpoint system for consistency guarantees.
  • Checksum system for data integrity.
  • Wide client platform/framework support.

- https://x.com/powersync_/status/1796599179143524589
  - This is what a successful PowerSync self-hosted deployment looks like

- ## PowerSync is officially out of Beta! _20231130
- https://x.com/powersync_/status/1730234674117546174
  - We built a live demo to show how it works (that uses @supabase !)

# discuss-collab-crdt/ot
- ## 

- ## 

- ## “One of the (perhaps surprising) key decisions about the PowerSync architecture was not to use CRDTs to merge changes”
- https://x.com/powersync_/status/1730698638681067633
  - It's possible/optional to use CRDTs on top of PowerSync + Postgres (akin to pg_crdt), but the PowerSync internal protocol does not actually use CRDTs to merge changes.

- [Introducing PowerSync v1.0: Postgres<>SQLite sync layer _202311](https://www.powersync.com/blog/introducing-powersync-v1-0-postgres-sqlite-sync-layer)
  - One of the (perhaps surprising) key decisions about the PowerSync architecture was not to use CRDTs to merge changes. 
  - A quick primer just in case: CRDTs are data structures where all operations are commutative, meaning they can be applied in any order on different replicas of the data, and each replica converges to the same state. This is useful for syncing data peer-to-peer, but the downside is that CRDTs come with significant overhead and more complexity
  - an alternative to CRDTs is to keep a global ordered list of operations/events. By applying operations in the same order on each replica, they converge to the same state.
  - having an authoritative server in a system architecture means that a global ordering of operations can be enforced, typically without adding much complexity to the system.
  - With PowerSync, writes are sent through the developers’ own application backend, allowing them to apply their own business logic, fine-grained authorization, validations and server-side integrations.
  - While PowerSync does not use CRDTs for its internal protocol, it can leverage another important strength of CRDTs: very fine-grained collaboration like document/text editing. CRDTs can actually be implemented on top of PowerSync + Postgres for collaborative document editing: For example, using Yjs and storing its CRDT data structure in Postgres using blobs, and keeping it in sync between clients in real-time
# discuss-sync-solutions
- ## 

- ## 

- ## 

- ## We built Y-Sweet to be the zero-lock-in sync engine, so it uses your storage as the source-of-truth.
- https://x.com/JamsocketHQ/status/1863589701765960122

# discuss-sync
- ## 

- ## 

- ## When we built PowerSync using @PostgreSQL logical replication, we ran into some challenges making the PowerSync architecture compatible with logical replication assumptions. _20240509
- https://x.com/powersync_/status/1788582123424604223
  - @cahofmeyr 's post explores some of those challenges and how we solved them, including:
  - Handling schema/DDL changes
  - LSNs that overlap between transactions
  - Accessing TOASTed values
  - Handling different row identifier permutations
- [Postgres logical replication challenges & solutions _202405](https://www.powersync.com/blog/postgres-logical-replication-challenges-solutions)
  - [Postgres Conf 2024: Local-first apps using Postgres logical replication - YouTube](https://www.youtube.com/watch?v=mPrM6lnd5wU)
  - [Inside logical replication in PostgreSQL: How it works _202303](https://www.postgresql.fastware.com/blog/inside-logical-replication-in-postgresql)

# discuss-internals
- ## 

- ## 

- ## 

- ## Decoupling the write path from the read path is NB for flexibility.
- https://x.com/powersync_/status/1829145650564378777
  - Writes are applied directly to the local SQLite db, then also placed into an upload queue.
  - Our client SDK sequentially processes writes in the upload queue using an `uploadData()` function defined by the developer.
  - So, developers control how writes are applied to Postgres, typically via their backend API.

# discuss
- ## 

- ## 

- ## 

- ## Instantly reflect backend changes in your app w/ built-in real-time streaming:
- https://x.com/powersync_/status/1853416575598051522
  - Backend data changes stream from PowerSync Service to SDK clients via HTTPS
  - With watch(), on-device SQLite changes stream to your app UI
  - Offline? Streaming pauses, resumes once reconnected.

- ## 🆚️ Electric has changed its approach and trying to do it similar to powersync now(pg + pglite). They've depreciated their original repo _202409
- https://x.com/AkshitBanta/status/1836363683762454587

- ## What developers/owners fear is vendor lock-in and technical debt. 
- https://x.com/powersync_/status/1742206272676475324
  - @supabase and @powersync_ both are taking a hands off approach to the database at least in comparison to what other companies are doing. Couldn't think of a better partner than Supabase for PowerSync

- ## 🛢️📡 PocketBase uses SQLite as its backend database, and PowerSync doesn't support that as a backend database at this time 
- https://x.com/powersync_/status/1754540130767863917
  - (currently only Postgres is supported on the backend, while SQLite is supported on the client). 
  - It may be possible for PowerSync to support SQLite on the backend in the future, but there aren't currently near-term plans for this.
- One of the things we'd need to replicate from SQLite is support for Sessions. Not sure if pocketbase supports that
- You would use @litestreamio for that though right?
  - Nope, that streams the WAL from place to place, but we actually need something that builds up CDC for us (which is what Sessions does). This is because we provide dynamic partial replication, not just full sync of the entire DB

- ## How to build infinite scrolling with local-first?
- https://x.com/powersync_/status/1779888442161135654
  - You can sync a larger data set and query data from the local SQLite database. Or you can use "lazy-loading" or "lazy-syncing" techniques to get data from your backend.
- We've documented 4 options 

- ## If you're curious about building local-first, YSK about dynamic data partitioning.
- https://twitter.com/powersync_/status/1763579694220259533
  - Unless all data should be shared across all users, you need a system that controls which data gets replicated to which users' local databases.
  - For this we have Sync Rules, a system that creates "data buckets" (akin to live views) of exactly the data that each app user should have access to, at any point in time. Put differently, Sync Rules create dynamic data partitions.
  - For example, if a user creates a new record, their data bucket dynamically grows to include that record. If that record should be shared with any other users, their data buckets will dynamically adjust as well.

# discuss-license/open-edition
- ## 

- ## 

- ## 
# discuss-electicsql
- ## 

- ## 

- ## [Electric (Postgres sync engine) beta release | Hacker News _202412](https://news.ycombinator.com/item?id=42383136)
- This is how DuckDB is structured too:
  - DuckDB Labs: The core contributors. Instead of developing features that will be behind a paywall, they provide support and consulting.
  - DuckDB Foundation: A non-profit that ensures DuckDB remains MIT licensed.

- This is really amazing as is their standalone pglite project, which is a WASM port of Postgres. 
  - One surprise for me though is that Electric is a read only replica. In particular, “Electric does read-path sync. It syncs data out-of Postgres, into local apps and services. 
  - Electric does not do write-path sync. It doesn't provide (or prescribe) a built-in solution for getting data back into Postgres from local apps and services.
- We hit on exactly the same pattern for our product and it works really well. We use Hasura as the read engine. That updates a graph of mobx objects that drive the ui. We apply updates directly to those objects so the ui updates immediately. The mutations are posted back to a Python api that applies them to the db.

- The ElectricSQL concept of 'shapes' is interesting.
  - In my experience, the "outbox" approach means a lot more manual work for developers. It requires developers to create a message for every type of change they want to sync to the client, and then also interpret that on the client. 
  - ElectricSQL's Shapes does a lot more work to keep the shape in sync between the client and the server, reducing the need for the developer to do that work.
  - 👷🏻 You're right that "single-table sync" does have its limitations. At PowerSync we effectively support one level of "joins", and even then it's often not enough for more complex schemas. An older version of ElectricSQL did also actually have multi-table shape sync support, but I believe doing that at scale proved to be difficult.
  - One solution to this is often denormalizing data - either adding more denormalized columns in the existing table, or creating new tables dedicated to sync data. Conceptually, keeping these tables up to date is not that different from writing updates to an outbox table.
