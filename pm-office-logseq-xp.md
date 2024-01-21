---
title: pm-office-logseq-xp
tags: [logseq, note-taking, pm, xp]
created: 2022-06-02T04:32:59.545Z
modified: 2022-06-02T06:11:16.758Z
---

# pm-office-logseq-xp

# guide

- features
  - No data lock-in, no proprietary formats
    - you can edit the same Markdown/Org-mode file with any tools
  - 支持用 [[]] 引用任何page，自动生成文档关系图
  - 任务管理很方便
    - 支持 deadline，支持优先级
  - pdf阅读批注很方便
    - 支持分屏查看
    - 支持复制后链接到pdf位置
  - 支持多设备，包括网页版、移动端

- pros
  - 编辑器类似typora，支持即时预览和编辑文本
    - 即时预览的切换预览和源码文本经常导致页面重排layout

- cons
  - 支持浏览器直接打开本地文件夹
  - 不支持 database

- user-xp
  - 每一行前面都有类似无序列表的小点
    - 优点是点击小点时，每一行都可以作为单独的page打开
    - 缺点是左边的小点和竖线使得页面看起来有点乱
  - 配置文件格式是 config.edn
    - 类似json，支持注释
# who is using #logseq
- https://note.xuanwo.io/#/all-pages
# discuss-obsidian
- ## 

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
# discuss
- ## 

- ## 

- ## 

- ## [[WIP] Database version](https://github.com/logseq/logseq/pull/9858)

- ### @logseq DB / Database version on the way?_20230715
- https://twitter.com/ednico_/status/1680134195484434432
  - There's not a switch. Two storage methods (file, DB) will be in parallel.
  - DB storage is for users looking for good outliner performance and structured data support. Also, there will be a full graph markdown export with automatic refreshing to cover the local-first demands.
- benefits
  - Performance +++
  - No more re-index required
  - No more structural parsing required
  - Reliable page & block timestamp
  - Reliable page & block history
  - Reliable sync & RTC
  - Reliable & snappy multi-window
  - Enabling more features on web app"

- How will it compare to other database products on the market?

- ### A nice little update on the @logseq db / database version  - getting closer and closer
- https://twitter.com/ednico_/status/1674111439173189660
- Easy converting between MD and db will make this a winner for sure. Seems to be going in a similar direction to @notesnook

- Imo this defeats the purpose completely of using logseq, which is to have markdown as the source of truth
# more
