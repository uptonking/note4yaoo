---
title: lib-collab-lab-peritext
tags: [automerge, collaboration, crdt, peritext, prosemirror]
created: 2023-06-15T02:05:59.639Z
modified: 2023-09-01T05:13:55.075Z
---

# lib-collab-lab-peritext

# guide

# examples
- https://github.com/inkandswitch/peritext /MIT/ts
  - https://www.inkandswitch.com/peritext/
  - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
  - Peritext builds upon RGA, which is similar to Causal Trees, although our algorithm could use any of these plain text CRDTs with minor adaptations. 
  - This repo includes:
    - A Typescript implementation of the core Peritext CRDT algorithm
    - A prototype integration with ProseMirror editor
    - An interactive demo UI where you can try out the editor
  - forks
  - https://github.com/philschatz/peritext
    - 更新了版本、迁移到vite、基于automerge-wasm

- https://github.com/loro-dev/crdt-richtext /169Star/MIT/202305/rust
  - https://crdt-richtext-quill-demo.vercel.app/
  - Rich text CRDT that implements Peritext and Fugue
  - This CRDT lib combines Peritext and Fugue's power, delivering impressive performance specifically tailored for rich text. 
  - It leverages the `generic-btree` library to boost speed, and the `serde-columnar` simplifies the implementation of efficient columnar encoding.
  - loro-wasm and fugue only support plain text for now
  - This crate contains a subset of Loro CRDT(which is not yet open-source)
  - [The Art of the Fugue: Minimizing Interleaving in Collaborative Text Editing](https://arxiv.org/abs/2305.00583)

- https://github.com/jaredly/local-first/tree/master/packages/text-crdt
  - This algorithm is largely based on RGA, with support for rich-text formatting added, along with a number of optimizations.
  - integrate with Quill.
  - Your approach seems to resemble RGASplit which I believe is bases for
  - Hybric Logical Clocks was very much based on [this go implementation] and [james long's demo]
# issues
- [Peritext algorithm may attach deleted mark to new inserted text](https://github.com/inkandswitch/peritext/issues/32)

- [What could be the direction for making Peritext support block elements](https://github.com/inkandswitch/peritext/issues/27)
  - I helped design a convergent data model for tables at Notion recently that would work well using 3 convergent data types: Map (to group and address fields), Ordered Set (for defining the order of rows and the order of columns), and Rich Text (for defining the contents of cells).
# dev

# blogs

## [Peritext: A CRDT for Rich-Text Collaboration_202111](https://www.inkandswitch.com/peritext/)

- [cscw-pdf](https://www.inkandswitch.com/peritext/static/cscw-publication.pdf)

- The key idea is to **store formatting spans alongside the plaintext character sequence**, linked to a stable identifier for the first and last character of each span, and then to derive the final formatted text from these spans in a deterministic way that ensures concurrent operations commute.

- ot drawback
  - all known OT algorithms for rich text require a **central server** to mediate(调解) edits.
  - This limits scalability, precludes peer-to-peer decentralized sharing, and limits the flexibility of branching and merging workflows on a document.
  - 不支持offline编辑后合并
  - ot转换是synchronous实时的，难以支持分支合并

- we present a novel CRDT called Peritext with the following four contributions:
  - We demonstrate how naively extending existing plaintext or tree CRDTs does not accurately preserve user intent in the context of rich text editing. 
  - We propose a general model of intent preservation in collaborative rich text editing, using a series of example scenarios
  - We describe a novel CRDT for rich text called Peritext that satisfies all the criteria of our model for intent preservation. 
  - We show that Peritext complies with a widely-used consistency model for collaborative editing

- Peritext supports both real-time and asynchronous collaboration
  - it does not yet visualize differences between document versions.
- In this paper we focus only on inline formatting such as bold, italic, font, text color, links, and comments, which can occur within a single paragraph of text. 
  - In a future paper we will extend our algorithm to support block elements such as headings, bullet points, block quotes, and tables

- Rich text is often represented as a tree structure such as HTML, XML, or JSON
  - However, generic tree algorithms are not suitable for rich text collaboration because concurrent edits to the tree can result in anomalies.

- Many CRDTs for plain text have been proposed
  - woot, logoot, treedoc, rga, lseq, yata
- Peritext builds upon RGA, which is similar to Causal Trees, although our algorithm could use any of these plain text CRDTs with minor adaptations.
  - All of these algorithms work by assigning a unique identifier to each character.

- Ritzy uses the Causal Trees CRDT as the underlying data model for the sequence of characters. 
  - Each character is extended with an `attributes` property containing the formatting (e.g. bold, italic) of that character. 
- yjs adds formatting by embedding **hidden control characters** in the sequence of characters to denote the beginning and end of formatting spans, for example “start bold” or “end bold.”
  - The general problem with control characters it that they make it difficult to represent changes of formatting over time. 
  - When partially overlapping spans of text are toggled between bold and non-bold several times, control characters tell us where a span begins or ends, but they do not tell us which formatting is older and which is newer.
- Citrea/Papyrus is similar to Peritext in that it stores formatting annotations outside of the document text by referencing the unique identifier of the first and last character of the formatted span. 
  - However, unlike Peritext, it does not support different policies for text insertion at span boundaries
- Another approach would be to use a tree-structured representation of formatted text, akin to HTML, XML
  - For example, Automerge provides a CRDT that can store a JSON object with nested maps and lists. We could store each contiguous span of formatted text as an object containing the string text contents and a list of format markers
  - Unfortunately, when we use the Automerge semantics for merging JSON documents, this representation does a poor job at preserving user intent. 比如`删除+改样式`会合并为添加新元素和新样式
  - The problem here is that users intended to only change the formatting, but their actions were represented in the JSON document in a way that suggested they were also modifying the text content. 

- a model of intent-preserving merge behavior
  - Concurrent formatting and insertion
  - Overlapping formatting
  - Text insertion at span boundaries
  - Generalizing to other mark types

- The formatting types we have described can be categorized along two axes:
  - Can marks overlap?
  - Do marks expand?

- peritext: We describe our algorithm in four parts:
  - Representing the textual content of a rich text document using an existing plain text CRDT
  - Generating CRDT operations representing formatting changes
  - Applying these operations to produce an internal document state
  - Deriving a document suitable for a text editor, based on the internal state 

- Our text crdt implementation uses RGA/Causal Trees as its basis, although in principle it could extend any plain text CRDT
  - Our document model stores a Boolean flag alongside each character, which becomes True when the character is deleted. 
  - Deleted characters remain in the document model as tombstones, which are needed to handle concurrent edits.
- Every operation that modifies the state of the document is given a unique, immutable identifier called opId (operation ID). 
  - An opId is a Lamport timestamp; we write it as a string of the form `counter@nodeId`
  - Whenever we make a new operation, we give it a counter that is one greater than the greatest counter value of any existing operation in the document, from any client.
  - if counter1 == counter2 we break ties using a string comparison of node1 and node2.

- The key idea of most text CRDTs is to represent the text as a sequence of characters, and to give each character a unique identifier
  - To determine the position where a character is inserted, we always reference the ID of the existing character after which we want to insert, because these IDs remain stable over time.
  - If two users concurrently insert at the same position (i.e. with the same afterId), we order the insertions by their opId to ensure both users converge towards the same sequence of characters.
- Larger operations, such as cutting or pasting an entire paragraph, turn into many single-character operations.

- We must ensure that applying concurrent operations is commutative: 
  - when two operations were generated concurrently, we can apply those operations in any order, and the resulting document must be the same.

- for the purposes of determining the current formatting of a document, it is not strictly necessary to store the sets of all historical formatting operations
  - However, storing the set of formatting operations is useful if we want to compute what a document looked like sometime in the past, for the purpose of visualizing the differences between versions of a document. 
  - Although the current version of Peritext does not support this feature
- Not all mark types are mutually exclusive—in the case of comments, it is possible for several comments to be associated with the same span, and thus we retain all of the comments

- We have described a “from-scratch” method for iterating over all the spans in a document and producing a current document state
- we have implemented an incremental approach to sending updates to the text editor UI. 
  - The key idea is to augment the process of applying an operation: in addition to updating the internal op-sets, we also produce patches that describe the effects of that operation on the publicly visible formatted document.
- Note that patches use indexes, whereas operations use opIds to identify positions in the text. 
  - This is fine because patches are only used to propagate updates from the CRDT to the text editing UI; 
  - by running the CRDT logic on the same thread as the UI, we can avoid having to handle concurrency between these two components.

- We have implemented a working prototype of the Peritext CRDT in TypeScript. 
  - Our code is based on a simplified version of the Automerge
- We have tested random edit traces of over 5000 operations being exchanged between three peers without violating convergence. 
  - This gives us confidence that the implementation is correct
  - A formal proof that our algorithm converges is presented in AppendixA.
- We also expect that Peritext would integrate well with other editor UIs since we did not specialize the design to ProseMirror in particular.

- Our algorithm is designed with performance in mind: 
  - in particular, updates only operate locally on the text they touch, and do not require scanning or recomputing the entire document. 
- 👉🏻 However, we have prioritized simplicity over performance in some areas: 
  - we store each character as a separate object (which uses a lot of memory); 
  - we remember all tombstones and the history of all formatting operations; 
  - and the process of finding the character with a particular opId, and computing its index, is not optimized.
- These areas in which we have prioritized simplicity are not fundamental to the algorithm, and can be addressed with some implementation effort.
  - For example, Automerge and other CRDTs that support plain text collaboration use a compressed representation of the character sequence, in which characters with consecutive opIds are represented as a simple string rather than an object per character. 
- We have described Peritext in a simple system model where every operation is stored forever, and it is based on the RGA plain text CRDT, which needs to remember deleted characters as tombstones.
- This design leads to unbounded storage growth, but it can be optimized in several ways:
  - Instead of storing an op-set of addMark/removeMark operations at an anchor position, it is sufficient to store the value (e.g. bold or non-bold) and highest opId for each mark type
  - Mechanisms for garbage-collecting tombstones in RGA apply also to Peritext
  - It is also possible to use a tombstone-free plain text CRDT, such as Logoot, instead of RGA
  - Even without garbage collection, storing all of the operations forever is not as expensive as it may seem

### CONCLUSION

- our approach of storing formatting annotations outside of the text, and attaching them to characters via unique IDs, satisfies all of our intent preservation scenarios and guarantees convergence
- Peritext is only the first step towards a system for collaboration on rich text: 
  - it simply allows two versions of a rich text document to be merged automatically
  - further work on visualizing editing history and changes, highlighting conflicts for manual resolution, and other features
- Since Peritext works by capturing a document’s edit history as a log of operations, it provides a good basis for implementing those further features in the future.

## [Papyrus: rich text CRDT from 2012](https://github.com/gritzko/citrea-model/blob/master/story.md)

- This text is mostly a reply to the Ink&Switch Peritext project article. 
  - As it turned out, the algorithms they devised are very close to what I developed for the Papyrus real-time editor circa 2012. 
  - Actually, I tried different algorithms at the time (also, very close to what Ink&Switch did) and settled more or less on the same thing. 
- it was in 2011-2012, Google's v8 was three years old. 
  - **The code used regexes for most of its heavy-lifting because regexes compile directly into machine code in most browsers**. 
  - I don't recommend it these days, as JavaScript got a great deal of other performance features in the past 10 years.
  - Frankly, these days I wouldn't recommend JavaScript at all. 

- The text was stored as a weave, a string consisting of all the characters that ever existed in the document. So, any historical version is a subsequence of the weave. 
  - all the versioning and merge and undo/redo functionality is based on the weave. 
  - For performance reasons, the document's weave was split into paragraphs.

- But the Causal Tree machinery implements plain text only. 
- 💡 How did we upgrade that to rich text? 
  - Papyrus implements all the structural and inline formatting as a separate overlay.
  - **With CRDT, each symbol has its unique id**. 
  - That id is not always stored explicitly, but it can be derived. 
  - Differently from text offsets/positions, ids are not affected by edits. 
  - That is the superpower of a CRDT text: everything is addressable. 
  - Hence, there is no need for embedded markup, like with Markdown or HTML. 
  - The markup might live as a separate overlay referencing text ranges! 
  - That is an extremely powerful approach. 
  - Overlays can be activated and deactivated, generated, stored, and so on.
- The Papyrus editor renders through HTML, so all the formatting overlays eventually end up as one of four HTML markup types:
  - html attributes, css attributes, css classnames, blocks elements
- Structural formatting records point to paragraphs, while inline formatting points to text ranges. 
  - The renderer walks the text and the formatting, producing HTML. 
- Easy? Actually, not. 
  - There are two invisible sagas here: intention preservation and performance. 
  - Regarding the former, the Peritext paper explains the subject pretty well. 
- Papyrus did that slightly differently, e.g. it considered '\n' to be the first (invisible) symbol of the paragraph, but the effect was basically the same, so that is not worth studying.

- Compared to the Peritext approach, Papyrus cut a couple corners. 
  - First, Papyrus formatting ranges always used strictly last-write-wins merge logic. 
  - Second, there was no distinction between left and right attachment points and all formatting ranges worked the same way. For example, links grow at the end, exactly like bold or italic ranges. That way, every formatting range was a mathematically nice semi-open [b, e) interval. But MS Word does it differently (for a currently unknown reason). In my opinion, copying that leads into the legacy behavior trap: a "business user" will demand every MS Word feature to be implemented exactly as in MS Word. Google Docs is a good example of the resulting evolution. Whether it makes sense to re-implement every glitch from the 80s is an interesting question.

- Rerendering HTML takes time, redrawing the DOM also takes time. How did Papyrus manage that? Effectively, it has its small internal build system able of incremental rebuilds
  - Once you edit a paragraph, it updates that entire paragraph, or maybe just one span inside it if the case is straightforward enough. 
  - Actually, most of the cases are pretty straightforward: sequential typing and backspacing. Once you optimize that happy path, you are half way done.
- The way it worked, every incoming change, be it locally or remotely originated, triggers a rebuild of a weave segment (a paragraph weave). 
  - Those segments are stored in one big hash table, together with formatting records, rendered HTML pieces and many other things. 
  - **Every text or formatting change marks some content dirty. **
  - Once all the changes get applied, all the dirty content is rebuilt. Then, the resulting HTML gets applied to the DOM
  - At the time, my experiments have shown that the HTML rendering code path is extremely well-optimized in modern browsers, so it did not make sense to update DOM incrementally the React way. 
- I have to specially mention the Papyrus content addressing system. 
  - It all started from my 2010 article. As every event in a CRDT document has a permanent id, you can address everything. 
  - So, I devised a formal language for addressing things in a versioned document. 
  - This approach was greatly extended in Papyrus. 
  - Patches, hashtable keys, API calls and many other things used expressions in that language. 
  - Eventually, that language evolved into what is now a big chunk of the **Replicated Object Notation**.

- Other parts of the system also evolved into different things. In this regard, I recommend the chronofold data structure, which I believe is an improvement over the classic weave.

- User edits in Papyrus are highlighted with colors, like in many collaborative editors
- One interesting bug we encountered was a "poisoned document". The URL parsing regex in the code was superlinear, but the problem only becomes apparent on multiline URLs which almost noone uses.
- The Chrome JavaScript engine was slower than Firefox in many cases as Chrome's v8 used to wrap every temporary string as a garbage-collected JavaScript string.
- The project was axed(关闭) as the management decided to buy a proper solution from a reputable supplier (Microsoft). So they leased Office 365. 
  - Eventually, that partnership also ceased and Yandex switched to an open-source solution

## [Where is the CRDT for syntax trees](https://writer.zohopublic.com/writer/published/grcwy5c699d67b9c444219b60cdb90ccbabc7)

- While the community around distributed data structures are settling on CRDTs as the future, 
I’m surprised there is not much CRDT literature/projects for dealing with rich text. 
- While Peritext has got a lot of things right with how content and formatting is weaved together, dealing with block elements like lists and tables was declared as a work in progress. 
  - To be honest, handling semantic blocks like lists and tables is a different beast altogether.
  - When we move on to block elements, we are now making the content of the document into a tree (like how most UI representations are trees). 
  - To be specific, the document is now a proper tree with flat character arrays existing at the leaf nodes. Imagine DOM.  

- To put it in perspective, the algorithm might end up having to compose a delete character operation, a node addition operation and a formatting operation - all landing concurrently with overlapping locations and somehow the algorithm has to figure out how to resolve this with the most sensible outcome - all while keeping your rich-text tree semantically correct- i.e renderable by the rendering program. 
- This last part about keeping the tree renderable is the key. 
  - That is the reason why we would not be able to apply generic JSON based CRDTs like Automerge. 
  - Automerge will have zero idea about what will make a renderable tree. 
  - While Automerge will always give you an eventually consistent JSON tree, it cannot guarantee the tree follows all the rules of your grammar.  
- Talking about trees with certain grammar, does it ring any bells? Yes, ASTs! Almost all abstract syntax trees of programming languages are trees that follow a specification or a grammar. 
- if we are able to arrive at a CRDT for syntax trees, we’ll be able to make collaborative programming always auto-resolve with the syntactically correct program (hypothetically) and we’ll also be able to deal with block elements in rich text in such a way the resolved rich-text data structure is always renderable!  
# discuss
- ## 

- ## 

- ## 

- ## ✨ [CRDT-richtext: Rust implementation of Peritext and Fugue | Hacker News_202305](https://news.ycombinator.com/item?id=35988046)
- I'm happy to see even further performance improvements towards rich-text CRDTs but at this point, I think the barrier to adoption isn't speed or compactness but instead integration with existing backends and databases.
  - I have a hunch that we're reinventing the wheel by creating new B-Tree implementations in Rust when we could be figuring out how to make an existing database do the hard work of storing and retrieving characters in the correct order. 
  - I know Martin Kleppmann has looked at Datalog being a potential solution to this problem but until we have a good full-stack solution to collaborative text editing, I don't think we'll see major adoption of these CRDT solutions.
- I agree that full stack support is the missing pice that's need to make use explode. But I do think the current implementations will get there.
  - Also most general purpose CRDTs are a combination of JSON and XML like data structures, it's useful to be able to query the structures in your database. For example if you build a notes app that supports inline tags, it's useful to be able to query and index those from within the XML like structure without having to dump the whole thing out at another layer of your stack.

- 
- 

- ## 🆚️ yjs vs peritext
- https://news.ycombinator.com/item?id=29328431
- They way I see it there are two (or maybe more of a spectrum of) types of CRDT, from generic and to domain specific. 
  - Yjs actually has multiple different types, very generic types (Array and Map), slightly more specific types (XMLFragment and XMLElement), and then there is the Text type that covers both a generic plain text type but also has provision for rich formatting if needed. 
  - Peritext is basically a different method of implementing the Text type which aims to maintain a little more editor intent than Yjs currently does.
- For a full document, you need to represent both text elements with rich text formatting marks, but also block elements. 
  - With Yjs you would do this with the XMLElement type which as you would expect has attributes and can nest further XMLElements or Text within it. 
  - **Peritext does not yet have support for block types.**
- So, although the most common use of Yjs is for collaborative rich text editing, it can be used for many other things such as 2D/3D drawing or even gaming.

- ## ✨ Peritext: a CRDT for rich text collab
- https://twitter.com/geoffreylitt/status/1463244227412824066
- It's a data structure for async collaborative editing of rich text documents. 
- I believe the tools we use to collaborate can deeply shape the outcomes.
  - Real-time writing tools like Google Docs are an incredible step forward from emailing files, but they do promote a very specific workflow: "one live doc", that everyone is editing at the same time
  - This is fine for light docs, but in my experience it's not great for serious writing, like an essay or academic paper.
  - I want private calm space to try out edits; I want to suggest changes and discuss them as a batch... I want version control; "one live doc" is not enough! 
  - BTW, if you've ever developed software, you're probably familiar with the benefits of version control and branching workflows--maybe overkill for a tiny solo project, but indispensable for serious collaborative work.
- collaboration algorithms underpinning services like Google Docs are generally designed with "one live doc" in mind, not async collaboration. 
- So that brings us to this project.
  - CRDTs are a kind of data structure that allow people to asynchronously make local changes, and then merge those changes back together when people are ready to sync. 
  - The thing is, there has been a _ton_ of research on CRDTs for plain text, but barely any on rich text... which is essential for real writing.
- So that brings us to Peritext: a CRDT for rich text.
  - We've tried to pin down how async edits on rich text should be merged in a bunch of example cases, and proposed an algorithm that just always does the right thing.

- Circa 2012, I did CRDT rich text along the same lines. Compared to your case, I cut some corners though. 
- https://twitter.com/gritzko/status/1463404022212304898
  - Regarding the performance, the key trick was to use paragraph ids along with character ids (paragraph id is the id of the '\n'). Paragraphs/lines have manageable size, can put them in a hash table, then just scan them.

- Any thoughts on how @ProseMirror does this ?
  - One difference is that Prosemirror's collaboration system is designed to work with a single central server, whereas CRDTs are designed to work in distributed settings without a central authority.

- https://twitter.com/geoffreylitt/status/1463291185032679425
  - In my view the main problem with non-realtime merging is that undesirable merges (which any algorithm will sometimes produce) are harder to notice, so you'll want some kind of interactive UX that detects and points out potential conflicts to the user.
  - I'm curious, does Prosemirror's OT system have a notion of conflicts? We currently just arbitrarily resolve conflicts, but our approach would support detecting + showing conflicts a different way
  - Would also love to chat more sometime about Prosemirror's OT and understand better. It seems like key differences are:
  - 1) CRDT works in distributed setting, as you note (if you care about that property)
  - 2) It seems more straightforward to me to reason about correctness of CRDT w/ char IDs and commutative ops, than position mappings and rebasing operations. But that's subjective and I'm curious if you agree
- That's definitely true wrt to OT that supports reordering, but dumbed-down OT where every client ends up applying the operations in the same order converges pretty much trivially, and is not hard to reason about.
  - That being said, there's definitely advantages to adressable tokens, if you can afford the general conceptual complexity it introduces

- https://twitter.com/simonw/status/1463352229746786307
- I'm really excited for one with robust JavaScript and Python libraries that's well suited to using SQLite as the backend data store - I want to build a collaborative editor on top of Datasette which supports offline editing that can be merged back in when the client reconnects. Basically I want to build my own version of Apple Notes, crossed with Google Docs, crossed with a Markdown wiki
- Interesting! Offhand, **maybe could store/sync a SQLite table storing the history of CRDT operations, and replay that into a text doc format?** Although that table would get fairly large, and wouldn't get the benefit of a custom file format to compress down at all
  - That's pretty much what I want to do - I figure I can have a table of operations and every 10 days or so compress it down to a single savepoint and start building up the operations again to avoid size problems
  - Yeah seems sensible, and not much of a loss if you rarely have edits come in on top of a really stale version
