---
title: lib-office-note-taking-community
tags: [app, community, joplin, note-taking, notion-like, typora, zettlr]
created: 2024-01-29T17:20:09.671Z
modified: 2024-01-29T17:21:25.476Z
---

# lib-office-note-taking-community

# guide

# discuss-stars
- ## 

- ## 

- ## [Evernote to be acquired by Bending Spoons | Hacker News _202211](https://news.ycombinator.com/item?id=33623402)
- I learned three things watching EN snatch defeat from the jaws of victory:
  1) There is almost never a case for a total ground up rewrite of your core product. Just don’t do it.
  2) Don’t abandon the users who made you successful in the first place. They’re the ones who advocate for you and get your foot in the door.
  3) real time google docs style collaborative editing is table stakes for this software category. Build your V1 with it in mind. Otherwise you’ll have to do a rewrite later. See 1.
- "Collaborative editing" is table stakes for a modern note editor because even in a single user scenario you will have the same user editing the same note from multiple devices with different levels of connectivity. The product needs a reputation that it will not lose its user's edits, nor will it make annoying branch-style merge conflicts.
- Agreed on point 3 for modern editors in 2022, as real-time collaboration and collaborative editing are table stakes today if you want to compete. 
  - We started with OT in mind for V1 of Taskade with the intention to make our editor collaborative, but it was still a bumpy road before we were able to iterate on the product and speed up our dev cycle, . It continues to be a challenge to support the various use cases and customers, as improvements for offline editing, cross-device syncing, and recovery never ends.

- Google docs didn't exist when Evernote started. Their competitor was OneNote.
# discuss
- ## 

- ## 

- ## [国内新兴笔记软件wolai、Roamedit、FlowUs、思源、太记，你更看好哪一个的发展前景？](https://www.zhihu.com/question/444890872/answers/updated)
- 一个都不看好。
  - 按照现在的行业管理定义笔记软件，
  - 只要你带上云的功能，就是个内容发布的平台。
  - 只要内容可以分享到其他人，那它就属于一个社交信息平台。
  - 什么意思呢？ 只要符合这两种定义，那服务提供商就必须要提供内容审核机制，所以我们笔记里的这些信息内容就需要对服务提供商完全开放阅读权限。

# discuss-files-first
- ## 

- ## [Show HN: Supernotes 3 – Offline-Ready, Collaborative and Cross-Platform Notes | Hacker News _202309](https://news.ycombinator.com/item?id=37403444)
- One thing that always comes up with posts about CRDT is how they typically don't handle formatting markers when resolving edits. How is this (and CRDT) handled in SN?
  - First off, that is one reason we decided to stay with Markdown and picked YJs for our CRDT library. Markdown because it is plaintext, and in our testing we found it was a lot easier to conserve user intent when merging plain text than actual rich text (i.e. JSON). YJs because the CRDTs are already fairly robust and designed with intent-preservation in mind.
  - That being said, we did end up writing a somewhat large system around our editor (we're using CodeMirror, which is also great to work with), because we wanted to take things further by excessively labeling transactions with additional context not included in the plaintext which allows us to batch certain types of transactions together and better preserve intent that way. We also use fractional indexing for some things (like lists) which generally do a good job of preserving multi-user intent.
  - Finally, in cases where sending edits over WebSockets via our own servers is suitable, we actually prefer that to sending them peer-to-peer (via WebRTC) as certain types of atomic operations become difficult in P2P scenarios. This kinda reduces one of the key benefits of CRDTs (over OT), but the P2P is still possible (and works), it's just sometimes not as good at intent preservation.

- ## 📓🎯 [Typora 1.0 | Hacker News _202111](https://news.ycombinator.com/item?id=29360720)
- Document editing is only a part of maintaining a system of notes and there are so many competitors in this market compared to just a few years ago. And with Obsidian soon to release their live preview I don't know how competitive Typora with such a small feature set.
- Typora is a markdown reader/writer not a note taking or knowledge base application. It's strange for you to compare them like that.

- Typora is bad. It avoid the GPLv2+ from pandoc by writing their own HTML writer and the menu has additional export options that requires the user to install pandoc to be functional. It would have been much better if it is GPL and contribute back to pandoc in the first place 

- I love using Typora. My favorite feature is the mathjax support. It has replaced latex for me for grad school assignments and saves a lot of time.

- ## 📓 [Zettlr – FOSS markdown editor for personal knowledge management and publishing | Hacker News _202007](https://news.ycombinator.com/item?id=23723775)
- I've just been using Google Docs. It's simple, searchable, and I can read/edit my notes while sitting on the can.

- If anybody is sad about Zettlr not having the graph view of like the one in Obsidian or RoamResearch, please be patient. A PR is already open for it.
- Does anybody find that graph view (like in Obsidian) useful? I play around with it for a while, but I don't really find it useful for any particular thing. Also overtime that graph grows too big to be visually easy to see patterns etc.
  - Sometimes it's an alternative to search. If you don't know exactly what to search for but remember generally what it's related to, you can zoom in to nodes you know are somewhat related and find something you're looking for that way. I can't say it's something I do every day but it's come in handy.
  - The graph view in Obsidian would become particularly powerful if you could progressively filter brightness of items based on a search term. Or, for example, if you could make matching items brighter based on clicking / typing a tag name.
  - I've mainly found it to be inspirational when working creatively, especially when I'm writing a 'dirty first draft' of something, e.g. a research embryo, collecting interviews about a subject, doing brainstorming sessions, even book reviews. I've still got to come to grips with segmenting Obsidian vaults so that the cloud doesn't grow too far...

- The drawback to working directly on Markdown files is that it's hard to synchronize your notes from/to mobile.

- ## [Marktext – Elegant Markdown Editor for Linux, macOS, Windows | Hacker News _202112](https://news.ycombinator.com/item?id=29687061)
- To the best of my knowledge this (Marktext) is the only free/open-source Markdown editor that has WYSIWYG like Typora
  - Obsidian very recently added this too, and it works great.
  - Another free and open source note taking app with WYSIWYG is TagSpaces 
  - Jupyter notebooks does it the way I prefer the most.l: It renders italics, bolds headings and whatnot as you edit but keeps showing the tags.

- I recommend something like Obsidian instead which is a markdown editor (newly upgraded) along with an entire knowledge base and note taking system that can create and maintain references across files.

- Things I want in a markdown editor: Grammar check. Auto-capitalise start of sentence and known proper nouns. Auto fix obvious typos without bothering me. Grammatically smart spellcheck. Detect and flag accidental double space. Detect and flag duplicate words. Word count excluding headlines. It's nice when I use Google docs and it has that stuff. I wish I had it in markdown.

- ## [Mark Text: Simple and Elegant Markdown Editor Focused on Speed and Usability | Hacker News _201911](https://news.ycombinator.com/item?id=21462832)
- it directly renders the Markdown (in the editor itself, not in a separate pane or window), giving a WYSIWYG feel while still being backed by a plain-text (markdown)
  - I’ve tried Bear, Ulysses, IA writer, and countless others. None have this clever blended preview like Typora.
