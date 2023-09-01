---
title: lib-utils-git-community
tags: [community, git]
created: 2023-08-29T10:13:16.125Z
modified: 2023-08-29T10:13:31.070Z
---

# lib-utils-git-community

# guide

# discuss-git-db
- ## 

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
