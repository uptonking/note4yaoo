---
title: lib-utils-git-blog
tags: [blog, git]
created: 2023-08-29T10:24:00.429Z
modified: 2023-08-29T10:24:09.136Z
---

# lib-utils-git-blog

# guide

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
