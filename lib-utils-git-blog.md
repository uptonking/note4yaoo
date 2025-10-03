---
title: lib-utils-git-blog
tags: [blog, git]
created: 2023-08-29T10:24:00.429Z
modified: 2023-08-29T10:24:09.136Z
---

# lib-utils-git-blog

# guide

# blogs-github-vendor
- [MySQL High Availability at GitHub - The GitHub Blog _201806](https://github.blog/engineering/infrastructure/mysql-high-availability-at-github/?utm_source=chatgpt.com)
  - GitHub uses MySQL as its main datastore for all things non-git

- [Git at GitHub Scale - Git Merge 2022 - YouTube _202210](https://www.youtube.com/watch?v=QK6EkWqjN2s)

- [How We Made GitHub Fast - The GitHub Blog _200910](https://github.blog/news-insights/how-we-made-github-fast/?utm_source=chatgpt.com)

## ⚡️ [How GitHub Reduced Repo Storage Size by Over 90% _202411](https://newsletter.betterstack.com/p/how-github-reduced-repo-storage-size)

- 
- 
- 
- 
- 

## 🤔 [How does Github store millions of repo and billions of files? _202104](https://www.pankajtanwar.in/blog/how-does-github-store-millions-of-repo-and-billions-of-files)

- 
- 
- 
- 
- 
- 
- 
- 

### 👥 [We put half a million files in one Git repository (2022) | Hacker News _202308](https://news.ycombinator.com/item?id=37291765)

### 👥 [git with billion json files : r/git _202403](https://www.reddit.com/r/git/comments/1baognp/git_with_billion_json_files/)

- 
- 
- 

## [Stretching Spokes - The GitHub Blog _201710](https://github.blog/engineering/infrastructure/stretching-spokes/)

- GitHub’s Spokes system stores multiple distributed copies of Git repositories. 
- This article discusses how we got Spokes replication to span widely separated datacenters.

- 
- 
- 
- 
- 

## [Building resilience in Spokes - The GitHub Blog _201609](https://github.blog/engineering/building-resilience-in-spokes/)

- Spokes is the replication system for the file servers where we store over 38 million Git repositories and over 36 million gists. 
  - It keeps at least three copies of every repository and every gist so that we can provide durable, highly available access to content even when servers and networks fail. 
  - Spokes uses a combination of Git and rsync to replicate, repair, and rebalance repositories.

- 
- 
- 
- 
- 
- 
- 

## [Introducing DGit - The GitHub Blog _201604](https://github.blog/engineering/architecture-optimization/introducing-dgit/)

> DGit is now called Spokes

- GitHub hosts over 35 million repositories and over 30 million Gists on hundreds of servers. 
  - Over the past year, we’ve built DGit, a new distributed storage system that dramatically improves the availability, reliability, and performance of serving and storing Git content.
- DGit is short for “Distributed Git
- DGit performs replication at the application layer, rather than at the disk layer. Think of the replicas as three loosely-coupled Git repositories kept in sync via Git protocols, rather than identical disk images full of repositories. This design gives us great flexibility to decide where to store the replicas of a repository and which replica to use for read operations.
- If a file server needs to be taken offline, DGit automatically determines which repositories are left with fewer than three replicas and creates new replicas of those repositories on other file servers. This “healing” process uses all remaining servers as both sources and destinations. Since healing throughput is N-by-N, it is quite fast. And all this happens without any downtime.

- 🏠 DGit uses plain Git
  - Most end users store their Git repositories as objects, pack files, and references in a single .git directory. They access the repository using the Git command-line client or using graphical clients like GitHub Desktop or the built-in support for Git in IDEs like Visual Studio. 
  - Perhaps it’s surprising that GitHub’s repository-storage tier, DGit, is built using the same technologies. 
  - Why not a SAN? A distributed file system? Some other magical cloud technology that abstracts away the problem of storing bits durably?
  - The answer is simple: it’s fast and it’s robust.
- Git is very sensitive to latency. A simple git log or git blame might require thousands of Git objects to be loaded and traversed sequentially. If there’s any latency in these low-level disk accesses, performance suffers dramatically. Thus, storing the repository in a distributed file system is not viable. Git is optimized to be fast when accessing fast disks, so the DGit file servers store repositories on fast, local SSDs.

- 
- 
- 
- 

## [Git's database internals I: packed object store - The GitHub Blog _202208](https://github.blog/open-source/git/gits-database-internals-i-packed-object-store/?utm_source=chatgpt.com)

- In this five-part blog post series, we will illuminate Git’s internals to help you collaborate via Git, especially at scale.
- The core idea I want to convey is this: Git is the distributed database at the core of your engineering system.

- 
- 
- 

## [Scaling Git’s garbage collection - The GitHub Blog _202209](https://github.blog/engineering/architecture-optimization/scaling-gits-garbage-collection/?utm_source=chatgpt.com)

- At GitHub, we store a lot of Git data: more than 18.6 petabytes of it, to be precise.
- The process for permanently removing unreachable objects from a repository’s history has a history of causing problems within GitHub, especially in busy repositories or ones with lots of objects. In this post, we’ll talk about what those problems were, why we had them

- 
- 

# blogs-git-database
- [make a blog post about git like databases](https://github.com/multun/blog/issues/4)

## [Using Git as a key-value database](https://secure-git.guide/015_How-to-use-Git-as-a-database/)

- With Git you can store data in two different ways: Git objects, References
- Git internally uses a key-value database with only 4 types of objects: blobs, trees, commits and annotated-tags
- Each object is stored in the database and the way to reference the object is by using its sha1 (a checksum of the content).
- This database is immutable. You can only add new content.

- You can store your data inside blob objects. When you want to update the version of your object you can store a new object
- When you update a blob object you could create a commit.
  - This model uses an orphan branch for each object. An "orphan" branch is a branch that is not connected to any other branch. That means the first commit does not have any ancestors.

- We normally have two options to fix that problem with normal databases, you can either lock the record when you want to modify it (pessimistic locking) or try to modify it always and make the update fail if the record has changed (optimistic locking).
- Git only allows us to use the optimistic approach. When you try to “push” your object version by updating the reference in the origin repo you will get an error if the reference (branch) was already changed.
# blogs-git-usage
- [Git从入门到应付日常工作](https://jumpshare.com/s/P42MV2FmKfnzSLXjaFUk)

- [示意图多 Git Branching and Merging: A Step-By-Step Guide](https://www.varonis.com/blog/git-branching)
# blogs-fossil
- [Fossil Versus Git](https://fossil-scm.org/home/doc/trunk/www/fossil-v-git.wiki)
# blog-git-version-history

## [ipld-version-control _201706](https://gist.github.com/flyingzumwalt/a6821e843366d606aeb1ba53525b8669)

- hypercore-protocol.org is built on version control, if anyone's interested 
# blogs-diff 🆚

## 🧑‍🏫 [Git Diff | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/saving-changes/git-diff)

```diff
# the input sources of the diff
diff --git a/diff_test.txt b/diff_test.txt
# internal Git metadata. correspond to Git object version hash identifiers
index 6b0c6cf..b37e70a 100644
# a legend that assigns symbols to each diff input source
--- a/diff_test.txt
+++ b/diff_test.txt
# a list of diff 'chunks'
# A diff only displays the sections of the file that have changes
# The first line is the chunk header. Each chunk is prepended by a header enclosed within @@ symbols. The content of the header is a summary of changes made to the file.
# -1 +1 meaning line one had changes. 
# @@ -34,6 +34,8 @@ meaning 6 lines have been extracted starting from line number 34. Additionally, 8 lines have been added starting at line number 34.
@@ -1 +1 @@
# The remaining content of the diff chunk displays the recent changes
-this is a git diff test example
+this is a diff example
```

```shell
# When a file path is passed, the diff operation will be scoped to the specified file.
# By default git diff will execute the comparison against HEAD
# 👉 compare the specific changes in the working directory, against the index, showing the changes that are not staged yet
git diff HEAD ./path/to/file
# with the --cached option the diff will compare the staged changes with the local repository
# --cached option is synonymous with --staged.
git diff --cached ./path/to/file

# Comparing files between two different commits
git diff commitId1 commitId2

# Comparing files from two branches
git diff main new_branch ./diff_test.txt

# Branches are compared like all other ref inputs to git diff
# two dots indicate the diff input is the tips of both branches. 
# The same effect happens if the dots are omitted and a space is used between the branches.
git diff branch1..other-feature-branch

# three dot operator initiates the diff by changing the first input parameter branch1. It changes branch1 into a ref of the shared common ancestor commit between the two diff inputs, the shared ancestor of branch1 and other-feature-branch. The last parameter input parameter remains unchanged as the tip of other-feature-branch.
git diff branch1...other-feature-branch

```

- git diff --color-words
  - 可以展示行内diff, 删除的字符是红色，新增的字符为普通黑色而不是绿色

- `git diff` can be run on binary files. Unfortunately, the default output is not very helpful.
  - Git does have a feature that allows you to specify a shell command to transform the content of your binary files into text prior to performing the diff.
# more-blogs
- [Git's database internals I: packed object store - The GitHub Blog](https://github.blog/2022-08-29-gits-database-internals-i-packed-object-store/)

- [Git as a NoSql database](https://www.kenneth-truyers.net/2016/10/13/git-nosql-database/)
