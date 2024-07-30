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
# disccuss-stars
- ## 

- ## 

- ## 

- ## 

- ## Pinterest decreased clone times by 99% (40min -> 30 sec) with a one-line change.
- https://x.com/ryanlpeterman/status/1801285133200482346
  - Pinterest's largest monorepo had more than 350k commits and was 20GB in size.
  - Their continuous build pipelines (Jenkins) took 40 minutes to clone that massive repo.
  - What was odd was that they were telling Git to do a shallow clone.
  - Digging into the script that used Git, they realized they left off the `refspec` option. If you leave that off, the default is to tell Git to fetch all refspecs (e.g. "+refs/heads/*:refs/remotes/origin/*") In their case, this fetched more than 2500 branches.
  - To fix this, they added one line to their build config which specified that they only cared about master (e.g. "+refs/heads/master:refs/remotes/origin/master")
  - Specifying this decreased cloning times from 40 minutes to 30 seconds.
  - [How a one line change decreased our clone times by 99% | by Pinterest Engineering _202010](https://medium.com/pinterest-engineering/how-a-one-line-change-decreased-our-build-times-by-99-b98453265370)

- they could have just used `git clone --depth 1`; 
  - Not everyone knows about this trick, unfortunately
# disccuss-usage-github
- ## 

- ## 

- ## [Getting permanent links to files - GitHub Docs](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files)
- When viewing a file on GitHub.com, you can press the "y" key to update the URL to a permalink to the exact version of the file you see.
- [Creating a permanent link to a code snippet - GitHub Docs](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-a-permanent-link-to-a-code-snippet)
  - You can create a permanent link to a specific line or range of lines of code in a specific version of a file or pull request.

# disccuss-git-not-yet 🐛
- ## 

- ## [Git Status Takes a Long Time to Complete - Stack Overflow](https://stackoverflow.com/questions/1183769/git-status-takes-a-long-time-to-complete)
- For me, the slowness was due to having a lot of untracked files (temporary and output files from scripts.) Running `git status -uno`, which excludes the untracked files, ran much faster, and meets my requirements

- ## [Ways to improve git status performance - Stack Overflow](https://stackoverflow.com/questions/4994772/ways-to-improve-git-status-performance)
- To be more precise, git depends on the efficiency of the lstat(2) system call, so tweaking your client’s “attribute cache timeout” might do the trick.
  - The manual for git-update-index — essentially a manual mode for git-status — describes what you can do to alleviate this, by using the --assume-unchanged flag to suppress its normal behavior and manually update the paths that you have changed. You might even program your editor to unset this flag every time you save a file.
- 👣 The alternative, as you suggest, is to reduce the size of your checkout (the size of the packfiles doesn’t really come into play here). The options are a sparse checkout, submodules, or Google’s repo tool.

- git config --global core.preloadIndex true
  - This is now enabled by default already.


- 
- 

# disccuss
- ## 

- ## 

- ## 

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
