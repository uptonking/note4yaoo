---
title: lib-utils-git-community-usage
tags: [community, dev-xp, git]
created: 2024-05-27T09:11:46.652Z
modified: 2024-05-27T09:12:06.925Z
---

# lib-utils-git-community-usage

# guide

# git-commands
- [alias from ohmyzsh](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh)

- [Git Operations Simulator to get git commands](https://github-branching-antdx316.vercel.app/)
# disccuss-stars
- ## 

- ## 

- ## 在一个分支下本地有改动，又需要拉远端代码时，以前总是手动 stash 后再拉，比较繁琐
- https://x.com/cosmtrek/status/1831965619706872051
  - 现在只需要 `git pull --autostash` ，好方便
  - 推薦同時上 rebase 和 autoStash
- 求稳，diff出patch，再stash，再pull，最后apply diff
- 我是写一个alias执行: 
  - git pull --rebase origin --autostash branch
- 其实，如果你用fork或者sourcetree之类的客户端，点击pull按钮会全自动做这个操作。

- ## 有 Fork 这样的可视化，什么 squash，普通 merge 之争都是浮云了。
- https://x.com/middlefeng/status/1824595077345448074
- fork是我用过最好的git可视化工具，尤其是他的merge 功能

- ## Pinterest decreased clone times by 99% (40min -> 30 sec) with a one-line change.
- https://x.com/ryanlpeterman/status/1801285133200482346
  - Pinterest's largest monorepo had more than 350k commits and was 20GB in size.
  - Their continuous build pipelines (Jenkins) took 40 minutes to clone that massive repo.
  - What was odd was that they were telling Git to do a shallow clone.
  - Digging into the script that used Git, they realized they left off the `refspec` option. If you leave that off, the default is to tell Git to fetch all refspecs (e.g. "+refs/heads/ *:refs/remotes/origin/* ") In their case, this fetched more than 2500 branches.
  - To fix this, they added one line to their build config which specified that they only cared about master (e.g. "+refs/heads/master:refs/remotes/origin/master")
  - Specifying this decreased cloning times from 40 minutes to 30 seconds.
  - [How a one line change decreased our clone times by 99% | by Pinterest Engineering _202010](https://medium.com/pinterest-engineering/how-a-one-line-change-decreased-our-build-times-by-99-b98453265370)

- they could have just used `git clone --depth 1`; 
  - Not everyone knows about this trick, unfortunately

- ## 🤔 [Ask HN: Can we do better than Git for version control? | Hacker News _202312](https://news.ycombinator.com/item?id=38590080)
- Git is absolutely not suited to the workflow of several industries, including the one I work in: games.
  - Git, even with LFS and partial clone and shallow copies and fsnotify just falls apart at this scale. Add to that the necessity for less-technical people (artists, designers, VFX, audio, etc) to use it, and it is really just a non starter.
  - I absolutely loathe(讨厌；厌恶) Perforce (having used and occasionally admin'd it professionally since 2007), but I begrudgingly(begrudgingly) admit that is is currently the only publicly available VCS that can fulfill all of the requirements of this industry in a practical way. Plastic and the others just aren't there yet.
- Microsoft had a bunch of solutions to handle their massive Windows repo: VFS for Git (GVFS), Scalar, and now it has a bunch of MS specific patches on top of the official git client, but apparently that one is also not required any more as partial clone is now supported on azure as well (which is another such implementation from Microsoft employees that made it to both GitHub and upstream git).

- Git is basically content-addressable storage with a couple of layers on top (heads/tags/trees) which is itself content-addressable storage. If you can offload that storage to a remote, you still have git... and can use git as you've always used git. The tricky part is making it feel like the storage is local and your own, instead of shared.

- That’s why you need a binary repository like Artifactory and not store your large files in Git. But you can still track them in Git with the large files in a binary repository like Artifactory.

- Patch based VCS systems (Darcs, Pijul) are apparently better.

- Git views the codebase as mutable. It's really well set up for changing the historical record to reflect how you wish it had been done.
  - Fossil views the historical record as immutable. Your sequences of mistakes, iteration, failed experiments are all diligently recorded. 

- Git is great for keeping track of logical history, but personally I find that it is missing tools for handling physical history. Reflog is a step in the right direction but it has a limited size and AFAIK it is not possible to share a reflog between clones. Which leaves "cp -r repo repo.backup" as the best option.

- ## 🤔 [Ask HN: Why hasn't Git been adopted outside of software engineering? | Hacker News _202205](https://news.ycombinator.com/item?id=31406550)
- Maybe the better question to ask is "why isn't file reversion control adopted more outside of software engineer?"
  - Git a is distributed version control system that most people shouldn't have to deal with. It has awful tools and doesn't work well with binary files, large files and moved files. Just an example: How do you diff two copies of an excel document with Git?
  - Most people don't have to deal with multiple "master" branches with no single source of truth because that's really what Git is for.
  - I believe a tool like Dropbox or even centralized version control systems like Subversion or Perforce are better positioned to solve this than Git.

- Git isn't the best for office documents. Revision marking (aka, change tracking), document comparisons, and merging are all available in Office suites. Git isn't really used here because there features predate Git, operated on binary files or complex XML documents (neither of which are conducive to diffs).
  - Git isn't good for databases or data lakes. The files are huge and typically aren't modified (CSV) or are binary/compressed (Parquet).

- git (and more generally diff) is not very efficient for detecting and showing moved text (which it displays as deletion+addition)
# disccuss-news
- ## 

- ## 

- ## Git 2.54 is here with features like config-based hooks, new ways to rewrite history, and much more
- https://x.com/birch_js/status/2047339672679137748
- maybe we don’t need husky anymore!

- native git hooks are cool but they don't talk to your AI agents

- I think you still need something because this config can’t live in the repo so you’ll need some sort of bridge to do the setup. It’s cool for other reasons, though!
  - Git only reads ~/.gitconfig. It doesn’t read .gitconfig for each repo. It reads .git/config which cannot be checked in.
  - You can set yourself up for repo-specific config to be loaded, but this is just a convention and requires you to change settings in your global git config. There is no way for a repo to define git hooks that are always and automatically installed when you clone. For good reason! Arbitrary code execution is scary! See npm post-install scripts for an example of how that has caused havoc.

- That config lives under the “.git/config” file inside the repo. The .git folder is not versioned, so you still need some mechanism to ensure everyone has that config + the minimum git version that supports it, so… it seems easier to still use husky, doesn’t it? am I missing something?
# disccuss-usage-github
- ## 

- ## 

- ## 

- ## [Can forks be synced automatically in GitHub? - Stack Overflow](https://stackoverflow.com/questions/23793062/can-forks-be-synced-automatically-in-github)
- You can create a Github App that use Github API to check the upstream repo periodically. Once an update is found, use Github API to create a pull request then call updateRef to update your branch to match master.
  - Or, just install this Github App that does exactly that

- ## TIL you can add `.diff` to the end of a Github pull request URL and you'll get a diff file.
- https://x.com/davidfowl/status/1916541569638834509
  - you can also add `.patch` to get a git patch file
- Currently using this in a power automate flow

- ## [Getting permanent links to files - GitHub Docs](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files)
- When viewing a file on GitHub.com, you can press the "y" key to update the URL to a permalink to the exact version of the file you see.
- [Creating a permanent link to a code snippet - GitHub Docs](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-a-permanent-link-to-a-code-snippet)
  - You can create a permanent link to a specific line or range of lines of code in a specific version of a file or pull request.

# disccuss-git-ui 💄
- ## 

- ## 

- ## 

- ## [Looking for a good alternative to the Git Graph VS Code extension : r/vscode _202603](https://www.reddit.com/r/vscode/comments/1rrcx9k/looking_for_a_good_alternative_to_the_git_graph/)
  - I've been using the Git Graph extension for a long time, and it's been my absolute favorite tool for visualizing commit history and managing branches directly inside VS Code.
  - However, it looks like the repository is no longer being actively maintained
  - Does anyone have good recommendations for a replacement?  

- https://github.com/git-hub-tig/vscode-git-graph
  - Fork of Michael Hutchisons repository with some updates.
  - This fork includes critical fixes for recent VS Code versions and new features not present in the original.

- I use GitLG as a replacement which is no fork but started from scratch (the read me has a comparison to git-graph)
  - https://github.com/phil294/GitLG /MIT/202511/js/vue/inactive

- GitLens feature is cool for line by line commit history. The GitKraken graphs is cool too but not sure if I would pay for it.
  - Use GitLess if you want a nag free version of GitLens from before it got annoying.

- fork.dev tool.
  - Nicer, free, and works on Linux: SourceGit

- I use sourcetree. The git tree with change parts in 1 screen is the best for me.  

- ## VSCode git UI is awesome
- https://x.com/aidenybai/status/1885810358138667140
- Until you realise that lazygit exists
- gitlens extension is pretty good too

- if you think this is good it's because you haven't yet tried 

```sh
git log --online --graph --decorate
```

- ## UGit：腾讯自研Git客户端
- https://x.com/javayhu/status/1831348801032081527
  - [UGit - Making Git easy for everyone](https://ugit.qq.com/en/)
  - 这个是真的好用，我们的代码量很大，用过很多Git GUI工具基本上都卡住了，但是公司自研的这个却没有，非常值得推荐。其他工具都有点缺点，例如GithubDesktop功能太少，SourceTree/Tower卡住了，SublimeMerge显示和操作没卡但是用不习惯。
- 我用的GitButler，分支管理很方便
- 我用过fork，感觉很丝滑，之前直接开Android的Repo下面的一些源码提交记录也是非常多，一点都不卡。
- 我给公司的技术经理推荐过这个…他只说了一句：企鹅的尿性很可能未来收费，鉴于这点…选择开源

- ## [如何评价腾讯的Git可视化工具腾讯UGit? - 知乎](https://www.zhihu.com/question/826636693)
- 对一般 Git 用户毫无意义。但对于游戏的版本管理和非研发人员有一些意义。

- GUI界面做的还不错, 设计风格和Github Desktop不能说很像, 只能说一模一样

- 用了几年，UGit对于美术来说太好了。随便说几个功能。
  - 1锁文件和解锁文件，共用关卡的地编ta应该经常能遇到，出现文件冲突。git本身也可以解锁和取消解锁，但是可视化很差，UGit美术可以直接看到文件是否被锁，以及被谁锁了。
  - 2切分支。从主干拉的分支全部可以直接切，重合的文件不会再复制，只复制不一样的文件，超级快，有冲突的文件还会问你是否储藏或者保留。
  - 3储藏文件。你可以随意保存很多文件很多版本，随时可以恢复，每次存储还可以写标题。
  - 5查看上传人员。git是code引擎编好美术引擎给美术用，美术看不到程序的提交人员，有时候很难受。UGit是程序美术共用，可以看到所有人的提交。

- 
- 

# disccuss-pm-git
- ## 

- ## 

- ## GitChat - 用自然语言去做 Git
- https://x.com/hwwaanng/status/1986674586696798271
  - 要做的足够简单，只满足切分支、合并分支、解决冲突的基础功能。
  - 目标的用户是产品/设计师 。
  - 顺带可以把分支预览之类的工作做了（接个 vercel 
  - 难点： UX 层面让普通用户在不理解 git 的情况下，能够自然的完成一套简单的 git flow
- 这个场景很窄，大部分人只是需要版本管理，不需要引入 git 的抽象概念, 只有那些不懂 git 又要强制使用 git 的产品来有这个需求。
  - 就是你说的，下层是git flow上层是对用户可见的版本管理。这样的 产品/设计 可以在这个东西上继续协同。不需要理解git，不需要了解git。并且合理的git记录，可以交付给合作者。
- 如果设计师需要git，那么Photoshop早就有版本管理的功能了，但是事实是设计师只需要ctrl-z
  - 一年以前的设计师也不需要 vibe demo。只能说，时代变了
- gitchat 这事 codex 做的确实蛮好了。 我最近的一些冲突都是它自己解决的。

- ## The next hypermedia platform should be based on Git. Creating a text file in a Git repo should be all you need to participate. 
- https://x.com/msimoni/status/1884333920080257053
  - In contrast to plain HTTP, Git also solves incremental updates efficiently, so everyone can locally store a complete copy of the sites they follow.

# disccuss-git-submodule/monorepo
- ## 

- ## 

- ## 

- ## 🧩 [Git Monorepo vs Multi-repo vs Submodules vs subtrees : Explained : r/git _202511](https://www.reddit.com/r/git/comments/1orcznk/git_monorepo_vs_multirepo_vs_submodules_vs/)
  - [Monorepo vs Multi-repo vs Git submodule vs Git Subtree: A Complete Guide for Developers ](https://levelup.gitconnected.com/monorepo-vs-multi-repo-vs-git-submodule-vs-git-subtree-a-complete-guide-for-developers-961535aa6d4c?gi=4131dafc18a3&sk=f78b740c4afbf7e0584eac0c2bc2ed2a)

- What's more important than monorepo vs multirepo is how the code is architected.
  - If the dependencies between projects are a mess such that a minor change will trigger a rebuild of hundreds of projects, then both options are going to be a nightmare.
  - Monorepos put more pressure on infrastructure developers. Multirepos put more pressure on product developers.
- The main rule of thumb that has worked for me is, if everything has the same release cycle, such that a git tag versions all products as a whole, then yes, a monorepo makes sense. 
  - If you start having a need to have different sets of tags, then that's probably a hint that you should have separate repositories.
  - It's always easier to merge things together than to split them apart.
- 100% agree. I just built a hybrid with submodules. Each repo is individually compilable. But when you setup the right directory structure, it becomes a mono repo.

- I am going to explore subtrees. In certain CI tooling, submodules are simply not downloaded / recognized. This is even after initializing the submodules. The simple git clone from subtrees would fix these issues.

- Submodules are a GD nightmare. If you are using Python. It makes imports for anything a frick'n nightmare. For Go it is a hard no to. It is an antipattern - use separate repos packages. And the same for AWS CDK and probably Terraform.
# disccuss-lfs/large-file
- ## 

- ## 

- ## 

- ## [Is this a right way to use husky + lint-staged? - Stack Overflow](https://stackoverflow.com/questions/51748246/is-this-a-right-way-to-use-husky-lint-staged)

- ⚠ Some of your tasks use `git add` command. Please remove it from the config since all modifications made by tasks will be automatically added to the git commit index.

```JS
{
  "lint-staged": {
    "src/ **/* .{js,jsx,ts,tsx,mjs,mts,json,css}": [
      "prettier --write",
      "eslint --fix src/",
      "tslint --fix --project .",
      "git add"
    ]
  },
}
```

- ## [ `git lfs clone` does not respect `--mirror` (bare) · Issue · git-lfs/git-lfs _201706](https://github.com/git-lfs/git-lfs/issues/2342)

- Yes, this is an incompatibility between git-lfs and the default directory name that git uses for bare repos. 
  - There is a simple work-around for now: `git lfs clone git@bitbucket.org:foo/bar.git bar.git`.
  - That explicitly states the output directory name, and "git lfs clone" honors that. You can actually put anything at all for the directory name, just so long as it's explicitly stated.
# discuss-gitea
- ## 

- ## 

- ## [[solved] Re-run Gitea first time installation? - Install/Maintain/Configure - Gitea](https://forum.gitea.com/t/solved-re-run-gitea-first-time-installation/599)
- instead of going to the /install URL again, as you are already modifying your `app.ini` you can just change the relevant settings there.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 询问面试官加班情况，但得到的答案往往不太真实。但是代码的提交时间不会骗人，因此就有了这个工具。
- https://x.com/yuki_yang0202/status/1990996580930105478
  - https://github.com/hellodigua/code996
  - 统计 Git 项目的 commit 时间分布，进而推导出项目的编码工作强度。

- 不同时区的话这个就没什么参考价值了

- 加不加班，待一周就知道了

- ## [gpg: Screen or window too small · Issue · kovidgoyal/kitty _202302](https://github.com/kovidgoyal/kitty/issues/6018)

```sh
gpgconf --kill gpg-agent
gpgconf --launch gpg-agent
```

- ## [How to show full-file Git blame in Visual Studio Code - Stack Overflow](https://stackoverflow.com/questions/44161997/how-to-show-full-file-git-blame-in-visual-studio-code)
- If you use the GitLens plugin, you can also use the "File Annotations" icon in the top right of Visual Studio Code

- ## git clone --mirror git@github.com:ueberdosis/tiptap.git
- Git creates a bare-“mirror” repository, which contains all of the refs (branches, tags, notes) and the entire object database, but no working tree—so you won’t see any checked-out files.

- if you’ve already got the mirror locally, you can “clone from your mirror”:

```sh
git clone ~/backups/tiptap.git tiptap-working-copy
```

- ## 我用 Git 的时候有一个很常见的 combo 来合并 main 分支的最新代码：
- https://x.com/tison1096/status/1926191882360455190
- 接 git pull origin main -r 就可以了吧
  - -r: rebase

- ## [How do I remove the passphrase for the SSH key without having to create a new key? - Stack Overflow](https://stackoverflow.com/questions/112396/how-do-i-remove-the-passphrase-for-the-ssh-key-without-having-to-create-a-new-ke)
- ssh-keygen -p [-P old_passphrase] [-N new_passphrase] [-f keyfile]
  - ssh-keygen -p -P oldpassphrase -N "" -f ~/.ssh/id_rsa
- To be explicit: you can just run `ssh-keygen -p` in a terminal. It will then prompt you for a keyfile (defaulted to the correct file for me, ~/.ssh/id_rsa), the old passphrase (enter what you have now) and the new passphrase (enter nothing).

- ## [Case Insensitive Search on Git log comments - Stack Overflow](https://stackoverflow.com/questions/77910421/case-insensitive-search-on-git-log-comments)
  - 'git log' it is always case sensitive. Which make it difficult to find the relevant text. 

- git log typically sends its output to a pager program, you can use that to search.
- Git does not use vim as a pager by default, it uses less.
  - you can use -i or -I (they're subtly different) to make less searches ignore case.
  - You can set the `LESS` environment variable to -i or -I, then less searches are case-insensitive by default everywhere. 
  - Or set `core.pager` to less -i or less -I so only it is only case-insensitive with Git.

- 另一种方式 `git log -i --author=jin`  ; 
  - -i, --regexp-ignore-case: Match the regular expression limiting patterns without regard to letter case.

- ## 🆚 [Gitk vs Git Gui | Atlassian](https://www.atlassian.com/git/tutorials/gitk)
- Gitk can be thought of as a GUI wrapper for git log. 
  - It’s written in tcl/tk which makes it portable across operating systems.
  - Gitk will reflect the current state of the repository. If the repository state is modified through separate command line usage like changing branches Gitk will need to be reloaded.

- Git Gui is another Tcl/Tk based graphical user interface to Git. 
  - Whereas Gitk focuses on navigating and visualizing the history of a repository, Git Gui focuses on refining individual commits, single file annotation and does not show project history. 
  - Git Gui also supplies menu actions to launch Gitk for history exploration.

- [git-gui Documentation](https://git-scm.com/docs/git-gui)
  - git gui focuses on allowing users to make changes to their repository by making new commits, amending existing ones, creating branches, performing local merges, and fetching/pushing to remote repositories.
  - Unlike gitk, git gui focuses on commit generation and single file annotation and does not show project history. 
  - It does however supply menu actions to start a gitk session from within git gui.

- ## [How can I view a git log of just one user's commits? - Stack Overflow](https://stackoverflow.com/questions/4259996/how-can-i-view-a-git-log-of-just-one-users-commits)

```sh
# You don't need to use the whole name. The quotes are optional if you don't need any spaces.
# Add --all if you intend to search all branches and not just the current commit's ancestors in your repo.
git log --author=Jon
git log --author="Jon"
gitk --author=Jon

# You can also easily match on multiple authors as regex is the underlying mechanism for this filter.
git log --author="\(Adam\)\|\(Jon\)"

```

- ## 如果经常在终端上操作 Git 可以安装这款实用的命令行工具：git-who。
- https://x.com/GitHub_Daily/status/1902918146782269478
  - 与 git blame 只能告诉你某行代码的作者不同，它能够解答 “谁写的这段代码？”，可以展示整个组件或子系统的责任人，而非针对单个文件。
  - 执行命令可查看项目主要贡献者、最后编辑时间、修改行数、提交次数等等信息，并且还可进行排序。

- ## 🆚 [How to retrieve a single file from a specific revision in Git? - Stack Overflow](https://stackoverflow.com/questions/610208/how-to-retrieve-a-single-file-from-a-specific-revision-in-git)

```sh
# git show REV:PATH ,  SHA1 hash可以只写几位，实测下面4位能work，github的ui一般是7位
git show 514a:README.md
# 使用HEAD查看旧文件的顺序: HEAD(最新commit的内容，也许不是最新文件内容), HEAD~(与～1相同), HEAD~2
git show HEAD^^^:test/test.py
git show somebranch:from/the/root/myfile.txt
```



```sh
# shows a diff, and not the file contents, 显示的是指定commit的git diff输出，只显示一个
git show a44d7 README.md
# 显示倒数第一个git diff输出
git show -1 filename.txt > to compare against the last revision of file
# 显示倒数两2个commit的git diff输出，显示了2个； git show -3 会显示3个git diff的输出
git show -2 filename.txt > to compare against the 2nd last revision

# replace/overwrite the content of a file in your current branch with the content of the file from a previous commit or a different branch
git checkout 086181 path/to/file.txt
git checkout branchName path/to/file.txt
```

- It's important to remember that when using "git show", always specify a path from the root of the repository, not your current directory position.
  - Although Mike Morearty mentions that, at least with git 1.7.5.4, you can specify a relative path by putting "./" at the beginning of the path
- `git show` essentially dump the content on the stdout (standard output), you could simply redirect that output to any file you want
  - `git checkout` would override your file by another version, as opposed to `git show`, which allows you to save it under a different name
- I would like to note that `^^^` can also be written more generally as `~~~` or, better,  `~3` . Using tildes also has the advantage of not triggering the file name matching of some shells (zsh, for instance)

- `git show FileName` produces a diff-like output, but `git show HEAD:FileName` should give the committed file contents

- ## what is .gitignore is added in .gitignore file
- https://x.com/GithubProjects/status/1887402959136260482
- gitignore ignoring itself like a true recursion pro 
- This doesn’t work. 

- ## [How to fetch all git history after I clone the repo with `--depth 1` ? - Stack Overflow](https://stackoverflow.com/questions/29270058/how-to-fetch-all-git-history-after-i-clone-the-repo-with-depth-1)

```
git fetch --unshallow

git fetch --depth=1000000
```

- ## Problem: You want to push your changes, but skip CI because you're not done yet, so running CI would be wasteful.
- https://x.com/housecor/status/1868376700033413151
  - Solution: Put this in the push commit message: [no ci]

- What we do is that we only run CI if the PR has a "Run CI" label, that is manually added by the dev when they're ready for it
  - Feels backward to me since it risks CI not running

- Why not create Draft PR instead?
  - That works too

- ## [gitignore does not ignore folder - Stack Overflow](https://stackoverflow.com/questions/24410208/gitignore-does-not-ignore-folder)
- Here's the steps I took to ensure my .gitignore file ignored the folder I wanted it to ignore:
  - Commit any changes that you need to fix/change.
  - Run this command: `git rm -r --cached .` (which removes everything from the git index in order to refresh your git repository)
  - Then run this command: `git add .` (to add everything back to the repo)
  - Finally, commit these changes using `git commit -m ".gitignore Fixed"` 

- ## [git - warning: ignoring broken ref refs/remotes/origin/HEAD - Stack Overflow](https://stackoverflow.com/questions/45811971/warning-ignoring-broken-ref-refs-remotes-origin-head)

- Since you may have excluded the branch that origin/HEAD was initially pointed to.

- ## 🆚 [Git - see changes across multiple commits? : r/vscode](https://www.reddit.com/r/vscode/comments/y6oti0/git_see_changes_across_multiple_commits/)
  - Jetbrains IDEs have a feature where you can select multiple commits and you can see the files and changes that were made in the selected commits.
  - Can this be actieved in vscode? Thanks.

- I'd recommend using a proper git gui like Fork. It says it's paid, but you can just keep clicking a button every month to keep using it free forever.

- I use the git graph plugin, it will allow you to do exactly what you are asking
- I tried using GitGraph extension: you can only select 2 commits and it does a diff between commit 1 until commit 2, showing changes in all commits between commit 1 and 2.

- Git in VSCode is messy. I suggest getting comfortable with the CLI as it works everywhere and does anything you ever need. You can use things like delta to make the experience better. If you want to avoid the terminal at all costs and prefer working through a GUI, check git clients like Fork, Sourcetree, TortoiseGit etc.

- ## 📝 [git rebase，看这一篇就够了 - 掘金](https://juejin.cn/post/6969101234338791432)
- 先放上建议
  - git merge：当需要保留详细的合并信息的时候建议使用，特别是需要将分支合并进入master分支时
  - git rebase：当发现自己修改某个功能时，频繁进行了git commit提交时，发现其实过多的提交信息没有必要时使用，分支多，内容多时也可以考虑使用
- 假设现在有基于远程分支“origin/master”，更新至本地最新“master”，创建一个叫“feature/mywork”的分支进行说明
  - master和feature/mywork这两个分支各自"前进"了
  - 你可以用pull命令把master分支上的修改拉下来并且和你的修改合并；结果看起来就像一个新的"合并的提交"(merge commit)
- git rebase会把feature/mywork分支里的每个提交(commit)取消掉，并且把它们临时保存为补丁(patch)，然后把feature/mywork分支更新到最新的master分支，最后把保存的这些补丁应用到feature/mywork分支上
  - 在rebase的过程中，也许会出现冲突(conflict)。在这种情况，Git会停止rebase并会让你去解决冲突；
  - 在解决完冲突后，用git add命令去更新这些内容的索引(index)，然后，你无需执行 git commit，只要执行： `git rebase --continue` , 这样git会继续应用(apply)余下的补丁

- 在任何时候，你可以终止rebase的行动，并且feature/mywork分支会回到rebase开始前的状态。 git rebase --abort
  - 在命令行使用git rebase存在多个commit、多个冲突时需要我们多次解决同一个地方的冲突，然后执行git rebase --continue，反复，直到冲突解决为止，稍显麻烦，可以使用IDE辅助进行

- 有过git rebase经验的同学都知道，多人协作并行开发时刚解决完一堆冲突后，松了一口气，push时又提示拒绝，什么情况？？？然后一查，用-f或者--force参数强制推送
  - 推荐 --force-with-lease 参数，让我们可以更安全地进行强制推送

- ## [git rebase 用法详解与工作原理 | Shall We Code?](https://waynerv.com/posts/git-rebase-intro/)

- git rebase 命令的文档描述是 Reapply commits on top of another base tip
  - rebase 的执行过程是首先找到这两个分支（即当前分支 Feature、 rebase 操作的目标基底分支 Master） 的最近共同祖先提交 A，然后对比当前分支相对于该祖先提交的历次提交（D 和 E），提取相应的修改并存为临时文件，然后将当前分支指向目标基底 Master 所指向的提交 C, 最后以此作为新的基端将之前另存为临时文件的修改依序应用。

- 另使用 rebase 的常见场景是在推送到远程进行合并之前执行 rebase，一般这样做的目的是为了确保提交历史的整洁。
  - 我们首先在自己的功能分支里进行开发，当开发完成时需要先将当前功能分支 rebase 到最新的主分支上，提前解决可能出现的冲突，然后再向远程提交修改

- git pull 时也可以通过 rebase 来进行合并，这是因为 git pull 实际上等于 git fetch + git merge ，我们可以在第二步直接用 git rebase 替换 git merge来合并 fetch 取得的变更，作用同样是避免额外的 merge 提交以保持线性的提交历史。

- 如果涉及到已经推送过的提交，需要强制推送才能将本地 rebase 后的提交推送到远程。因此绝对不要在一个公共分支（也就是说还有其他人基于这个分支进行开发）执行 rebase，否则其他人之后执行 git pull 会合并出一条令人困惑的本地提交历史，进一步推送回远程分支后又会将远程的提交历史打乱（详见Rebase and the golden rule explained），较严重的情况下可能会对你的人身安全带来风险。

- [5.1 代码合并：Merge、Rebase 的选择 · geeeeeeeeek/git-recipes Wiki](https://github.com/geeeeeeeeek/git-recipes/wiki/5.1-%E4%BB%A3%E7%A0%81%E5%90%88%E5%B9%B6%EF%BC%9AMerge%E3%80%81Rebase-%E7%9A%84%E9%80%89%E6%8B%A9)

- ## 🤔 [When should I use git pull --rebase? - Stack Overflow](https://stackoverflow.com/questions/2472254/when-should-i-use-git-pull-rebase)
- pull = fetch + merge
  - pull --rebase = fetch + rebase
- I think you should use git pull --rebase when collaborating with others on the same branch. 

- [Difference between git pull and git pull --rebase - Stack Overflow](https://stackoverflow.com/questions/18930527/difference-between-git-pull-and-git-pull-rebase)
  - git pull = git fetch + git merge   against tracking upstream branch
  - git pull --rebase = git fetch + git rebase   against tracking upstream branch
  - 注意默认的base分支

- ## [Duplicate commits after rebase have been merged into the develop branch - Stack Overflow](https://stackoverflow.com/questions/40551486/duplicate-commits-after-rebase-have-been-merged-into-the-develop-branch)
- "Copy commits" is just what git rebase does. It copies some commits, then shuffles the branch pointers around so as to "forget" or "abandon" the original commits. 
- You will encounter this problem whenever you copy commits that you or someone else made, and both you and the "someone else" (perhaps the "other you") are also still using the originals.
  - Hence the standard advice is to rebase only private (unpublished) commits, since you know who is using them—it's just you of course—and you can check with yourself and make sure you're not using them

- ## interactive rebase
- https://x.com/b0rk/status/1801944634936926362
  - (this is #bonuscomic #1 for How Git Works http://wizardzines.com/zines/git, covering some topics that didn't make it into the zine!)

- ## [git pull on a different branch - Stack Overflow](https://stackoverflow.com/questions/34344034/git-pull-on-a-different-branch)
- If I'm working on a branch and then realize I need to merge another branch into mine here is my current workflow

```sh
git stash
git checkout master
git pull
git checkout my-branch
git merge master
git stash pop
```



```sh
# you want to pull in changes from branch1 to branch2
git checkout branch2
git pull origin branch1
# git rebase master

# git fetch <remote> <src>:<dst>
git fetch origin master:master
git merge master
```

- [Pull another Git branch without switching - Super User](https://superuser.com/questions/163033/pull-another-git-branch-without-switching)

- ## [Difference between stash vs stage files in GIT - Stack Overflow](https://stackoverflow.com/questions/31596869/difference-between-stash-vs-stage-files-in-git)
- Stash will move your modified files into a stack. So, later in the same or in another branch, you will be able to bring them back and see those modifications in your project.
  - you stash your files with $git stash
- Stage is the step before to make a commit, you add modified files to "Staged files" to create your next commit.
  - you add files (stage) with $git add

- You can not checkout to another branch before commit or stash current changes.
  - Therefore, if you want to not commit your changes, and also want to checkout to another branch, solution is to stash current changes, checkout to another branch. And after returning to first branch, you can apply stashed changes.

- ## 🆚️ [What's the difference between `'git switch' and 'git checkout' <branch>` ? - Stack Overflow](https://stackoverflow.com/questions/57265785/whats-the-difference-between-git-switch-and-git-checkout-branch)
- The `switch` command indeed does the same thing as `checkout` , but only for those usages that switch branches. 
  - It cannot restore working tree files — that is done using `restore` , the other command split off from checkout.
  - switch and restore commands were introduced to split the checkout command into two separate pieces

- switch can be safer than checkout if your intention is "just change the branch."
  - With checkout, you can accidentally "restore" your work-in-progress files to their original state (and they are gone) like in this case. 
  - A single mistake like typing `checkout` instead of `add` can lead to a loss of changes (and I did this mistake by frequently changing branches and creating commits).

- ## [git - Get back the changes after accidental checkout? - Stack Overflow](https://stackoverflow.com/questions/2961240/get-back-the-changes-after-accidental-checkout)
- I end up just using `git switch` instead of `git checkout` for branch switching. Yes, you need to change your habit, but that's the ultimate solution from my point of view.
  - the ambiguity of git checkout is the root cause here. But creating checkpoints might leave your stash with a huge mess and eventually not usable if not well maintained.

- Unless you have ever used `git add` or `git stash` with those files previously, then unfortunately no. If you have added or stashed them, then you should be able to find their hashes through `git reflog`.

- ## 🚨 [Is it possible to undo `git checkout -- .` to retrieve unstagged changes - Stack Overflow](https://stackoverflow.com/questions/45726367/is-it-possible-to-undo-git-checkout-to-retrieve-unstagged-changes)
- `git checkout -- .` is one of the few destructive commands (along with `git reset --hard` and `git clean -f` ), which can remove content from your disk without storing it in git beforehand.
  - the content of your files has to somehow land in git if you want to retrieve your files.
  - So git alone will not help you there ; you would have to turn to your IDE's history, or file recovery utilities.

- [Is their a way to revert `git checkout`? - Stack Overflow](https://stackoverflow.com/questions/46666880/is-their-a-way-to-revert-git-checkout)
  - You cannot undo such operation. The reflog is a great tool, but records only what happens to refs (branch, tag, HEAD, ...), and here you did not modify any ref.

- ## 🚨 [Developer accidentally deletes 3 months of work with Visual Studio Code | Hacker News _201708](https://news.ycombinator.com/item?id=15044264)
- The problem obviously isn't with Visual Studio Code, but with Git (or whatever version control software he tried out). 
  - It seems that he didn't know anything about using git and accidentally checked out a bare repo instead of adding his files to stage. 
  - Learning about version control, especially Git, is the most important thing a software developer can learn as early as possible in his career.

- ## [Git checkout -- recover lost files - Stack Overflow](https://stackoverflow.com/questions/30643119/git-checkout-recover-lost-files)
  - `git checkout -- smdr` Then files changes disappeared.

- git reflog/reset/revert
  - No, you can't. All these commands deal with committed history

- ## [How does git checkout delete files? : r/git](https://www.reddit.com/r/git/comments/ohebe4/how_does_git_checkout_delete_files/)
- Git checkout will overwrite files if you specify `pathspec` .
  - this is why Git now has `git switch` and `git restore` ... `git checkout` does too many different things

- ## 💡 [git checkout automatically merges local modifications - Stack Overflow](https://stackoverflow.com/questions/12822727/git-checkout-automatically-merges-local-modifications)
  - After `checkout` to branch `test` all local modifications from `master` get merged.

- git tries hard to not lose possibly valuable data.
  - when you do a `git checkout`, it attempts to preserve newly made but not committed yet modifications, so it checks out the commit you are requesting, and adds your uncommitted changes. 
  - If you really want to discard the uncommitted changes, use `git checkout -f`, or `git checkout` followed by `git reset --hard HEAD`. 

- `git checkout` replaces locally changed files.
  - `git merge` merges local & incoming changes, alerting to any conflicts.

- ## [Does git checkout file can raise a conflict - Stack Overflow](https://stackoverflow.com/questions/72718156/does-git-checkout-file-can-raise-a-conflict)
- If you only remember one or two things here, remember that `git merge` has three inputs, not two, and that it runs two `git diff` commands. 
  - Well, that, and that commits hold snapshots and metadata (snapshots, plus stuff like the log message and commit author), and that branch names help Git find commits for you: Git needs the big ugly hash IDs, but humans are bad at those, so Git lets us use branch names, and the branch names find the hash IDs.
- In the snapshots saved with commits, Git keeps each files' content in a de-duplicated form, so that identical contents are shared across separate commits, and even within a single commit. (The files' names are stored separately from their content.) 
  - This de-duplication not only saves tremendous amounts of space, since most commits mostly duplicate most of the files from the previous commit, it also makes identifying unchanged files very easy, speeding up the process of turning a commit into a diff.

- ## git rebase 是干什么用的，可以在master 分支使用嘛？squash merge 又是做什么的，有什么缺点？
- https://twitter.com/nextify2024/status/1783071318013059135
- 我通常的做法非常简单，如果本地branch还没有push到remote，用git rebase把自己的branch移至main前，否则就git merge
- rebase在本地多个commits合并成一个commit 这样提交到合作分支上，就是一次。很容易维护个人的提交。撤销，cherry pick都很方便。

- 只用rebase不用merge，本地开自己的开发分支，这条分支永远不会push。提交代码前切到远程分支，pull，然后cherry pick本地开发分支，有冲突这个时候要自己解决，然后无痛push。再switch回自己本地开发分支，rebase一下开发分支。

- rebase 可以保持主分支干净，并且保留了在其他分支最后一个提交的信息
  - squash 可以保持主分支干净，但是最后一个提交是命令执行人，而不是其他分支的真实提交人
  - 我用rebase，一定要先合并主分支，推送的时候一定加上 --force-with-lease

- merge commit也有好处。同样是解决冲突，merge就一次。rebase 恶心的地方在于，根据新分支上提交的commit数量，你有可能要多次解决冲突，没记错的话rebase会给每个commit给rebase一下。

- 
- 

- ## git log searcher, as a webapp. Took me 1 hr to assemble with clj-git + clojure's datafy/nav + hyperfiddle datagrid + @ElectricClojure .
- https://twitter.com/dustingetz/status/1773035945379484041

- ## 🔀 大家都用什么方式处理git merge/rebase conflict?
- https://twitter.com/changwei1006/status/1768927296570921435
  - 用IDEA内置的merge revisions功能，可以很方便的三栏查看代码的差别，并且会用红色和蓝色高亮标识出新旧代码和当前代码之间存在【添加/删除】的冲突代码块，然后【行号】旁边的【小箭头】还可以快速把需要保留的代码应用到当前文件
- 这种在 Git 里叫 diff3
  - 除了 diff3 还有很多, 像是 Changes、DiffMerge、ECMerge 啥的
- idea是除了命令行以外最好的git客户端没有之一。在我的workflow里，唯一不能替代命令行的就是git rebase -i ，
  - 但idea也有不可替代的我经常用到的一个功能：idea可以让我快速直观选择具体哪几行作为一次commit，而不用stage整个文件。（git add -p 或-i 太慢了）
- 最喜欢冲突合并时的那个魔法棒
- 比命令行下搞可视化好太多 同样操作
