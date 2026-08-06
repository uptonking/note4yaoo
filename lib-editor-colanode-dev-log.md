---
title: lib-editor-colanode-dev-log
tags: [colanode, dev-log]
created: 2025-07-23T15:49:07.494Z
modified: 2025-07-23T15:49:15.527Z
---

# lib-editor-colanode-dev-log

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-usage/tips
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## "Create workspace" vs "Create space"
- "Create workspace" 
  - A new top-level workspace
  - Create workspace (desktop): workspace + DB + sync folder + default Personal space
  - 
- "Create space"
  - A new content area inside the current workspace
  - A space is a node type — a top-level content container within one workspace. It holds pages, folders, databases, chats, etc. 
  - Create space: space node + Home page only
  - Think of it as: “Add another team/project area inside this workspace.”

- Both page and folder are nodes with a parentId. From space settings you create either as a direct child of the space
- Opening a folder shows an upload-centric view. Create/upload uses file.create with parentId: folder.id. The folder body only lists files, not pages.
  - The folder sidebar row also does not expand to show nested pages — unlike pages, which can show nested children.

- A page with subpages is a content-bearing index page. 
  - children visible in sidebar
- A folder is a contentless structural container, currently optimized for files.
  - children invisible in sidebar
