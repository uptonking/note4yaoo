---
title: pattern-arch-time-travel-undo-redo
tags: [architecture, data-structure, time-travel, undo]
created: 2023-08-25T21:52:48.494Z
modified: 2023-09-12T09:36:25.608Z
---

# pattern-arch-time-travel-undo-redo

# guide
- branching和versioning的参考方案
  - 同类产品，如git
  - 编辑器，如vscode、ckeditor、ospreadsheet
  - 数据库，如dolt、mongodb-doc-ver
  - undo/history类产品的形态可参考git commits的交互和设计
# dev

# products-replay

- [Replay - Time Travel Browser DevTools](https://www.replay.io/)

- etherpad timeline
  - [Getting Started with Etherpad _201305](https://archive.flossmanuals.net/etherpad/getting-started-with-etherpad.html)

- [Replit File History](https://docs.replit.com/replit-workspace/workspace-features/file-history)
  - To make sure you never lose any of your work, Replit auto-saves your code as you write
  - view previous versions of a file by using the scroll bar, the arrow buttons, or the left and right arrow keys
  - Comparing previous versions to the current file
  - Restoring a previous version of a file: When you restore to a previous version, it is added as a new version to the file's history
  - use the playback feature of File History to watch your file change over time like a movie

- [Revision History for Google Docs](https://www.revisionhistory.com/)
  - Revision History is an extension for Chrome and Edge browsers, enabling educators to see the edit history of students' assignments in Google Docs
  - adds a bar to the top of Google Docs with basic statistics like time spent writing, number of deletions and copy/pastes
  - The replay feature (in beta) lets you watch a video of the student writing their paper
  - Click on the details button to open a sidebar with more information about revsion history

- [Draftback for google docs](https://chromewebstore.google.com/detail/draftback/nnajoiemfpldioamchanognpjmocgkbg)
  - [How I reverse-engineered Google Docs to play back any document's keystrokes _201411](https://features.jsomers.net/how-i-reverse-engineered-google-docs/)
    - we have the complete history of every single character. Draftback is aware of this history, and assigns each character a persistent unique ID
    - The playback is an epiphenomenon(附带现象：因另一现象而发生或伴随的次要现象) of real-time collaboration, as it was with Etherpad.

- 
- 
- 

# blogs
- [Making Data Structures Persistent_1986](http://www.cs.cmu.edu/~sleator/papers/Persistence.htm)

## 🔡 [Time-Travel Debugging Production Code | Hacker News _202308](https://news.ycombinator.com/item?id=37037130)

- from the article: "Being able to debug any past production code is a huge step up..." this is pretty epic. but it also means you need to keep track of what version of your code ran every past workflow because you need to run it the exact same way when you replay it, right? 
  - You do need to run it on the same code version. There are different ways deploy code changes. If you use one of our in-built versioning systems, the version is recorded in the workflow history (and you can either keep track of version-sha mapping or use a sha as the version). Otherwise, you can add code that adds the current code version as workflow metadata.

## ✏️ [Text Editor Data Structures: Rethinking Undo](https://cdacamar.github.io/data%20structures/algorithms/benchmarking/text%20editors/c++/rethinking-undo/)

- There are a few properties of undo that are very nice to have:
  - The undo operation should create a corresponding redo operation, more on redo later.
  - If undo is applied to the beginning of edit history, the system should report that an undo is not possible and do nothing as a result.
  - If you undo (or redo) to the point of the last save of the document the system should recognize that there is nothing to save.

- Conclusion
  - Immutable data structures remain a fascinating point of interest for me. They enable so many interesting avenues to solve problems.
  - The Myers diff algorithm is incredibly easy to implement, but takes a lot of time to understand what is happening so that you can render it properly.
  - It is going to be hard for me to go back to linear undo/redo of most editors

## 🦀 [In Rust, ordinary vectors are values _201802](https://smallcultfollowing.com/babysteps/blog/2018/02/01/in-rust-ordinary-vectors-are-values/)

- Traditionally, persistent collections are seen as this “wildly different” way to setup your collection. Instead of having methods like push, which grow a vector in place
  - vec.push(element); // add element to `vec`.
  - you have a method like add, which leaves the original vector alone but returns a new vector that has been modified:
  - let vec2 = vec.add(element); 
- The key property here is that vec does not change. 
  - This makes persistent collections a good fit for functional languages (as well as, potentially, for parallelism).

- 🤔 How do persistent collections work?
  - I won’t go into the details of any particular design, but most of them are based around some kind of tree. 
  - For example, if you have a vector like [1, 2, 3, 4, 5, 6], you can imagine that instead of storing those values as one big block, you store them in some kind of tree, the values at the leaves. 
  - Now imagine that we want to mutate one of those values in the vector. Say, we want to change the 6 to a 10. This means we have to change the right node, but we can keep using left one. Then we also have to re-create the parent node so that it can reference the new right node.
  - Typically speaking, in a balanced sort of tree, this means that an insert opertion in a persistent vector tends to be O(log n) – we have to clone some leaf and mutate it, and then we have to clone and mutate all the parent nodes on the way up the trees. 
  - This is quite a bit more expensive than mutating a traditional vector, which is just a couple of CPU instructions.
- In Rust, the “ordinary collections” that we use every day already act like values: in fact, so does any Rust type that doesn’t use a Cell or a RefCell.
  - This implies to me that persistent collections in Rust don’t necessarily want to have a “different interface” than ordinary ones.
  - I created a persistent vector library called dogged
  - Dogged offers a vector type called DVec, which is based on the persistent vectors offered by Clojure.
- DVec is a persistent data structure. Under the hood, a DVec is implemented as a trie. It contains an Arc (ref-counted value) that refers to its internal data. When you call push, we will update that Arc to refer to the new vector, leaving the old data in place.
- The main difference then between a Vec and a DVec lies not in the operations it offers, but in how much they cost. That is, when you push on a standard Vec, it is an O(1) operation. But when you clone, that is O(n). For a DVec, those costs are sort of inverted: pushing is O(log n), but cloning is O(1).
  - when you do a push on a DVec, it will clone some portion of the data as it rebuilds the affected parts of the tree (whereas a Vec typically can just write into the end of the array).

- One problem I’ve seen with DVec is that it’s pretty tough to compete with the standard Vec in terms of raw performance. 
  - It’s often just faster to copy a whole bunch of data than to deal with updating trees and allocating memory. 
  - I’ve found you have to go to pretty extreme lengths to justify using a DVec – e.g., making tons of clones and things, and having a lot of data.

- Conclusion
  - I’ve tried to illustrate here how Rust’s ownership system offers an intriguing blend of functional and imperative styles, through the lens of persistent collections. 
  - That is, Rust’s standard collections, while implemented in the typical imperative way, actually act as if they are “values”: when you assign a vector from one place to another, if you want to keep using the original, you must clone it, and that makes the new copy independent from the old one.
  - That said, I think there is another reason that some have taken interest in persistent collections for Rust specifically. That is, while simultaneous sharing and mutation can be a risky pattern, it is sometimes a necessary and dang useful one, and Rust currently makes it kind of unergonomic

- ### Here's a blog post that explains it beautifully why persistent collections are not as useful in Rust as in other languages
- https://twitter.com/debasishg/status/1755249637962002649
- There two pairs of constraints in the design of programming language memory abstractions:
  - sharing/aliasing + immutability
  - unique-ownership/noalias + mutability
- There’s a duality(双重性；两面性) between them.
  - If you give up aliasing, you can’t give up mutability. You would be forced to deep-copy objects all the time.
  - If you want the right to share objects, you “have to” give up mutability. Because when you mutate an object through a reference you might break the assumptions of someone else holding that same reference.
- Languages with GCs are all about sharing references. Clojure with its focus on data structures with sub-structural sharing brings in immutability while leveraging sharing to the maximum extent.
- If you drop a GC and mostly forbid aliasing in your PL design like Rust does, you can’t efficiently implement the persistent DSs you find in Clojure. But with unique ownership, mutability becomes much less scary because you know your mutation affects only your reference.

## [Undo/Redo](https://gist.github.com/mlynch/ab554d84dc3b7b8be3d6)

- The best way to look at undo/redo is two stacks of operations the user has performed:
  - The Undo stack is the "history" of what they've done
  - The redo stack is the breadcrumbs back to the initial state before they started undoing
- If the user "undos" an action, we POP off the undo stack, do the operation, then we PUSH an action onto the redo stack.
- If the user undos multiple times, then does not redo but instead performs a unique action, we consider the redo stack lost. A complicated undo/redo system that needs to preserve these lost operations will probably FORK off here. 

## 💡 [History Data Structures](https://gist.github.com/CMCDragonkai/d266a3055735545447439f0fa662a0e1)

- For stateful applications, there are 5 different ways of managing the history of state:
  - No History - Living in the moment. - Examples: Any stateful application that doesn't discards all previous states upon mutation.
  - Ad Hoc Snapshotting - Allows restoration to manually saved snapshots. - Examples: Memento Pattern.
  - Singleton - Only remembers the previous snapshot, where undoing the undo is just another undo. - Examples: Xerox PARC Bravo.
  - 1 Stack - Allows linear undo. - Examples: AtariWriter.
  - 2 Stack - Allows linear undo and redo. - Examples: Browser History, Microsoft Word, Adobe Photoshop.
  - Append-Only Log - Allows moving forward with reversed patches/deltas (a.k.a. compensating transactions). - Examples: Git-Revert, Datomic, Blockchain, Event Sourcing.
  - Tree - The Multiverse Approach. - Examples: Git, Vim, Emacs with UndoTree, Delorean.
- There's variations and hybrid approaches that have to deal with special cases involving multi-user history, which is relevant to operational transformation applications such as Google Docs.

- there are 2 different ways of encoding states. 
  - The snapshot method and the delta method. 
- The snapshot method is where every "state" is a complete and independent snapshot of what the state was. 
- Whereas the delta method (a.k.a. delta encoding) is the (ideally minimal) difference between the past and present. 
- The snapshot method uses more storage space, while the delta method requires more computation to merge the differences.
- the time to construct the snapshots takes much longer then when using the delta method.
  - This is because you may need to transitively apply all the deltas from origin.
- There's also a theory formalising how deltas works called "Patch Theory", which is used by the Darcs and Pijul version control system.

## [Arrays that let us time travel](https://arpitbhayani.me/blogs/fully-persistent-arrays/)

## [Introduction to a data structure that let's us time travel](https://arpitbhayani.me/blogs/persistent-data-structures-introduction/)

- Ordinary data structures are ephemeral implying that any update made to it destroys the old version and all we are left with is the updated latest one. 
  - Persistent Data Structures change this notion and allow us to hold multiple versions of a data structure at any given instant of time. 
  - This enables us to go back in “time” and access any version that we want.

- Persistent Data Structures preserve previous versions of themselves allowing us to revisit and audit any historical version. 

- Depending on the operations allowed on the previous versions, persistence is classified into three categories
- **Partially Persisten**t Data Structures allows access to all the historical versions but allows modification to only the newest one. 
  - This typically makes historical versions of the data structure immutable (read-only).
- **Fully Persistent** Data Structures allows access and modification to all the historical versions. 
  - It does not restrict any modifications whatsoever. 
  - This means we can typically revisit any historical version and modify it and thus fork out a new branch.
- **Confluently Persistent** Data Structures allow modifications to historical versions while also allowing them to be merged with existing ones to create a new version from the previous two.

- Implementing Partial Persistence
- Copy on Write Semantics
- Copy on Write Semantics
- Copy on Write Semantics
- Path-Copying Method

- Since persistent data structures thrive on high memory usage, they require some garbage collection system to prevent memory leaks. 
  - Algorithms like Reference Counting or Mark and Sweep serves the purpose pretty well.

## [Persisting the version history of a complex data structure](https://medium.com/@mmdGhanbari/persisting-a-persistent-data-structure-3f4cfd46036)

- In this article, we learned about persistent data structures and the different methods available to copy a complex one, as well as how to persist them in a relational database.
  - you may also want to check the Event Sourcing pattern, which suggests persisting the change itself instead of the changed data.

## [Undo, the art of – Part 1](https://maxliani.wordpress.com/2021/09/01/undo-the-art-of-part-1/)

- I’ll touch on the fact that there is no right or wrong, that undo can be implemented in a variety of different ways and that the best practice strongly depends on the choice of data structures you designed for your application.
- At its essence, undo is a history of changes in the data within a program
- Undo must record the sequence of edit events the user executes, and unwind or rewind the changes in the data. 

## more-blogs

- [onlyoffice: Simplify History Structure](https://github.com/ONLYOFFICE/document-server-integration/issues/437)

- [Version Control · vkbo/novelWriter](https://github.com/vkbo/novelWriter/issues/383)
# blogs-version-history

## [Version History and Lifecycle Policies for Postgres Tables | Tembo _202309](https://tembo.io/blog/table-version-history)

- A nice feature of AWS S3 is version history and lifecycle policies. 
  - When objects are updated or deleted, the old object version remains in the bucket, but it’s hidden. 
  - Old versions are deleted eventually by the lifecycle policy.
- I would like something like that for my Postgres table data. 
  - We can use the `temporal_tables` extension for version history, and combine it with `pg_partman` to partition by time, automatically expiring old versions.
# more
- [Data model for storing revision history in FoundationDB · couchdb](https://github.com/apache/couchdb/issues/1957)

- [Immutable Data Structures - DEV Community](https://dev.to/martinhaeusler/immutable-data-structures-2m70)
# discuss-stars
- ## 

- ## 🌰 尝试复刻了 manus 的 replay 功能, 从 TARS 的开源 repo 学到的两个架构特点
- https://x.com/Nin19536/status/1905975354227040314
1️⃣mcp 统一工具协议
可插拔，可扩展非常关键，且 tool 定义和 tool 执行对外只暴露接口，agent 端不关心实现。
2️⃣事件管理
管理好所有流式输出、任何工具 update，都需要考虑到前端展示 event 的方式，提供更好交互。而且事件管理有利于模型统一管理上下文。以事件时间戳永远自增，便于时间回溯和用户观测。
- 代码是基于我去年八月就实现的原型 MVP重构 cosmos 项目
  - 可以去看看 TARS 的代码还挺清晰的
  - 你看一下 manus 返回的数据结构就行了，前端复刻不复杂。

- ## you need to wait until the previous layer has fully dried
- https://x.com/palekirill/status/1865049187282292823
  - 不完全3d的界面移动，适合实现版本历史
- I don’t like oil paint for that reason
  - yes i know that feeling—when you’re eager to keep going, but the painting makes you wait

- ## ✏️ [How does Etherpad's timeline feature work? - Stack Overflow _201206](https://stackoverflow.com/questions/11242188/how-does-etherpads-timeline-feature-work)
  - I am very much interested in understanding the JSON response and how it works. Also what database is most suitable for such apps (etherpad, google docs, etc.). Nosql (like mongodb) or sql (like mysql).

- When you drag on the timeslider, the relevant changes are sent from the server to the client as you've discovered.
- Changes are encoded as instructions that edit the existing document contents to become the new document contents. See https://github.com/ether/etherpad-lite/wiki/Changeset-Library
- Etherpad runs on SQL primarily. 
  - Maybe there is experiments with other DB:s, but most important for etherpad is reading/writing raw tables of changesets. A relational DB is probably the best choice for performance and sanity. 
  - MySQL is the default for etherpad. Postgres has been worked on. 

- any thoughts on mongodb ? actually i am making a similar application that will record other things apart from text changes. i thought maybe just storing the json object sent from client while creating the pad inside mongodb (its api is json based, so you just sent/retrieve jsons) would be a good idea. 
  - Don't use MongoDB for changesets. (Or do, but then promise to write back when it fails so help others avoid the mistake :-). Use MongoDB for complicated documents/objects to avoid creating hundreds of relational tables. If you wanted MongoDB to be buzzword compliant, I recommend instead an in-memory database. HSQLDB and VoltDB are cooler than Mongo. And much much faster.
# discuss-db-history
- ## 

- ## 

- ## 🤔 [How to version control a record in a database - Stack Overflow](https://stackoverflow.com/questions/323065/how-to-version-control-a-record-in-a-database)
- A good starting point might be looking at some database model that uses revision tracking.
  - The best example that comes to mind is MediaWiki, the Wikipedia engine. Compare the database diagram here, particularly the revision table.
  - Depending on what technologies you're using, you'll have to find some good diff/merge algorithms.

- Two options:
  - Have a history table - insert the old data into this history table whenever the original is updated.
  - Audit table - store the before and after values - just for the modified columns in an audit table along with other information like who updated and when.

- another way is to make a version column and keep all your versions in the same table. For one table approach you either:
  - Use a flag to indicate the latest ala Word Press
  - OR do a nasty greater than version outer join.
# discuss-redux-like
- ## 

- ## 

- ## 💥 [Huge performance issue when dispatching hundreds of actions · reduxjs/react-redux _201601](https://github.com/reduxjs/react-redux/issues/263)
- On boot, the app I'm building gets a stream of data from a server. This stream can have hundreds of messages and entities and each message is handled separately.
  - It takes a tremendous amount of time to dispatch actions after UI has rendered, because every state change re-renders the @connected component.

- Try this: Collect those those messages into an array and flush it with store.dispatch in a single tick with every 50ms (or whatever is required). You must use redux-batched-updates to avoid rendering on every dispatch on the tick.
- https://github.com/acdlite/redux-batched-updates /201507/js
  - redux-batched-updates uses deprecated api
- https://github.com/tappleby/redux-batched-subscribe /MIT/201604/js
  - Store enhancer for redux which allows batching of subscribe notifications that occur as a result of dispatches.

- I'm glad it solved your issue but you should note that debouncing and update batching are completely different things.
  - With debouncing you end up just completely ignoring most of the messages. That can be ok but if your store state requires to see every message, for example you need sum up some numbers from them, that will not work as expected.
  - React update batching and the `setInterval` trick I presented will dispatch every message to the store but will only do it batches to avoid excessive rendering.

- ## [How to implement Replay functionality in a React based game? : r/reactjs](https://www.reddit.com/r/reactjs/comments/i9ga7n/how_to_implement_replay_functionality_in_a_react/)
- If you want to go for "wow factor", use the `patches` features from Immer with Redux to track changes to the store and be able to undo.
  - Redux Toolkit already used Immer internally, so it's not much more work to track each patch as it's applied to the store. 
  - When any Redux action modifies the game state, you listen for the patch using Immer, and push it into an array of the game moves. When you need to replay, you just iterate through the array. To undo, just pop items off the array.
  - If you want to do this without Immer, Redux has some docs that describe history and undo functionality with code examples

# discuss-rrweb
- ## 

- ## [iframe录制与回放 · Issue #654 · rrweb-io/rrweb _202108](https://github.com/rrweb-io/rrweb/issues/654)
- 回放的时候不会执行 JS 代码。

- ## [Fabric JS Image object shows blank while replaying · Issue · rrweb-io/rrweb _202103](https://github.com/rrweb-io/rrweb/issues/516)
- Current workaround I did is to take a screenshot ( `html2canvas` ) and set that `dataURL` to an image hid behind the actual canvas while recording. While replaying the canvas is empty but the screenshot is shown in it's place so works for me.

# discuss-replay-solutions
- ## 

- ## 

- ## [DOM recording for web application demos | Hacker News _202011](https://news.ycombinator.com/item?id=25195454)
- This is very cool, but for me the problem has always been the repeatability of demo videos. I make a demo video of our product, and two weeks later that demo is out of date and now I need to make the same video again.
  - Additionally, the need to add fake CSS pseudo classes to get it to work with focus, etc. seems like a bummer.

- That's addressed in the post too. They make their demos as Selenium scripts so in many cases they can simply re-record the demo when the UI changes.

- In my experience, Mutation Observers can be very punishing in terms of performance if you have large DOM structures, especially on page load.

- ## [Show HN: Wirequery – Full-stack session replay and more | Hacker News _202403](https://news.ycombinator.com/item?id=39802120)
- How does this compare to rrweb, the library that Sentry and many other commercial offerings for frontend monitoring use?
  - WireQuery uses rrweb for capturing the frontend interactions. However, perhaps I can answer a similar question, which is how it compares to other offerings.
  - The main difference between existing tools and WireQuery is that WireQuery was designed for capturing the interactions within the complete stack. This manifests itself in the following ways:
  - The frontend recording is paired with the network calls on the backend, which can consist of the entire trace (i.e. the data of system A calling system B, system B calling system C, etc.), including the actual request and response bodies, headers, etc; - There is an exploration and query-in-the-background feature. These features allow you to run arbitrary queries against a backend system that will capture any network request that meets your criteria, optionally paired with the complete trace and some transformations.

- ## [Launch HN: Highlight.io (YC W23) – Open-source, full stack web app monitoring | Hacker News _202307](https://news.ycombinator.com/item?id=36774611)
- Congrats on being the only commercial company to actually sponsor rrweb rather than just fork it and contribute absolutely nothing back (or in the case of Sentry - remove their copyright and violate their license).
  - Sentry’s license change on the fork was a mistake. It has been fixed though.

- Why using 6 databases? Kafka, redis, Postgres, ClickHouse, influxdb, opensearch
  - The open-source infra we use allows us to have a highly-available, scale-able system.

- what's the advantage over MS Clarity, which seems to offer the same features, is free forever, and easy to setup?
  - On session replay, clarity if definitely comparable to an extent. Keep in mind that the tool is very fine-tuned for a more marketing use case (w/ heatmaps, analytics, etc..). On the other hand, Highlight.io will monitor the content of network requests, trace request all the way to your backend, let you inspect the DOM, report on errors and much more.
- Clarity is meant for high level analytics around product usage, while Highlight is built for engineering observability (catching and debugging errors). Highlight offers network tracing, log ingest (both client and server side), and error monitoring to serve that use-case which Clarity does not.

- ## [highlight: Show HN: We’re open-sourcing our session replay tool | Hacker News _202302](https://news.ycombinator.com/item?id=34897645)
  - We’re open-sourcing highlight.io, a session replay and error monitoring tool. 
- We've actually had quite a few customers switch off Logrocket because of our support for things like Canvas recording
- Our frontend session replay happens in two parts:
  - The HTML DOM Recording using rrweb
  - The monkey patching of fetch, xhr, console methods, combined with data from `window.performance` .
  - The rrweb repo has a good in-depth explanation of how the DOM recording works. In short, it captures the full HTML of a page when a user first loads it, then tracks DOM changes via the `MutationObserver` api. From our client, these are all shipped to our backend as serialized events. We process the events per 'user session', storing them temporarily in redis, then compressing a permanent payload once the session no longer is sending new events in the local filesystem or S3.
  - Monkey patching network and console methods allows us to capture request/response payloads, headers, status code, etc. We then combine that data with the `window.performance` api's notion of network requests to ensure we capture all requests (even ones that happened before our monkey-patch had time to apply), as well as to get precision timing data.

- Following up regarding the other points I missed. Compared to OpenReplay, we have similar functionality in our session replay, but we've focused a lot of effort on making a cohesive error monitoring (backend and frontend) experience. We closely link sessions with errors (stacktraces and associated metadata) and vice versa to make it easy to get to the root cause of a bug.

- On the OpenReplay end, its seems we have feature parity for session replay, but they don't have support for error monitoring and therefore linking errors to corresponding sessions (as far as I can see).

- PostHog, Highlight and Sentry are all using rrweb. 
  - At OpenReplay, we use a full proprietary solution that we built from the ground up and covers all session replay aspects (tracker, protocol and replayer).

- PostHog started as a product analytics tool but we now have a fully fledged session recordings product including handling console logging and network requests for debugging. Mobile support is coming shortly too

- ## [Rrweb – record and replay debugger for the web | Hacker News _202407](https://news.ycombinator.com/item?id=41030862)
- We use rrweb as a DOM-recorder in our extension, and it does come with some limitations. Taken from our docs:
  - DOM recording has the fundamental trait that nothing outside the DOM can be recorded. This latter limitation means that only content on the specific page is recorded: Data in popup dialogs or other tabs is not recorded, neither is anything outside the HTML document like native MacOS/Windows menus shown for native HTML selects.
  - On top of that, some embeddable elements like `<canvas>` are not recorded (e.g. Google Maps, Figma).
  - When playing back DOM recordings, there can be visual glitches, like duplicate elements being shown. Even when there’s no obvious glitches, a DOM recording is unlikely to look exactly like the page as experienced by the session reported.
  - Security configuration like CORS on the recorded site’s hosting, and Bird’s own CSP policy can prevent the loading and rendering of embedded elements, like the original page’s font.
  - Because DOM recordings don’t include all information (e.g. image files are only linked to), DOM recordings can drift apart from the time of the recording in fidelity over time, if the content of the asset behind the URL changes, or even degrade, or when the assets are no longer accessible at all at the URL.
- Having said that, we found that rrweb is quite reliable on most situations and works well for most of our users.

- 🧐 rrweb is capable of canvas recording. We use it at sentry but there are inherent challenges with canvas you have to be aware of. Most importantly we're very careful about PII handling and if you have canvases you will sooner or later capture stuff you do not want to have on there unless you are very careful yourself.

- Replay.io is a different beast altogether. They implement their tooling on their own browser (Chromium-based), so they have access to much more precise data than a JS-library like rrweb does.

- 👷🏻 Maintainer of rrweb here. I used replay.io for debugging sometimes, it’s really quite useful. 
  - It is however a standalone browser and it works by intercepting quite low level browser calls which is only possible to do with a forked version of a browser. 
  - So it’s great for debugging if you know what you’d like to reproduce or deep-dive into. 
  - rrweb is more versatile as it can run in any browser and you could use it for analytics, live streaming for support, or recording tutorial videos like we do at https://recordonce.com

- RRWeb only records changes to the DOM, it doesn't actually replay the JavaScript that makes those changes happen. So you see exactly what the user sees, but you're not able to inspect memory or anything like that.
  - There are a few caveats since not everything is captured in the DOM, such as media playback state and content in canvases. The user may also have some configurations that change their media queries, such as dark mode or prefers reduced motion.
- 👷🏻 Maintainer of rrweb here: media playback was added a little while ago and was recently improved quite a lot. 
  - Canvas recording is also available but there are three different ways of doing that as all three have their own pros/cons.

- Everything is open source and from what I see there is no official server – you can store captured sessions anywhere you want.

- Believe Sentry use it in their session replay product
  - We do and we're not alone. I really like rrweb and I think it's the strongest library in the space.
- Posthog uses it for their session replay product as well
  - pendo, as well
- DataDog, Sentry and Highlight use rrweb quite heavily in their tools to give you an idea of where things went wrong

- Zipy is also a session replay and error tracking tool, which uses rrweb to capture the DOM. On top of that they have many small and big features which adds value to their product, must visit https://zipy.ai

- I studied rrweb's MutationObserver-based DOM event handling & recording when rebuilding the Notion editor a few years ago. I've never used the full thing but liked the code quality I encountered.

- I wish we had an rr for nodejs.
  - Today I found EffectfulJS Debugger, which is a DAP debugger with time travel and state persistence for JS

- ## 🤔 [Ask HN: How does software such as rrweb and OpenReplay work? | Hacker News _202208](https://news.ycombinator.com/item?id=32658825)

- 录制界面方案的优点是支持浏览器外的元素，
  - 缺点是子元素不可交互，视频体积大
- 录制DOM方案的优点是元素可点击，
  - 缺点是不支持浏览器外的元素，部分元素可能错位或缺失
  - 方便回放时渲染与操作时不同的交互，如diff-view

- 👷🏻 Core team member of rrweb here. rrweb and other tools that do user session recording heavily depend on the mutation observer to surface changes to a webpage, each of those changes gets serialized into a JSON event and get captured for later viewing.
  - part from the things we can get directly from the Mutation Observer we also end up monkey patching things like the WebGLRender... and record each call that is done to it so that we can play those back in the same order for replay.
  - Before we do all of the diff recording we start with a full snapshot of the webpage which captures every dom node. And it does a lot more than just your plain old `document.documentElement.outerHTML` , it captures contents of style sheets, images, scroll positions etc.. We use those full snapshots as keyframes to base our diffs off of. This works in a similar way to how video files work, but the snapshots don't contain any pixel data, just DOM information.
  - On replay we go ahead and rebuild the DOM as close to how it was recorded and we then animate the changes as they occurred.

- OR is opensource so you can pretty much explore it on your own but TLDR is that it records diffs of DOM, network and state alongside with mouse and send it as a byte array batches to the backend that gzip this files, and then this process is going the other way (unpack, bytes to diff to display) in the player parts.
  - Videos would take too much space plus API is limited as I can see on MDN

- ## 🚀 [rrweb - Show HN: Open source JavaScript library to record and replay the web | Hacker News _201812](https://news.ycombinator.com/item?id=18776496)

- Security and Privacy are extremely hard to get right here. 
  - Some of the challenges: 
  - CSPs can often be bypassed using Google API libraries `<Object/>`/ `<SVG>`.
  - Blacklisting `<SCRIPT/>` tags can often be bypassed with an XML namespace - CSS based data or password exfiltration. 
  - Clickjacking, "data:" urls etc. 
  - Could you imagine a web request proxy server deploying Service Workers? 
  - postMsg() from further nested frames
  - Substantial work goes into sandboxing replay environments and limiting PII. Defense in depth is particularly important here. Enterprise level research, auditing, monitoring and care should be taken seriously.

- You should offer a commercial and open source version. The commercial service could provide a few extra features at a modest price point, but support development of the open source platform. Perhaps it could pay your bills and be a cheaper alternative to the existing expensive commercial offerings.
# discuss
- ## 

- ## 

- ## [Text Editor Data Structures: Rethinking Undo | Hacker News _202312](https://news.ycombinator.com/item?id=38601435)
- Some points that often get left out of 'undo' discussions:
  * The usual linked-list (or tree) implementation is very cache-unfriendly if you're undoing several steps at a time. Using "linked list inside a buffer" is better; this does not preclude trees, the back "pointer" just has to specify the offset as well as the previous buffer (when you reach the fixed-size allocation you will also have to do this). If you undo across a buffer change you'll also need to update the "most recent redo" backlink from the new buffer.
  * SSO strings will usually beat external strings for small edits (this can be variable-size in the linked-list-in-a-buffer case); for large edits see if you can just incref part of the main editing buffer rope.
  * It is highly useful to expose a few "shortcut" undo commands: undo to previous save, undo to previous build, etc. Manual tags is probably not very practical most of the time, and "save" is essentially one anyway.

- If you are looking for counter examples, take a look at Excel on windows. It undoes in multiple windows. Say you have two documents open. You make a change in the first then change the second document then go back to the first and make a change. One document has two changes and the other has one. First undo impacts document one. Second alters document two. Infuriating
  - The behavior in Excel tricks you into using the feature by working as you'd expect in a single document scenario. Then you open a second document and end up trashing one or the other when you undo the wrong thing.
- more interesting part is, when you find these are shared in powerpoint and word, too. there is not warning about I modified another file, if I dare to work on multiple task, everything probably wreck.
  - Devil's advocate: For Excel, it makes a bit sense to have app global undo because sometimes Excel books refer other opened books' data. For Word and PowerPoint, it's hard to advocate because I've never seen referring other docs.

- 
- 
- 
- 
- 

- ## Converting file system changes into ops for a rewindable Obsidian.
- https://twitter.com/JungleSilicon/status/1734394464289132751
  - Obsidian autosaves as you make changes leading to semi-realtime updates.
  - It also respects changes that other programs make, so if a *revert* button was added, Obsidian would update when you pressed it.
  - It wouldn't work for concurrent updates but it gets you to *semi-collaborative* documents.
  - The history is periodically saved to a file and can be recovered when re-opened. If the server is not running then on next open it can do a diff to create the ops.

- ## [Build Your Own X | Hacker News](https://news.ycombinator.com/item?id=32157759)
- One advice: for any of these topics take a tutorial directed at language X and implement the solution in language Y. This will prevent you from mindlessly copying the code and will force you to understand what you are doing.

- I wonder what resources it would contain to help design a software with undo/redo feature.
  - A Merkle-tree data structure + an append only log with checkpoints + a command processor would provide a basic foundation.
  - Your data can be represented in a Merkle-tree. You provide operations add-node, delete-node, move-node etc., on the Merkle-tree and build a command processor that takes as input a checkpointed Merkle-tree snapshot (could be empty when you start) and a log of operations (essentially an sequence of operations). The command processor then applies the series of tree operations in the log to build the final state of the tree. The special checkpoint operation saves a snapshot of the Merkle-tree.
- This basic set of operations should allow you to do unlimited undo/redo/transaction playback capabilities.
- check out emacs' undo-tree for a cool implementation
  - [Emacs has a powerful undo system.](https://www.dr-qubit.org/undo-tree/undo-tree.txt)
  - Unlike the standard undo/redo system in most software, it allows you to recover *any* past state of a buffer (whereas the standard undo/redo system can lose past states as soon as you redo). 
  - Emacs’s undo system is quite frankly amazing. Not only can you recover any state through an arbitrary number of undo and redo operations, but you can also localize the undo/redo operations to a selected region of the buffer.

- ## 🤔 how would you write an undo system for a raster graphics illustration/painting application?
- https://twitter.com/FreyaHolmer/status/1441541405298630657
  - there's some low hanging fruit - only storing the rectangular region of the pixels that were changed, and its content, would save a lot
  - maybe some RLE compression? especially when the alpha channel is 0, but that would add compression/decompression to the time undo/redo takes
  - then there's also the question of where the data should be stored: GPU-VRAM? RAM? Disk?
- a radical alternative is to store actions on an action stack rather than raster/image data, but, this has massive implications on the architecture of, uh, everything, and has lots of drawbacks that I don't think would make it worth it
- I don’t know if it’s a good way, but what I’ve done in the past is get the delta, changed pixels, between before/after, and use RLE style compression - all non-changed pixels would compress away as “empty”. Applying the delta would undo the action.
- Reapplying deltas to a buffer repeatedly is likely to introduce small variations and possibly artifacts. The only system I'd seen in the past worked via snapshots and a stack of actions. Curious how PS Lightroom works. Has a "complete" history and is non destructive.
- Hm. I wonder if you could take that idea further with a quadtree style structure? Slice down to a min cell size to cull transparent cells... or would that contain too much overhead for the tree? Could make pixel storage more challenging.
  - iirc photoshop does it by storing every version and sharing overlapping data between them using a persistent data structure.

- this is far and away the best solution in my experience, for any kind of editor (outside of implementation practicality). i normally store the entire state each undo step in my tools since like. i'm never working with a lot of data, its super easy to implement and never breaks
- storing the entire state for image editors I feel like wouldn't work because of how much data it involves
  - storing actions means everything needs to serialize and also be reapplyable quickly on undo, and you'd likely need a hybrid model so that you can keyframe every n actions
- hybrid makes a lot of sense! the work with delta is in like. the framework (and fixing consistency bugs). the implementation of each action could definitely be sometimes just pixel data and sometimes purely tool/action information
  - maybe pixel data is the default thing that gets stored, with zero implementation (you just create a new undo state and it gets the pixel data thats changed), then you can add better data for the steps when you need to, like performance optimisations
- the drawback would be that if you have an undo history length of 80 actions, then undoing a single action means reapplying/rerendering 79 things, which, may or may not have been expensive actions, right?not to mention all actions now need to be serializable
- Make the actions reversable. When you draw, capture the data of the pixel you overwrite. That way you can undo by doing the inverse of the do.
  - this is not always possible, many actions are irreversible (gaussian blur, for example)
- Making the actions serializable shouldn't be too hard... For the redo thing, you could smooth it over by caching a certain number of previous states, as tractable. If the state is cached just swap it in; if it's past the cache window then regenerate it

- NSUndoManager on macOS implements a generic version of this
  - [NSUndoManager | Apple Developer Documentation](https://developer.apple.com/documentation/foundation/nsundomanager)

- Every X actions, you make copy of the state and mark it as a checkpoint. Reroll from there.
- Action object that holds everything for the do/undo + push(do), pop(undo) from a stack is good. For doing 80+ things, need to use OpenGL/WebGL which will easily re-render everything quickly. CPU shouldn’t really touch pixel data. E.g. a brush stroke will end up being a GL drawcall

- I briefly worked on a little touchscreen drawing app that never saw the light of day and my plan was a hybrid approach of an action stack and bitmap history - store full-frame bitmaps every few actions, and undo by re-performing just the actions since the most recent snapshot.

- Action stacks would be the way, pen down to pen up as the separator, then everything in between is tweakable (though usually forgotten)

- In my experience, you’ll need this anyway, to unify all ops into a single undo stack. Where an op is reversible, you can store it parametrically, where it isn’t, you have to fall back to storing previous states. That’s when you get into as you said, dirty regions and compression!

- We do this the old-fashioned way: a layer is split up in 64x64 pixel tiles, and we store the before-tiles in the undo/redo action. We don't keep per-stroke data -- though we're considering doing that.
  - neat! seems similar to what SAI is doing judging by the other replies I saw
  - I feel like it makes more sense than my initial idea of saving/loading the bounding rectangle of the changed regions, diagonal strokes and all that

- A good way is to divide image into fixed size blocks (say 64x64). 
  - Before editing a block, make sure it's either exclusively owned, or first copy the block (copy-on-write). Different versions of the image (for undo/redo) share the blocks that haven't changed
  - The blocks need to be reference counted and GC'd so you can determine when a block is no longer used (can be freed), exclusively owned (so you don't need to copy-on-write), or shared (so you need to first COW it before editing)

- Substance Painter stores the strokes in world space.  Which fucking sucks because you can't update your model

- I have a very simple system in rx (http://rx.cloudhead.io) -- I save a compressed snapshot of the canvas everytime it is changed. With google's 'snappy' compression library, the delay is not perceptible for reasonably sized canvases.
  - The problem with implementing brush-based optimizations is that they don't work for other types of edits, eg. flipping the canvas, filling, color replacement etc.

- Continuous undo/redo: record unit over time, use a slider/dial to move backwards or forwards in time.

- Take the diff between your start and end image and store it in a quad tree. Then serialize as byte array and gzip if you want it as small as possible.

- I think I remember a talk from adobe that said something like their canvas is basically a 2d array of pointers rather than values, so when you paint, you're just changing the pointers of those specific pixels allowing low memory footprint and enables things like the history brush
  - [GoingNative 2013 Inheritance Is The Base Class of Evil - YouTube](https://www.youtube.com/watch?v=2bLkxj6EVoM)
  - Had some free time to prototype this. Very good balance between simplicity and memory efficiency

- Refing some stuff other people mentioned in the comments, but keeping a hist of modified but also keeping a space-efficient history of each tile sounds like something a modern GPU's sparse-texture/sparse-residency would perfectly lend itself to
  - Maintain a current-state image, a change happens, you mark the tiles touched, save their state(lots of compression decisions happen here) and an undo would just be rebinding those tiles to that memory, and the older it gets, it goes from vram>ram>disc. Sparse textures are soo good
  - I've reverse engineered Paintool Sai, and they do a tile-based approach. I haven't looked at the undo system in particular, but I have reason to believe that they probably do just-that for their undo system based on how it's their core intermediate format
- 
- 
- 
- 
