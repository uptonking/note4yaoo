---
title: lib-utils-git-community-issues
tags: [community, git, issues]
created: 2025-01-01T17:09:32.810Z
modified: 2025-01-01T17:09:51.075Z
---

# lib-utils-git-community-issues

# guide

# discuss-stars
- ## 

- ## 

- ## 
# disccuss-not-yet 🐛
- ## 

- ## [Git Status Takes a Long Time to Complete - Stack Overflow](https://stackoverflow.com/questions/1183769/git-status-takes-a-long-time-to-complete)
- For me, the slowness was due to having a lot of untracked files (temporary and output files from scripts.) Running `git status -uno` , which excludes the untracked files, ran much faster, and meets my requirements

- ## [Ways to improve git status performance - Stack Overflow](https://stackoverflow.com/questions/4994772/ways-to-improve-git-status-performance)
- To be more precise, git depends on the efficiency of the lstat(2) system call, so tweaking your client’s “attribute cache timeout” might do the trick.
  - The manual for git-update-index — essentially a manual mode for git-status — describes what you can do to alleviate this, by using the --assume-unchanged flag to suppress its normal behavior and manually update the paths that you have changed. You might even program your editor to unset this flag every time you save a file.
- 👣 The alternative, as you suggest, is to reduce the size of your checkout (the size of the packfiles doesn’t really come into play here). The options are a sparse checkout, submodules, or Google’s repo tool.

- git config --global core.preloadIndex true
  - This is now enabled by default already.
# discuss-done
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 
