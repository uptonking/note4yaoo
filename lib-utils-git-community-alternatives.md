---
title: lib-utils-git-community-alternatives
tags: [alternatives, community, git, version-control]
created: 2025-01-01T17:05:39.534Z
modified: 2025-01-01T17:05:58.461Z
---

# lib-utils-git-community-alternatives

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 
# discuss-github
- ## 

- ## 

- ## 

- ## [Why GitHub won | Hacker News _202409](https://news.ycombinator.com/item?id=41490161)
- > your remote GitHub repo can be located on any machine with an ssh connection
  - Technically true, but GitHub provides so many more tools that it's almost silly to do so.
  - Aside from the "hub" in GitHub such that it is often the first and only way that some people will look for projects they're interested in, you also get the nice web interface for quick code browsing, issue queues, the ability to add and remove people with a simple GUI rather than SSH key management, wikis, email notifications, and so on and so on.
- They invented "pull requests" and offered (initially minimal) code review tools. This made contributing in the open.much easier, and making small contributions, vastly easier.
  - Pull requests predate Git. The kernel developers used them in the Bitkeeper days

- GitHub won because Git won. It was obvious by the late 00s that some DVCS was going to upend subversion (and more niche VCS like TFS). It ended up a two horse race between Git and Mercurial. GitHub bet on Git. Bitbucket bet on Mercurial.
  - GitHub's competitors were too slow to embrace Git. So GitHub dominated developer mindshare.
# discuss-gitlab-gogs-gitea-platform
- ## 

- ## 

- ## 

- ## 

- ## [I'm stuck with Gitea 1.25 now... should I do the work to migrate to Forgejo? : r/selfhosted _202512](https://www.reddit.com/r/selfhosted/comments/1pheg8p/im_stuck_with_gitea_125_now_should_i_do_the_work/)
- [Forgejo makes a full break from Gitea _202402](https://lwn.net/Articles/963095/)
  - Forgejo only exists because some contributors were upset that the founder decided to retake control over the domain and trademarks.
  - For the last few years, Forgejo has regularly rebased on Gitea's source. Only recently has the project reduced their dependency on Gitea to occasional cherry-picking..

- I remember trying this like 10 years ago with the community version of gitlab, and it worked fine but it chugged resources as crazy and I had no benefit to just using their free tier on their own site. So over the last 10 years I've been hosting all my code/IaC directly on gitlab without any issues at all.
  - gitea is much lighter on resources than gitlab. you don't have to use gitea if you github is fine. it's also a good way to backup your repo's with the mirror function

- Github Private repos are restricted from using some features. With my own Forgejo insurance, I can unlock those features.

- ## [Any GitHub/GitLab alternatives built for non-technical users? : r/git _202101](https://www.reddit.com/r/git/comments/l2ae04/any_githubgitlab_alternatives_built_for/)
- The difficulty, IMO, is that Git works best with plain-text files. But many non-IT (NIT) people are wedded to proprietary file formats like MS-Word. So, merely making Git more intuitive ain't going to help—NITs still won't be able to take advantage of Git.

- Wikis can provide good collaboration and version control for text, though, and most people should have at least a passing familiarity with the concept by now.

- I Agree. The answer is something like Confluence.

- What is your goal / what should this software mainly be used for? (What problem are you trying to solve?)
  - If you just need versioning, there are many simple backup or synching programs.
  - If you need "forking", there are online collaboration office tools which might be a better fit.

- Gitea is a lot simpler than GitLab/GitHub and still has the core functionalities.

- Check out gitbook.

- ## [Harness launches Gitness, an open-source GitHub competitor | Hacker News _202309](https://news.ycombinator.com/item?id=37598082)
- Codeberg (2019), which was based on Gitea until they forked it into Forgejo (2022).
  - Codeberg is a service not a separate software. Just like you wouldn't count salsa.debian.org or framagit.org as separate from GitLab, they are the same with maybe some local customization.

- How does Gitness differ from already existing open source alternatives, such as Gitlab, Gitea, Gogs, Forgejo, Codeberg, Gitweb?
  - Gitness actually launched in 2012 under the name Drone, with a focus on continuous integration. 
  - So Gitness has a very strong, mature pipeline engine that is also very popular in the Gogs and Gitea community (Gitness is backward compatible with any Drone yaml). 
  - Of course, this is just our initial launch which is a very important milestone, but we have a lot of feature gaps and a lot of work to do to make our Code Hosting solution a more interesting replacement. Stay tuned.

- I won't trust Harness with anything open source. It's the same company that killed the open source Drone CI after acquiring it. They changed the license such that you could contribute to it but could not use it if your revenue was more than 1 million USD. They didn't fix bugs that were well known to them because they were working on the enterprise version of it.

- How does this compare to e.g. Forgejo, Gitea, Gogs, self-hosted GitLab, or other alternatives?
  - Forgejo in particular has self-hosted actions runners that can be registered offline, and the runners themselves can be given labels and execute most existing GitHub actions (in fact, the yaml format they use is intentionally meant to be compatible with GitHub actions).
  - While the Pipelines UI looks nice, it hides all the very real details of deployment (and configuration) in a variety of environments. This is one thing Forgejo does well compared to e.g. Gitea for CI/CD, thanks to being very flexible in configuring runner secrets, registering runners, and so on. 
  - The reason I am emphasizing CI/CD is because hosting code and a bug tracker is only one small aspect of GitHub IMO. The real big things are its popularity and GitHub Actions. It's not enough for many people (and businesses) to simply host code anymore. Many now expect commits pushed to certain branches to execute a variety of workflows -- from unit tests to full-on Kubernetes deployments.

- They should host a demo instance like Gitea does.

- Interestingly it looks like this is partly a fork of Gitea (or at least, incorporates large amounts of code from Gitea)
  - It is largely based on the existing Drone repository, but for Git capabilities we used the Gitea fork of https://github.com/gogs/git-module

- looks more complicated than forgeo/gitea . gitea already servers all github needs for us

- ## [Four years of SourceHut (SourceHut is a open source github alternative) : r/linux _202211](https://www.reddit.com/r/linux/comments/ywbrtc/four_years_of_sourcehut_sourcehut_is_a_open/)
- if only sourcehut was in any way user friendly. making pull requests and looking for issues is such a pain
  - It's email-based, not PR-based. Although devs use git-request-pull instead of git-send-email.
  - Also, issues go to the https://todo.sr.ht page. It's just that some devs don't use that.

- ## [Gitlab like server in nodejs _201702](https://github.com/open-source-ideas/ideas/issues/29)
- I created a basic ssh server that can now clone and push changes. Still needs work on public key auth. Currently using password authentication.

- I feel like Gitea already fills this niche. GitLab supports many features. It's arguable the most complete of the OSS Git front end web apps. Gitea lacks many of its features, but it's considered extremely lightweight, enough so to run well on a Raspberry Pi.

- We need a decentralized open-source alternative, not Gitea or Gogs.

- ## [Does anyone know of a Node.js alternative to GitLab? : r/node _201309](https://www.reddit.com/r/node/comments/1n9byh/does_anyone_know_of_a_nodejs_alternative_to_gitlab/)
- I'm pretty sure nothing like that exists. 
- Well Github was originally written on top of a library called Grit which allowed for Ruby to interact with repos. Theyce since moved on to use a C library called libgit. It's possible to write a Node plugin that will interact with libgit, of one doesnt already exist. This would be my first move if I were in your shoes. Once you have a javascript implementation of something like Grit, you'll be able to manipulate and pull information from repos.

- ## [OneDev - Selfhosted open source alternative to GitHub/GitLab : r/selfhosted _202108](https://www.reddit.com/r/selfhosted/comments/p1fikz/selfhosted_open_source_alternative_to_githubgitlab/)
- Gitea is certainly a really nice project. 
  - We even used its predecessor gogs for some time, before switching to OneDev. 
  - The main reason is lacking of functionality such as pull request approval, reviewer auto-assignment based on contribution history, easy symbol navigation while reviewing pull request, selecting any diff/code to start discussion, real-time preview when authoring markdown, customizable issue field and state etc.

- Gogs/Gitea is perfect for personal usage. But for teams with dozens/hundreds of people, some solid features need to exist to be efficient. This is what we built into OneDev.

- ## [Re: [jgit-dev] Introducing OneDev - an open source git server _201901](https://www.eclipse.org/lists/jgit-dev/msg03748.html)
  - Looking at https://github.com/theonedev/onedev/blob/master/core/pom.xml, it appears this is a web interface that uses JGit for Git support.

- Yes it is using JGit for most operations. JGit API is very well designed and is a joy to use. 
  - The performance is very good, except for long operations such as full clone. 
  - So for pull/push I am calling native git, but for other operations which may need to be executed several times during a request I am using JGit which is much faster thanks for the in-process cache. 
# discuss-git-alternatives 🆚️
- ## 

- ## [Steve's Jujutsu Tutorial | Hacker News _202410](https://news.ycombinator.com/item?id=41881204)
- The auto committing behavior is a bit weird at first, but now I don't want to go back to git.

- The holy grail of a stacked diff workflow would be making multiple Github PRs each made against the previous branch instead of trunk, and then updating the branch that's closest to trunk and rebasing all of the children PRs without having to force push into any of them.
  - Git and Github do not support this workflow directly, and this creates space for all the other tools.
  - Jujutsu comes close to supporting this workflow directly, without having to provide any specialized utilities that mention "stacked diffs" at all.

- ## 🧩 [Jujutsu: A Git-compatible DVCS that is both simple and powerful | Hacker News _202308](https://news.ycombinator.com/item?id=36952796)
  - Jujutsu started as author's personal project and now author's full-time project at Google. It's presented at Git Merge 2022

- There's no longer a time to think about what's being committed, because all file changes automatically amend the working copy commit.
  - What happens if you accidentally save a file with some sort of secret that gets sucked in?

- For 90% of git users 90% of the time, the staging area is an inconvenience that adds an extra step.

- If you're storing 1TB of binary files in git, you're just doing it wrong anyways. You have a bunch of other tools and capabilities for doing this in a way that doesn't make your repository nightmarishly stupid to deal with because of its size.
- Nexus, Artifactory, Packages (deb, rpm, nix), Cache, GitHub Releases... There are so many places you can grab a signed binary from that are just outright better for the health of your repo, and will respect your developers time.
- The issue is not limited to archives, artifacts, and packaging. Game projects, for example, have large directories with many binary assets which need to be change-controlled. Artifact repositories address distribution, in a way, but don't generally support change control much if at all. (And yeah, git's historically a poor choice for this – so you may see companies sticking with Perforce or other non-distributed solutions.)

- Why do you want such big files in a git repo?
  - The point is to have an easy way to distribute code as data. This is important for many areas, such as training neural networks (code with proper seeds can ensure the weights output by training), various applications in basic physics, database creation via ETL, etc.

- We were storing binary files separately via Maven for Java projects for almost 20 years now.
  - This was done with SVN projects. Keeping the blobs out of your source repos has been the preferred way for a long time.
  - The only folks who seem to want to do this are game developers, and they are generally not people you would want to emulate.

- Currently,  `git bisect` works best if every commit is buildable and runnable, in order that any commit can be automatically tested for the presence of the bug, to narrow down the problem commit as quickly as possible. 
- Yeah git bisect is great. And CRDTs on their own probably won’t preserve enough information to allow bisecting to happen - since we don’t know which points in time have working builds.
  - One approach to preserve the ability to bisect would be to allow users to periodically mark points in time with “commits” if they want. The commits wouldn’t be used for synchronisation or merging (since we have the crdt information for that). Instead, they could act semantically much more like anonymous git tags. But they would still be useful as landmarks to mark working builds and milestones. And for git bisect. We could give them associated commit logs. (“Got feature X working”, “Release 1.0.5”, etc).

- 
- 
- 

- ## [Darcs - Another open source version control system | Hacker News _201205](https://news.ycombinator.com/item?id=3947103)
- The primary pull of the "patch theory" is that it will allow you to share code more easily between different "patch sets" (branches / forks). 
  - The reality of software projects means that you can't automate such a process except in the most trivial cases, and other VCSs handle the trivial cases already.
  - By contrast, Git/SVN/Hg folk think about snapshots of development. So it's a different paradigm.

- 
- 
- 

- ## 要想实现 Google 代码管理方案，目前开源解决方案只有 Meta 的 Sapling ，但是对 Git 兼容不太好；
- https://x.com/genedna/status/1797927349624901967
  - 我在做一个 Git 兼容开源方案 Mega， 实现确实很复杂，但是慢慢能看到雏形，争取今年能 Release 一个版本。 
- FYI：我们正在给 Sapling 加 .git 的支持，这样用户可以既可以用 sl 命令也可以用 git 命令
  - Mega is an unofficial open source implementation of Google Piper.

- ## [为什么很多大企业都在用收费的perforce而不是免费的svn或者git？ - 知乎](https://www.zhihu.com/question/23930380)
- 主要还是SVN和GIT都对二进制文件支持很差. GITHUB还特别针对大型文件做了GIT-LFS插件用来支持这种超大文件.
  - 而大型研发公司. 特别是做3D软件的. 分分钟容量爆棚

- 之前不觉得P4有多屌，直到在P4里面创建了有分支功能的stream库，我只能说实在太好用了，一切都是那么清晰。
  - 问了一下，初创公司，每个用户授权大概8000+

- 好像是从15年版本后开始的，还有个1000次提交次数的限制，需要扩展人数可以联系我

- ## 🌵 [Pijul is a free and open source (GPL2) distributed version control system | Hacker News _202402](https://news.ycombinator.com/item?id=39452543)
- Do you know of any FOSS alternatives that handle that stuff better (specifically binary asset handling and permissions)?
  - Pijul does binary files natively, actually. Permissions aren't hard to add, if anybody had a real-world case I'd be happy to help.

- the places where I've seen people leverage the folder-level permissions in Perforce (in the games industry) would be like: a contractor that provides art would only have access to the portions of the project that relate to the art they're working on but not the code; translators might have read access on one directory and write access on another directory. 
  - In academic settings I've seen Perforce used such that an instructor has read-write access on a directory and students have read-only access on the directory, and then each student has a subdirectory where they have read-write access and everyone else has read access, so that everyone can play each other's games. 
  - You can do stuff like this in git with submodules but it's somewhat complicated and difficult to teach to non-programmers.
  - The mathematical/theoretical foundations are clear, but the target audience is unclear, so I'm not sure if these are use-cases that you consider to be within the project's scope or not; just sharing how I've seen the permissions models used in the games industry.

- some indies use Subversion, but Perforce is the industry standard.

- Git compatibility is a great way around this problem. I have been enjoying Jujutsu lately.
- Supporting conversion with some lossy tendencies is a good idea, but maintaining compatibility will stifle innovation as al bugs & design decisions cannot be fundamentally worked around.
  - Adjacent, I heard folks praising Forgejo for its Actions & Microsoft GitHub compatibility, but that means you are still left with the same YAML spaghetti and its other limitations. What would have been nice is something better for CI--something that prompts the project to want to switch to get a better experience. 
  - As such, while I agree with the moral reasons to switch to non-proprietary software, the reason for switching is philosophical, not philosophical + technical. I feel being a wrapper around Git or Git compatibility will likely fall in this category rather than being more compelling.
- Not really. The real innovation of a lot of these alternative DVCS systems is that they free the state of the source from being dependent on the history that got you there. Such that applying patches A & B in that order is the same as applying B' & A' -- it results in the same tree. Git, on the other hand, hashes the actual list of changes to the state identifier, which is why rebasing results in a different git hash id.
  - So long as you require git compatibility, you're kinda stuck with git's view of what history looks like. Which is rather the point.
- jj is not patch based, like pijul, but snapshots, like git.
  - A sibling commentor points out the change id stored by jj: it is true that at the moment, this isn't really exportable to git in a native way. However, there is a path forward here, and it may come to pass. Until then, systems like Gerrit or Phabricator work better with jj than systems like GitHub.
- Jujutsu uses change IDs, which are an abstraction over commit IDs, that are stable over operations like rebasing.

- So Pijul is patch-based. And not in the boring implementation-sense of storing changes as a series of patches. In the interesting sense that patches can be ordered in more arbitrary ways. 
  - On the other hand Git is snapshot-based. And Git was built for the Linux Kernel (specifically from the perspective of the lead maintainer).
- My understanding is that a big part of the reason that Git is snapshot based is for reliability and for ease of checkout -- being snapshot based means Git doesn't need to replay commits every time you check things out.
  - That likely comes with some downsides (cherry-picking does come to mind, yes), but also seems like some serious upsides, one of the biggest one being that simplicity. It's relatively easy for me to reason about what Git is doing under the hood. 
  - I like that I'm seeing that Pijul's patch operations are associative, I like at first glance what I'm seeing it say about merges, but it's not making it clear to me what the downsides are.
- There's no reason you can't cache tree snapshots in a pijul/darcs setting. That's just an implementation detail. The difference is more in how a rebase or merge operation works internally, and how essential the particular history is to the current workplace state.

- 🆚 Pijul has a number of stated strengths over Git, and looks like the version history is implemented as a CRDT from my first impression. Some of the statements make me wonder how many conflicts occur in real use. If they are equal to or less than the number it produces, great. If more than what Git produces, that's a barrier to adoption, as merge conflicts are one of the biggest pains when using Git.
  - 🐛 Git compatibility is a key missing feature. Git had this with Subversion, and I think it's a big reason why Git won over many of the Subversion crowd.

- I'm watching this (and Jujitsu, Sapling, etc.) with interest, but I wish there was more focus on Git's real weak areas. Yes it sometimes makes merge conflicts more difficult than it could, but you can generally deal with that. 
- 🐛 The bigger problems are:
  * Poor support for large/binary files. LFS is bare-minimum proof of concept.
  * Poor support for large projects. Big monorepo support is definitely getting better thanks to Microsoft. Submodules are a disaster though.
  - The basic premise of Pijul is that the way they model changes leads to better merges, fewer conflicts, and (crucially) no cases of bad merges. Git can complete merges and do it incorrectly
- Large/binary files: Pijul splits patches into operations + contents. You can download a patch saying "I added 1Tb there" without downloading any single byte of the 1Tb. No need to add any extra feature.
  - Large projects: Pijul solves that easily using commutativity, you can work on partial repos natively, and your changes will commute with changes on other parts of the monorepo.

- Just like how Sapling is compatible with GitHub, I'd love to see Pijul being compatible with GitHub wrt creating at least a read-only mirror.
- Is sapling compatible? It gets rid of your .git directory.
  - It's network compatible in that you can clone, pull, push, etc with a github repo.

- All version control tools have the same problem since AFAIK none of them care about the semantics of the program being version-controlled (except Unison).

- 🆚️ IIUC, Pijul has all the good parts of Darcs, with the exponential merge issue resolved.

- Does Pijul handle branches better than Darcs? I _love_ using Darcs but I had to stop because there was no good way for my teammates to see my new branches (really separate repos) unless I told them myself.
  - pijul fork. There you go, I wrote an entire key-value store just to get that to work. It turned out to be faster than all others, but that wasn't intentional.
# discuss-fossil
- ## 

- ## 

- ## 🔁⚖️ [The Fossil Sync Protocol | Hacker News _202402](https://news.ycombinator.com/item?id=39464938)
- The problem with single file formats is they don't play nicely with file sync tools in what I'd call "common" scenarios.
  - Due to the way it's laid out, a git bare repository will work quite well with a per-file syncing system because references are stored as files pointing at the hashed object store.
  - So the worst you can do even without central coordination is have a reference conflict. I'm sure bad things can happen, but for the purposes of "keeping repos synced via syncthing" it works well enough (note: this is different to trying to keep a working repository synced, which I wouldn't recommend).

- Since it uses SQLite under the hood, Fossil as a version control system might be able to scale much more gracefully than git for huge monorepos. I think about this often but haven't found a way to effectively use this knowledge yet, since I haven't worked in a giant monorepo shop yet, nor have I found any third parties talking about their experience with this.
- 🐛 They tried using Fossil for netbsd (and may still use it for some things, I'm not sure). Fossil was not designed for large repositories
  - [Fossil Forum: Fossil and large repos? _20200908](https://fossil-scm.org/forum/forumpost/5ad122663cbae98f)
  - It could be optimized for that case, but since there doesn't seem to be a lot of interest, I don't know that anyone is going to do the work.

- Microsoft uses git for Windows repository pretty successfully. It started with custom VFS implementation and fork of git but by now everthing is upstreamed and VFS is not used anymore.
  - Git original implementation did not scale to huge sizes. Needed specific development work to change assumptions. Presumably similar design improvements could change fossil.

- I love the concept of Fossil being in SQLite, but there's a reason that Mercurial invented revlogs and Git tries to keep related objects close to each other in packfiles. Sometimes, you really do need a dedicated file format optimized for specific use cases. I'm completely unsurprised OpenBSD wasn't able to pull this off.

- For a large monorepo network filesystem approach is inevitable. Every local storage approach has limits and breaks down eventually.

- > The "bag of artifacts" data model used by Fossil is apparently an implementation of a particular Conflict-Free Replicated Datatype (CRDT) called a "G-Set" or "Grow-only Set".
  - Isn’t this just by virtue of content addressing objects? In that sense Git’s odb is also a G-set.
- If you look at the definition of CRDTS, it seems trivial that all distributed scms must satisfy CRDT properties. Some observations are trivial once you think about it, but worth saying to connect to different audiences with different interests or backgrounds. I wouldn't be surprised if they added this because they got the question many times. The rest of the paragraph makes clear that they did not develop fossil in the context of CRDTs, and nothing in the rest of the document depends on this observation.

- 🤔 Is this, or could this be modified to be, able to sync an sqlite database (or really the data it contains) between devices? I'm aware of other ways to do this but if there was an internal sqlite way to do this...
  - No, this protocol doesn't deal with SQLite. In fact, SQLite in Fossil is just an implementation detail, the design doesn't depend on it.

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
