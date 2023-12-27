---
title: thread-tool-scripts
tags: [scripts, thread, tool]
created: 2023-12-11T10:11:55.588Z
modified: 2023-12-11T10:12:09.159Z
---

# thread-tool-scripts

# guide

# discuss-stars
- ## 

- ## 

- ## [shell - Make `rm` move to trash - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/42757/make-rm-move-to-trash)
- The previous answers mention commands `trash-cli` and `rmtrash` . Neither of those are found by default on Ubuntu 18.04, but the command `gio` is. 

# discuss
- ## 

- ## 又学到了，当你 format 了整个仓库之后， git blame 就会废掉，全是 format 的 commit。
- https://twitter.com/liruifengv/status/1737636700489470058
  - 可以创建一个 .git-blame-ignore-revs 文件，写入要忽略的 commit id。
  - 执行命令： `git config --local blame.ignoreRevsFile .git-blame-ignore-revs` 就好了
  - GitHub 也会自动读取 .git-blame-ignore-revs 文件
- 可以在服务端做一个 hook  如果没有通过 lint  的就拒绝

- ## 我也有个多repo的网盘git脚本... 用来没事fetch一下常用repo, 工作时少几秒fetch的等待, 心情会好一点点
- https://twitter.com/drmingdrmer/status/1734143991564902683
  - [watch and auto fetch/rebase/merge/push git-repo.](https://gist.github.com/drmingdrmer/07faee6c4f7c8e31da3c5210cfa04034)
