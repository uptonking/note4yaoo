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
- [The future of document editing - inspirations](https://lukasmurdock.com/cms/)

## [从浏览器源码开始实现 Canvas 富文本编辑器 - 知乎_](https://zhuanlan.zhihu.com/p/642703113)

- https://github.com/WaiSiuKei/neditor /MIT/202308/ts
  - https://waisiukei.github.io/neditor/
  - rich text editor aimed at running in Canvas.
  - 在事件模型和 DOM 模型都准备好之后，移植 ProseMirror 就非常容易了。

- 作为行业的跟随者，效仿业界的标杆公司去做同样的事情往往会让你在技术评审中胜出。
  - 因此，我也选择了走向同一条技术路线：在浏览器中运行另一个浏览器。

- 最终，我发现了 YouTube 的 Cobalt 项目，它能够运行 HTML5 标准的子集。
  - 他们最初也是维护一个基于 Chromium 移植版，但为了在游戏主机、机顶盒等资源受限的环境中实现基于 HTML5 的视频浏览和播放应用程序
  - 他们从头开始构建了一个简化的 HTML 子集实现和 CSS Box 模型所需的代码，没有使用复杂的 Blink 内核，也没有使用 Chromium 复杂的合成器和渲染管线的代码。
  - DOM 层：这是实现 W3C 标准子集的地方，可以支持常用的 HTML 标签，布局方面支持流式布局和 Flex 布局。 
  - 布局引擎：基于 DOM 树计算布局树，并进一步生成用于指示绘图的渲染树，以发送到渲染器。 
  - 渲染器/ Skia：渲染器遍历布局引擎生成的渲染树，使用 Skia 图形库对其进行绘制、光栅化输出

- 在将 Cobalt 内核移植用于渲染后，我可以使用 HTML 来描述 DOM 结构，然后渲染内核就可以在 Canvas 元素内绘制出界面内容，但是这只是一个单纯的数据展示层，我还需要完成完整的架构设计，将各个分层模块组合起来才能形成富文本编辑器。

- 我使用了 Vue 来构建 DOM 树。然而，在现在这个基于移植的虚拟 DOM 的富文本编辑器中，我们可以选择一些没有虚拟 DOM 层的前端框架（例如 Svelte），以减少不必要的层级。我选择了 Pettie-vue 项目，它类似于 Vue，可以将响应式对象转换为想要的页面，但比 Vue 更简单，更容易移植到我所定义的虚拟 DOM 层上。

- Model -> ViewModel -> View（DOM 树）-> Layout 树数据 -> Render 树数据

- 在完成了上述事件机制之后，我回头结合之前研究的浏览器源码来对 ProseMirror 进行移植。

- Cobalt 源码中没有 Chromium 中所有与文本编辑相关的部分，但是两者都是基于遵守 HTML 标准去实现 Node、Text、Element 和 HTMLElement 这些类。
  - 这使得我可以直接从 Chromium 的 Editing 模块中复制与 Range 和 Selection 相关的代码来使用。
  - 在事件模型和 DOM 模型都准备好之后，移植 ProseMirror 就非常容易了。

- 作为一个练手项目，这个编辑器已经验证了将浏览器应用移植到 Canvas 中的可行性。

## [vscode: Text Buffer Reimplementation, a Visual Studio Code Story to piece-tree](https://code.visualstudio.com/blogs/2018/03/23/text-buffer-reimplementation)

## [Text Editor Data Structures](https://cdacamar.github.io/data%20structures/algorithms/benchmarking/text%20editors/c++/editor-data-structures/)

- I wanted to solve all the problems that having a single giant text buffer had
  - Efficient insertion/deletion.
  - Efficient undo/redo.
  - Must be flexible enough to enable UTF-8 encoding.
  - Efficient multi-cursor editing.

- Gap buffer
  - gap buffer is very simple to implement and Emacs famously uses a gap buffer as its data structure
  - pros
    - Efficient insertion/deletion
    - Must be flexible enough to enable UTF-8 encoding
  - cons
    - Efficient undo/redo
    - Efficient multi-cursor editing

- Rope
  - rope splits the file up into several smaller allocations which allow for very fast amortized insertions or deletions at any point in the file, O(lg n). 
  - pros
    - Efficient insertion/deletion
    - Must be flexible enough to enable UTF-8 encoding
    - Efficient multi-cursor editing
  - cons
    - Efficient multi-cursor editing

- Piece Table
  - Microsoft Word used a piece table once upon a time to implement features like fast undo/redo as well as efficient file saving
  - drawback: Due to the fact that the traditional piece table is implemented as a contiguous array of historical edits, it implies that long edit sessions could end up in a place where adding lots of small edits to the same file will cause some of the artifacts we saw with the giant text buffer start to appear, e.g. randomly your editor may slow down because the piece table is reallocated to a larger array. Not only this, undo/redo stacks need to store this potentially large array of entries.
  - Then, the VSCode team went and solved the problem. Enter **piece tree**
  - pros
    - Efficient insertion/deletion (minus very long edit sessions).
    - Efficient undo/redo (minus very long edit sessions).
    - Must be flexible enough to enable UTF-8 encoding.
    - Efficient multi-cursor editing

- Piece Tree
  - The piece table that VSCode implemented is like if the traditional piece table and a rope data structure had a baby
  - You get all of the beauty of rope-like insertion amortization cost with the memory compression of a piece table. 
  - The piece tree achieves the fast and compressed insertion times through the use of a red-black tree (RB tree) to store the individual pieces. 
  - This data structure is useful because its guarantees about being a balanced search tree allow it to maintain a O(lg n) search time no matter how many pieces are added over time.
  - the VSCode implementation does not use immutable data structures, which means that I will need to copy the entire piece tree (not the underlying data of course) in order to capture undo/redo stacks. So it does have some of the drawback of the piece table, so let’s just fix it! it's hard

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

## 📝 [Browsertech Digest: Figma is a File Editor](https://digest.browsertech.com/archive/browsertech-digest-figma-is-a-file-editor/)

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

## 👥 [Figma Is a File Editor | Hacker News_202307](https://news.ycombinator.com/item?id=36702939)

- 
- 
- 

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
  - Each of them might be relying on some form of `Tree` to store the content which actuates the views to react. I'm only guessing. A deeper, closer look might be interesting and useful.

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
