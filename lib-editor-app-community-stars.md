---
title: lib-editor-app-community-stars
tags: [community, editor]
created: 2022-06-12T22:14:05.479Z
modified: 2022-08-21T10:12:02.964Z
---

# lib-editor-app-community-stars

# guide

- 编辑器研发方向
  - 实时协作
  - 版本控制
  - 离线存储
  - features
    - 开放api
    - 双向链接

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
    - 虚拟渲染能提高安全性?
  - defer render

- not-yet
  - 搜索编辑器内容时，如何搜索带格式的文本，如关键词为 解构`props` 时如何搜索
  - 将bibtex插入编辑器的逻辑实现有问题，如何只在光标点击editor内容后才执行插入bibtex的command，否则就会出现现在的问题，鼠标若不再editor中点击一下就不执行该逻辑

- https://github.com/powcoding/etherpad-core  /仅文档和示意图/无代码
  - etherpad产生diff的2种方式
    - 点击菜单栏上的功能按钮
    - 用户在编辑器内不断的输入文字，那么etherpad通过定时检测来获取内容的变化
  - etherpad内嵌了自己的一个编辑器ace editor，不支持接入第三方富文本编辑器
  - 但etherpad具备了完整的实时协作机制，包括：客户端、服务器端的模型设计，多人冲突的设计，对富文本格式的解析，对输入法的支持等。
  - 如果能利用etherpad的实时协作机制，又能接入第三方编辑器，那就是一个完美的方案
  - etherpad产生diff的2种方式中的第1种方式，完全是etherpad自己的私有机制，没法接入第三方编辑器
  - 但是利用第2种方式，不管第三方编辑器如何改变编辑器内容，只要让etherpad定时去检测到变化，就能生成diff，后续流程完全和原生etherpad一致
  - 将etherpad对内置编辑器的绑定解耦，通过设计api暴露出来，可绑定到第三方编辑器上。这样第三方编辑器就具备了和原生etherpad相同的整套实时协作编辑的能力
# discuss
- ## 

- ## 

- ## [I reverse engineered Google Docs to play back any document's keystrokes (2014) | Hacker News _202012](https://news.ycombinator.com/item?id=25545361)
- I was working on the Google Slides team at the time this blog post was originally published back in 2014. 
  - Slides and Doc are extremely closely related projects, sharing lots of code (and even sitting next to eachother, at the time at least). 
  - Our entire team was impressed with the details of the operational transform protocols that the author was able to reverse engineer, and for the most part get correct. IIRC our engineering director ended up calling the guy up for a lunch.
- Sending around protobufs encoded as JSON makes reverse engineering much easier than you might imagine.
- It's crazy how vast and powerful databases of even the most simple things turn out to be. You just store characters and context information when someone types them, and this is the result.

- ## Have we talked about sub-documents?
- https://twitter.com/blaine/status/1409611697157918728
  - Long story short, we have recursive logic in atjson to render atjson documents that are embedded in annotations. Useful for lots of things; e.g., comments can be fully annotated/formatted, tombstones of deleted text can contain the full deleted text (including formatting, etc)
- A sub-document in an annotation is definitely a convenient solution for first level footnotes, margin notes, etc., but if you want an indefinitely extensible text canvas then at some point you would want to reference external texts, I think. It leans more into the graph model.
- Do you contain the other document inside an annotation or do you reference it? 
  - We just store it straight in the document, but whether it's a reference or embedded is an implementation detail, I think?
- I'm not very comfortable with the idea of annotations containing a whole new document, which itself contains another one, but how can it be prevented? Force the user to write shorter notes
- Yes, you're quite right about circular reference - if the sub-documents are not literally stored on the annotations, but say in a parallel structure. In any case, I doubt it is practical to carry around a large document graph in JSON when you can fetch each one as needed.

- ## [kilo: Build Your Own Text Editor | Hacker News_201908](https://news.ycombinator.com/item?id=20603567)
- What I instantly liked is, how literally it starts from scratch and builds a couple of lines at a time.
  - Can anybody refer to a similar step by step guide to building a compiler?

- ## [Ask HN: How to learn about text editor architectures and implementations? | Hacker News](https://news.ycombinator.com/item?id=29874669)
- Similar suggestion: if you're trying to learn the architecture of a big established project like Vim or Emacs, don't start at the top and try to follow everything. Start with a small feature you would like to tweak, implement, or understand. How does Emacs render the modeline, for example
- probably you are studying editors that are too big for your purposes - find something smaller in scope

- [Build Your Own Text Editor](https://viewsourcecode.org/snaptoken/kilo/)
  - This is an instruction booklet that shows you how to build a text editor in C.

- [Hecto: Build your own text editor in Rust](https://www.flenker.blog/hecto/)
  - This is a series of blog posts that shows you how to build a text editor in Rust. 
  - It’s a re-implementation of kilo in Rust

- There’s also the Racket editors, which includes a text editor control, in the Racket Graphical Interface Toolkit. It’s what is used to implement the DrRacket IDE.
  - [Editors](https://docs.racket-lang.org/gui/editor-overview.html)

- Rob Pike has published several great papers about sam, the Plan 9 text editor he wrote.

- Architecture-wise, you can start with an ordered list of lines, with each line stored as a string.
- Features that complicate things are:
  - supporting large documents and staying speedy (“replace all” is a good test case)
  - supporting line wrapping or proportional fonts (makes it harder to translate between screen locations and (line, character) offsets)
  - supporting Unicode (makes it harder to translate between screen locations and (line, byte position) offsets)
  - syntax-colouring
  - plug-ins
  - regular expression based search (fairly simple for single-line search _if_ you store each line as a string; harder for custom data structures, as you can’t just use a regexp library)
  - supporting larger-than-memory files (especially on systems without virtual memory, but I think that’s somewhat of a lost art)
  - safely saving documents even if the disk doesn’t have space for two files (a lost art. Might not even have been fully solved, ever)

- Rope was my original thought too as one of the original data structures for text editing. It's used to quickly insert/delete within a very large string.
- In my opinion, the rope is easily superior to these other types, but it also depends on whether your language supports abstractions well. The problem with an "array of paragraphs" is that it helps when your problem involves the paragraph boundary, but gets in the way when it doesn't. For example, pressing backspace at the beginning of paragraph 2 causes a merge of paragraphs 1 and 2, which is not trivial. With a rope, it's the same as deleting a backspace within a simple string, once you have a good rope library under you.
- The other big reason to prefer a rope is that the worst case complexity is excellent. 
  - Basically all incremental operations are O(log n). 
  - With an "array of paragraphs" you get various pathological performance cases such as a huge number of small paragraphs or one very big one.

- I used a double-linked list of gap buffers (each in its own fixed length block that can swapped out to disk) for JOE. It works great on large files, but still I would start with rope these days.
  - Gap buffer was appealing on really slow machines, where you are counting cycles on each key-press. If the gap is at the right position, the cycle count is very low. But you can probably do the same even with a tree-structure: you need to keep a pointer to the leaf in the abstract pointer used for the cursor.
  - Also I would tie in the undo system to the data structure if possible. Rope does this with copy-on-write. Every version of the file could be a different top-node, and most middle and leaf nodes would be shared between revisions.

- [A Brief Glance at How Various Text Editors Manage Their Textual Data (2015) | Hacker News](https://news.ycombinator.com/item?id=11244103)
  - JOE was written in the final days of expensive memory and was written so that it can edit files larger than memory. Even today this is sometimes useful: you can edit an 8 GB file on a 32-bit machine.
  - It uses a doubly linked list of gap buffers. Each gap buffer has a header and a 4K data page. The headers are always in memory, but the data pages can be swapped out to a file in /tmp. The memory usage limit is 32 MB. Possibly this is no longer a good idea- it's easily possible that you could have more RAM than /tmp space.
  - The header has the data page's offset in the swap file, the link pointers, the gap location and a count of the number of newlines in the gap buffer.
  - When a file is read in, the gap buffers are completely full. So read-in turns into a direct read of the file into memory (or into the swap file). The only thing it has to do is count the newlines in each 4K data page and generate the headers.
  - The newline count is to speed up seeks to specific line numbers. [A long standing enhancement idea is to generate the newline count on demand and use mmap. This would allow the read in to be a NOP- just demand load the pages from the original file as needed and use copy-on-write when any change is made to preserve the original. But I'm also not sure it's a good idea to not take a snapshot of the original file- so this probably should be optional.]
  - JOE uses smart pointers to the edit buffer. Each pointer has the address of the header and a memory pointer to the data page (which is always swapped in if there is a pointer to it). The software virtual memory system has a reference count on each page. Each pointer holds a reference on the data page it's pointing to. If there is no pointer to a page, the reference count is zero, so it can be swapped out.
  - The other purpose of the smart pointers is automatically stick to the text they are pointing to, even through insert and delete operations. So if you insert at one point in the file, any pointers to further locations are updated (including line number, byte offset, column number and memory offset).

- ## 📝 [Writing Software to Last 50 Years | Hacker News_202001](https://news.ycombinator.com/item?id=22042186)
- Text files are king! I store every single byte I can in text files. Examples:
  - Tabular data     : TSV   (almost all Un*x/GNU tools handle this out of the box)
  - Simple "records" : GNU Recutils format (https://www.gnu.org/software/recutils/)
  - Formatted texts  : Markdown, LaTeX, ...
- If I need some hierarchical kind of information, I use a folder structure to handle this.
- I know that not everything can be stored as text. But I try to use open, well documented and future proof formats.
- If I really need to preserve original format/design of a web page: PDF

- [GNU Recutils - GNU Project - Free Software Foundation](https://www.gnu.org/software/recutils/)
  - GNU Recutils is a set of tools and libraries to access human-editable, plain text databases called recfiles. 
  - The data is stored as a sequence of records, each record containing an arbitrary number of named fields. 

- ## what's the best hybrid-structure code editor you've seen? an editor that combines tokens (eg values or references) and text
- https://twitter.com/_paulshen/status/1575187234449334273
  - do you back the semantic tokens with text? feels like you want some richer repr but hard for me to see how to make hybrid work

- honestly, soulver is the only hybrid editor I’ve found comfortable enough to use regularly
  - https://soulver.app/
  - Soulver is a notepad calculator app for Mac. It's a notepad that gives instant answers to calculations in your text.
  - Soulver is a better way to work things out than a classic calculator, and a more lightweight tool than a spreadsheet.

- https://www.jetbrains.com/mps/
  - MPS提供的软件开发环境可以创建新的定制语言，也可以扩展现有语言，然后用它们开发面向领域的应用。
  - MPS还可以定义新语言的类型系统、约束和专门的编辑器。MPS用一棵抽象句法树（AST）来维护代码。
  - MPS还采用了代码生成的办法：用新语言在更高的层次上表达，然后MPS生成Java、XML、HTML、JavaScript等语言的可编译代码。 用MPS建立新语言的时候，必须从BaseLanguage扩展。MPS已经提供了一些常用的BaseLanguage扩展，协助开发者处理字符串、容器、日期、正则表达式等语言成分。

- ## [对可多人协同编辑的在线编辑器，如何设计其 undo/redo 的逻辑？](https://www.zhihu.com/question/367915946/answer/985845505)
