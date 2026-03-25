---
title: lib-editor-app-community-architecture
tags: [architecture, community, editor, text-editor]
created: 2024-12-28T19:10:41.691Z
modified: 2024-12-28T19:11:01.446Z
---

# lib-editor-app-community-architecture

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## There is no reason a rich text editor has to be coupled with a UI framework. None. It's just a state machine. It has to be headless.
- https://x.com/thesegunadebayo/status/2027936212036534652
  - TipTap is headless. It has bindings for React and Solid, but I completely forewent those and built my own UI on top. Works like a charm.
- Is there any good such option out there? The @formisch_dev approach could work here too.

- The same goes for most UI components, regardless of complexity. With a state machine or any event-driven architecture, you can model components without coupling them to a framework. Working on @zag_js proved this for me.
  - yep - this is why frameworks like XState catch on. the hard part isn't drawing boxes and arrows, it's making state transitions explicit and testable. we cut bugs 40% in a complex form flow just by modeling it as a proper FSM first

- Slate (mostly) works this way  2 years ago I, AI assisted, built a fully customizable internal text editor using it, pretty powerful, that said the complexity and platejs has built ontop of slate isn't ideal imo. I'm super tempted to see if I could build a tiptap version

- You might like the Portable Text Editor, BYOUI
  - Also worth pointing out it is state machines all the way down, with xstate 

- afaik although lexical is focused to be used with react, it is agnostic and low level. it have a good set of primitives
# discuss-edit-with-diff
- ## 

- ## 

- ## 

- ## Sonnet-4 is trained to use a specific Text Editor Tool that is super well designed to understand diffs, make edits etc drastically increasing the quality of every change.
- https://x.com/pelaseyed/status/1948835276127973689

- I gave claude a more advanced edit tool (with white-space forgiving context, line-scoped edits, etc.) But claude defaults to only use `old_string` and `new_string` without the fancy arguments. This could explain why.
- The edit tool is just search replace. There’s nothing magic about it, but they did train the model to be great at that task.

- the magic sauce is probably the detailed structuredPatch tool result, which allows claude to keep track of the current content of the file

- the diff understanding is game-changing. use claude code for workflow debugging when n8n nodes break. it reads the entire workflow structure, identifies the failing connection, and suggests fixes with surgical precision. other coding assistants just generate code. claude code actually understands the system it's modifying
# discuss-typora-like-inline-toggle
- ## 

- ## 

- ## 

- ## 做了个简陋的 demo，大概长这样，开个 thread 随便说说开发这类编辑器需要注意的细节。
- https://x.com/kk_shinkai/status/2036618066080202780
  - 实现这类编辑器有两种思路。一种是富文本思路，把它当作结构化编辑器去做，把每一个样式的转换和触发条件整理清楚；另一种是代码高亮思路，把它当作一种特殊的代码编辑器，隐藏特定的 token。
  - 富文本思路最大的难题是很难靠枚举触发条件来保证格式转换不被遗漏，下面的视频演示了一种最常见的情况 (有些编辑器甚至连这种情况都没照顾到)，但由于 Markdown 还有软换行和缩进等造成的边角条件，事情还要更复杂得多。
  - 代码高亮思路则恰相反，对它们来说准确的转换样式没有难度，问题是由于所有空格和空行都被暴露在外，因此很难做出好看的样式。“空行” 和 “段落间距” 不是同一个概念，缺少了结构化的树状表示，你会发现这类编辑器不管怎么调主题看起来都不太协调，而且难以应付带前导空格的嵌套结构。
  - 其实还有第三种思路，我称之为鸵鸟思路，就是做出来一个纯粹的垃圾然后假装它没有任何问题，其中最出名的就是 Obsidian。我不想显得太 mean，而且之前也骂过很多次了，就不多说了。
  - Typora 是混合的，块级别的节点是富文本思路，行内文字则是代码高亮思路，利用 Markdown 的解析结果高亮并折叠特殊字符，同时判断块的类型是否需要转换。这弥补了两种思路的致命缺陷，但是不致命的缺陷仍然很多，需要花大量精力去缓解。
  - 富文本思路最糟糕的一点就是你很难保持源码形态，如果用户只是用你的软件修改几个字，列表开头的 “*” 就变成了 “-”，或者段落间的三个空行变成了一个，那么这显然是不可接受的。这需要你为 Markdown 设计 CST (具体语法树) 而不是 AST，主流的开源 Markdown 解析器根本没有这种功能。
  - 富文本思路帮我解决了样式问题，让我的编辑器可以轻松地通过 CSS 调出合适的段落间距，嵌套和缩进，所以我没什么好抱怨的，但是它仍然有很多让人血压飙升的时刻

- 以前做过类似的功能，技巧：用 prosemirror 的 decorate 功能，而不是 mark，定制一个 tokenizer 提取 markdown 的 inline mark，光标进入 [a, b] 时显示 mark，否则将 mark absolute 到 -999px 的地方。 decorate 是非阻塞的，编辑体验会比较好。

- https://x.com/kk_shinkai/status/2036612473923817493
  - 准备做一个类 Typora 的 Markdown 编辑器，本以为这种 AI 时代 infra 级别的东西应该有大厂愿意主动站出来做，结果大家好像兴致寥寥。在被各种 Typora 的拙劣模仿者做出的半成品折磨后，我觉得我应该是等不到了，还是让我自己试试吧。

- 能基于zed做一个吗？受够的要点preview，还不好看mermaid
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Got carried away with this minimap. Took me a while to figure out the drag scaling maths.
- https://x.com/DanHollick/status/1891205758399701319
- it's where you want element() to have better support. assuming you're doing something fancy and not duping the content in there? 

- ## [NotepadNext: A cross-platform reimplementation of Notepad++ | Hacker News _202204](https://news.ycombinator.com/item?id=30959025)
- Efficiently handling large text files requires extra special care.
  - ~2x memory looks like a naive implementation of just allocating an std::string from heap for each line. Due to heap fragmentation and various overhead it would quickly blow up.
  - ~1x memory looks like just reading the entire file into RAM (that would still be slow).
- A truly efficient implementation would never need to load the entire original file in RAM.
  - It would just need to remember the binary offset of each line in a way that combines random access and reasonably fast insertion/deletion (e.g. K-fold trees). You can even keep everything beyond the top-level directory in an temporary on-disk file, so your RAM usage could be less than 1MB with nearly instant performance.
  - The efficient implementation is tricky, error-prone, and involves handling a solid amount of corner cases, which is beyond the amount of hassle a typical hobbyist developer is willing to go through.
- > To know the offset of each line, you'll need to load the entire file from disk.
  - No. You will need to read the file, not load it all at once in memory. And for a sequential scan, you need very little memory at any one time.

- With a 64-bit address space, you're probably better off just mapping the entire file into memory, not specifically loading it all. Let the OS swap in and out the pieces you need as you access it (and build your index of line offsets or whatever other structures you need).
- The big advantage to mapping is that you only read from disk the portions of the file you need, and only when you need them. Disk access is monumentally slow, so this can be a big win: if you don’t need to access all of a large file, or don’t need to access it all at once, mapping saves you very expensive operations or spreads them out over time.
  - The problem with that for a text editor is that probably the first thing you want to do is process the line endings. So you’re just going to access the entire file, right away, as fast as possible anyway.
  - The problem with that for a text editor is that probably the first thing you want to do is process the line endings. So you’re just going to access the entire file, right away, as fast as possible anyway.

- Why not just use mmap() or the Windows equivalent?
  - Let me rant for a bit because I've dealt with the following: Another downside is you'll get people complaining about memory usage despite mmap only paging in what's needed.
  - Mmap is a brilliant way to have the os handle which parts of the file actually reside in memory but you'll seriously have to deal with users that know only enough to be dangerous complaining that your app uses gb of ram when it's merely mapping a file into virtual address space to allow the os to page as it sees fit.
- Because then all your edits have to go directly into the file, so you have no real "save" flow unless you make a swap file for every file and then mmap that (which can be an appropriate approach, to a degree). Then all your caching and memory use subject to OS I/O and filesystem concerns, and you can't optimize for specific use. And inserting or deleting the middle of the file means shifting all the bytes after it.
  - I could think of a reasonable implementation for Linux that would use mmap and fallocate, but it wouldn't "just" be an mmap, as the swap file would still need to represent a rope or a gap buffer or something else of the sort for efficient editing.

- 
- 
- 
