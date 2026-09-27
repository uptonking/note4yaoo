---
title: lib-office-papermerge-community
tags: [community, docs, papermerge, pdf]
created: 2025-12-09T13:51:06.475Z
modified: 2025-12-09T13:51:18.940Z
---

# lib-office-papermerge-community

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

- ## [How I would like to use papermerge as a paperless user · Issue · ciur/papermerge _202007](https://github.com/ciur/papermerge/issues/34)

# discuss-issues
- ## 

- ## 

- ## [Please ignore dot files from macOS _202104](https://github.com/ciur/papermerge/issues/363)

- ## [Deleting nodes does not get rid of underlying filesystem folders · Issue · ciur/papermerge _202403](https://github.com/ciur/papermerge/issues/607)
  - When deleting nodes/files in papermerge I noticed that the folders created for the nodes are still present.
  - Also I'm curious as to the reasoning of the folder structures. I can understand the need to provide the GUID folder for uniqueness of uploaded files, file versioning, merging etc, but the extra folder structures on top of the GUID folder seems weird to me. 
  - It seems to me applying only the GUID folder should be sufficient, and would allow for easier manual decorruption in the event something catastrophic happened and you needed to piece an instance back together.

- Regarding your question about extra folder on top of GUID folder.
  - The reason is to reduce number of file system nodes (files or folders) in a specific folder.
  - Example: let's say you have 120, 000 pages; then with just GUID folder, the pages folder will contain 120, 000 entries! The problem is that usually there is a limit of number of subfolders on fiven file system. By adding one extra folder, with two digits of the UUID, the limitation is reduced by factor of 256. Thus if you have 120, 000 pages, on the file system there will be max 120, 000 / 256 ~ 468 folders.

- ## 🐛 [When user is deleted - delete all its storage data as well · Issue · ciur/papermerge _202209](https://github.com/ciur/papermerge/issues/485)
  - Storage data - is (are?) document files and document OCR data stored under media root.
  - Expected: when user is deleted, both its folders should be deleted as well
  - Actual: both folders are still there and contain documents!

- 似乎修复的pr实现逻辑存在问题
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
