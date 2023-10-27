---
title: lib-utils-git-community
tags: [community, git]
created: 2023-08-29T10:13:16.125Z
modified: 2023-08-29T10:13:31.070Z
---

# lib-utils-git-community

# guide

# discuss-stars
- ## 

- ## 

- ## [Fossil versus Git | Hacker News_202309](https://news.ycombinator.com/item?id=37622064)

- My problem with Fossil is that it is a "one solution for all problems". Fossil packs all solutions together while the Git ecosystem provides several different solutions for each problem.
  - When you want to do things that Fossil is not meant to do, then you're in trouble. I have no idea on how to do CI/CD and DevOps with Fossil and how to integrate it with AWS/Azure/GCP.
  - I find the whole ecosystem of Gitlab/Github, Notion, Jira and stand-alone alternatives like Gitea, Gogs, Gitprep and others to be more flexible and versatile.
- To get publicity or outside contributions it's hard to avoid the GitHub trap.

- I don't know Fossil. However, the first entry in the comparison table puts me off. "VCS, tickets, wiki, docs, notes, forum, chat, UI, RBAC" I don't want my version control system to be a wiki. Or a chat app, or any of that
- These additional capabilities are available for Git as 3rd-party add-ons, but with Fossil they are integrated into the design, to the point that it approximates "GitHub-in-a-box.
  - To clarify the actual benefit: this means that tickets, etc. are also distributed, i.e. available and backed up locally with every contributor, and not dependent on lock-in to a single vendor like GitHub.
- Versioning/distributing tickets is indeed useful; but can't this be "implemented" in git already, by defining a file-based format ( `issue/$YYYYMMDDHHMMSS-$title.md`, but the variants are endless), and versioning those files?

- 🤔 If Fossil is so against deleting commits, what do you do if you've accidentally committed sensitive information that cannot live in any form in the repo?
  - Fossil provides a mechanism called "shunning" for removing content from a repository.
  - Every Fossil repository maintains a list of the hash names of "shunned" artifacts. Fossil will refuse to push or pull any shunned artifact. Furthermore, all shunned artifacts (but not the shunning list itself) are removed from the repository whenever the repository is reconstructed using the "rebuild" command.
- It is a problem in all decentralized systems. Once you publish something, there is no going back. Anyone of your peers can decide to leave with your sensitive data. That's also what make them so resistant to data loss.

- Source control is all about managing diffs. Large files are fine, binary doesn’t make sense. Most of the time binary file diffs aren’t human readable.
  - I store binary files outside of git but keep build logs containing binary file CRCs on git

- Most binary files that people want to store in a VCS are stuff like .psd, .xlsx, .docx, and the like - data that's created by people by hand, but not stored as text.
  - Xlsx and docx are just zipped up xml text. You can store it as text if you like and I think there are many git modules to handle this. But the xml isn’t really that diffable so I don’t bother.

- if you have large files in your repository, you have a design problem.
  - Not in gamedev where you can have hundreds of gigs of art assets (models, textures, audio...), but you still want to version them or even have people working on them at the same time (maps...). But that is a different can of worms entirely.
- git is for when you want to track changes to part of a file.
  - In your scenario, you just want to track different versions of a file.
- That's what object storage with versioning turned on is for e.g. GCS or S3
  - Although blob storage work well for versioning, you have to make heavy use of the underlying proprietary API to get these versions, and I am not quite sure you can do more complex operations, like diff and bisect between those versions the way you could with git.
- Why use git at all then? Just use an object store with versioning turned on.
  - Because git excels in relatively small size text files and patching and difficult. You can't binary blobs like jpegs, audio, video easily.

- Git is designed with a strong emphasis on text source and patches. It simply isn't designed for projects with large assets like 3D animation, game dev, etc. 
  - Having said that, solutions like **LFS, Annex and DVC** (not git-specific) work really well (IMO). If you don't like that, there are solutions like Restic that can version large files reasonably well (though it's a backup program).

- Lots of people are saying that having large files in a repo is wrong, bad, bad design, incorrect usage. Forget that you know git, github, git-lfs, even software engineering for a moment. All you know is that you're developing a general project on a computer, you are using files, and you want version history on everything. What's wrong with that?
  - The major issue with big files is resources: storage, and network bandwidth. But for both of these it is the sum of all object sizes in a repo that matters, not any particular file, so it's weird to be harking on big files being bad design or evil.

- That's why Perforce is still the SCM of choice for a lot of creatives. I don't know if they still do it, but Unreal used to ship a Perforce license with their SDK.
  - That's also why perforce is slow as heck unless you throw massive resources at it. 

- In the age of Large Language Models, large blobs will become the rule, not the exception. You’re not going to retrain models costing $100M to build from scratch because of the limitations of your SCM.
  - I don’t store those in my scm. It’s not a limitation of my scm that I can’t store a 20gig model directly in the repo.

- I like the “separation of powers” between git and GitHub functions (and gitlab).
  - It’s nice to be able to start git repos locally and only push to GitHub when I need to.
  - Git is sort of like a protocol with gitlab, GitHub, and others built on top.
- Gitea is already "GitHub in a box".

- I haven’t used Fossil but I have used gittrac, cvstrac in git mode. Cvstrac was what SQLite used before fossil, basically wiki and issue tracker built on top of SQLite, just add CVS, SVN or Git. A very small system compared to Gitea or other forges, but incredibly powerful thanks to SQL and very productive. Fossil is just the logical continuation and shares the same clarity of design and elegant implementation of SQLite.

- why would I want my versioning system coupled to a bunch of random services?
  - Doing one thing and one thing only is a feature, not a bug.

- ## [Git vs. Fossil: what you should have done vs. what you did | Hacker News_202107](https://news.ycombinator.com/item?id=27736980)

- Fossil does anything Git will do, except for one thing: Fossil does not (easily) sync individual branches. (You can do it, but it is a pain.) Git comes with the idea that individual developers keep their own private branches and only share them after they've been cleaned up. The idea behind Fossil is that everybody shares everything.
  - There are advantages and disadvantages to both approaches.

- Fossil's bisect works better than Git's in my experience, since Fossil's data model permits bidirectional tracing, whereas Git can go backwards in time only. This allows commands like "fossil bisect status" to show where you are in the decision tree, since it has to trace forward in time as well to provide the answer.

- The only reason I am aware of for keeping history is bisecting it to track regressions. The "development history" is completely useless for this purpose. What I want is the version history. That's why git is called a version control system.

- 🤔 what if I accidentally commit (not push) a piece of sensitive data (say a private key), but notice before I commit. In Git, I would simply remove it, and amend, and it is now gone from the Git history. It sounds like with Fossil, it would remain in the history, or am I misunderstanding something?
- Careful, amending doesn’t actually remove the bad commit, but it rather creates a new one and changes the appropriate branch pointer towards it. The old commit is still there, browsable if you know what you’re doing. 
- In Fossil it will remain in your local repository but you can put the hash for the data you accidentally committed in a "blacklist" so that it wont be pushed/pulled. I think you can also rebuild the local repository to purge any data, though i'm not 100% sure about that.
  - Fossil has autosync by default, so the commit has probably reached another instance anyway. But it has a provision exactly for those cases, the shunning mechanism.

- One of the repos I interact with, the team rebases all their local branch commits to master. It is very difficult to read the commit history and get a sense of anything except Jira issue codes. One needs to look at the individual files and read the code to understand what the commit was for.
  - This is why the best Git workflows IMO involve rebasing and squashing the branch down to a couple of well-defined "logical commits", then merging that (with --no-ff of course) into master/main/trunk. This forces individual programmers to think somewhat carefully about leaving a sensible commit history behind.
- I think that's a consequence of rebasing. If you just merge instead, you can use the branching/merging to get a sense of complete features/changes.

- ## [Fossil vs Git | Hacker News_201901](https://news.ycombinator.com/item?id=19006036)

- SQLite uses cathedral-style development. 95% of the code in SQLite comes from just three programmers, 64% from just the lead developer. And all SQLite developers know each other well and interact daily. Fossil is designed for this development model.

- It's sad because Fossil underneath the covers is a lot like Git, but with a SQL RDBMS as the store. Fossil's design is much more powerful than Git's for that reason alone. But **that super-opinionated attitude they have is a disaster**. Run away.
- I'm also not convinced it's a good idea to merge your bug tracker and version control.

- I choose fossil at a time when it wasn't clear which one of fossil, Mercurial, or git would "win".
  - I choose it because it had a very clear and easy UI, guided you towards a way of working that is suitable for small teams (ie 99.99% of all projects), and had an approach to history which made it unlikely you'd ever accidentally lose work.
- For what it's worth, Git has a command for an instant web server https://git-scm.com/docs/gitweb

- Branches in Fossil have persistent names that are propagated to collaborators via push and pull. All developers see the same name on the same branch. Git, in contrast, uses only local branch names, so developers working on the same project can (and frequently do) use a different name for the same branch.
- branches are just bookmarks for commits. And Git very much has local tracking branches (that track upstream branches), so it's as Fossil-like as you want, but doesn't pretend to enforce a merge-only workflow.
- That's really the bottom line when it comes to Git vs. all the others: Git doesn't enforce a merge-only workflow, not even as a default, while all the others generally do.

- One thing that isn't mentioned is whether Fossil supports working offline as well as Git does.
  - The way fossil works is that by default autosync is turned on, which means that if you are connected to the internet all of your commits, wiki and issue tracker changes are synced to the server.
  - In the case that you're not connected, everything still works as expected, and will sync back up next time you're online and try to commit or just run fossil update.

- Your commit history should read like a published novel, not a first draft.
  - I think I might’ve read something like that in the Pro Git book and it rings true with me.
  - The philosophy of Fossil is to preserve the full history, which I think is a mistake.
- Both approaches have value. And you'll find books advocating both ways.
- A nice feature would be the ability to group and split commits afterwards; like adding a "novel branch". So that you could keep both the exact history and a parallel high level description.
  - Your high-level description resemble a cover letter used on some open-source project to introduce a patch series, justifying the changes. You could achieve the same by using an empty commit, or tracking those in the bug tracker.
  - DCVSs are already complex enough, this just seems like scope creep, trying to emulate a feature that is actually part of another tool (the bug tracker or the mailing list, depending on the structure).
  - Another issue is that it would foster a mentality where people would simply don't care about the exact history and push really badly structured commits, relying on the second-level history to explain their work.

- Fossil's design and implementation are indeed admirable. Its insistence on merges is not.

- As someone currently working in a project where parts are managed with git and others with fossil, I have a strong preference towards git. 
  - One major issue with fossil is the non-existent ecosystem. It simply does not integrate well with other frameworks and tools (e.g. Yocto/OE)
  - The irony is that they have big performance issues with fossil, precisely due to the fact that **fossil records everything and the push/pull commands sync the entire repo, not just one branch**.
- Fossil also lacks an equivalent to git submodules, which should be added to the list of features found in git, but not in fossil.

- I agree with those who said they prefer git's "clean" commit history.

- Fossil is better. Because it has a better design. 
  - Because it uses SQL (which makes it possible to write queries on the fly in ways that cannot be done in other VCSes). 
  - The use of SQL, and Fossil's use of fairly generic SQL, allowing the use of RDBMSes other than SQLite3, is brilliant, and would make it trivial to make Fossil scale better than MSFT is making Git scale, though with the caveat that you'd probably still end up wanting things like a Bloom filter for speeding up file-level log/blame, but you could probably make Bloom filters a transparent, RDBMS-level query optimization.
- Fossil is worse. 
  - Because it doesn't have a CoW design in the format of its DB, though it does have a CoW design in its SQL schema. 
  - However, because SQLite3 is so good at handling power failures and such, this has not been a big deal (and indeed, Git has had more problems there owing to its ad-hoc storage model). 
  - This, of course, could be fixed by adopting a CoW backend for Fossil. This problem is hardly fatal.
- Fossil is worse. Because of its insistence on merge workflows and not implementing rebase.
- Fossil is worse. Because it has minimal mindshare(心理份额, 认知份额). Mindshare is absolutely critical. The lack of rebase support is part of the reason that Fossil cannot get the kind of mindshare that would allow it to replace Git.
  - rebase is really just a feature that can be built by using scripting on top of a cherry-pick primitive (which Fossil does have)
- Incidentally, GitHub used to also insist on merges in its browser UI, but eventually they added the "rebase and merge" feature.
- Mercurial too resisted rebase. Boy did they. And they gave in and implemented it. Ironically many people rebased in Mercurial long before the feature was adopted

- Fossil does have private branches and the recommended way to publish private work is to integrate it into a non-private branch and sync as usual.

- Git has the following shortcomings which are major (some shared by other VCS too)
  - 1) UI- terrible, terrible UI
  - 2) Unncessarily complex data model
  - 3) Doesn't scale well to large repos (until Microsoft's VFS- windows only)
- I think git and hg are both pretty bad in different ways.
  - Both have pretty terrible UI but so long as one uses magit, git comes out way on top.
  - The data models are different and suffer different problems.
    - A **main issue with git is that it is stupid about file copies and renames**. 
    - An issue with hg is that it doesn’t work well with long running forked histories (i.e. like git branches) because it stores the set of revisions of a file as a list of blocks of “complete file” or “diff from previous version in this list”
  - Both have scaling problems to large repos and algorithm/data structure problems which cause too many operations to be e.g. O(size of history) at least. 
- Another interesting vc system being developed at the moment is pijul which can be simply described as “like darcs but fast and more likely to be correct”. It feels a bit like it’s fitting in with the current trend of CRDTs, although it’s core data structure is not a CRDT as that would imply that all merges have some deterministic resolution (ie merge conflicts do not happen) and that is not the case, instead files are allowed to be merged into a first-class conflicted state which can then be resolved by later patches.
- Git has no first-class concept of file name changes. Instead it tries to use heuristics to spot renames and sometimes they work and sometimes they won’t.
- The data model in Git is hardly more complex than Fossil's or Mercurial's, and it's copy-on-write all the way, which makes it very safe (think ZFS).
- The simple data model is the best part of git so I have no idea what you are referring to. I do not see how one could make it any simpler and still use it to implement a DVCS. The main reasons I picked Git over Mercurial were the data model and the performance.

- ## 🔥 [Git’s database internals II: commit history queries | Hacker News_202208](https://news.ycombinator.com/item?id=32651934)
- 
- 
- 

- ## 🔥 [Git’s database internals I: packed object store | Hacker News_202208](https://news.ycombinator.com/item?id=32637643)
- 
- 
- 

# discuss-git-db
- ## 

- ## 

- ## 🔥 [Git as a NoSql Database (2016) | Hacker News_202104](https://news.ycombinator.com/item?id=26703808)
- 
- 
- 

- ## 🌵🔥 [GitDB, a distributed embeddable database on top of Git | Hacker News_202207](https://news.ycombinator.com/item?id=31987240)
- version control in general turns out to be highly applicable in many areas far beyond source code. I think it's still under-utilized.
  - Yes, it's extremely common to see applications which need a datastore to end up needing lots of version control type features later on, which end up implemented ad-hoc over a general database.
- Git is an abstraction over file trees (or even more generally just chunks of data), and it turns out a ton of problems in software are easily modeled and dealt with as files in a tree.
  - Lots of problems in software are easily modeled as ordered lists, but that doesn't mean linked lists are the right tool for accomplishing that.

- GitDB doesn't handle merge conflicts, so I'm not convinced it would handle multiple clients well. The It's again marked as something they might do in the future someday. I suspect this is pretty fragile. (Note: I was _not_ claiming litestream would do such a thing. Just replication.)

- You can already store and sync issues in git repo metadata, check out git-bug: https://github.com/MichaelMure/git-bug

- How does merging work? Would it even be acceptable to allow automatic merging in all types of application?
  - To be honest, I would be completely fine with a use case that offloads conflict prevention to the application.

- ## [How to implement git-like "branching" on a MongoDB database in Node.js - Stack Overflow](https://stackoverflow.com/questions/64635567/how-to-implement-git-like-branching-on-a-mongodb-database-in-node-js)
- I think you are diving into the world of temporal data so it would probably help a lot to start drawing timelines.

- ## [Does git use databases? - Quora](https://www.quora.com/Does-git-use-databases)
- Git stores everything inside objects found inside .git directory.
- All the references (40 characters hash) pointing to those references are stored inside refs directory.
- git treats files and directories in 3 stages: your normal files/directories, staging area, committed area(repo). 

- ## [Is there a better database than Git (with serializable, immutable, versioned trees)? - Stack Overflow](https://stackoverflow.com/questions/7152276/is-there-a-better-database-than-git-with-serializable-immutable-versioned-tre)
- Datomic provides a persistent data storage and a built-in time notion.

- Although the index/working copy parts of git can be separated out easily enough, git is not designed for merges or commits at the rate of thousands per second on a single machine. The core code is not even threadsafe, for the most part. You will likely need to create some new system for your data (you can still use git for the code, of course, and can also look into generating git commits to represent your data when necessary, etc).
- So libgit2 isn't thread-safe? It would seem that Git would be inherently thread-safe considering it's data structure
  - Nope! It has cache structures, etc, that are not thread-safe. The core git code was only designed to run in a single-threaded manner as command line tools, after all.

- [Git: the NoSQL Database - Speaker Deck](https://speakerdeck.com/bkeepers/git-the-nosql-database)
# discuss
- ## 

- ## 

- ## 

- ## 用 git 来当网盘用如何？
- https://v2ex.com/t/525782
- 相比传统网盘的优势
  - 方便迁移
  - 版本管理更方便
  - 程序员的代码和工作空间可以一起上云了

- 缺点
  - git处理二进制文件太慢了
  - 正规用法是用 GitHub LFS 服务（收费）
  - dropbox一类的网盘都是你编辑完文件保存就自动上传了，git 还需要 commit push，相比之下 git 的存在感还是太强了

- ## [随着版本不断的更新，以前的版本内容会不会越积越多，导致占据太多硬盘容量？](https://www.zhihu.com/question/370933878)
- 会，非二进制文件只记录差异部分
- 会的。git会保留你每次更新的完整文件, 所以随着commit的增加, 仓库所占体积肯定会随着增加。并且git会把远端仓库的所有commit拉到本地, 本地存储也会增加.
  - git设计的初衷主要是为了代码管理, 代码作为文本文件经过压缩之后不会很大. 
- 那么如果一定要添加二进制的大文件怎么办?
  - 建议使用Git LFS, 这个模块专门用来管理大文件的. 大概原理就是, 在添加大文件的时候, 如果被标记为LFS, 相应的git会自动添加一个描述文档. 推送到远端的时候会完整上传文件和描述文档. 在其他开发者拉取代码时, 标记为LFS的文件只拉取一个相关的描述性文档. 只有在必须获取该文件时才会下载. 这样其他开发者反应更快速.
- .git文件主要用来记录每次提交的变动，当我们的项目越来越大的时候，我们发现 .git文件越来越大。
  - git给出了解决方案，使用 `git branch-filter` 来遍历git history tree, 可以永久删除history中的大文件，达到让.git文件瘦身的目的。

- ref
  - [gitee仓库体积过大，如何减小？](https://gitee.com/help/articles/4232#article-header0)

- ## [为什么其他办公领域不使用git?](https://www.zhihu.com/question/329750471)
- Git对非纯文本内容支持并不好，虽然能管理版本，但是无法方便的diff，merge。
- Git一般对文本文件支持比较好，但word、excel等office文档是二进制文件。
- 最好的方案是在加工内容阶段和格式优化阶段完全剥离。
- svn给美术策划用, git给程序用

- ## [使用git管理ppt版本等文档吗？](https://www.zhihu.com/question/22322435)
- Git适合管理文本内容, 但不适合管理二进制内容
  - Git 属于分布式版本控制系统, 需要 clone 整个仓库后才能 checkout 出最新的版本, 修改后提交. 而二进制内容比较难压缩, 会导致整个仓库占用的空间飞速增长. 没多久你可能就会发现, 你需要修改一个 2MB 的 PPT, 却需要先 clone 一个 200MB 的仓库, 而且过去的那些版本基本上又不再需要使用了.
  - 出现冲突时, 二进制内容(特别是你使用场景中提到的PPT)基本不存在自动完成 merge 且不出现 conflict 的可能性. 换言之, 一旦出现分歧, 就必然需要手工合并, 代价不小, 而且容易出现操作失误.
  - 根据你的使用场景来判断, 应该主要是在 Windows 下工作的. Git 在 Windows 下相比在其他平台下要难用得多..
- 像你这种场景, 要么使用传统中心式版本控制系统, 比如 SVN, 要么通过在线的协作环境, 比如 Microsoft 自己的 Office Web 版, 或者 Google Doc. 
- 但回到最初的问题: 你需要的真的是一个"版本控制系统"吗? 也许仅仅是一个集中分享的地方, 也许仅仅是希望一个人修改的时候, 另一个人不能修改, 而已.
- 其实！你们忽略了一件事情！pptx文件实际上是个zip文件，解压开来全是文本的xml和你加进去的视频、图片，是可以用git管理的！

# discuss-fossil
- ## 

- ## 

- ## 

- ## [Fossil | Hacker News_202203](https://news.ycombinator.com/item?id=30815693)
- Git's 'killer-feature' by now is simply its ubiquity
  - for Fossil's this could be claimed as a single binary that does it all.
  - Just download the binary, and you've got the ubiquitous set of project-related facilities: VCS/tickets/docs/wiki/team/forum/chat with simple aporoach to sync and self-host.

- It sounds to me that people are split on whether or not SCM should include things like issues and wikis directly, or let others solve it.
  - Considering this is the largest point between fossil and git that I can see, maybe we should just make it so git has the capability to expose an extension API for plugging additional capabilities like this in.
  - Then we could probably all use git and just be happy. You could theoretically use fossil's issues and wikis with git.

- It's pretty much Gitea in a single SQLite file (Wiki, tickets, version control, etc.). It's weird, but you can edit all of these things off-line and then sync everything back. fossil ui hosting the server for my docs locally, and from my home server is super useful and easy.

- Issues and pull requests don't get replicated by git. If github goes down, you can't interact with issues. If github ever turns evil, or you decide you want to self host git over ssh or something, you lose the history of all your issues and conversations.
  - Git is a distributed, replicated data format. Why are issues fully centralized? Its bizarre
  - Fossil is far from perfect, but I think putting the issues and stuff into the repository itself is brilliant.
- It is brilliant to integrate things with the decentralized source control itself
- But despite its brilliance it's not always the right approach. 
  - It's very easy and reasonable to want more than what is realistic for something deeply integrated with the source code itself to provide, if only for inherent conflicts of desire, let alone any question of manpower. 
  - There are very good reasons to have entirely separate (and even multiple-of-kind partially overlapping/integrating/cross-referencing) systems for source code management, issue tracking, code review, forums, IM communication, wikis, public websites, docs (of whatever kinds and types for various audiences and authors, or public or not, or team-level spikes or plannings or retrospectives)... 
  - One aspect of Fossil I found weak was its user capabilities (no custom user categories alone is a deal breaker for so many things) but flaws in the execution of a fully integrated thing isn't really my point, my point here again is just that full integration despite its overlooked benefits and brilliance when applied to certain things is still not necessarily the right choice for something.

- My favourite thing about fossil is that the repo is a single SQLite database file so it’s extremely to just back it up or keep the repo in cloud storage. With Git I’ve always had problems with conflicts in the .git directory which messes things up, but fossil is a single file so it backs up to the cloud wonderfully.

- I'm curious how others do **code review** in fossil? It's something that GitHub is quite good at in my opinion; raising pull requests, having pre-merge checks, commenting on individual lines of changes, etc etc is all useful. It's something I can't see how to do in fossil.

- I am not sold on the wiki and issue tracker. What would be a killer feature is a web UI interface to fossil commands like sublime merge for git.

- One thing that has prevented me from trying out fossil is there is no squash. The team has a principled stand on not having it.
- The author of Fossil considers rebase harmful, and because of that, it wasn't implemented
  - Fossil has private branches which can serve the same purpose. When you merge a private branch it looks just a single commit, similar to a squashed merge.

- ## [Fossil | Hacker News_202009](https://news.ycombinator.com/item?id=24643200)
- having issue tracking in the repo prevents lock-in of that data - in the way that the github platform works, for example.

- I use fossil mostly as a Customer/Project KB/Documentation tool, when a new project starts i have all the documentation, code snippets/examples in one single file, when the project is finished, i have to give one sqlite.db file over to the customer and that's it. LOVE IT, a really great tool!

- Would like to see a SCM that:
  - handles large files effectively (build artifacts, 10-40GiBs each, and other binary dependencies)
  - partial checkout of the repo/view
  - git style operations (have stage area, can stage parts of a file, can stash changes and reapply later, cherry pick)
  - can view the history of an individual file (support file relocation)
  - access control on individual files, and partial review of the repository (views are "granted" to developers)
  - good tooling
  - immutable when it makes sense (e.g. you cannot changed a published commit)
  - works offline (if possible)
  - large mono repo
- I evaluated git annex and git lfs, and finally chosen Perforce, mainly for its large file handling, view for each developer and ACL, but the lack of flexibility makes me don't want to commit, and every time I do a merge, I say to myself, "uuh, this again". The other thing it lacks is the "ease of mind", with git, everything is checksummed, if the content changes, it will be noticed by git, with Perforce, you have to tell it you want to edit it.

- There are several bug tracking systems that store their data inside the repository (and as a result, branch / merge / push / pull automatically) -- including the venerable "vi bugs.txt" system which works surprisingly well from experience.
  - What fossil brings that those systems don't is indeed the network effect as you pointed out. It's integrated with the web frontend, and is thus used by everyone using fossil and fossil's bug tracking, based on experience with cvstrac, is low ceremony, easy to use and reasonably effective -- even more than "vi bugs.txt" which sets a remarkably low ceremony bar.

- ## [Fossil – Simple, high-reliability, distributed software configuration management | Hacker News_201412](https://news.ycombinator.com/item?id=8697028)

- Fossil is version control software with "embedded" wiki and issue tracker, while Trac is a wiki and issue tracker which can, optionally, interface with one or more external vcs systems. 
  - Fossil stores the wiki and issue data in the repository itself (SQLite), while Trac stores it in an external database (PostgreSQL, MySQL etc.. SQLite would probably work too!).

- ## [Show HN: Grit – a multitree-based personal task manager | Hacker News_202104](https://news.ycombinator.com/item?id=26673221)
- What's the difference between a dag and a multitree?
  - prevents diamond shapes
  - An earlier version of the program actually used DAGs, but I found it a little underconstrained. I got pretty excited when I discovered multitrees, as it seemed to be exactly what I needed the whole time.
- Precisely; a multi-tree has a unique path between two nodes.
  - On the same note, I wonder what is the relation between dags/multitrees and semilattices. They seem to be very similar concepts afaict.

- 🤔 How is the data stored? Would it be difficult to sync among different machines?
  - Just SQLite - two tables, one for the nodes, one for edges + some fancy constraints and queries. 
  - As for the syncing, that would be really nice, but I haven't come up with an elegant way to do it yet. Suggestions welcome, if anyone has ideas!
- git. The right storage backend is either git, or a git-like Merkle tree. This is small data. Individual files for objects are fine. Compacting is better, but not critical.
  - sqlite is the wrong tool for the job, beyond an initial prototype. git and hg figured this stuff out decades ago.
- Fossil would disagree that SQLite is somehow wrong for this use-case.
  - Fossil does seems to have issues when the VCS grows into many many gigabytes of data, like the entire OpenBSD source tree didn't work out very well in Fossil, but the chances of a personal task manager ever growing that size is slim to none I would imagine. 

- I use a flat text file with exactly this structure, just indenting when I need a new layer.
  - this supports a slightly more interesting structure than an indented text file: it's actually a DAG where large subgraphs are trees. This allows links between different nodes. That's not possible in an indented text file.

- TiddlyWiki uses a similar data model for table of contents by default and I love it! I think the multitree constraint is a good idea over a general DAG.

- ## [Why I'm using Fossil SCM instead of other source control systems (2016) | Hacker News_202206](https://news.ycombinator.com/item?id=31634560)
- I’m just waiting for the next VCS that brings significant changes. We’d absolutely switch over if there was some feature we wouldn’t get elsewhere. But it’d need a couple of months/years of sustained advocacy.
  - The next big thing will be semantic code versioning. I.e. a tool that **understands language syntax and can track when a symbol is changed**.
  - There are already experiments in this area, but I don't think any are ready for mass adoption yet.
  - The fact that it's 2022 and we're still working with red/green line-based diffs is absurd. Our tools should be smarter and we shouldn't have to handhold them as much as we do with Git. It wouldn't surprise me if the next big VCS used ML to track code changes and resolve conflicts. I personally can't wait.

- Feature for feature Fossil is more like a competitor to Github or gitlab. 
  - Basically it is a SCM based on sqlite that is a lightweight version of those websites offer.
  - To add some detail here. The features it offers (tickets, wiki, chat, forums, etc) are stored within the repo, unlike github or gitlab where those things may be separate.
  - Basically, if you have the repo and the fossil binary you have everything. Is this better? I never saw a lot of advantages in my style of work, but i could see this being huge for someone who has intermittent connectivity. Or maybe someone who wants to use the ticket tracking, etc without setting up a separate server or public instance.
  - I just love that fossil exists and there is a diversity of opinion on how things can work.

- Fossil came out in a time when your options were basically CVS, SVN, or something commercial like Perforce. 
  - Git is an innovation that came out around 2005 (A year before Fossil), and it took a few years to get some traction, but holy moly are either of these better than what came before. 

- I suppose a competitor could also have some kind of git compatibility shim built in to ease the adoption.
  - Fossil does let you import and export git I think. Fossil just has the wiki and issues on its side

- I hear a lot of larger teams insist on squash commits for PRs. Fossil isn't a fan of squashing.

- Would the wiki part of fossil be a good static site generator?
  - Not in the general case, no. Fossil-generated wiki/markdown output expect to be browsed within the context of a fossil repository, and will generate links accordingly.
  - There might be very limited use cases where it would work reasonably well, but not generically. e.g. adding a link to a local file or another wiki page will not work if the output is browsed from outside of a fossil repo instance.
