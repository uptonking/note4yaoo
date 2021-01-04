---
title: spec-git-commit-convention
tags: [convention, git, spec]
created: '2020-12-07T14:16:41.805Z'
modified: '2020-12-07T14:17:56.061Z'
---

# spec-git-commit-convention

# guide

# [Conventional Commits](https://www.conventionalcommits.org/)

- The Conventional Commits specification is a lightweight convention on top of commit messages.
- The commit message should be structured as follows:

``` 

<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- fix
- feat
- refactor
- chore
- docs
- style
- perf
- test
- more types
  - ci
- BREAKING CHANGE
  - a commit that has a footer BREAKING CHANGE:, or appends a ! after the type/scope, introduces a breaking API change
  - A BREAKING CHANGE can be part of commits of any type.

# ref

- [Git Commit Message Standard](https://gist.github.com/turbo/efb8d57c145e00dc38907f9526b60f17)
  - Subject Line Standard Terminology
  - add, remove, bump, make(build), start, stop, reformat
