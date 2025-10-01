---
title: lib-saas-lasuite-drive-community
tags: [cloud-drive, community, lasuite-drive]
created: 2025-09-30T08:59:33.389Z
modified: 2025-09-30T08:59:53.837Z
---

# lib-saas-lasuite-drive-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## [Desktop client · Issue · suitenumerique/drive _202504](https://github.com/suitenumerique/drive/issues/118)
  -  I would like to know if you plan to add a desktop client that will synchronize the files between a local computer and the Drive cloud.
- We didn't have act on this feature but already discuss about it. Does it mean implementing the webdav protocol ?
  - Webdav is one way to do it. Its advantage is the simplicity, but it means that you have to be connected (Internet) to have access to your files.
  - The 2 other main ways are fuse and FS watchers. 
  - By fuse, I means creating a virtual disk, and implementing the synchronization of the changes + cache to edit offline: `fuse` is the technology to do that on Linux, and there are ports like `winfsp` on windows and `macfuse` on macOS. 
  - For FS watchers, the user have a normal directory on their computer, and the desktop client watches the changes in this directory with `inotify` (linux), `fsevents` (macOS), or `ReadDirectoryChangesW` (windows). The client can synchronize the files between the local directory and the Drive app.
  - With FS watchers, you have 2 hard problems: the synchronization, and watching the file system. Watching the file system looks quite easy at first, as inotify&co should be doing this job, but there are lots of edge cases. For example, the inode number on Linux (the identifier for the files) can be reused, so moving a file can be confused with deleting a file and creating another file.
  - So, the good answer depends of the level of convenience expected for the users vs the effort that can be spent on that task. I hope it helps.

- https://github.com/nextcloud/desktop is using Webdav to sync. Maybe a good starting point?
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
