---
title: pm-office-obsidian-community
tags: [community, markdown, note-taking, obsidian]
created: 2024-01-23T02:51:44.425Z
modified: 2024-01-23T02:52:23.932Z
---

# pm-office-obsidian-community

# guide
- pros
  - ?

- cons
  - ?

- features
  - ?
# examples-plugins
- https://github.com/tmcw/obsidian-freeform /MIT/202405/js
  - Obsidian freeform plugin. This lets you write arbitrary JavaScript, including importing ESM modules, injecting styles, and much more
  - This brings a taste of Observable to Obsidian. 
  - give you an @observablehq -like experience with editable code blocks that run in isolated iframes.
  - Based on iframes: Everything you write is run within a sandboxed iframe, making it safer to do more creative coding within Obsidian without affecting the surrounding page.

- https://github.com/PlayerMiller109/obsidian-sheets-basic /202408/js
  - merge markdown table cells after Obsidian v1.5.0
  - [小插件 Sheets Basic：合并 Markdown 表格单元格 - 经验分享 - Obsidian 中文论坛 _202405](https://forum-zh.obsidian.md/t/topic/35091)
# discuss-stars
- ## 

- ## 

- ## 

- ## The file over app philosophy does not make a distinction between data and file. Both are one and the same. 
- https://twitter.com/kepano/status/1764775797444026557
  - The source is the output, and vice versa. It's a two-way door.
  - Exports are useful if you want to exit the tool. Exports are not useful if you want to directly manipulate your data. Exporting requires your explicit intention, whereas file over app requires no intention at all. 

- Collaboration can be solved with git or CRDTs.

- Have you seen anyone implement the file over app philosophy well on web or mobile apps? I’m curious if it works as well as Obsidian does.
  - On mobile you can store files locally just like you can on desktop, but interoperability is somewhat limited by sandboxing, especially on iOS. With web apps there are various ways to store data locally, but I am not sure if that's what you had in mind. 
  - Cloud has its benefits but is inherently opposed to files.

- An export is sufficient for most people. Of course there are edge cases.

- ## 📏 File over app is a philosophy: 
- https://twitter.com/kepano/status/1675626836821409792
  - if you want to create digital artifacts that last, they must be files you can control, in formats that are easy to retrieve and read. 
  - Use tools that give you this freedom.
  - In the fullness of time, the files you create are more important than the tools you use to create them. Apps are ephemeral, but your files have a chance to last.

- Why not more generally "Data over app"? (or information, knowledge, content; a file is just a container)
  - They are related but different. Both are good. Files are a more specific, retrievable instantiation of the data.
  - > Obsidian mainly uses CommonMark, with some functionality from GitHub Flavored Markdown and LaTeX.
- data can live in some opaque container 
  - or it can live in an internal db 
  - or it can live in an easily understood and self-documenting json or markdown file 
  - you can choose

- This is exactly the approach I'm taking with SEN: extending the golden (quality and age wise) UNIX mantra of "everything is a file", you can express any entity as a file. 

- I prefer to prioritize content over files and files over tools. While files are undoubtedly important, they merely serve as containers for our content. The content itself is what truly matters and should be considered eternal, whereas files may come and go over time.
  - there's a lot of content stored in the container that is my head. if that content is not transferred to an externalized container, no one else can interact with it, and it may become degraded or forgotten
  - ideas can only survive and reproduce through externalization

- I don’t need files when I can export with Shortcuts – I can get structured data in whatever format I want.
  - Export-based workflows make sense when non-destructive formats are essential to the process (e.g. video editing, music production, etc) since the editable content is expected to be ephemeral, and is in service of a rendered output. 
  - For workflows where the editable content is the same as the final output then writing directly to a file is preferable to me
  - 🧩 "non-destructive editing" it means that editing does not modify the source data (pixels, audio, etc), but rather adds metadata about the edits, such that those edits can be recreated on top of the same or other source data

- I use @obsdmd but once you add plugins (dataviews, db_folders, etc.) your files lose value. Not to mention the hours I've wasted trying to replicate functions like @NotionHQ tables inside Obsidian - I can just do it NOW w/ an app. Sometimes time value trumps philosophy.

- real-time collaboration is compatible with file-based storage... you need good conflict resolution but everything has its tradeoffs

- This is a great philosophy, but expecting files to be read by older systems isn’t always feasible. For example sparse matrix storage, direct object serialization like pickles, or neural network compression. I love obsidian but not everything can be a txt file

- Apps are files too.
  - Applications are binary’s, tied to a specific processor architecture and OS. They are designed to be read by a specific family of machines, not humans.

- I have Word Docs from when I was young that I don't know if I can open any more. Word doesn't open them. Today:
  - Notes: md in Obsidian
  - Slides: md in Deckset
  - Screenplays: Fountain
  - Equations: Latex

- Even with text files as output, there's still complexity of line ending differences when crossing from Windows to Linux or vice-versa. Small price to pay. Aside from writing, your same point applies for software applications reading/writing data. Often, text file storage of data is a preferred long-term solution over databases.

- ## 🆚️ [Why Logseq is not popular like Obsidian? : logseq_202308](https://www.reddit.com/r/logseq/comments/15yvx2s/why_logseq_is_not_popular_like_obsidian/)
- In theory I wanted to love Logseq, but whenever I tried to build a serious workflow with it, the software felt too buggy and unpolished, especially when compared to Obsidian (which arguably has a smaller team and all), so I had to move on.
  - he portability factor is also an issue: the Markdown produced by Logseq (so obviously I'm not talking about queries) is or at least used to be horrid. Plus the constant orphan files with incomplete titles whenever I created new links, etc., etc.

- Logseq feels buggy and unpolished to me too (including plug-ins), the query language is too difficult/confusing to start with and in obsidian it's very similar to SQL and you can even use javascript, which blows my mind.
  - So far, I've been able to set things up as I wanted in obsidian without restrictions, whereas in Logseq I couldn't do that.
  - The most simple example is folders. I still don't understand why logseq has no folders, and I don't understand why should you be that rigid with your ideals when building an app, just make it more versatile cmon.
  - That said, I have no plans on ditching logseq for work because the task management is just simpler and better for what I use it, which is to track time for tasks. I haven't digged in much in task management in obsidian yet though.
- Folder structure is an obstacle for building a genuine knowledge graph. Try to live the logseq knowledge graph. It is so liberating and refreshing
- Logseq is opinionated in the way of organizing information. Some people may not like it. For other people including myself, Logseq is much more productive than obsidian. Fewest keystrokes can accomplish things in Logseq. A great time saver!

- for me personally the lack of tree hierarchy structure of pages is putting me off from Logseq. The funny thing about Logseq is that users try to overcome this building hierarchy anyway, out of properties or by starred tree.
  - I get the impression that users of Logseq by using add-ons want to make it more similar to Obsidian, because it lacks some Obsidian features, while users of Obsidian want per block functionality and want to make it similar to Logseq.
  - 🤔 That is I got interested in Siyuan because it has features of both.

- Because they are very different apps:
  - Obsidian is more a Markdown documents editor and documents organizer. Most people just need this and some build workflows on top of it using plugins.
  - Logseq is more a knowledge management app with some fixed core concepts, like organizing knowledge in blocks, organized hierarchically in each page and with unique powerful capabilities to retrieve specific blocks (mainly thanks to page references and tags being "inherited by children", filters in Linked References sections, queries and block properties). Some people like this, others' not and it's OK.

- Logseqs weakness is in it's versatility, there's almost too much you could do with it.
- Logseq has a TON of functionality but I was so confused as to how to do x or y or z.

- Logseq performance is poor.

- I used Obsidian for about a year, then switched to Logseq. I used logseq for a little over 2 months, and am now back to using Obsidian. For me, the UI in Obsidian is better and more easily customisable. The performance of Obsidian is better. The sync feature for logseq feels too buggy. I liked the idea of using the outlined daily note to record everything, but for things that were longer notes that may take a few days or more (modules and courses that I'm studying), the references section didn't show them in an order that I wanted it that made sense to me. Queries in Obsidian are far easier (especially with dataview and dataviewjs) although that may be because I have 15+ years of experience of SQL so felt more natural to me.

- The embrace of LLMs and AI permanently soured me on logseq. It's also not very accessible (not that Obsidian is either).

- Obsidian was first. It has a lot of devotees that came from Notion and Roam Research, so there's a lot more chatter about it online. It's closed source but programmable, so the huge list of plugins makes it a lot more flexible than stuff like Notion.
  - Logseq may be FOSS, but the outliner design isn't for everyone, and there are no plugins on mobile.

- In my opinion, that's mostly due to two main things:
  - Logseq is, unfortunately, less polished than Obsidian. Luckily, the team seems to be improving in this regard a lot, but it still has some work to be made
  - By being an outliner, getting used to it is more complicated than Obsidian, who it's basically a text editor with plugins.

- i love logseq concepts but indeed it is buggy and unpolished. and the markdown files are a mess, i agree. im curious to see how it will change when they release the database version.

- ## 🆚️ [Logseq vs Obsidian? is there actually a difference? : logseq _202304](https://www.reddit.com/r/logseq/comments/12hxo9c/logseq_vs_obsidian_is_there_actually_a_difference/)
- I use both but for different things. They’re so different that I consider them complimentary rather than competitive. Neither one is really a drop-in replacement for the other.
- Logseq makes blocks and outlines first-class citizens. You can switch to document mode and hide the bullets but they’re still there in the file.
- Obsidian makes plaintext .md markdown files and prose first-class citizens. You can link to blocks and use nested bullet lists, but not as seamlessly and powerfully.
- Logseq makes it easier to work with blocks, transclusions can be edited in place, and you can automatically be building another page consisting of blocks 
  - The PDF and (I hear) video annotation is much better in Logseq. 
- Obsidian runs faster and produces cleaner and more interoperable markdown documents. 
  - It’s much better for longform writing. 
  - There are far more plugins (nearly a thousand as of this writing) and themes (over 100). 
- I use Logseq for tasks and all the transitory things going on in my life currently and in the not-too-distant future—lists, temporary reference, etc—and Obsidian for my long-term notes and for writing. If I had to only use one, it would be Obsidian, but I’m glad I can use both because I also really like Logseq’s very different set of strengths.

- IMO logseq produces documents that are not a good reading experience in other apps. Therefore I would only use it for a day to day capture and todo system. Basically short term documents. 
  - If you open logseq files in other tools you will see the markdown it generates is very noisy. It is still plaintext and all that but it's not enjoyable to read. Therefore I keep all of my book notes and long term knowledge in plain markdown that I can view in obsidian or any other editor. Logseq's block structure and hierarchy is incredible for backlinks that pull in enough context to make the them actionable. Also the query system and block embeds are core to my workflow. 

- Logseq is open source software and Obsidian isn't.
- Logseq is VC funded and Obsidian is bootstrapped.
  - In layman's terms: Obsidian is already profitable while Logseq isn't, which means there is a chance that Logseq can die. Example of open-source apps that are now dead are Athens and Dendron.

- I tried to use Logseq for more stuff, but it's really nasty when you have nicely packaged structure that you want to use for years, and that's what I have. Not to mention it's jumpy, slower and less reliable.

- Logseq has better block level support, better looking image embed previews, and some more advanced features that require plugins from obsidian. Fewer plugins in Logseq and seems to get stability complaints with larger graphs.
  - Obsidian has a more flexible writing environment and many plugins. It's pretty stable.

- Former obsidian user here. Don’t forget working between two windows and dragging blocks in between them. Impossible in obsidian and so important. 

- Logseq is too complex, and the tasks management is not reliable enough. I switched to Obsidian
  - 🧐 灵活性过高的代价
# discuss-news-obsdmd
- ## 

- ## Obsidian Bases can be exported to CSV or copy-pasted anywhere — as Markdown, or even into your favorite spreadsheet app
- https://x.com/kepano/status/1927501007480582467
- 
- 
- 

- ## [Obsidian 1.9.0 (early access): Introducing Bases! Turn any set of notes into a powerful database. : r/ObsidianMD _202505](https://www.reddit.com/r/ObsidianMD/comments/1ks0ebr/obsidian_190_early_access_introducing_bases_turn/)
  - Introducing Bases, a new core plugin that lets you turn any set of notes into a powerful database. With Bases you can organize everything from projects to travel plans, reading lists, and more.
  - All the data in a base is backed by your local Markdown files and properties stored in YAML. 
  - To support Bases, we're introducing the `.base` file format and syntax.

- Is this `.base` an open source file format that can work outside of Obsidian also?
  - All the data in a base is stored in your Markdown files. You can also export a view to CSV or copy the content as a plain Markdown table. Any app that can read/edit Markdown files can interoperate with Bases.
  - The `.base` file stores the query information, like SQL or Dataview. It is a new open format based on YAML. It can also be used in code blocks similar to Dataview.
  - You can edit .base files in any code editor, and the format is completely open for any app to implement.
- Maybe Im misunderstanding but why have two files? and not just use frontmatter to contain the YAML like format for base query info, and the body of the markdown for the data?
  - It's not two files, it's one base file and an arbitrary number of markdown files. Bases use your existing markdown files.

- Does this kill Dataview?
  - Base will probably be more useful for standard database things, just showing stuff in tabular form. Possibly even editing the stuff on the spot? That'd be helluva useful. I use Dataview for much more advanced purposes, so Dataview will probably stay.
- I think this will more completely replace DB Folder than it does Dataview, but, like you said, it's going to replace many of Dataview's common use cases.
- Not at all but mostly. When this see the light of day I will move my journaling to base!
  - bases isn’t gonna run JavaScript. It’s not gonna do inline psuedojs functions.
- Nope, this more likely to kill "Projects" plugin. Dataview is still way more flexible, relies on text queries vs UI clicking around + works with tasks and inline properties. 

- o7 dataview kanban and projects ur time has come but ur time was well served
- I use Dataview in ways that it's barely table-based anymore, so I don't think its time has come yet. Unless Base can go jam multiple values together in one cell, formatted to my liking.
- whether there will be anything like in-line bases yet.
  - There is. The docs mention embedding bases into notes as well as inline “code block” bases

- Kanban still works plenty well and it is in MD format, not Yaml disguishes as MD so still this cannot replace kanban for me.
  - any property you add to a markdown file is stored as yaml. The YAML portion is just a comment in the source markdown file in of itself? So it’s still markdown. This can easily replace Kanban. Confirmed that this works with note properties

- inline properties is the biggest thing missing for me currently. Until Properties are properly viewable in Publish, I still have a need for inline values, which means DB Folder will be have a place in my setup for the time being.
  - Since inline properties were a concept from Dataview, and Obsidian doesn't support them in the core product or core plugins, I bet this will have to come as a community plugin like you said.

- Currently you can edit the base file directly in any code editor. But yes, perhaps at some point it would make sense to have something like "source mode" for base files.

- You can also create Bases as codeblocks within existing Markdown notes, which is how I mostly expect to be using the feature (how I use Dataview today). In that case, you can see and work with the code directly without opening in an external editor.

- Can the Base file also query text inside the note itself? like collecting open checkboxes under a specific header of a note?
  - Currently no.

- ## one fun thing in Obsidian 1.8 is that it lets you browse the web in plain text — the "reader mode" is persistent as you click links
- https://x.com/kepano/status/1885022352209306085

# discuss
- ## 

- ## 

- ## Obsidian is local, offline, and privacy-first, so we won't consider adding AI features until they can fit with the principles in our Manifesto. _202406
- https://x.com/kepano/status/1799165623395881129
  - In the meantime, there are dozens of awesome @obsdmd plugins that allow you to work with LLMs
  - I have lots of ideas about how AI could fit in, I shared a few in "Photoshop for text". But local inference is still very challenging to implement across OSes. For now I prefer to remain conservative and leave experimentation to plugins.

- ## 了解并同时使用 Obsidian 和 Logseq 已经有好几年了，刚开始的时候我同样看好 Obsidian 和 Logseq 的生态和未来
- https://twitter.com/realexblue/status/1761049182893449374
  - 时间过去了好几年，无意间看到这个主题并安装设置好之后，我突然意识到好像最近一年自己打开 Logseq 的次数屈指可数，反倒是 Obsidian 上记录了很多内容。
  - 四年前的时候我以为 Logseq 可以追上 Obsidian，其实当时市面上也充斥着各种各样的双链笔记软件，双链风潮下，当时 Logseq 给我的感觉太惊艳了，当时的我也对 Logseq 充满了希望。
  - 但是在今天这个节点，一个软件已经做了四年了，Obsidian 更久，当我同时打开两个软件，对比之下两者的差距实在有点太大，不仅仅是软件的成熟度、生态和社区的配合程度，都差太多了。Logseq 的同步做了这么多年也还是 beta 内测，主题几乎找不到一个好看且完全兼容软件显示效果的，显示错位，开关左右侧栏闪白。
  - 插件倒是挺多的，但是和 Obsidian 相比之下就有点不够看了，质量上也有差距。
  - 一个软件，开发这么久，依然还在内测阶段，没有正式向用户收费，长久的资金消耗肯定是一个不小的负担，坚持到这个程度，依然没有放出正式版，我其实是蛮佩服开发者团队的，
  - 但是再反过来想一下，一个笔记软件，开发了四年，依然无法推出正式版，其实也能说明一些问题，可能是开发路线的问题，也有可能是开发团队的问题，也有可能是软件架构的问题，肯定是哪个方面出了一些问题

- ## [Chinese note-taking app copied Obsidian? : ObsidianMD _202311](https://www.reddit.com/r/ObsidianMD/comments/17yjex3/chinese_notetaking_app_copied_obsidian/)
- It is similar to Obsidian in many way, to be sure.
  - I also was a bit saddened that they have easy, notion-like multi-column support, but Obsidian doesn't.
- Obsidian limitations are mainly because of Markdown. Siyuan uses JSON format. Anyway, table is coming in the next update

- Obsidian is that it uses Markdown, whereas Siyuan uses a database format
  - This immediately makes those two completely different apps. 
  - Remember that Obsidian is a Markdown editor at its very very core, and it target the notion of "notes for your grandchildren" because of its future-proof format.
  - SiYuan looks more like a WYSIWYG editor with text-based shortcuts. It also uses a block structure, which Obsidian subtly uses in links and embeds but never advertises.
