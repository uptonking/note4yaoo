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

## [Introduction to Loro's Rich Text CRDT – Loro_202401](https://www.loro.dev/blog/loro-richtext)

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
# discuss
- ## 

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
