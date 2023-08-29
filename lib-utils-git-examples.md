---
title: lib-utils-git-examples
tags: [examples, git]
created: 2023-08-29T10:12:03.868Z
modified: 2023-08-29T10:12:22.345Z
---

# lib-utils-git-examples

# guide

# popular
- https://github.com/isomorphic-git/isomorphic-git /7kStar/MIT/202307/js
  - https://isomorphic-git.org/
  - a pure JavaScript reimplementation of git that works in both Node.js and browser 
  - It can read and write to git repositories, fetch from and push to git remotes (such as GitHub), all without any native C++ module dependencies.
    - rather than relying on the `fs` and `http` modules, isomorphic-git lets you bring your own file system and HTTP client.
    - work with LightningFS/BrowserFS/Filer
  - Isomorphic-git aims for 100% interoperability with the canonical git implementation. 
    - This means it does all its operations by modifying files in a ".git" directory just like the git you are used to.
  - https://github.com/isomorphic-git/lightning-fs /js
    - I wanted to see if I could make something faster than BrowserFS or filer that still implements enough of the fs API to run the isomorphic-git test suite in browsers.
- https://github.com/creationix/js-git /3.8kStar/MIT/201907/js/inactive
  - A JavaScript implementation of Git.
  - It also enables using git as a database to replace SQL and no-SQL data stores in many applications.
  - https://github.com/es-git/es-git /202012/ts/inactive
    - Git implemented in EcmaScript (a fork of JS-Git)
  - https://github.com/creationix/git-node-fs
    - A node adapter for the fs-db mixin for js-git. This enables access to Git repositories on the filesystem using Node.js.
  - https://github.com/creationix/js-github
    - An implementation of the js-git interface that mounts a live github repo.

- https://github.com/Byron/gitoxide /rust
  - an implementation of git written in Rust
  - for the most part, git operations are heavily reliant on memory mapped IO as well as CPU to decompress data, which doesn't lend itself well to async IO out of the box.
  - https://github.com/chrisdickinson/git-rs
    - Implementing git in rust for fun and education!

- https://github.com/aergoio/litetree 202003/c/inactive
  - It is a modification of the SQLite engine to support branching, like git!
  - Each database transaction is saved as a commit, and each commit has an incremental number
  - We cannot write to the database when we are in a defined commit, writing is only possible at the head of each branch. If you want to make modifications to some previous commit you must create a new branch that starts at that commit.
# git-like
- https://github.com/GerritCodeReview/jgit /EDL(BSD)/java
  - https://eclipse.dev/jgit/
  - An implementation of the Git version control system in pure Java.
  - JGit 6.0 and newer requires at least Java 11. Older versions require at least Java 1.8.
  - Native symbolic links are supported, provided the file system supports them. 
  - For Windows you must use a non-administrator account and have the SeCreateSymbolicLinkPrivilege.

- https://github.com/jelmer/dulwich /python
  - Pure-Python Git implementation
  - It aims to provide an interface to git repos (both local and remote) that doesn't call out to git directly but instead uses pure Python.
# git-ui
- https://github.com/corylus-git/corylus /ts/electron
  - https://corylus.dev/
  - Corylus is a graphical user interface for Git. 
  - It aims to offer much of the power and flexibility of Git without having to remember CLI commands.
# apps

# examples

# utils
- https://github.com/brawnski/git-annex /hs
  - git-annex allows managing files with git, without checking the file contents into git. 
  - While that may seem paradoxical, it is useful when dealing with files larger than git can currently easily handle, whether due to limitations in memory, checksumming time, or disk space.
# git-data
- https://github.com/datalad/datalad /python
  - http://datalad.org/
  - it stands on the shoulders of Git and Git-annex to deliver a decentralized system for data exchange. 
  - This includes automated ingestion of data from online portals and exposing it in readily usable form as Git(-annex) repositories, so-called datasets. 
  - The actual data storage and permission management, however, remains with the original data providers.
# more
