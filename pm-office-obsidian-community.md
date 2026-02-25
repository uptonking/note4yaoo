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

- ## 🤔 [10, 000 notes in Obsidian. I think it's just not working for me anymore. : r/PKMS _202602](https://www.reddit.com/r/PKMS/comments/1qvnvxu/10000_notes_in_obsidian_i_think_its_just_not/)
  - Been using Obsidian since 2020 pretty much since public launch. 10, 000+ notes now.
  - I have an inbox in a completely different app because getting stuff into Obsidian feels like too much. I add ## Log sections with dates to notes because I never know where to put new thoughts on old ideas. Half my thinking now happens in Claude or ChatGPT and never makes it to Obsidian.
  - As a result more and more things end up outside of my knowledge base. I looked at the stats and the number of notes I'm creating dropped to almost just a couple of notes per month. And I didn't stop my work and consuming materials, so clearly something is not working.
  - I started looking into other stuff: notebooklm, mem, outliners (feel like a great idea but I haven't found a decent implementation) but nothing really feels right. And I don't want to abandon my 4 years of notes.

- I have 8819 notes, it is working fine for me. I use PARA as a methodology.

- Of those 10, 000+ notes, how many are basically web clippings (with or without annotation, markup) and how many of them are original writings?
  - The reason for asking is that I've noticed a connection between large vaults and struggles similar to yours.
  - Data hoarding is a thing. And just like those who hoard physical things, it becomes impossible to find the things you have. Whether it is an inbox or "uncataloged" folder, it shouldn't be a dumping ground, but a queue of things to be processed.
  - If you are consistently adding to it faster than you are processing it then perhaps the things you are adding aren't as important as you initially thought.
  - My vault is a little over 2400+ notes (all but about 50 are original writings) spanning 49 years. I use the Johnny Decimal method for my folder/notebook hierarchy and make generous but deliberate use of links (approx. 5200 links in the vault)... nearly all are internal to the vault. Tags are the 3rd ligaments of connection.

- ## The future is plain text files — it's just not evenly distributed
- https://x.com/kepano/status/2007461645438849484
- yeah you're right, increasingly I don't care about the web ui or mobile app, I just want an LLM friendly data dump from stuff like banks and mortgage cos

- I’m making a headless CMS based around plaintext formats: markdown and json

- I used pandoc to convert our Word-based security program docs into Markdown. It let me use AI dev tools to knock out annual edits in an afternoon instead of a week. I keep it in git and check it out in an Obsidian project. This makes cross-referencing durable and searching FAST

- I’m in the process of switching most of the apps I use to plain text files and then coding my own interfaces to interact with them. So useful!

- Plain text already won. We’re just still wrapping it in layers of UI to feel productive.

- ## if you're using Obsidian with Claude Code, tell me about your workflow, and what you've used it for _202601
- https://x.com/kepano/status/2007223691315499199
  - 讨论中分享了很多开源工具

- I used Claude code yesterday to review 2025, and I have all my goals from the last few years on there, asked it to find trends! To help plan 2026

- Identify new backlinks to add, synthesize knowledge base and generate summaries, batch re-organization.

- mass metadata editing, mostly, also "insert backlinks that I missed"
- Can you give examples of mass metadata editing? Are you having Claude generate Python scripts or how do you control hallucinations?
  - "assign the type of 'movie' or 'book' to all of the items in this folder that don't have a 'type'", that kind of thing. for things like director/isbn though I had it proxy out to a script
- The consumer/mass-market does not care about hallucinations. Most of them can’t spot them or prefer to keep using the tools and not think. The loss of Critical Thinking is one of the most significant losses of our current society.

- I have started maintaining specific master context files in Obsidian that I repeatedly pass into Claude Code instead of explaining things repeatedly. I have a file like this now for every major project or area of my life

- 1. batch editing that use more complicated bash commands i wouldn't have done otherwise: adding links, editing properties, .etc; 
  - 2. create specific folders for current projects that im working on and load all the notes/pdfs/there for claude to read. make claude put on a critique lens; make claude role play different perspectives/backgrounds; make claude put valuable points into notes and keep iterating like this
  - claude code isn't great at adding tags - maybe a context window thing. but my notes aren't that long.

- I migrated from Notion to Obsidian specifically for this. Because the vault is just local text files, I can point Claude Code at the directory to get cross-file insights, auto-organize folders, and batch-edit metadata. It's a game changer for maintenance

- I ask claude to aggregate ideas using keyword search of my vault. Then collect all the thoughts into an idea doc. Then iterate from there into a final form.

- used opus 4.5 to write obsidian-style notes today. turns out wikilinks are basically a mini knowledge graph for the llm. it can traverse your thoughts like a filesystem. huge unlock.

- Adding frontmatter, adding backlinks, categorizing / organizing / aggregating documents, importing from lesser apps (this didn’t go great). Built an MCP server for myself so it didn’t burn as many tokens the way it was trying, that’s a real issue.

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
# discuss-internals
- ## 

- ## 

- ## 

- ## 

- ## [Why is Obsidian not running sandboxed under macOS? : r/ObsidianMD _202509](https://www.reddit.com/r/ObsidianMD/comments/1nofbwc/why_is_obsidian_not_running_sandboxed_under_macos/)
  - Regarding the latest discussions about potentially insecure plugin updates, I am searching for methods to run Obsidian securely with plugins.
  - I stumbled over sandboxing which can be activated and configured by the developer. I checked if Obsidian is running sandboxed and found that it is not.

- kepano said: Yes, on desktop, Obsidian plugins can access files on your system, unless you run it in a container. On iOS, iPadOS, and Android the app is sandboxed so plugins are more constrained.
  - This is not unique to Obsidian. VS Code (and Cursor) works the same way despite Microsoft being a multi-trillion dollar company. This is why Obsidian ships in restricted mode and there's a full-screen warning before you turn on community plugins
- it seems if you sandbox obsidian, the plugins don't work.

- On macOS, the sandboxing can be configured in many details. So in theory, I could generate a configuration for Obsidian running specific plugins allowing just the access it needs.
# discuss-author
- ## 

- ## 

- ## if you're wondering why this or that feature hasn't been added to Obsidian, remember we only have three full-time developers (and not trying to grow the team)
- https://x.com/kepano/status/1908728301700735439
  - everyone that we have hired was once an active community contributor, including myself. That's always where we look first.

- People keep looking for new features in notetaking apps as productivity procrastination, whereas, if they actually do real work they realise obsidian doesn’t need anything more. It does the job. Let’s keep it simple !

- Adding most of those features would not make Obsidian better anyway. Focus.
# discuss-news-obsdmd
- ## 

- ## 

- ## one fun thing in Obsidian 1.8 is that it lets you browse the web in plain text — the "reader mode" is persistent as you click links
- https://x.com/kepano/status/1885022352209306085

# discuss-showcase-ob
- ## 

- ## 

- ## 

- ## [Combined all notes/writing apps I've ever used into a single vault : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1rdpwmw/combined_all_noteswriting_apps_ive_ever_used_into/)
  - graph关系图，样式友好

- ## 🗺️ [Chorographia Update: 0.3.0 beta release : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1r91mid/chorographia_update_030_beta_release/)
  - my plugin that turns your vault into a semantic map. Notes embedded, projected into 2D via UMAP, and clustered into thematic zones. 
  - the overlapping zone issue. I still really like the original (now called “Star Map”), so instead of redesigning I added a new mode: “World Map.”

# discuss-pm-ob
- ## 

- ## 

- ## 

- ## 

- ## [Do you use Daily Notes in Obsidian? Is this something you would want? : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1q8zw78/do_you_use_daily_notes_in_obsidian_is_this/)
  - 热力图换成了背景图
- I don't have images on my daily notes but would definitely start if there was a feature like this!

- Yes, that would be very useful! I’ve already been using something very similar with the Diarian plugin, but it’s not quite there yet.

- ## [Project Folders now available in Lovely Bases Plugin : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1q89nct/project_folders_now_available_in_lovely_bases/)
  - I didn't do the design, I reused this component from shadcn and adapted it to work within Obsidian
  - https://github.com/aitorllj93/obsidian-lovely-bases

- Is there a way to show an image itself? E.g. A base that filters on png files and the view type is infinite gallery. I tried with thr file path but that didn't seem to work.

- ## 🤔 [I know many folks do not use folders… : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1ppcmic/i_know_many_folks_do_not_use_folders/)
- Use folders. Stop worrying about what others do. Your assumption is on point. Obsidian can dissapear and even tho there are some other tools that can be an 'alternative', it's not the same. Folders will give you the peace of mind that even in a file browser you will find your files more easily than a bunch of files together. Don't overthink.

- Folders are the way to go. Stop treating your own notes like you need a google spider to crawl, tag, index, and find them for you. 

- The same logic used in the folder-less method can be applied with a very simple bash script to generate directories and assign files to them, should Obsidian vanish one day.

- ## [What's one improvement you'd like to see in Obsidian in 2026? : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1pogn6w/whats_one_improvement_youd_like_to_see_in/)
- A good, comprehensive attachements/media management tool. 
  - I know there are some good plugins out there, but imo it should be built in, to make sure it's properly maintain over time
- Clean up orphaned attachments (using sync storage)

- Lightweight for mobile would be my top choice, it’s too clunky and sync takes too long, and control too complicated to be used for mobile

- Better search would be nice. Not only better relevance ranking but to be able to search for symbols like colons in between terms. And also presentation of results in the center of the screen.

- advanced outliner options like nested code blocks, callouts etc. Obsidian can do a lot to make better UX regarding outline approach

- editable block embeds is #1 for me

- Embeddings that can be modified in-place would be lovely. I miss them from Roam, I loved them as a part of my workflows.

- In general I’d like to see more work done to improve the experience of embedding one note in another. The ability to embed notes in other notes is one of Obsidian’s core strengths. But it’s like you are 90% of the way there and then the last 10% really stops me from being able to use this feature seriously.

- All I want is a Kanban view for bases so I can make my Now Playing/Break/Finished notion Kansan again, and do my tier lists for what I played. (I know I can sort of get it with Kanban status updater but it's not the same)

- Look forward to native PDF support for highlights and comments.

- Make everything faster, even with plugins.

- ## [Do you all know how I can get something like this? : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1p7qs4p/do_you_all_know_how_i_can_get_something_like_this/)
  - 类似仪表大盘

- With the Dataview plugin you can query your vault and render whatever content you want with it with JavaScript. The sky's the limit if you're willing to put in the time.
  - there's not a lot of actual dataview code online, at least not on public repos. I would suggest referring to the dataview plugin's documentation and trying by yourself. 

- Don't hold me to this because its been awhile since I looked at financial type plugins but there used to be a couple called Obsidian Ledger and another Hledger but I don't know if they are still active.

- Google sheet looks sufficient for this

- ## [Obsidian alternatives that are open source (free) and sync feature as well : r/ObsidianMD _202209](https://www.reddit.com/r/ObsidianMD/comments/x95y56/obsidian_alternatives_that_are_open_source_free/)
- The only good opensource alternative to Obsidian right now is Logseq. I don't think it supports sync though.

- I've been using Zim Desktop for a while now and it's great for note taking and keeping things organized. The one thing it's missing is node-graph linking. 
# discuss-feat-database/bases
- ## 

- ## 

- ## 

- ## [What are the best plugins in relation to bases already created for Obsidian so far? : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1pp25ul/what_are_the_best_plugins_in_relation_to_bases/)
- Virtual Content. You can add specific base views to files based on their property values without actually typing them in the note. It's great because if you want to change something in that base view, you can do it through the plugin settings tab and the change will happen in every file. Also, it doesn't alter the Markdown files.

- ## [Obsidian Bases support in Flowershow (Alpha) : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1pevh7g/obsidian_bases_support_in_flowershow_alpha/)

- ## [Obsidian bases are great, but is making a separate note for each item practical? : r/ObsidianMD _202509](https://www.reddit.com/r/ObsidianMD/comments/1nq0mci/obsidian_bases_are_great_but_is_making_a_separate/)
  - I really like Obsidian bases in terms of automation, customization and overall look. It's pretty and functional. 
  - However, there are cases where making a note for each entry can be a bit excessive. Do you think it's possible to have multiple items from one note?
  - Example use case: movies to watch, games to play. Say you want to have 200 entries, do you really have to make 200 notes? If you make lists like this you end up with potentially thousands of empty notes (besides the metadata).

- The Bases core plugin is not a database. It provides filtered views, generally based on Properties. If you need true database functionality, Obsidian might not be the right solution.
  - The idea of Bases is to provide a managed jumping-off point to dig deeper. (Heck, a Base is, arguably, a Map of Contents.) The way that Bases' Table and Card views aggregate information amps up Obsidian's capabilities, so how the data (notes) are handled behind the scenes really depends on what you are trying to do.

- Why not both? For example, I’ll create a note for each book that I want to create a note for. I separately have a note called “Books consumed” that just has a bulleted list of books that I’ve read by year, which may or may not link to a note.

- This is why I still use dataview, too, not only bases. For some notes I need to collect pieces from notes that contain many things.

- Remember Base is just a view and not a database. It doesn't change anything nor depends on how your notes are made. It just style so to speak what's already in your vault (for simplicity sake).
  - So write and organize your notes however you want. Experiment to discover what works for you, and it might be the same or different for each use case. You can always tweak and change.
- Yes, Base doesn't display the content of a note, rather it displays the properties or YAML.

- In some cases Dataview is still a better fit (and probably Datacore, although this is still unexplored territory for me) if you want to use the note's contents instead of the YAML frontmatter properties.

- This has me thinking that the community could use a plugin that converts each line in a table into a note with metadata, and then generates a Base for those notes with the same look as the original table. Then you can start modest and there's no FOMO of not starting it as a Base. Because you're right, a lot of knowledge management starts smaller than what a Base is.

- ## [Obsidian Bases | Hacker News _202508](https://news.ycombinator.com/item?id=44945532)
- 
- 
- 
- 
- 
- 
- 
- 

- ## Obsidian Bases can be exported to CSV or copy-pasted anywhere — as Markdown, or even into your favorite spreadsheet app
- https://x.com/kepano/status/1927501007480582467
- 
- 

- ## [Introduction to Bases | Lobsters _202505](https://lobste.rs/s/nxroup/introduction_bases_obsidian_help)
- but when you really lock-in with bases or obsidian plugins like tasks and dataview, you really rely on thing, not being that easily to replicate if obsidian would go paid or something else.

- This is very interesting. In 2019 I wrote a small hack using Pandoc that parsed a Markdown file and:
  - Detected tables and dumped them into a SQLite database.
  - Detected SQL code blocks, run the SQL on the SQLite database and replaced the code block with the query results as a table.
  - I was obviously inspired by Notion (2016) and Coda (2019). I still think that the slow death of Access and similar tools, the abuse of spreadsheets, and a couple of other factors are a severe drag on global productivity. Easy CRUD on relational databases is an overlooked problem
  - I wanted to start a similar project based on some more modern lightweight markup language (such as Djot) and likely on some Datalog variant, but I stalled

- ## [Obsidian Bases | Hacker News _202505](https://news.ycombinator.com/item?id=44058972)
- They are using a yaml file with `.base` extension for this.
  - I believe their `.canvas` format is also just JSON.

- Bases seem like a great alternative to Dataview but better supported and with simpler syntax than literally writing inline JavaScript for more complicated stuff.

- Are there any good ways to attach files to notes? I often want to tie a memo or email to a note but have not found a convenient way.
  - Default way is drag and drop which adds a copy of the file to your attachments.
  - Another way is to put a file reference into your note (in a link). Your file stays where it is and you have a link to it in a note. Links are opened by default apps as per your OS config.

- ## 📈 [Obsidian 1.9.0 (early access): Introducing Bases! Turn any set of notes into a powerful database. : r/ObsidianMD _202505](https://www.reddit.com/r/ObsidianMD/comments/1ks0ebr/obsidian_190_early_access_introducing_bases_turn/)
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
# discuss
- ## 

- ## 

- ## [How do you decide what's a tag and what's a property? : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1pp6x5d/how_do_you_decide_whats_a_tag_and_whats_a_property/)
- I use properties more as a way of compartmentalizing specific aspects of notes and not cluttering my tags which would eventually have so many tags that it would become a mess. When I am done with it, I change the property to Archive.
  - I also have a property called type that I can then easily filter on in a base. I have many types; personal, company, document, note, task, etc.
  - I only use tags to give me a broad categorization of what something is. I personally wouldn’t want to use nested tags, it feels more akin to getting bogged down in folders.

- I think one variable is that tags end up in a cluster so they are hard to read on their own when reviewing a note. Meanwhile properties are separated out, one per line. So if the information is something you want to be able to easily reference/be aware of then making it a property lets you isolate it.
  - Meanwhile tags are great for lots of single phrases where you might need them to create search results or to find information with; but where you don't really need to "read" that information specifically.
  - Properties can also be things like image links (eg a cover image for a table) or links and so forth. However there I'd note that for those instances they really only work easily as single data entry points. So one link for the property. so if you've a variable which might have multiple links, that might be better as information in the main body of the note instead of as lots of endless link properties.

- I have used zero tags so far but about 25 properties. I keep things lean. I am prefer folder over tag so have about 125 folders

- Remember that these are tools. You can use them both, in the same note, for different purposes.

- As for tags, I use them as intended: for search. A note may have dozens of tags, if needed. Tags are one of the main reasons for using a program like this. Otherwise, I would go back to bare folders.

- I use tags for types of notes. I don’t put types of notes in folders because sometimes my notes are more than one kind of note (and some are more specific than others).
  - I use properties when I have finer details that I would like to store for later use.

- I use `properties` to define the formal type and content `tags` to define the purpose of notes.

- Tags are categories, properties are data specific to that note. Some properties may also be categories, but only if it's specific. Or maybe property categories are more "permanent" and tags could be more ephemeral. Changing a property is changing the thing the note is about, but changing its tags doesn't. Something like that.

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
