---
title: pm-office-obsidian-community
tags: [community, markdown, note-taking, obsidian]
created: 2024-01-23T02:51:44.425Z
modified: 2024-01-23T02:52:23.932Z
---

# pm-office-obsidian-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

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
# discuss-showcase/examples 🌰
- ## 

- ## 

- ## 

- ## [Thank you Obsidian community for having such vast resources ❤️ Vault Showcase + Yaps : r/ObsidianMD _202604](https://www.reddit.com/r/ObsidianMD/comments/1sde5jm/thank_you_obsidian_community_for_having_such_vast/)
  - 

- ## [Combined all notes/writing apps I've ever used into a single vault : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1rdpwmw/combined_all_noteswriting_apps_ive_ever_used_into/)
  - graph关系图，样式友好

- ## 🗺️ [Chorographia Update: 0.3.0 beta release : r/ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/1r91mid/chorographia_update_030_beta_release/)
  - my plugin that turns your vault into a semantic map. Notes embedded, projected into 2D via UMAP, and clustered into thematic zones. 
  - the overlapping zone issue. I still really like the original (now called “Star Map”), so instead of redesigning I added a new mode: “World Map.”

# discuss-feat-backlinks
- ## 

- ## 

- ## 

- ## [Automatic Backlinks : r/ObsidianMD _202409](https://www.reddit.com/r/ObsidianMD/comments/1fg0ycy/automatic_backlinks/)
  - Is there a way for Obsidian to automatically backlink to a file when I type it out? For instance, I have a folder called "Definitions" where I store all the definitions of words. So when I create a new file outside that folder, and write down a word, Obsidian can detect that the word is in the "Definitions" folder and automatically backlink to it.
- Virtual Linker / Glossary Plugin is close to automatic but it's not consistent for some reason.
  - Various Complements is another option as well. I like this one because it shows you what to link to which I really like when I'm typing away on my phone I don't have to think about what I need to link.

- ## [Does anybody use Obsidian URL with []() instead of Backlinks with [[]]? : r/ObsidianMD _202407](https://www.reddit.com/r/ObsidianMD/comments/1dwodo1/does_anybody_use_obsidian_url_with_instead_of/)
- I don't recommend using Obsidian's note url. If you rename the file, the link breaks. Use something like Advanced URI. It has an option to use UUIDs instead, which doesn't break after the file being renamed.

- Wikilinks seem to be gradually replacing internal URLs as the defacto standard even in simple markdown editors like iA Writer. It will be interesting to see whether that trend continues.

- Wikilinks are great. They don't show the full path, so they appear better on linked mentions.

- I use tags for stuff I don't want linked in graph view. 

- ## [I built a tool that automatically adds semantic backlinks to your vault — fully local, no cloud, no API key : r/ObsidianMD _202603](https://www.reddit.com/r/ObsidianMD/comments/1s46wxu/i_built_a_tool_that_automatically_adds_semantic/)
- I checked it out, and I think it is not possible to run this on a single file, which i would like that to test it out. I do not want every note in my entire vault to have wikilinks to its related notes.
- This may pair well with Wikilink Types. Rhizome finds that notes are related; Wikilink Types lets you specify how they are related (supersedes, contradicts, supports, etc.) via typed @ syntax, synced to YAML frontmatter.

- Great idea why not a plugin in obsidian?
  - the main challenge is the technical environment. Obsidian’s JavaScript context isn’t built to handle the heavy lifting of downloading a ~250 MB ONNX model and running dense vector searches—that would likely hog memory and freeze the UI. Python is simply better suited for that kind of workload, which is why keeping it as an external CLI keeps Obsidian itself fast and lightweight.
  - That said, a companion plugin is possible in theory: a lightweight plugin could act as a UI wrapper, spawning the Python CLI in the background. The tricky part is distribution—users would still need to install Python, run pip install rhizome, and configure the plugin with the executable’s path, which goes against the usual one‑click install expectation. But for power users, it’s a brilliant workaround, and I might explore building it as an optional plugin down the road.

- 
- 
- 

- ## [How many of you have never used or needeed the backlinking feature at all? : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mo7ohj/how_many_of_you_have_never_used_or_needeed_the/)
- I have a handful of empty notes that are only there for backlinking. If I'm taking notes somewhere else and I start thinking "Hey, this would be a good blog post, " I can add a link to my blog post ideas note. When I go to that ideas note, I see all the backlinks with a bit of surrounding context. For me, it feels a little bit like tags, but the context is a sentence rather than a whole note.

- I use it for citations, reference, related or direct mentions. I also use paragraph embeds a lot. I have empty notes that basically functions as a connection node.
  - Even the H1 (title) is in double brackets to reference itself. So when I change the file name, the H1 also automatically changes.

- I even barely use the forward links. I rely on a folder system for structure between my notes.
# discuss-feat-sync
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [佬们都用什么方案同步 Obsidian？求推荐 - LINUX DO _202606](https://linux.do/t/topic/2441916)
- 之前试过 Github，坚果云，因为是苹果全家桶，现在用的苹果 ICloud，实测秒同步很方便。

- 之前用 Remotely Save + Cloudflare R2，现在用 Git 了，自动生成提交并推送

- tailscale + syncthing, 日常使用够用，直接把这两个弄成windows服务在后台了

- 我使用的是onedrive，5GB足够我用了，平时同步也没啥问题，

- Windows、iPad、安卓手机混合用户，用的坚果云同步，但是插件同步有时候会出问题

- 如果自己有NAS或者VPS的话，推荐fast-note-sync-service
- 有条件服务器或者自建的话，fast note sync真的是降维打击

- 我认为最合适的方式就是将 obsidian 的数据文件夹变成 git 仓库，使用GitHub Desktop 来手动同步，不限容量，又做了历史版本管理，真的是非常的香，我现在就是这么用的

- 我obsidian vault 在 7G 左右，你看你的 vault 多大，正常如果你 icloud 没有其他照片什么的，买个 6 块一个月 50G 够用了，甚至内容少也可以先用免费 5G 试试。win上我记得微软商店里有 icloud 的软件，不过我没试过。总之苹果全家桶是很顺畅的，你电脑手机登同个 ID，把 vault 放在 icloud 里，记得打开保留下载就行了。

- 用的阿里的s3存储服务，一年也就几块钱，很稳定省心

- git: 能够网页预览，版本管理, 能忽略文件夹。支持Linux、mac、win
坚果云：能够网页预览，无版本管理，不能忽略文件夹。支持Linux、mac、win
iCloud：无法网页预览，能同步到Iphone, 无版本管理，不能忽略文件夹。支持mac、win

坚果云和iCloud不能忽略文件夹，就会把一些配置文件夹或者不想同步的内容也同步。
跨平台时快捷键或者啥的冲突，就会在配置文件夹生成很多冲突文件。

最推荐的还是git, git+双链，git提供了纵向的以时间顺序的迭代记录，双链提供了当前时间点横向的各个文档的关联。

我目前是git手动提交+icloud。obsidian的git插件如果你不用其他同步手段可以使用防止忘记提交。

- onedrive→webdave云盘→自建webdav→飞牛同步，现在感觉飞牛同步用的很舒服。

- ## [Easiest alternative to Obsidian Sync? : r/ObsidianMD _202510](https://www.reddit.com/r/ObsidianMD/comments/1ohrlyw/easiest_alternative_to_obsidian_sync/)
- Syncthing. A note of caution is that Syncthing is good at huge sizes, not low latency. So if you have lots of frequent tiny edits that you need to keep immediately, probably not for you. I only ever edit on one client at a time, so I don't care about latency as long as they "eventually" synchronize, so Syncthing is really good.
- You’ll want to exclude the .obsidian folder on syncthing.
  - No need to exclude the whole folder, just exclude workspaces and plugins

- Git Sync Plug-in
  - It's a good plugin. However the mobile version is still unstable.
- And that's why we have Git Sync as a separate app

- The best cloud is the one you have already paid for. Onedrive suits me as I subscribe to Office365. iCloud, Google drive, Dropbox, WebDAV, etc if you already have paid for them.

- ## [Which cloud sync do you use with Obsidian? (and what are the pros/cons?) : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mw3dav/which_cloud_sync_do_you_use_with_obsidian_and/)
  - poll, votes(685)
  - official, 210
  - icloud, 122
  - g-drive/dropbox, 103
  - git, 84
  - syncthing, 112
  - other, 54
- Obsidian Sync—I just want to support the team at Obsidian for all the hard work they put into developing and designing an amazing product

- obsidian-livesync https://github.com/vrtmrz/obsidian-livesync I use it with self-hosted CouchDB. Works fine for me.

- Git (via https://github.com/Vinzent03/obsidian-git ), have to ignore some obsidian files to avoid repeated conflicts but I just set everything up on one device, commited it all, pulled it on other devices and .gitignore the workspace. I already run a gitea instance so data all goes to that. So far so good. Only downside is I haven't fully sorted mobile and I find that interface hugely clunky for anything that's not notes

- Not perfect. Syncthing local only discovery with devices using tailscale magicdns names as tcp connections. That way I never have to use the syncthing relays as I use tailscale anyway.

- I selfhost my vault in my NAS. 

- I use git.

Pros:

Free and open source tool widely used by millions of developers

Extremely portable. Git runs on everything.

Zero vendor lock in. You can start with a cloud host, and later move to any other service, or host your own git server.

Not only syncs my data, but preserves the history of the vault.

Every copy is a full backup of the whole history

Cons:

None.

- https://github.com/ViscousPot/GitSync Supports automated background syncing of a git repo, made specifically with Obsidian in mind. Freely available on Android and iOS through the respective stores

- I don't use Obsidian on mobile, but there are mobile git clients.

- Rsync + SSH between desktop and laptop. My vaults are not and won't ever be online.

- OneDrive usually works like a charm for me. Occasionally an older version of a note will overwrite a newer version but I can just go into note history and get the version I need.
- My Vault exists peacfully in an OneDrive-Folder. From there it's synced to my smartphone and also to my linux server machine, where my AI is able to have a direct eye and hand in all my .md contents.

- running a WebDAV server is a simple server to run, but you also need a way to access it when you're away from home and not on your network. To do that I run another simple App in my Homelab called Wireguard. It creates a VPN that I connect with when I'm away. Once I connect to the VPN, it's just like I'm on my home network and I have access to all the services I host.
# discuss-multi-lang
- ## 

- ## 

- ## 

- ## 

- ## [Pages in multiple languages - Feature requests _202108](https://forum.obsidian.md/t/pages-in-multiple-languages/22063)
  - Current workaround: 
  - A user could always simply use multiple pages, one for each language, and link them between each other. However, this would bloat the browser and the graph, and the links associated with the page in one language would be separate from those associated with the page in another language.
  - An alternative is to put the various languages together on the same page, but that is rather inconvenient and inelegant, especially for pages with a lot of text.
- 
- 
- 
- 
- 
- 

# discuss-tags
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Categories vs tags : r/ObsidianMD _202607](https://www.reddit.com/r/ObsidianMD/comments/1ulcw1k/categories_vs_tags/)
- properties are more versatile and can be tailored to each case. Tags can't. But, tags have an implicit search, properties don't.

- A native tag is essentially a text label used for filtering. A category note is an object in the vault with its own content, links, and metadata. Because it's a note, it can serve as a hub or Map of Content (MOC). You can document what belongs in that category, describe how you use it, or record conventions that would otherwise exist only in your head. In other words, the category carries meaning, not just a name.

- Tags are built in to Obsidian's functionality, and work very well. Doing the same thing will Links, Properties and Bases requires a lot more work on your part.

- ## [Why I use folders over tags or categories : r/ObsidianMD _202607](https://www.reddit.com/r/ObsidianMD/comments/1ukpxu1/why_i_use_folders_over_tags_or_categories/)
  - Speed. 
  - When using Dataview or inline Javascript to build tables or other views, giving the script a specific place to look dramatically speeds things up (in my experience). I have 30K+ notes in my vault, so some queries can take a bit to run if they target the entire vault. If I had a flat hierarchy, saying "show me all the notes with #meeting between dateX and dateY" means it scans the metadata of 30k notes to find all the #meeting notes with the proper dates.
  - With a folder structure, saying "look in Meetings/2026/06 for notes between dateX and dateY" means it scans at most a few dozen notes for dates. Narrowing the scope is just plain faster. It's the difference between a second or two and instant.

- I consider my Obsidian vault a system that must be easily consulted even without Obsidian itself, so I try to use folders if possible, which are accessible and can be organised even without Obsidian and a little less tags that instead need Obsidian to be able to be consulted, filtered and searched with ease

- I use both folder structures and tags. Tags are used when building dashboards using bases, and then folder structures can be used when going through files using AI agents. Both have their own use cases and value.
- Tags annotate and label content. Folders chunk related content by a unit.

- This works if your folder structures remain pretty static. If you tend to rearrange folders, folder queries break unless you manually update them each new folder path, which is very annoying. Its why I am using tags more myself.

- I have a folder structure two levels deep, no more. First level is broad, second much less so, but still not specific. Anything more specific comes from metadata as needed. Similar to your setup. My tables and searches can be broad, vault-wide, or directed as needed. Metadata templates are useful for this.

- don't have 15 more folders under that because then you spend more time organizing than you do creating notes which is what the thing is actually for. I work in IT and in almost every situation search is faster than clicking through to where something lives.

- Most of my folder sorting is done by default when I choose a template, so it's just simple stuff like person or company or movie or book, but it makes these files manageable in my actual computer operating system which at some point would struggle with a flat storage system.

- Flat structure is against everything I got used to. I think it's kepano's effect that flat structure is so popular.

- Too many things fit in more than one category, so I can't use folders, unless it is for very specific things. Having to reorganize a vault because a folder name takes on a new meaning would be far too hard.

- ## [I use links and notes instead of tags : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1ue3fi1/i_use_links_and_notes_instead_of_tags/)
  - I don’t use tags at all in my Vault. Instead, I use links in place of tags
  - Advantage: Since they’re notes, I can add details
  - While you can name tags, the downside is that you can’t add any additional information about what the tag actually means. I think this can become a pretty critical problem over the long term.
- I had previously thought I could use tags for note status, but theoretically, I could do the same thing you’re saying here and just set a base in the note that filters for the appropriate notes. 
- Tags are good for filtering datasets. So if you use bases then tags are a great complement.
   - Links are good for mapping relationships.
   - 2 notes could be linked but not share the same tag. 2 notes could share the same tag but not be linked.
   - Tags get more useful as you have more notes. Like in the thousands.
   - They make it possible to categorise your whole note graph, multi dimensionally, for quick filtering or traversal.

- Because you focus only on concepts and definitions. You just group notes by explaining them. Tags are for properties and classification so group notes by common labels. Using tags you can find and filter then - anywhere. Do you know that you can (should?) use both? Using only links forces you sometimes to use fake concepts like TODO or IMPORTANT - this are tags.

- I am also trying to move away from tags, As a first step I am now only keeping tags for status, like #pending #TODO #on_going #complete so I can use them in bases. So I can quickly pull a list of notes that are on going for example.
# discuss-large/massive
- ## 

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

- ## [My vault is too big : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1uiqawe/my_vault_is_too_big/)
  - I've got a little more than 12, 000 notes.
  - It's starting to get heavy, specially on my phone. I'm considering nested vaults. Any suggestions or alternative solutions?
  - I haven't measured, but startup takes about a minute. But it's not rebuilding index. At least i don't get the message.
  - And sometimes it kind of freezes in a note. I can use that specific note, but can't navigate to others by any means.
  - I have some images and excalidraw drawings. 755 less than 100kb webp images, 185 jpeg, 128 png. No pdfs, videos or audios. Everything within the vault, no external links.

- With this amount of notes i can assure you, no other software will help you. You need to consider some form of refactor. Maybe merge some notes? Delete or archive? Multiple vaults?

- Yeah, I'm considering multiple vaults. But since they recommend against it, I'm studying possibilities and hownto properly use multiple vaults without screwing something up
  - A lot of us have lots of vaults for different reasons. The program is even set up to switch between them easily.

- Have you tried stripping out all the images and non-plain text files and hosting them elsewhere so you link to them in your notes rather than have them in your vault. I've been doing this for a few years now and my vaults load very quickly.
  - I used to do that in the beginning. Then I had to use it offline and noticed it wouldn't be all that rare. Besides the google photos links didn't last forever. So I gave up that strategy a long time ago.

- I’m well over 50k and don’t have an issue. Could by hardware as well potentially, and I do not use on my phone.
  - One thing that worked really well for me was using Claude code and I spent about 2 weeks on a cloned vault and with Claude just simply rearchitecting for stronger discovery, better performance, tag management and cleaning up orphans.

- I have close to 40, 000 notes in my vault. But it’s not bigger than your vault. All my notes are about something that does not reside in the vault. Using it without any issues on my mobile phone (iPhone), macOS, and Windows PC. I use Obsidian Sync.
# discuss-ob-cli
- ## 

- ## 

- ## 

- ## 

- ## [What’s the best use of the Obsidian CLI? : r/ObsidianMD _202602](https://www.reddit.com/r/ObsidianMD/comments/1racz6l/whats_the_best_use_of_the_obsidian_cli/)
- It's agents and composibility. You can describe a highly constrained workflow and package it in a skill.

But the best win is automation in building plugins. This was a big pain point because I had to go to settings manually to re-activate but now the coding agent gets a feedback loop.

- I think it could be useful for creating small scripts that allow you to perform automations using notes as an input source or as a writing destination. Add tasks, for example.

- Fetching Jira details from a ticket ID and generating a note based on a template on a default vault path.
# discuss
- ## 

- ## 

- ## 

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
