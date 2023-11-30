---
title: lib-utils-storage-filesystem-web-community
tags: [filesystem, indexeddb, storage, web-storage]
created: 2022-11-27T14:19:27.900Z
modified: 2023-09-16T17:43:09.215Z
---

# lib-utils-storage-filesystem-web-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## This is one downside of having no hard links in an FS: renaming a directory means copying all the contained data to the new location.
- https://twitter.com/msimoni/status/1729921989408661877
  - If you have hard links, and you're moving a directory, you can just remove the old hard link and insert the new hard link. But if you don't have hard links ...
- I am surprised seasoned os designer made the decision to not have hard link!
  - I think the reasoning here is to keep the 9P protocol as simple and general as possible. If 9P supported hard links, then every file server has to support hard links, and in Plan 9's everything's a file server.
- Yes, it makes sense. Hard links break FS abstraction a bit since they don't work across file systems
- And soft links break FS abstraction a bit because they introduce cycles, turning tree into a graph (and for other reasons)
- I don't think cycles would _very_ problematic, actually. Tools like cp and rm would have to remember all objects they had already seen (and simply stop there), but that's no longer a real problem, with today's large RAMs.
  - Sure. Still complicates things a bit imo
- That's true also when moving across file systems, since hard links don't go across. Btw, interesting if Git uses some tricks to construct working copy of a commit quickly.

- If the OS provides a syscall for directory rename, the filesystem could internally do it in a hard link like way, without exposing the concept to userspace
