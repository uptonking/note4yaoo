---
title: lib-editor-editablejs-codebase
tags: [codebase, editablejs, slate-editor]
created: 2023-02-21T20:16:34.756Z
modified: 2023-02-21T20:17:00.638Z
---

# lib-editor-editablejs-codebase

# guide

# overview
- Desktop is a thin native wrapper around the exact same client core that the web app uses
  - Both render the same `<App type="desktop|web"/>` from @colanode/ui
  - both connect to remote Colanode servers (or self-hosted)
- Desktop
  - better-sqlite3 (Node native) via WebKyselyService
- Webapp
  - sql.js (WASM SQLite) via WebKyselyService + OPFS for files
- Storage backends
  - file (local FS), s3, gcs, azure

- Local Browser Storage (Web App) — SQLite via WASM
  - In the Dedicated Worker

- Mutation (Write) Flow — Optimistic Local-First
  - User edit → YDoc.update() generates binary CRDT update
  - Background batcher (every ~100ms) POSTs pending mutations to server
  - Server validates & merges using Yjs, broadcasts via WebSoc
  - Offline Editing — Fully Supported
- Sync (Read) Flow — Cursor-Based WebSocket Streams
  - WebSocket connection to server
  - Per-stream synchronizers (each tracks a cursor/revision)
  - Client applies updates to local SQLite, persists new cursor

- When you open the webapp in a fresh browser, the local SQLite DB is empty and every sync cursor starts at '0'.
  - The client sets up three tiers of synchronizers: 2 workspace-wide streams — users and collaborations (one each, always on); 5 streams PER root the user collaborates on
  - A "root" is a top-level node (e.g. a Space) that the user has a collaboration row for.
- there is no "current state" stream
  - The client reconstructs the current state of every node by replaying the node_updates CRDT blobs through Yjs and merging into the local node_states table. The server's background node-updates-merge job collapses old updates so this history is bounded, not infinite.

- Is it full or partial sync?
  - Per-root scoping — you only sync roots (spaces) you have a collaboration on. You never pull the whole server or even the whole workspace. A guest with access to one space syncs only that one space's 5 streams.
  - Files are lazy — binary file content is not part of these streams. Files come through the separate downloads / local_files tables, fetched on-demand. Only file metadata rides on the node streams.
- But within a root you have access to, it IS a full backfill of all CRDT updates, interactions, reactions, tombstones, and document updates from revision 0 onward — chunked 100 rows per WebSocket round-trip.
- Chunk size: Fixed LIMIT 100 per round-trip (node-updates.ts:54). For a root with 50k updates → 500 sequential WS round-trips on first load.
- Sequential: Within a root, the 5 streams are Promise.all'd (sync-service.ts:193-197), but each stream's batches are strictly sequential.
- CRDT blobs, not snapshots: Because there's no "current state" snapshot stream, the client must replay the entire update history of the root to reconstruct current state. The server's node-updates-merge job is what keeps this bounded — without it, history would grow unbounded. This is the real scaling risk.
- No snapshot/compaction on the wire: There's no "give me the merged state as of cursor X" fast-path. A returning device with a stale/evicted DB pays the full replay cost again.

- 
- 
- 

# modules

## model

- 在slate model上扩展了Grid、List类型的element
  - Grid和List都只是一系列的工具方法

- selection使用的是slate的定义

## view

- 编辑器内容div
  - userSelect: 'none'

- 编辑器内容div的下个兄弟元素是shadow dom，作为编辑器常用辅助元素
  - CaretComponent
  - DragCaretComponent
  - SelectionComponent
  - InputComponent/textarea-container

- TouchPointComponent

- Slots
  - block左边拖动按钮

## input

- 实现思路是在pointer事件的位置通过绝对定位放置一个oapcity为0宽约为1px的textarea来接收输入

## command

- reexport slate Transforms对象，修改了insertText/Nodes等方法
# more
