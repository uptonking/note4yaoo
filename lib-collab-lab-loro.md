---
title: lib-collab-lab-loro
tags: [collaboration, crdt, loro]
created: 2024-01-06T15:36:32.941Z
modified: 2024-01-06T15:37:08.031Z
---

# lib-collab-lab-loro

# guide

# dev

# blogs

## [Introduction to Loro's Rich Text CRDT – Loro _202401](https://www.loro.dev/blog/loro-richtext)

- This article presents the rich text CRDT algorithm implemented in Loro, complying with Peritext's criteria for seamless rich text collaboration. 
  - Furthermore, it can be built on top of any List CRDT algorithms and turn them into rich text CRDTs.
- Above is an online demo of Loro's rich text CRDT, built with Quill. 
  - After the replay, you can simulate real-time collaboration and concurrent editing while offline. 
  - You can also drag on the history view to replay the editing history.
- Loro is based on the Replayable Event Graph (REG) algorithm proposed by Seph Gentle, but this algorithm cannot integrate the original version of Peritext. 
  - This motivates us to create a new rich text algorithm. 
  - It is independent of the specific List CRDTs, thus working nicely with REG, and is developed on top of them to establish a rich text CRDT.
- Reconstructing history might seem time-consuming, but REG can backtrack only some. When merging updates from remote sources, it only needs to replay operations parallel to the remote update, reconstructing the local CRDTs to calculate the diff after applying remote operations to the current document.
  - The REG algorithm excels with its fast local update speeds and eliminate concerns about tombstone collection in CRDTs.
# discuss-stars
- ## 

- ## 

- ## 

- ## [Movable tree CRDTs and Loro's implementation | Hacker News _202407](https://news.ycombinator.com/item?id=41099901)
- https://thymer.com We're building a new multiplayer editor for tasks/notes which supports both text and outliner operations. Although it behaves like a flat text document, the outliner features essentially turn the document into a large tree under the hood. We do something similar to the highly-available move operation to sync changes
  - There is one operation to change the tree, called insmov (move-or-insert). Whenever a client is online it can sync changes C to a server.
  - We don't use any fractional indices though. Instead, our insmov tuple not only contains a parent P, but also a previous sibling guid A. Because all tree ops will eventually be applied in the global linear order as determined by the server, "sorting" is handled by just using the insmov operation.
- For what it's worth, this sounds equivalent to the RGA list CRDT, using the server's global linear order as a logical timestamp (in place of e.g. Lamport timestamps).

- I have open sourced React Table Library with the focus on tree operations. They are handling a folder/file tree structure of 100 thousands nodes where it is possible to move folders/files, clone them, lazy load them on a top and nested level, etc. And all of it in the same table structure. After I finished the project, I kinda knew why Google Drive only allows to display and modify on the same hierarchical level. There are so many constraints that you have to consider when implementing this in a nested view with many nodes.

- When working with formatted text content like in Google Docs / Zoho Writer: moving a list item down or adding a new column or any table/list operation is essentially a tree manipulation op. Concurrent conflicts in such cases are notoriously hard to converge without contextual special handling. Does this implementation generalize a solution for such use-cases? 
  - I guess it should be possible to combine a list(or string) CRDT for leaf nodes (i.e text blocks) and use this tree CRDT for structural nodes (lists & tables). But that will make augmenting every op with two-dimensional address (parent-id, index_offset_into_that_parent)
- 🤔💡🌲 That’s always how I’ve imagined it. Rich text is plain text with 2 additions: Annotation ranges (for bolded regions and such) and non-character elements (Eg a table or embedded image). A text crdt is fundamentally just a list crdt that happens to contain character data. So embedded elements can easily be modelled as a special item (the embedded child node), and with size of 1 like any other item in the string. And then with the right approach, you can mix and match different CRDTs in a tree as needed. (Rich text, contains a table, and one of the cells has an image and so on).
  - Augmenting every op with a parent-crdt-id field is unfortunate but I think unavoidable. Thankfully I suspect that in most real world use cases, it would be very common for runs of operations to share the same parent crdt. As such, I think those ID fields would run-length encode very well.

- The implementation can indeed combine multiple different CRDTs. Within Loro's internal implementation, each op does need to store a parent ID. However, as Seph mentioned, consecutive operations under the same parent can be effectively compressed, so the amortized overhead of these parent IDs is often not significant.

- I wonder if there has been any practical CRDT for data dense applications, such as images (pixels) and 3D models?
  - With any collaborative application, you need to start with a conceptual framework for the edits a user may perform, and how to best preserve the intention of the user (1) and the coherency of the resulting document (2) when any such edits may occur asynchronously. 

- ## [Loro's rich text CRDT | Hacker News _202401](https://news.ycombinator.com/item?id=39102577)
- I invented replayable event graphs. 
- If you remove these ops from history, does that remove the ability to time travel
  - Yes it does. You also need the ops from history to be able to merge changes. You can only merge changes so long as you have the operations going back to the point at which the fork happened.
- is it possible to put the removed historical/tombstone ops into a "cold storage" that's optional and only loaded for time-travel use?
  - Absolutely. And this is very practically useful. For example, you could have a web page which loads the current state of a document (just a string. Unlike CRDTs, it needs no additional metadata!). 
- All this said, with text documents the overhead of just keeping the historical operations is pretty tiny anyway. 
  - In my testing using diamond types (same algorithm, different library), storing the entire set of historical operations usually increases the file size by less than 50% compared to just storing the final text string. Its much more efficient on disk than git, and more efficient than other CRDTs like automerge and Yjs. 
  - So I think most of the time its easier to just keep the history around and not worry about the complexity.

- Similar to OT, in certain scenarios, it's sufficient to ensure that only a subset of peers have the complete data, while others don't need the full history. 
  - For instance, in real-time collaboration scenarios with a central server, we can, just like OT, allow clients to hold only a shallow clone instead of the complete history. 
  - This approach results in minimal overhead for the clients.

- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Synchronizing tree structure movements (like moving folders) has always been a challenging problem
- https://x.com/zx_loro/status/1817926647338983555
- Any reasons why you chose to use 128 as a "terminator" element instead of 255? I believe the article Bartosz talks about uses 255 as the maximal element (which seems to make sense when you are operating on the raw bytes level).
  - We forked https://github.com/jamsocket/fractional_index and made some extensions. This implementation is also 256 base. Uses 128 as the terminator because 128 will always be at the "end" of each fractional index. 

- ## 🆔️ An idea for storing the mapping between PeerID and application-level User ID in Loro documents:
- https://x.com/zx_loro/status/1818247647830081607
  - Since each PeerID in Loro is 64 bits, we could lock the first 32 bits to a specific user, for example, by calculating this value using a collision-resistant hash based on the user's email. The remaining 32 bits would be random. This would allow us to store the mapping between PeerID and application-level user ID at a very low cost.
  - However, this reduces randomness and increases the possibility of collisions of PeerIDs
  - The main issue I'm trying to solve is how to best map application-layer user IDs to CRDT PeerIDs. This information is important when developing related tools. One good option might be to create a dedicated CRDT type for this purpose.

- I would strongly advise against using identifiers that short. You really want astronomically low chances of conflict even with 1000s of participants - and no extra coordination.
  - @jazz_tools / CoJSON uses 19 byte account IDs + 8 byte session IDs
- Why 19 bytes for account ID? The most widely used UUID formats use 16 bytes with very low chance of collisions. Have you found 128 bits to be not enough in practice with Jazz?
  - IDs double as a cryptographic hash as well (truncated BLAKE3). Doesn’t need full blown preimage resistance because there are other checks, but just in case I went over the recommended 128bits as an absolute minimum there, without going full 32bytes, which is annoyingly long
- Oh, I see. Makes sense.

- ## For this meetup, we built this demo of importing the whole @loro_dev git repository into a single Loro document. 
- https://x.com/zx_loro/status/1805095256461115623
  - It contains 1300+ commits and 10M operations in CRDT history, and we can switch to any version in the history.
  - Every switch will trigger the diff calculation from the start version to the target version. It's not optimized yet, so it's kind of slow. And it's still in memory, so it cannot hold an enormous repo.
  - But it's a proof of concept that we may be able to build a better git for everyone and everything on top of CRDTs.
  - It's for everyone because we can combine the async collab with the real-time collab and make it much easier for entry-level usage. It's for everything because it's now not limited to plain text.

- 
- 
- 

- ## [[LORO-300] Fractional index _202311](https://github.com/loro-dev/loro/issues/140)
- 👷🏻202401: It's dropped. The fractional index suffers from interleaving problems. We will try building a movable list this season that can avoid this problem while remaining efficient. We hope to integrate it into tree as well.
  - The other reason we drop it is that the fractional index the solution can be implemented in the application code. It doesn't require special CRDT behaviors(LLW register is enough), so we can already use it with the current movable trees.

- Fair enough. Interleaving is OK for me, but I see that it can be a problem for others.

- ## In Loro, we maintain this property: 
- https://twitter.com/loro_dev/status/1773591628927598888
  - given the distance between versions A and B as m and the total number of operations in the document as n, the cost of computing the difference from version A to version B is O(m log n) instead of O(n log n).
  - Versions A and B can be arbitrary without requiring version B >= A. 
  - This allows us to perform fast version difference comparisons and supports undo/redo based on them.

- ## 💡 There's an alternative approach to rich-text formatting, keeping the formatting outside of the text
- https://discord.com/channels/1069799218614640721/1168069498918670336/1193907169708494898
  - Instead of embedding style information within the text, one would have a "stylesheet"* outside of the text that maps from relative positions to style information. Unlike HTML/CSS (and Peritext, Markdown, etc), where text is marked up for styling inline, the text would be plain and decoupled from its formatting. 
  - When formatting a text, the editor would only operate on the stylesheet (a specialized CRDT?), assigning styles to the current relative positions (start, end) in the text. To render the formatted text, editors/viewers would apply the stylesheet to the plain text.
  - One can think of it as a more basic CSS where instead of selectors you have pairs of relative positions ([start, end]) for spans of text and their formatting data (strong, italic, size, color, link, etc).
  - Some benefits: Separation of concerns. Text is pure text, less overhead. Ability to disregard formatting and load only plain text. Possibility of a specialized CRDT for stylesheets, with optimizations?
  - Possible drawbacks: Requires efficient and dependable relative positions. Higher memory/storage? More difficult to implement for editors/viewers?

- I think so you just described `Peritext`, styles are applied based on boundaries (like start and end)  and mostly decoupled from the text document except for the relative position (CRDT Semantic ID.) 
  - This is how the initial implementation of Loro stored this boundaries (called annotations in the diagram):
- you can develop a rich text algorithm using relative positions. 
  - Peritext fundamentally depends on them. However, it requires specific attention in scenarios involving tombstones. As a result, it's not completely detached from the base plain text CRDT algorithms. Peritext also supports storing the formatting outside the text.
  - 🧐 Loro has adopted a new rich text algorithm that meets the testing requirements outlined in the Peritext paper. It's compatible with the Replayable Event Graph and doesn't incur extra costs (in terms of memory, storage, or computing power) when styles aren't used. When styles are present, it supports all the behaviors of plain text. 
  - Could you share why you'd prefer to store styles separately? I'd like to explore how to design the API to better address these needs.
- I see that you have explored what I described, so that answered my question. Nice! Too bad it didn't work out.
  - My motivation for separating markers from plain text is that, like Ink&Switch, I'd like to use it for more than just formatting. Linking is my main use case (links are not formatting, as I see it).
  - I'm inspired by Ted Nelson's Xanadu (上都), again inspired by Vannevar Bush's Memex, where a link is much more powerful and expressive than the simple "jump link" we're used to from the web. 
  - In more powerful hypertext systems, a link is not just a one-way link embedded in the document, but a two-way link between positions/spans on both sides, stored as a separate entity outside the document, forming a graph.

- Giving it some more thought, I think I'm conflating two phases – editing and viewing.
  - I may not have a need to store formatting/marks outside the text anyway. I'd only need a relative position API. It would be nice to get a set of all marks in a text, with relative positions of each span
- I understand your objective. In this scenario, an API for Relative Position is probably sufficient, and the impact of tombstones can likely be ignored. The same result could be achieved through the built-in style API, which might simplify rendering. Additionally, it also allows for the export of bidirectional links
  - Using Relative Position to represent styles also supports time travel capability, as these positions adjust with content changes. Removing style information from a Snapshot can be challenging, but the size occupied by these styles is generally small
- For the storage format, I suggest saving snapshots at longer intervals, and saving a separate incremental update every few keystrokes

- you're looking for an API that can squash updates, similar to the behavior of Git's squash merge
  - Since our current design is already capable of computing the Diff from version A to B (by checking out from version A to version B, you obtain the events that occurred during this transition.), we only need to convert the Diff into updates to achieve a squash-like behavior. This isn't difficult to support, and we can include this feature in the future. For now, this functionality can also be implemented in application code (but it may be too complicated)

- ## [Loro: Reimagine state management with CRDTs | Hacker News_202311](https://news.ycombinator.com/item?id=38248900)
- The demo code for Loro looks very easy to use, I love how they infer a CRDT from an example plain JS object. I’ve played with a Zod schema <-> Yjs CRDT translator and found it kinda annoying to maintain. 
  - However this looks so easy I worry about apps building with too little thought about long term data modeling. 
  - Migrations on CRDTs are challenging, so it’s important to “get it right” at the beginning. 
  - I’m curious how this design works with longer term, more complex CRDT apps.
- The code in the blog is from Vue Pinia, a state management library, and not from Loro. It serves as an example demonstrating that CRDTs can be modeled similarly. Thus, you might expect to use Loro in a similar way.
  - Indeed, schema migration is challenging. There is a lot to explore, both in reducing the need for migration and in ensuring a smooth transition when it's required. We plan to tackle this issue in the future.
- Any tips or dos/don'ts you could share for how to "get it right" at the beginning? 
  - I don’t have anything better for you than “be careful” and “prototype a lot”. Adding new fields is fine, changing the meaning or type of existing fields is annoying.
  - 🧐 It’s more challenging because you need to accept updates in format v1 indefinitely even after you apply the v1->v2 migration, which makes it more like maintaining an API with backwards compatibility than the usual SQL migration pattern.

- I wonder if this is something that can be used for versioning database columns / fields.

- We've been using https://github.com/electric-sql/electric for real-time sync for the past month or so and it's been great. Rather than make you think about CRDTs explicitly, Electric syncs an in-browser sqlite db (WASM powered) with a central postgres instance. As a developer, you get local-first performance and real-time sync between users. And it's actually faster to ship an application without writing any APIs and just using the database directly. Only downside is Electric is immature and we often run into bugs, but as a startup we're willing to deal with it in exchange for shipping faster.
