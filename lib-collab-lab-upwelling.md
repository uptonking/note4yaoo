---
title: lib-collab-lab-upwelling
tags: [automerge, collaboration, crdt, prosemirror]
created: 2023-09-01T05:14:36.100Z
modified: 2023-09-01T05:15:33.858Z
---

# lib-collab-lab-upwelling

# guide

# blogs

## [Upwelling: Combining real-time collaboration with version control for writers.](https://www.inkandswitch.com/upwelling/)

### How Upwelling works

- The Upwelling text editor is a web application that works offline. 
  - Upwelling is written in Typescript and React, and communicates with a NodeJS server that stores data and connects users during live collaboration sessions. 
  - It uses ProseMirror as its underlying text editor.
- Upwelling’s collaboration features are built on top of the Automerge CRDT, which we use to track every single edit made to a document. 
  - To support asynchronous collaboration, the stack and any active drafts are combined into a single tarball (along with an additional Automerge document containing some metadata) then uploaded to the server. 
  - Real-time collaboration uses the sync protocol built into Automerge.
  - Upwelling is built on an experimental fork of Automerge
  - The fork adds support for rich text formatting and attributing edits to individual authors.

- Google Docs conflates(混合) change tracking with review, requiring writers to manually choose to track changes. 
  - Because tracking changes is visually distracting, this forces writers to select between a comfortable writing experience or supporting thorough review. 
  - Upwelling, in contrast, records the full history of the document and lets a writer decide on the fly how much historic detail to surface.

- Automatic merging is necessary but not sufficient
  - In the case of real-time collaboration, manually merging every keystroke would require an unreasonable amount of effort, so automatic merging is essential. 
  - With asynchronous collaboration, the situation is more nuanced, because merges happen less frequently, and greater divergence leads to a greater risk of conflicts. 
  - We believe that automatic merging is nevertheless useful in the asynchronous case, because it quickly produces a merged document that can then be reviewed for conflicts.

- It is tempting to try to devise more sophisticated merging policies or user interfaces for resolving syntactic conflicts. 
  - Unfortunately, since semantic conflicts cannot always be detected, human review of the merged result is necessary in any case. 
  - We therefore prioritized a design that makes reviewing changes easy rather than investing in more sophisticated merge behavior.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 
