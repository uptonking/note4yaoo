---
title: lib-editor-app-blog-stars
tags: [blog, editor, text-editor]
created: 2020-12-24T18:17:55.072Z
modified: 2022-08-21T10:11:43.095Z
---

# lib-editor-app-blog-stars

# guide

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
    - 虚拟渲染能提高安全性?
  - defer render

- virtualized render cons
  - 影响浏览器自带的功能，如页面内查找
  - 锚点自动滚动，如生成标题目录toc，评论

- 编辑器入门经典示例
  - slate
    - minimal-render > event-keydown > custom-element > custom-format > commands > save-to-local > api/transform
    - rich-text-editor, mention, search-highlight
  - ckeditor5
    - timestamp-plugin > abbreviation-plugin > box/card-widget > inline-word-widget > react-add-product
    - demos for every feature
  - prosemirror
    - example-setup > custom-node > toolbar-menu > tooltip > custom-schema > > img-upload > markdown
    - footnotes: inline node
    - linter
    - track-change
    - collab
# blogs

## [What is a JavaScript Data Grid? display-first vs edit-first](https://handsontable.com/blog/what-is-a-javascript-data-grid)

- A data grid is essentially a feature-rich interface for working with tabular data.
  - The traditional “table” refers to an interface that displays tabular data but doesn’t offer much interactivity.

- Display-first
  - Represents the data and its structure in easy to explore way
  - Column-oriented
  - filter/sort/group/pagination
  - pivot
  - tree-view
  - cell-types
  - virtualization

- Edit-first
  - Captures data and allows it to be modified
  - Cell-oriented
  - cell-editing
  - cells-spanning/merged
  - copy/paste
  - auto-fill
  - formula
  - comments

- If you need a well-made, edit-first data grid, consider Handsontable

## [Browsertech Digest: Figma is a File Editor](https://digest.browsertech.com/archive/browsertech-digest-figma-is-a-file-editor/)

- Most desktop applications are what I call file editors.
  - By file editor, I mean that the user selects a file on disk, and the program loads it into memory. User changes are applied in-memory and periodically saved back to disk.

- Most web apps, by contrast, are what I call database apps.
  - Instead of loading a whole file into memory upfront, database apps render views of the data by fetching data from a database as needed to render the UI. 
  - When the user makes changes to the data, those changes are persisted back to the database via API calls.
- Database apps are a good fit for “CRUD” tools like calendars, todo lists, and tools with three-letter acronyms containing “manager” (CMS, CRM, PIM).

- One of the challenges of writing desktop-class software that runs in the browser is that file editors do not translate as naturally to the architecture of the web as database apps do.

- The design tool Figma is a good example of a file editor that runs in the browser.
  - When you open a Figma design, your browser downloads (over WebSocket) a “Fig file” corresponding to that design. 
  - The file contains binary data serialized with kiwi. 
  - Kiwi is a binary format similar to Google’s Protobuf, open-sourced by former Figma CTO Evan Wallace.
  - You can think of a kiwi file essentially as compressed JSON.

- Figma persists these Fig files to Amazon S3.

- A naive approach would have been for the client to treat S3 like a network file system and use it the same way a desktop app would use its local file system. 
- This would have two problems:
  - The whole file would have to be sent for every change, which is a waste of bandwidth as files get large.
  - Figma supports multiple concurrent users per document. If every change caused the entire document to be rewritten, race conditions from concurrent edits would cause data loss.

- Figma avoids both of these problems by taking a more sophisticated approach. 
  - When you open a Fig file, it’s actually loaded in two places: in your browser, and on a server.
  - Instead of writing back the entire file on each change, clients stream back only the changed data. The server applies those changes to its own in-memory copy to keep it synchronized.
  - The tricky part is that when multiple users open the same Fig file concurrently, Figma’s infrastructure needs to ensure that they are all connected to the same server. That server can then be the sole authority on the state of that document, and write to it without race conditions.

- Why not use a database?
- Figma stores file metadata in a Postgres database. 
- Instead of going to the trouble of using S3 too, they could have also used the database for document data, in one of two ways:
  - They could stuff the whole document into a binary blob or json(b) column next to the metadata. using the database as a file system, which is bad.
  - They could represent the document itself as rows and tables in a relational database.using the database as a database, but it adds a bunch of complexity to the application layer, which needs to be able to translate between a document representation in memory and a relational representation in the database.

- In either case, another consideration at scale is that S3 can be 10-100x cheaper byte-for-byte than a database. The query capabilities available in a database come at the cost of computational overhead, and it’s a waste to pay that overhead when you have a known, file-like access pattern.

- Writing the whole document to S3 is relatively slow, so Figma only does it every 30-60 seconds. 
  - But if the system responsible for writing those checkpoints fails (say, the power goes out), Figma doesn’t want to lose 30-60 seconds worth of changes. So they buffer changes at a higher frequency by saving them to DynamoDB, as a write-ahead log.

- Generalizing Figma’s approach
  - This post came out of research we’ve been doing towards building an open-source document database that takes a similar approach.
  - Recently, we introduced “locking” into Jamsocket and Plane, which can guarantee that at most one backend runs per document, motivated by desire for a Figma-like data architecture.

## [ContentEditable  —  The Good, the Bad and the Ugly_201508](https://ckeditor.com/blog/ContentEditable-The-Good-the-Bad-and-the-Ugly/)

- ### ContentEditable is evil and the Selection API is its evil twin. Avoid them as much as possible. 
- You need a custom selection system. 
  - It must be doable nowadays to get position (represented by a range, but we’ll simplify this in a moment) in the DOM on mousedown/mousemove. 
  - You’ll display your custom caret (whoa… you can control its style now) and text selection (it’s a simple ).
- You need to handle typing. 
  - Let’s listen to the keyboard events and insert given character into the editor.
- You need to handle navigation using the Arrow keys. 
  - Left and right seem easy, up and down a bit trickier but if you have point 1, you’ll do this too. 
  - Wait, there’s the Alt modifier which makes the Left and Right Arrow keys jump entire words. 
  - But of course you’ll look for spaces in the text and that’s it — told you, it’s trivial!
- Then you need to do something with pasting. 
  - You see that with the Clipboard API you can listen to the paste event on the document and retrieve the data from the data transfer. 
  - You can also use the old paste bin mechanism.

- ### ContentEditable — the Good Parts
- It’s amazing that adding one attribute to an HTML element enables typing, selection, keyboard navigation, spell checking, drag and drop, pasting, undo manager. 
  - That all of this is integrated with the OS, 
  - that such editor can be used with a screen reader or on a touchscreen device 
  - and that it’s well internationalised. 

- ### CKEditor
- Over the past years, while working on CKEditor I noticed that we were gradually replacing native features with our own implementations. 
- Since version 4.0, CKEditor has its custom “insert HTML into selection” mechanism and a feature allowing reaching non-editable places.
- CKEditor 4.1 introduced highly customisable content filtering (no more mess on paste). 
- CKEditor 4.3 brought support for non-editable islands with editable islands inside which required overriding many native systems (selection, keyboard, focus, clipboard).
- Finally, just a few weeks ago we made a final takeover of the clipboard, which means that in some browsers copy, cut and paste operations are fully handled by CKEditor.
- It means that today CKEditor does not let the browser do anything to the content except handling typing, some deleting and that’s basically it. 
  - At the same time, it still uses the native selection system, keyboard navigation and other APIs such as those related to clipboard or focus management.

- With CKEditor 5 we are planning to conclude this process by letting the browser insert text only, but with CKEditor’s control.

## [Text Editor: Data Structures | Hacker News_201710](https://news.ycombinator.com/item?id=15381886)

- in my editor (CodeMirror) I'm also using a rope/tree style representation, because it's pleasantly general and easy to reason about
  - [CodeMirror's document representation_201209](https://marijnhaverbeke.nl/blog/codemirror-line-tree.html)

## [A Brief Glance at How Various Text Editors Manage Their Textual Data_201505](https://ecc-comp.blogspot.com/2015/05/a-brief-glance-at-how-5-text-editors.html)

- A review of how GNU Moe, Plan 9 Sam, Bill Joy's Ex/Vi, GNOME GtkTextView/GtkTextBuffer, GNU Emacs, and due to popular demand, Scintilla, manage their textual data. This article is subject to updates.

### [A Brief Glance at How Various Text Editors Manage Their Textual Data (2015) | Hacker News](https://news.ycombinator.com/item?id=11244103)

- If you are interested in this, [Data Structures for Text Sequences](https://www.cs.unm.edu/~crowley/papers/sds.pdf) by Charles Crowley is an excellent paper to study.

- The article is missing one of the important but commonly overlooked structures: a "piece chain" (aka "piece table"). 
  - Not easy to find editors using it, especially among the popular ones, but:
  - from what I've read somewhere, MS Word was/is (?) using it internally
  - AbiWord the text editor of the Oberon OS used it 

- I'd like to see someone write on how web based rich text editing tools store their textual data.
  - quill/draftjs/prosemirror/trix 
  - Each of them might be relying on some form of Tree to store the content which actuates the views to react. I'm only guessing. A deeper, closer look might be interesting and useful.

## [xi-editor retrospective_202006](https://raphlinus.github.io/xi/2020/06/27/xi-retrospective.html)

- The original goal was to deliver a very high quality editing experience. 
- To this end, the project spent a rather large number of “novelty points”:
  - Rust as the implementation language for the core.
  - A rope data structure for text storage.
  - A multiprocess architecture, with front-end and plug-ins each with their own process.
  - Fully embracing async design.
  - CRDT as a mechanism for concurrent modification.

- There are only a few data structures suitable for representation of text in a text editor. 
  - 👉🏻 I would enumerate them as: contiguous string, gapped buffer, array of lines, piece table, and rope. 
  - Array of lines has performance failure modes, most notably very long lines. 
  - Similarly, many good editors have been written using piece tables, but I’m not a huge fan; performance is very good when first opening the file, but degrades over time.

- My favorite aspect of the rope as a data structure is its excellent worst-case performance. 
  - Basically, there aren’t any cases where it performs badly. 
- The main argument against the rope is its complexity. 
- One of the best things about the rope is that it can readily and safely be shared across threads. 
  - Ironically we didn’t end up making much use of that in xi-editor, as it was more common to share across processes, using sophisticated diff/delta and caching protocols.

- The reality was that adding async made everything more complicated, in some cases considerably so.
- A particularly difficult example was dealing with word wrap. 
  - In particular, when the width of the viewport is tied to the window, then live-resizing the window causes text to rewrap continuously. 
  - With the process split between front-end and core, and an async protocol between them, all kinds of interesting things can go wrong, including races between editing actions and word wrap updates. 
  - More fundamentally, it is difficult to avoid tearing-style artifacts.

### [crdt retrospective of xi-editor](https://github.com/xi-editor/xi-editor/issues/1187#issuecomment-491473599)

- My conclusion now is that these different use cases are actually different, and a "one size fits all" approach does a disservice(损害，破坏).
- Successful software project management is mostly about taming complexity. 
  - CRDT's do not have this property. By now we have lots of examples where trying to design features around the structure imposed by CRDT turned out to be a lot more complicated than it would be in a more synchronous world 

- For a while, xi had difficulty making up its mind whether it was actually a collaborative editor or not.
  - At the back of my mind, I hoped that a solid CRDT engine would evolve into something that would relatively easily support collaborative editing.

- CRDT is a tradeoff
  - Aside from the mathematical foundation, the main thing CRDT buys you is the ability to propagate edits through a mesh-like network, exploiting local connections, as opposed to requiring a central server.
  - For large scale organizations (I'm familiar with those and have had great conversations more recently with @dsp), I think it does make sense to treat the set of analysis and review tools as a form of collaborative editing, but those are also cases where a centralized server is completely viable.
- The flip side of the tradeoff is that you have to express your application logic in CRDT-compatible form

- So I come to the conclusion that the CRDT is not pulling its (considerable) weight. 
  - When I think about a future evolution of xi-editor, I see a much brighter future with a simpler, largely synchronous model, that still of course has enough revision tracking to get good results with asynchronous peers like the language server. 
  - The basic editing commands, including indentation and paren matching, are more simply done as synchronous operations, and I think avoiding that complexity is key.
# blogs-dev
- [编辑器背后的数据结构](https://dontpanic.blog/data-structures-under-editors/)
  - 部分Emacs使用了**Gap Buffer**，包括古老的 Emacs on TECO、现代的GNU/Emacs及其前辈Gosling Emacs。
  - Scintilla (即包括Code:: Blocks在内的很多IDE/编辑器使用的代码编辑控件) 也使用了Gap Buffer
  - Emacs进入由Lisp实现的时代后，一些Emacs版本使用了**LinkedLine**。
  - Vim使用的是一种基于行的数据结构，但行与行之间不是简单地使用链表连接，而是用一种树结构进行管理。
  - KDE的Okteta 16进制编辑器使用了**Piece Table** Buffer

- [《从零开始, 开发一个 Web Office 套件》系列博客目录_赵康_202202](https://www.cnblogs.com/forzhaokang/p/15907371.html)
  - https://github.com/zhaokang555/canvas-text-editor
  - https://zhaokang555.github.io/canvas-text-editor/
  - 基于 HTML Canvas 的富文本编辑器

- [基于 Google Doc 思想的L2编辑器演示项目](https://zhuanlan.zhihu.com/p/392055486)
  - https://github.com/cg0101/docs
  - https://cg0101.github.io/docs/

- [现代编辑器技术原理](https://www.wenxi.tech/principles-of-modern-editor-technology)
# ref
- [前端——富文本编辑器专栏](https://www.yuque.com/xiaoxiaojianbojun/wt03g5)

- [张驰技术博客](https://juejin.cn/user/3456520286121437/posts)

- [自研一个word应用，需要哪些基本功能](https://juejin.cn/post/6922682336412696584)

- [基于Clipboard的复制粘贴实现](https://juejin.cn/post/7118899649687060487)
