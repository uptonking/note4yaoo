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
# more-blogs
- [Git's database internals I: packed object store - The GitHub Blog](https://github.blog/2022-08-29-gits-database-internals-i-packed-object-store/)

- [Git as a NoSql database](https://www.kenneth-truyers.net/2016/10/13/git-nosql-database/)
