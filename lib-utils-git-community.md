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

- ## 🔁 i have a `git clone` a repo named repo1 on my macbook, and i use cmd+c/v to make a hard copy of  repo1 to repo2. 
  - i have made many `git commit` to repo1, how can i migrate all changes from repo1 to repo2 using git commands locally. give me some suggestions and explain it
- Since you used cmd+c/v to copy the repository, repo2 is technically a valid Git repository that shares the same history as repo1 up until the moment you copied it. Because they are both on your local disk, you can simply tell Git to treat repo1 as a "server" for repo2

```sh

git remote add local_source ../repo1

git pull local_source main

```

- [Migrate Changes Between Repos](https://chatgpt.com/c/69622882-66c8-8332-9c96-4b14e2e2eede)

- the cleanest approaches are either 
  - (A) create a single squash commit directly into repo2 by cherry-picking the range from repo1 (no changes to repo1), 
  - or (B) create a squashed branch in repo1 then fetch/merge it into repo2.
  - plus a patch-based option (C) you can use if you prefer a portable file.

```sh
# squash - create a single squashed commit inside repo2 (no rewriting repo1)
cd /path/to/repo2
git remote add repo1 /path/to/repo1   # run once
git fetch repo1

git log --oneline repo2/main..repo1/main    # commits present in repo1 not in repo2

# Cherry-pick them into the index without committing, then make one commit
git checkout main 
# takes the last 4 commits on repo1/main and applies them to the index
# Using --no-commit accumulates all changes in the index
git cherry-pick --no-commit repo1/main~4..repo1/main

# If you want to preserve original authorship information, you’ll need to add Co-authored-by: lines manually in the commit message
```

```sh
# squash - Alternative: create a squashed branch in repo1, fetch it into repo2
cd /path/to/repo1
git checkout -b squashed-for-repo2 main
# Method 1: interactive rebase to combine N commits
git rebase -i HEAD~N   # mark the last N commits as `s` (squash) or `f` (fixup), then save

# OR Method 2: create a single commit from last N commits
git reset --soft HEAD~N
git commit -m "Squashed: short summary of N commits"

cd /path/to/repo2
git remote add repo1 /path/to/repo1   # if not already added
git fetch repo1

# either merge (creates a merge commit)
git merge repo1/squashed-for-repo2

# or cherry-pick that single squashed commit SHA from repo1:
git cherry-pick <sha-of-squashed-commit>
```

```sh

# Patch file / bundle approach (portable)
# Create a single squashed commit in repo1, export it as a patch
cd /path/to/repo1
# create squashed commit on branch squashed-for-repo2 (see B)
git format-patch -1 HEAD -o /tmp/patches   # creates a single patch file for the squashed commit

cd /path/to/repo2
git am /tmp/patches/*.patch
# or if you want to inspect before applying: git apply --check <patch>

# ✨ Or use git bundle to transfer full refs:
cd /path/to/repo1
git bundle create ../repo1.bundle repo1/main
# copy repo1.bundle to repo2 machine (local here)
cd /path/to/repo2
git fetch ../repo1.bundle refs/heads/*:refs/remotes/repo1/*
git merge repo1/main   # or cherry-pick, whatever you prefer

```

- `git format-patch` supports binaries automatically (Git ≥2.9).

```sh
# In repo1, check what commits exist on feat-editor
cd /path/to/repo1
git log --oneline --decorate

git checkout -b feat-editor-squashed
BASE=$(git merge-base feat-editor main)   # adjust if base branch ≠ main
git reset --soft $BASE
# git reset --soft HEAD~N
git commit -m "feat(editor): squashed changes"
# get 0001-feat-editor-squashed-changes.patch
git format-patch -1 HEAD -o /tmp/repo1-editor-patch

# git format-patch -o /tmp/patches $(git log --oneline repo2/main..HEAD | wc -l)

cd /path/to/repo2
# Dry run
git apply --check /tmp/repo1-editor-patch/*.patch
# If this passes, apply it properly with commit metadata:
git am /tmp/repo1-editor-patch/*.patch

```

- `git am` consumes patch files as commits (author/date/message preserved) and commits them for you, while `git apply` just applies the diff to your working tree/index and does not create commits or preserve commit metadata. 
- Use `git am` when you want to import patches as authored commits (the usual choice for git format-patch output). 
  - It takes the code changes AND the metadata (Author, Date, Commit Message) and creates a commit in repo2 for every `.patch` file found.
- Use `git apply` when you want to inspect or tweak the changes before committing.
  - Git treats the patches strictly as data. It modifies the files in your working directory, but it DOES NOT create any commits.

- 
- 
- 
- 
- 

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

# discuss-git-versioning/vcs
- ## 

- ## [Working with stacked branches in Git is easier with –update-refs (2022) | Hacker News _202407](https://news.ycombinator.com/item?id=40963427)
- I like to work with Gerrit, which approaches the core problem in a different way
  - "Stacked branches" seem to be a terminology which derives from Github/etc's approach to Pull Requests, where one PR maps to one atomic change. The PR can either be integrated in the repo as a merge, in which case you maintain the history of the PR and all its changes through its reviews, or as a squash-merge, in which case you flatten the PR's review history into one commit.
  - Gerrit took a different approach, and requires you to add metadata to each commit's message, the Change-Id. This way Gerrit can track your commit through its review evolution (since its SHA will change with each iteration). This also allows Gerrit to trivially track a series of related changes through their overall evolution
- In any case, both solutions demonstrate that Git lacks a way to track the evolution of specific commits throughout their review history (a 2D branch in a way), so review tools like Github/etc and Gerrit had to create their own solution on top of it.

- ## [Show HN: I created a plugin for Figma to track changes in the design | Hacker News](https://news.ycombinator.com/item?id=42098378)

- ## [Git scraping: track changes over time by scraping to a Git repository (2020) | Hacker News _202308](https://news.ycombinator.com/item?id=37082289)
- The core idea I believe is tracking incremental changes and keeping past history of items. Git is good for text, though for large amounts of binary data I would recommend filesystem snapshots like with btrfs.

- some covid datasets were published as git repositories. the cool part was that it added a publish date dimension for historical data so that one could understand how long it took for historical counts to reach a steady state.

- Git scraping also lets you easily track changes made to textual content, which I don't think would fit neatly in a time series database.

- ## [Extremely Linear Git History | Hacker News _202211](https://news.ycombinator.com/item?id=33704297)
- Github-style rebase-only PRs have revealed the best compromise between 'preserve history' and 'linear history' strategies

- Mercurial always has had sequential revision numbers in addition to hashes for every commit. They aren't perfect, of course. All they indicate is in which order the current clone of the repo saw the commits. So two clones could pull the commits in different order and each clone could have different revision numbers for the same commits.

- The problem is that rebasing commits has the potential of screwing up the integrity of your commit history.

- Sane revision numbers are among the many reasons I prefer SVN to GIT.
  - You could automatically tag each uploaded commit with a number drawn from a sequence - using a git post-update hook. The only problem is that this centralizes the process. It's not possible to have fully "blessed" commits without pushing them first. And that's how SVN works, too.

- Gitlab supports an option called "Fast-forward merge"

- A neat trick with this tool is to generate a commit message that corresponds to a given issue number. It could almost be useful.

- Another approach could be to use prefixes.

- ## [Git Is Not Revision Control (2017) | Hacker News _201807](https://news.ycombinator.com/item?id=17475392)
- I opened the link expecting to see an introduction to a patch-based system like Darcs or Pijul.

- For me, rewriting history is a feature of Git, and not a bug. I used to use Mercurial, which prioritized immutability of history

- ## [Git evolve: tracking changes to changes | Hacker News _202211](https://news.ycombinator.com/item?id=33567930)
- Git makes the commit history permanent and there are a lot of issues if you keep changing the commit using commit amend or rebase. Git kind of fights with you if you try to edit commits after the commits have been made and pushed to remote
  - One option is to “evolve” the commits without git. Create local branch but do not push them, convert the branch to a patch set, a series of files

- ## [Version Control Beyond Git | Hacker News _202405](https://news.ycombinator.com/item?id=40424452)
- The real issue is though, that each time someone writes a new VCS they seem to want to make it centralised again, often with silly ideas like auto-uploading changes. I do dislike the git stash and the "mess" of untracked files in git status, but I'm not sure what the true answer is.

- The feature I think I would most like to see is support for patches as a more first-class object. For example reverts and cherry picks have no real metadata. This leads to conflicts when merging branches that have cherry picks (although they often auto-resolve if they are exactly the same diff) and makes asking "Does $branch contain $patch" basically impossible to answer.
  - https://pijul.org/ greatly improves this by making patches a first class object (and commits are basically sets of patches). I think it has some great ideas to improve the really gnarly parts of Git low-level behaviour. (Not just surface-level UI issues)
# discuss-git-diff
- ## 

- ## 

- ## 💡 [Show HN: Locust – “Git diff” over abstract syntax trees | Hacker News _202011](https://news.ycombinator.com/item?id=24999775)
- I can't wait until the future when we have version control at the AST level instead of using text files.

# discuss-collab/crdt
- ## 

- ## 

- ## 

- ## Is the git data model a CRDT? If not, would a CRDT make for a "better git"?
- https://x.com/francesc/status/794647418222448640
- git objects are immutable and append-only so I believe so.  The main thing that isn't are repo-specific git refs
  - the commit graph itself is conflict free; it's only if you choose to try to merge the content of the tree you get conflicts
  - but if you don't (like with tracking refs or `git merge -s ours` ), the storage, replication, etc are all conflict free.

# discuss-internals-git
- ## 

- ## 

- ## 🕸️ Did you know Git implements its own network protocol?
- https://x.com/NeelShetty6/status/1985781254177091745
  - it doesn't utilize HTTP, it has its own binary wire format built on pkt-line communication over raw TCP
  - you can check it by setting the `GIT_TRACE_PACKET=1` environment variable, here you can see git negotiate with the remote in real time.
  - A pkt-line is a variable length binary string.  The first four bytes of the line, the pkt-len, indicates the total length of the line, in hexadecimal.  The pkt-len includes the 4 bytes used to contain the length’s hexadecimal representation.
  - Git sends a series of want and have lines to describe which objects it needs, and the server responds with compressed packfiles containing only the missing data. The result is a minimal, binary-efficient data stream designed for low latency and huge repositories.
  - 🆚 Compared to HTTPS, this native protocol is faster because it avoids the overhead of HTTP headers, TLS handshakes, and stateless request cycles. It’s a persistent, full-duplex channel optimized for Git’s data model
  - Git’s own protocol exists because sometimes you need a transport designed around your object graph

- Git also supports another non-HTTP protocol: SSH
  - Yes, it uses pkt line format even with an ssh connection. Ssh is just for establishing the connection, auth n stuff

- `GIT_TRACE_PACKET=1` also works with ssh remotes, so I guess it's the same protocol either it's raw TCP or tunneled through ssh
  - Yes, http is different

- Does it avoid TLS completely here ? Would that not be sec concern though i suppose the protocol could handle that on its own maybe
  - Yes, they address this and recommend to use it alongside ssh or making it read only
# discuss-parallel/worktree 🔀
- ## 

- ## 

- ## 🤼 I talked with @steipete yesterday and we both realized that we gave up on worktrees and just use multiple checkouts. 
- https://x.com/mitsuhiko/status/2011773404207337549
  - Turns out, we're simple people.
  - They are just stable checkouts with stable identities, stable node_modules, fixed ports and databases etc.
  - (And yes, I had a vibecoded worktree manager. Ended up just not using it)

- i think `--shared` shares the .git folder

- what are downsides to multiple checkouts
  - From my experience, with git clone --shared/--reference very little, I guess the main concern would be disk space. I just like it. YMMV
- Are stashes and branches shared?
  - No but if you do a reference clone then you can access them by sha
- Slower, can't share the stash, can't use branches without pushing and looking, rebasing is more work, in short I completely miss why people don't want to use it.
- When you wanna merge, pull master, and keep iterating in the same agent session you can't.
- The only benefit I see is, that you can easily view all local branches in one git client without push/pull. And you can easily merge them locally. 
  - Worktrees only share the .git folder, which is usually rather small.
- Agent sessions are also tied to the directory (at least in CC) so you can't resume a session when you close a worktree (I don't think).

- on macOS APFS you can duplicate the folder and rely on copy on write to save space, only files that would be updated are actually written to disk

- super interesting - i've really taken to worktrees (with a really lightweight manager). key thing i needed was a .scratchpad file in the root so i could tell them apart for context switching!
  - I find the UX around switching a work tree into the main folder to be pretty bad, and managing my node modules and other local DX things is also annoying. Also my diff viewer does not work well with worktrees, let alone me remembering which work trees are alive or not.
  - I'm sure there are ways, but now I have multiple checkouts named after "main", "papercuts", "refactor" and I only keep one type of activity going on simultaniously.

- I think switching a branch into the main folder is one of the best reasons to not use worktrees. without a 1:1 branch:worktree mapping, you lose many of the benefits; it's difficult to know where things are...

- I really tried getting used to worktrees as well, even tried a few different utils and I just couldn’t do it. Multiple directories and life is good now

- that’s what multiple users working on the same project would do

- today and yesterday had me feeling like this, worktrees confuse the agent too much

- two clone repos is enough for my brain

- have actually been using work trees lately and it's great, easier to be working on different things concurrently. It's not great if you have .env files and things like that though. Or if your package/build manager  is just not really worktree friendly

- ## 过往手敲代码的物理特性，Git 压根就没想过有一天我们可以在一台机器上开启任意数量的窗口并行开发，Worktree 这种为边缘场景设计的功能一跃成为开发标配，从无人问津到聚光灯下，它显然没适应好：
- https://x.com/victor_wu_eth/status/2010605107176710630
  - • 腐败和调试问题：Worktree 容易导致 Git 仓库、包依赖或构建过程腐败，调试这些问题往往抵消了并行开发的效率提升。例如，在并行处理时，环境不稳定会引发频繁的修复需求。
  - • 未跟踪文件不复制：Worktree 不会自动拉取未跟踪的文件（如 .env 或 node_modules），这会中断工作流程，需要手动处理，增加了认知负担和时间成本。如果不并行实现多个功能，这种痛点尤其不值得。
  - • UX 和管理复杂：Worktree 被视为低级 Hack，需要手动管理多个命名空间和目录，与 Git 的核心模型冲突。整体用户体验糟糕，容易出错，尤其在多会话时 AI Agent 会混淆任务，导致意外重置或切换。
  - • 隔离不足：对于需要端口监听或完整隔离的场景，Worktree 不够可靠。有些开发者建议用 Docker 容器替代，以避免端口冲突或环境污染。
  - • 合并和 AI 处理问题：AI Agent 有时无法正确在新的 Worktree 上启动工作，或处理诡异的合并冲突，导致整体体验糟糕。特别是在工具集成时（如 Windsurf），可能会默认回根目录，无法生成 Commit。
  - Vibe Coding 到现在，我对 Worktree 的评价就是：还能咋地，你只能用它了。

- 我现在是每个任务临时 local clone 一个完整的仓库，然后用完了删掉。
  - 用linux的话可以试试https://github.com/zhengbuqian/boq，容器完全复刻本来的开发环境，overlay模式是copy on write，继承所有依赖，修改不影响host，也可以快速复制多个。目前用下来唯一的问题是host修改了文件会导致在容器内也可见，我是尽量所有工作都在boq内完成

- 编译 cpu100% 的场景怎么破

- git 不会改，只会出现新git

- ## 我很好奇你们纯 vibe 不跑项目吗 如果要跑的这么解决每个 worktree 都要安装依赖的问题 用软连 or
- https://x.com/yetone/status/2006325355381137659
- 可以设置启动脚本，直接一键run

- pnpm 好像可以设置全局缓存，新的worktree装起来也很快

- 如果是 Node.js 项目，用 pnpm 就没那么大压力了。Python 项目，可以让不同 worktrees 共享同一个虚拟环境。 需要重复触发安装的问题可以交给 git hooks。

- 我现在搞了一个 skill 每次开 worktree 就自动配置环境

- 我现在 worktree 的最大问题是，两个 ts-server 直接让电脑卡住x

- 以试试，多个 AI agent 并发跑确实可以提高效率，那个 conductor 的搞法我还是可以接受的，降低了蛮多 worktree 的成本

- 要起多个 electron 进程也是很难以接受的
  - 测试的时候先关掉第一个进程再开第二个不行吗

- 这也是我不用 worktree 的原因，每次安装依赖花时间，主要是磁盘顶不住了。

- 这种模式我一直比较好奇。如果是一些玩具的项目，那就纯粹当时浪费token玩玩好了。如果是在真实的项目，人的注意力也完全不够啊，尽管AI可以生成部分代码，但还是需要人的注意力的，这种开N个的打断的成本会很大。
# discuss-git-ai 👾
- ## 

- ## 

- ## 

- ## Who's building an IDE for reviewing code instead of writing code?
- https://x.com/schickling/status/2015870972184662197
  - Don't only show me diffs. Show me before/after UIs, terminal output, benchmarks, historic trends, playgrounds, demos, test results etc.

- ci already solved this

- We're experimenting with many versions of this internally at @cursor_ai ! With an agent-first development flow, Cursor today is probably the most fleshed out IDE for reviewing code. But lots more that we are excited to do here!

- https://github.com/intent-solutions-io/iam-git-with-intent /ts
  - CLI tool that automates PR workflows. Resolves merge conflicts, creates PRs from issues, reviews code, runs in full autopilot with approval gating.

- https://github.com/peterjthomson/ledger /MIT/ts
  - modernised git interface for improved agent and human collaboration, review and control
  - A modernised git interface for macOS — view pull requests, worktrees, branches and stashes at a glance
  - 多列视图
# discuss-git-protocol/spec
- ## 

- ## 

- ## 

- ## 

- ## ⏳ the author of git ai put together a spec for annotating commits with information about what code is ai generated
- https://x.com/thdxr/status/2014689039958364209
  - need to review deeper but opencode will probably implement this
  - we can't have this kind of functionality only exist in proprietary products like cursor blame

- I find it annoying in Cursor how it treats AI edits with special diff UI elements for "Keep / Undo". I like to look at AI output and tweak edits by hand sometimes. I've found myself just hitting Cursor's "Keep All" button immediately and then using traditional git diff viewer

- this would be huge for debugging. half the time i'm staring at AI-generated code trying to reverse-engineer what prompt led to this decision. knowing "claude wrote this at iteration 3 with X context" would save so much time

- so basically we're adding metadata to commits so future devs can blame the ai instead of each other cool
# discuss
- ## 

- ## 

- ## 

- ## [Git Things | Hacker News _202401](https://news.ycombinator.com/item?id=38830194)
- 
- 
- 

- ## [Git 远程代码执行漏洞（CVE-2024-32002）复现 - starnight\_cyber - 博客园 _202405](https://www.cnblogs.com/Hi-blog/p/18224773/git_rce_CVE-2024-32002)
- [【已复现】Git存在远程代码执行漏洞（CVE-2024-32002）](https://mp.weixin.qq.com/s/BRr5PCTgYkfPkvHwDckVMQ)
- 原理是 利用 git submodule --recursive 将恶意代码注入到子项目的.git目录的git-hooks

- ## Git is and has always been local first, distributed model. 
- https://twitter.com/oleg008/status/1778716391488598085
  - Isn't it a bit weird that we ended up relying on centralized services even though there is no need at all? 
  - All the collaboration data could be equally in git just like the code, all synced and distributed.
- There is certainly a need for one primary remote repository. You would have crazy inconsistencies, availability-problems and merge-problems otherwise.

- That’s what I like about fossil-scm It has the other supporting functions that the centralized services give you. 
- I think Fossil SCM does this for issues, wiki, forum etc?

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
