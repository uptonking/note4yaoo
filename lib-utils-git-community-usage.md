---
title: lib-utils-git-community-usage
tags: [community, dev-xp, git]
created: 2024-05-27T09:11:46.652Z
modified: 2024-05-27T09:12:06.925Z
---

# lib-utils-git-community-usage

# guide

# disccuss-stars
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
# disccuss
- ## 

- ## 

- ## 

- ## 

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
