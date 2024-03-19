---
title: lib-utils-git-community
tags: [community, git]
created: 2023-08-29T10:13:16.125Z
modified: 2023-08-29T10:13:31.070Z
---

# lib-utils-git-community

# guide
- [Fossil: The Fossil Sync Protocol](https://www.fossil-scm.org/home/doc/trunk/www/sync.wiki)
  - The "bag of artifacts" data model used by Fossil is apparently an implementation of a particular Conflict-Free Replicated Datatype (CRDT) called a "G-Set" or "Grow-only Set". 
# discuss-stars
- ## 

- ## 

- ## 

- ## 🤔 What makes Git so popular?
- https://twitter.com/sahnlam/status/1765986551123882087
- 𝗕𝗲𝗳𝗼𝗿𝗲 𝗚𝗶𝘁, developers struggled with source control. Systems like CVS and Subversion caused:
  - Collaboration Bottlenecks - Pushing to a shared central codebase created bottlenecks and isolated work.
  - Slow Branching/Merging - Diverging code streams and combining changes was clumsy and inefficient.
  - Scaling Issues - Performance degraded as projects and users grew. Centralized systems didn't scale.
  - Release Headaches - Coordinating versions across teams was messy.
- Git 𝗿𝗲𝘃𝗼𝗹𝘂𝘁𝗶𝗼𝗻𝗶𝘇𝗲𝗱 source control by:
  - Enabling decentralized collaboration through distributed repositories.
  - Streamlining local branching and merges.
  - Allowing offline work with full local codebase copies.
  - Optimizing performance even for large projects.
  - Tracking every change at a granular level.
- 𝗚𝗶𝘁𝗛𝘂𝗯 𝗮𝗰𝗰𝗲𝗹𝗲𝗿𝗮𝘁𝗲𝗱 Git's popularity by adding:
  - Web-based collaboration around remote repositories
  - Pull requests and code reviews
  - Social coding features like stars and follows
- However, Git 𝗶𝘀𝗻'𝘁 𝘄𝗶𝘁𝗵𝗼𝘂𝘁 𝗱𝗼𝘄𝗻𝘀𝗶𝗱𝗲𝘀:
  - The conceptual model is complex with a steep learning curve.
  - The command line interface is unintuitive and confusing.
- Despite these complaints, Git's collaboration features and flexible workflows cement(加强；巩固) its place in modern development. This game-changing tool revolutionized source control for the better.

- ## 🚀🌵 [A Git client for simultaneous branches on top of your existing workflow | Hacker News _202402](https://news.ycombinator.com/item?id=39357068)
- > Quick warning. You cannot use both GitButler virtual branches and normal Git branching commands at the same time, you will have to "commit" to one approach or the other.
  - Basically anything you do with git (or another GUI) will get blown away by GitButler; or if you change branch away from it then it will stop working.
- This limitation stems from the fact that GB introduces an additional dimension of versioning on top of Git. 
  - One way of thinking of what it does with virtual branches is like "multiplexing" multiple branches onto the same working directory. On the way out they get "demuxed" into plain git trees.
  - With that said, the tool is very cautious not to mess with any existing branches. This is the very reason it operates on a separate integration branch. Switching between the "special/integration" branch and any other branch is also not an issue.

- For my own sake, allow me to articulate the core value proposition once more. GitButler's virtual branches permit two novel use cases:
  - A developer can lazily assign diffs/changes to belong to separate logical branches while maintaining their content within the same working dir. 
  - A developer can apply and unapply the content of remote branches to their working directory for the purpose of testing & review. 

- 🆚️ there _is_ a way to work on multiple branches at the same time: worktrees. What's the advantage of a tool like this over that?
  - With worktrees you can have different branches in different working directories and work on them at the same time. But practically, there is very little difference to just cloning the repo twice and working on different branches in the two checkouts.
  - The way we're doing it, the branches are both in the same working directory at the same time.
- This can have a couple of advantages 
  - one is if you have an annoying bugfix and you need it in order to keep working on your feature, you can have them both applied but you don't have to commit one into the history of the other. You cannot do this with worktrees.
  - Another is trying out multiple branches together. If they don't conflict, you can essentially get the result of a multi-way merge without creating any merge artifacts. Say you merge three work in progress branches to test them together, then keep working on each independently. Also, in this case, you _know_ that you can merge them in any order and the result will work because you've actually worked on the merged tree.

- 🔀 The CRDT thing happens in GitButler, but we hid the UI to search and find old changes for now
  - We still record the data locally and could theoretically recreate the state of your working directory and branches at any time.

- Is there a way to identify commits made by GitButler? Can I configure my host to reject them automatically?
  - GitButler creates normal Git commits and trees with libgit2. It's not dissimilar to using a tool that implements it's own interactive adding or something. The point is that Git is the database and Git hosts (such as GitHub) matter in our workflows, but actually creating the trees that represent the trees you want to share can happen in any way. We are changing how to conceptualize and execute how to get the trees you want, but the output is Git objects.

- Intellij IDE support this through changelists.
- The listed cons of “changelists”:
  1. Not part of Git at all—not committed
  2. Can’t be shared because, duh, not part of Git
  - That sounds like a fail to me. The whole point of using Git commits is that once committed, it’s just there. And things can be shared. The point of collaborative version control.

- doesn't work with other tools + GUI only => non starter

- 
- 
- 

- ## At Github, anyone can commit for you just by specifying your email in --author.
- https://twitter.com/sitnikcode/status/1759538798180876516
  - This is why I enabled signing commits in git using my SSH key using this guide
  - [Git Tips 2: New Stuff in Git](https://blog.gitbutler.com/git-tips-2-new-stuff-in-git/)

- ## 🆚️ Git Merge vs. Rebase vs. Squash Commit
- https://twitter.com/sahnlam/status/1767434052695621850
- 𝗚𝗶𝘁 𝗠𝗲𝗿𝗴𝗲 
  - This creates a new commit in the target branch. 
  - The new commit ties the histories of both main and feature branches together. 
  - Git merge is non-destructive - it introduces a new commit without altering existing ones.
- 𝗚𝗶𝘁 𝗥𝗲𝗯𝗮𝘀𝗲
  - Rebase transplants commits to the tip of another branch. It creates new commits for each one moved over.
  - The benefit is linear history. But be cautious with shared branches to avoid confusing collaborators.
- 𝗚𝗶𝘁 𝗦𝗾𝘂𝗮𝘀𝗵 𝗖𝗼𝗺𝗺𝗶𝘁
  - Squashing condenses multiple commits into one, streamlining the commit history.

- 
- 
- 
- 

- ## 🆚️ Git Merge vs. Rebase vs. Squash Commit
- https://twitter.com/alexxubyte/status/1751645221602152881
  - 示意图
- 𝐆𝐢𝐭 𝐌𝐞𝐫𝐠𝐞 This creates a new commit G’ in the main branch. G’ ties the histories of both main and feature branches.
  - Git merge is 𝐧𝐨𝐧-𝐝𝐞𝐬𝐭𝐫𝐮𝐜𝐭𝐢𝐯𝐞. Neither the main nor the feature branch is changed. 
- Git rebase moves the feature branch histories to the head of the main branch. It creates new commits E’, F’, and G’ for each commit in the feature branch. 
  - The benefit of rebase is that it has 𝐥𝐢𝐧𝐞𝐚𝐫 𝐜𝐨𝐦𝐦𝐢𝐭 𝐡𝐢𝐬𝐭𝐨𝐫𝐲. 
  - Rebase can be dangerous if “the golden rule of git rebase” is not followed. 

- ## [what's the difference between a DAG and a tree, specifically with regards to Git?](https://stackoverflow.com/questions/26395521/dag-vs-tree-using-git)
- The difference between them is that nodes in a DAG can have multiple parents. The most common case of this in Git is when you do a merge. A merge commit will have all of the commits that were merged as parents. 
  - A tree doesn't allow nodes to have multiple parents.
- a tree can have at most only one root, whereas a DAG can contain several roots, and even multiple disconnected subgraphs
- Most git repositories that I've worked with only have a single root commit. Although it's technically possible to create multiple root commits

- ## 🌵📡 [What comes after Git | Hacker News_202207](https://news.ycombinator.com/item?id=31984450)
- Kubernetes didn't brought open-source collaboration to a new level. No matter how relevant Kubernetes is today, it's just a drop in the huge ocean of OSS. Maybe level in this context refers to 'gitops' which many of us where doing years before the term was coined and without K8s involved. Or perhaps the author refers to the fact that most gitops K8s frameworks will work via polling which is a fundamental scalability flaw.

- My main complaint is it's leaking abstractions. You basically need a PhD in git's internal data structures to use git. Well not the 5% of git you typically need in your day-to-day, but the other 95%, which you need when the 5% you do need somehow goes wrong, through one of the many foot-guns git offers.

- The model's basically a directed acyclic graph (not a tree), with each edge being the diff between the two nodes it connects. I think the UX could be improved if it built on the language of graphs to make that model more apparent - node, edge, etc.
  - There are a lot of people, even in this comment section, whose internal model of git is "it's a tree". Langauge like "branch" reinforces that model, and I don't think it does beginners any favours in the long run.
- It stores a full copy of every node, not the diff. The diff is just something that's rendered on-demand, and "gc"/"repack" compaction and it being content-addressable makes sure that the storage space doesn't balloon as a result of everything being a full snapshot. This distinction makes a difference in some cases, there are other VCSs that store diffs as a fundamental property.

- I personally believe that making diffs more human friendly is the next step of evolution we need. I feel like git was perfect when "code" was nearly almost completely text and patches were sent over email, but there's a lot more boilerplate+blob data that goes into git today and git needs to evolve to support this.
- Semantic diffs are great, but we can't entirely automate away "narrative problems" in a PR. No matter how good a diff is, a diff tells you what changed but not why and sometimes not even how. That's what we need good commit messages for. That's what we need good PR descriptions to do. If a branch has a ton of seemingly unrelated files modified (automated tool output or not), sometimes you have to ask the narrative questions: "Why did this change? What does it have to do with the other changes in this branch?"
- Semantic diff – Can we figure out how to use version control to have more context-aware merges? Can you believe that we still rely on a text diffing algorithm from 1976 (and its shortcomings)? Git still has trouble with file renaming. GitHub Copilot, but for merge conflicts? Semantic diff has been tried before, but language-specific implementations will likely never work.
  - in case anyone missed it: https://github.com/Wilfred/difftastic
  - Difftastic output is intended for human consumption, and it does not generate patches that you can apply later.

- 🪨 I've been using fossil for personal projects for like a decade now and I much prefer it over git. The characteristics that get me to stick with it are 
  - 1. Single file executable. No dependencies to "install". Just the executable and you're good. 
  - 2. The whole repo is a single sqlite DB file. Fabulous for backups, sharing, hosting etc. 
  - 3. You cannot rewrite history unlike git. Hence the name. Folks using git have no idea what kind of a peace of mind this gives me. 
  - 4. Integrated issue tracker stored in the same repo. Complete with cross references to commits. 
  - 5. Allows repeated use of same tag name. This is so convenient in personal projects I miss it in git. You can mark a commit as "published" and later look at the whole history of all previous commits tagged as "published".
- Other niceties
  - 1. Integrated wiki - I've occasionally used it, but usually prefer to write documentation in separate files. 
  - 2. Integrated webserver - fossil ui runs on the same thing so I do use it. The webserver comes complete with user account management and permissioning. 
  - 3. Can export and import to/from git.
- How is large file support? What strategy is employed for binary file handling? How does it compare to git LFS / annex / mercurial? Aside from that, Fossil is very intriguing.
  - Fossil is, because of its sqlite dependency, limited to blobs no larger than 2GB each. Some of its algorithms require keeping two versions of a file in memory at once, so "stupidly huge" blobs are not something it's ideal for. 
  - it handles binaries just fine and can delta them just fine. It cannot do automatic merging of binary files which have been edited concurrently by 2+ users because doing so requires file-format-specific logic. (AFAIK _no_ SCM can merge (as opposed to delta) binaries of any sort.)
- I do hope someday git and others employ either a git annex or mercurial-style scheme where if it's a large binary file: 1. no diff is performed, and 2. only the latest version is kept within the history. This would blow wide open the possibilities for using Fossil in binary-heavy projects such as machine learning, games, simulation. I could see the SQLite limitation worked around by just splitting up binary data into multiple pieces.
  - 👉🏻 That will never happen in fossil: one of fossil's core-most design features and goals is that it remembers _everything_, not just the latest copy of a file. The way it records checkins, as a list of files and their hashes, is fundamentally incompatible with the notion of tossing out files. It is capable of permanently removing content, but that's a feature best reserved for removal of content which should never have been checked in (e.g. passwords, legally problematic checkins, etc.). Removing content from a fossil repo punches holes in the DAG/blockchain and is always to be considered a measure of last resort. In my 14+ years in the fossil community, i can count on 2 fingers the number of times i've recommended that a user use that capability.
  - Sharding large files over multiple blobs doesn't solve some of the underlying limitations, e.g. performing deltas. Fossil's delta algorithm requires that both the "v1" and "v2" versions of a given piece of content be in memory at once (along with the delta itself), and rewriting it to account for sharded blobs would be an undertaking in and of itself. That's almost certain to never happen until/unless the sqlite project needs such a feature (which, i'm confident in saying, it never will).
  - TL; DR: fossil is, plain and simple, not the SCM for projects which need massive blobs.

- The only major problem I see with Git is that it's just a pain if you're working in a gigantic monorepo.
  - Separate version control software can be designed for solving a specific problem - but I don't think Git should need to evolve beyond the problems it's designed to take on.

- The large file problem is a major issue in games, and basically means that developers who would much rather use Git, don't have the option of using Git because it would be crushed under the weight of all the art assets. So instead everyone's forced to use Perforce or Subversion, with all the workflow impediments that involves.
  - A lot of groups with large file problems seem to be converging on Git LFS at this point over Perforce/Subversion. Most of the major hosts (Github, Bitbucket, Gitlab) all have LFS hosting support, though it is not always cheap. (Arguably still cheaper than Perforce/Subversion, especially in accounting for those workflow impediments and the developer time they cost.)
  - LFS is a plugin to install, but that's maybe a strong indicator in favor of the git model that there are common plugins to solve some things like this. (And many distributions of git now also bundle LFS.)

- The project management features don’t have to live inside VCS, but it would be nice to sync them there or derive some of the primitive data structures there — comment trees, approvals, CI red/green results at integration time.

- My main headache with git — which is absent from the list in the blog – is that it tracks snapshots instead of tracking changes. 
  - All git can do is to compare snapshots and allow you to impose a resemblance causal order onto them (which you can freely manipulate anyway with rebasing, squashing etc.). If your workflow consists of trying out many different ideas and then choosing which of them to keep and which to discard, git can be extremely painful — you either end up with a history that is a complete mess or waste a lot of time rebasing and reorganising the (fake anyway) order of snapshots. That's why I am exited for tools like Pijul that attempt to actually track changes.

- Snapshots do have the advantage of not having to know anything about the data. Tracking changes necessarily needs to define a way to describe how things may change. Perhaps another take on the issue is that changing data should be structured to be more snapshot friendly?

- > Git is line-oriented and has no notion of semantic diffs and semantic merges. This makes it a raw tool when working with, ironically, source code.
  - Git is a content addressable snapshot system, with bolted on code to make it retrospectively appear to be a line-oriented system. It's worse than you thought.
- It's not worse. Snapshots are exactly what you want if you would like to have format-aware diff/merge or to experiment with alternate algorithms. But it's easier to complain about git and throw out pie-in-the-sky ideas about "modernizing our tools" than to try the actually-existing AST-based diff/merge tools and realize it's 100x more complex for no workflow gain.

- Diffs aren't actually a first-class object either, they're made up on the spot. Git just stores a complete snapshot for each commit; delta compression in the repo is incidental(次要的; 伴随的；补充的；附属的) and unrelated to the diffs you see.

- 😩 Git doesn't understand move and copy operations very well, and has to be tricked into doing it.

- I’m not qualified to go into specifics but I hate it. All version control needs to do is pull, push and branch. Version on branch is newer? You need to pull down before you can check in. Instead what we get is over complicated nonsense with commits and stashes, rebases and heads, reparenting etc. I get it you don’t want to store your code on your local machine but that’s what backups are for, that’s not what the version control system should be doing.

- 🆚️ I like the patch-based approach of Pijul and Darcs: rearranging patches seems less fragile than rebasing snapshots.
  - Pijul works quite differently from Darcs: the primary datastructure in Darcs is indeed a list of patches, and the main operation is rearrangement.
  - Pijul is instead a CRDT, meaning that independent patches can be applied in any order without changing the result, which makes rearrangement unnecessary, and the system much faster.

- Implicit branching in Pijul is a killer feature (IMO)
- for distributed version control, the "first-class conflicts" of Pijul seems to be a step in the right direction.

- My main issue with Git, other than the terrible UX of the CLI, is just how common it is for one to want to rewrite the commit history - an operation for which there's no version control.

- You might be interested in my project git-branchless https://github.com/arxanas/git-branchless or the Git-compatible Jujutsu SCM https://github.com/martinvonz/jj, both of which have version control for commit history via an operation log. Both feature sensible undo commands.

- A client side virtual file system (FUSE), so that you can work with large repos that exceed the size of your own system.
  - Version control systems like Piper (Google internal) and Eden (Facebook), GitVFS (Microsoft) already do this, but adoption is marginal.
- I really want a system-wide content addressable store that a lot of different things can use.
- It's also interesting to note that at this point Microsoft seems to be pivoting away from GitVFS. They've put a lot of collective engineering work in git sparse clones and git partial clones and the intersection of the two ("sparse cones") and optimizations like git commit graph pushing git itself to better at virtualizing its object store, not touching objects it doesn't need, and better handling just-in-time scenarios for object retrieval when it really does need them.

- Native large file support. Git annex functionality built in = gg every other source control system.
  - Git annex "competitor" Git LFS is bundled in many distros of git today and supported by most of the major hosting providers at this point (if you are willing to pay for LFS space).

- most of my problems with git went away when I started using worktrees

- The semantic diffing bullet point has me wondering what attempts there are at making open source semantic diff tools. I love the closed source tool SemanticMerge, but the company behind it decided to be shitwads and pull the product so they could add a selling point to their proprietary version control system.

- git is like cpp, you have to use a subset

- ## [What comes after Git? | Hacker News_202012](https://news.ycombinator.com/item?id=25535844)

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
- In almost every database-backed application I've ever built someone, at some point, inevitable asks for the ability to see what changes were made when and by whom. My current preferred strategy for dealing with this (at least for any table smaller than a few GBs) is to dump the entire table contents to a git repository on a schedule.

- I store all my dates in sql as text in iso format so I can easily sort them
  - Strong SQLite vibes... (SQLite doesn't have a date format, it has builtin functions that accept ISO format text or unix timestamps)
- Why is this bad?
  - Sql databases usually come with their own date types that are implemented with integers behind the curtains. They take up less space and are easier to sort than text fields.

- Why not have a history table and use SQL triggers to insert the new data as JSON everytime someone changes something?
  - Indeed. I have on multiple occasions written scripts to automatically generate the triggers and audit tables

- Git annex is pretty flexible, more of a framework for storing large files in git than a basic sync utility. ("Large" meaning larger than you'd want to directly commit to git.) If you're running Git Annex Assistant, it does pretty much work as basic file sync of a directory. But you can also use it with normal git commits, like you would Git LFS. Or as a file repository as chubot suggested. The flexibility makes it a little difficult to get started.

- Isn't the problem attempting to be solved here solved by event sourcing? Which lets you 're-create' your changes and is - ultimately- suppose to allow you effectively log each change in such a way its re-playable backwards and forwards
  - Kind of, but there’s more to it. “Event sourcing” is the pattern being implemented by git’s immutable object database, but there’s also all the hashing and reference management.

- 
- 
- 
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

- ## 

- ## 🧩 for git, there are 4 locations for your code:
- https://twitter.com/sahnlam/status/1769954179886547365
  - Working Directory
  - Staging Area
  - Local Repository
  - Remote Repository (like GitHub)
- Basic commands move code between these locations:
  - git add stages changes
  - git commit saves them locally
  - git push shares them remotely
  - git pull fetches updates from others
- Concepts like git clone, merge, rebase enable collaboration.

- ## 🌵 Explaining Git branching strategies.
- https://twitter.com/ChrisStaud/status/1752341883198853588
- Let's take a look at some common approaches to branching:
  - Feature branching is a popular approach as development tasks are usually revolved around a feature. It involves having a branch for every feature being developed to keep the changes isolated from the main branch.
  - Gitflow has two permanent branches — a production and a pre-production branch, often referred to as the “prod” and “dev” branches. There are additional temporary branches for each feature, scheduled releases, and urgent bug fixes.
  - Gitlab flow combines feature-branching and environment-based branching.
  - GitHub flow takes a simplified process that is similar to feature branching. 
  - With trunk-based development, branches are very short-lived. Changes are merged into the main branch within a day or two. Feature

- ## A rewindable file system demo I cooked up.
- https://twitter.com/JungleSilicon/status/1729012610048360626
- Have you ever managed to get a conflict free data type in front of git, so you can sync to GitHub? 
  - You can do it, but it usually involves diffs - there's also a problem that git uses snapshots where as crdt's/ot are more granular.
  - So let's say we are both collaborating using crdts, if someone then goes and makes a commit outside of that system, we need to then have a bridging layer that converts that snapshot into operations.
- I'm guessing because that git commit would likely be larger than a crdt change, that'd also cause issues?
  - The size isn't really a big issue, it's mostly that there's less information with git than crdts. Git just have *snapshots*, you don't *really* know how A transformed into B.

- ## 🌰 [Ask HN: Apps that are built with Git as the back end? | Hacker News_202210](https://news.ycombinator.com/item?id=33261862)
- The Office 365 backend uses git to store snapshots of documents
  - https://github.com/microsoft/FluidFramework/tree/main/server/gitrest
  - the content-addressable filesystem that it uses is git. It uses git with a javascript implementation of it 

- Using Git for content has some great benefits. Like complete version history, easy reverts (for devs at least), (feature) branch support, Git hooks, ... And of course, you own your content at all times.

- Git is good at creating files and managing versions/branches but not good at search files or their content. I'm not a git expert to fully backup that claim but that's been our experience. You can layer on your own search capabilities if you need it but then you might want to start asking if a full DB is better.

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

- ## 🆚️🤔 [为什么其他办公领域不使用git?](https://www.zhihu.com/question/329750471)
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

# discuss-gitlab-gogs-gitea-platform
- ## 

- ## 

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

- Pijul has a number of stated strengths over Git, and looks like the version history is implemented as a CRDT from my first impression. Some of the statements make me wonder how many conflicts occur in real use. If they are equal to or less than the number it produces, great. If more than what Git produces, that's a barrier to adoption, as merge conflicts are one of the biggest pains when using Git.
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
# disccuss-git-cli
- ## 

- ## 

- ## 

- ## 🔀 大家都用什么方式处理git merge/rebase conflict?
- https://twitter.com/changwei1006/status/1768927296570921435
  - 用IDEA内置的merge revisions功能，可以很方便的三栏查看代码的差别，并且会用红色和蓝色高亮标识出新旧代码和当前代码之间存在【添加/删除】的冲突代码块，然后【行号】旁边的【小箭头】还可以快速把需要保留的代码应用到当前文件
- 这种在 Git 里叫 diff3
  - 除了 diff3 还有很多, 像是 Changes、DiffMerge、ECMerge 啥的
- idea是除了命令行以外最好的git客户端没有之一。在我的workflow里，唯一不能替代命令行的就是git rebase -i ，
  - 但idea也有不可替代的我经常用到的一个功能：idea可以让我快速直观选择具体哪几行作为一次commit，而不用stage整个文件。（git add -p 或-i 太慢了）
- 最喜欢冲突合并时的那个魔法棒
- 比命令行下搞可视化好太多 同样操作
