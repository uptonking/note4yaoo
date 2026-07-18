---
title: lib-editor-colanode-codebase
tags: [codebase, colanode]
created: 2025-06-21T19:12:41.819Z
modified: 2025-06-21T19:12:59.931Z
---

# lib-editor-colanode-codebase

# guide

- self-host
  - pgvector: postgres://user:pass@localhost:5432/colanode_db
  - minio: http://localhost:9000
    - http://localhost:52119/ (minioadmin)
  - redis: redis://127.0.0.1:6379
  - AI_ENABLED
  - When you go to the login screen of Colanode, open the servers dropdown and click 'Add new server'. 
    - http://localhost:3000/config

```shell
# backend
minio server /Users/yaoo/Documents/runappdata/miniocolanodedata

cd cd apps/server
npm run dev

# frontend 
# http://localhost:4000/
cd apps/web
npm run dev

cd apps/desktop
npm run dev
```

# overview
- Desktop is a thin native wrapper around the exact same client core that the web app uses
  - Both render the same `<App type="desktop|web"/>` from @colanode/ui
  - both connect to remote Colanode servers (or self-hosted)
- Desktop
  - `better-sqlite3` (Node native) via `WebKyselyService`.
- Webapp
  - `sql.js` (WASM SQLite) via `WebKyselyService` + OPFS for files
- Storage backends
  - file (local FS), s3, gcs, azure

- Local Browser Storage (Web App) — SQLite via WASM
  - In the Dedicated Worker

- Sync (Read) Flow — Cursor-Based WebSocket Streams
  - WebSocket connection to server
  - Per-stream synchronizers (each tracks a cursor/revision)
  - Client applies updates to local SQLite, persists new cursor
- Mutation (Write) Flow — Optimistic Local-First
  - User edit → YDoc.update() generates binary CRDT update
  - Background batcher (every ~100ms) POSTs pending mutations to server
  - Server validates & merges using Yjs, broadcasts via WebSoc
  - editor has a 500 ms debounced save. It compares the previous structured document with the new content and generates a Yjs binary update
  - Mutations are posted in batches of at most 50, normally a delta, not the complete page
- For every document mutation, the server:
  1. Loads the retained document_updates rows for that document.
  2. Applies them to an empty Yjs document.
  3. Applies the new update.
  4. Extracts and validates the resulting full structured content.
  5. Stores the new binary delta in document_updates.
  6. Stores the materialized full JSON in documents.content.
  - The documents.content row is useful as the server’s current materialized view, but it is not sent to a new client during document sync.
- Offline Editing — Fully Supported
  - Edits go to local SQLite immediately
  - All data survives browser refresh/close — SQLite persists in OPFS (IndexedDB-backed)
  - Mutation queue (mutations table) holds unsynced operations with retry count
  - On reconnect: MutationService automatically flushes pending mutations; Synchronizer pulls missed updates via cursors

- server has a merge job that combines nearby Yjs updates, keeps the last row, records the merged update IDs, and deletes the redundant rows
  - the server does not normally keep one row per keystroke forever: a recurring merge job replaces eligible Yjs updates with a merged update and records which update IDs it represents.
  - the compaction job is disabled by the schema default.
  - Enabling jobs.documentUpdatesMerge reduces row count after the job runs, although merged payloads can still be large and contain metadata for every folded update. nodeUpdatesMerge affects node/title metadata similarly.

- Is it full or partial sync?
  - Per-root scoping — you only sync roots (spaces) you have a collaboration on. You never pull the whole server or even the whole workspace. A guest with access to one space syncs only that one space's 5 streams.
  - ✨ Files are lazy — binary file content is not part of these streams. Files come through the separate downloads / local_files tables, fetched on-demand. Only file metadata rides on the node streams.
- But within a root you have access to, it IS a full backfill of all CRDT updates, interactions, reactions, tombstones, and document updates from revision 0 onward — chunked 100 rows per WebSocket round-trip.
- Chunk size: Fixed LIMIT 100 per round-trip (node-updates.ts:54). For a root with 50k updates → 500 sequential WS round-trips on first load.
- Sequential: Within a root, the 5 streams are Promise.all'd (sync-service.ts:193-197), but each stream's batches are strictly sequential.
- CRDT blobs, not snapshots: Because there's no "current state" snapshot stream, the client must replay the entire update history of the root to reconstruct current state. The server's node-updates-merge job is what keeps this bounded — without it, history would grow unbounded. This is the real scaling risk.
- No snapshot/compaction on the wire: There's no "give me the merged state as of cursor X" fast-path. A returning device with a stale/evicted DB pays the full replay cost again.
- 👀 Colanode does not replicate SQLite tables or columns to Postgres. It synchronizes explicit domain messages, then each side maintains its own tables and derived state.
  - most client tables/columns are local-only
  - The only workspace WebSocket streams are users, collaborations, node updates, interactions, reactions, tombstones, and document updates
  - metadata table is written only into local SQLite with no server request
- The server also has server-only data such as devices, node paths, storage upload records, embeddings and job counters
- Attachment state cleanly demonstrates the split: the file node’s shared attributes, such as name, size, version, and whether the upload is ready, sync through the normal node CRDT stream. 
  - Device paths, cached bytes, download progress, retry counts, completion times, and error messages live only in that device’s SQLite and filesystem.

- The key pattern: every synced table that supports local edits has a split local_revision / server_revision.

- Server does not provide a conventional note CRUD API. Note changes use an internal mutation and synchronization protocol, and conflict handling happens on both the client and server using Yjs.
- The server routing inventory confirms there is no conventional GET/POST/PATCH/DELETE /notes/:id API. Notes and records are represented as nodes plus optional documents; reads come from local SQLite, writes are posted as typed mutations, and server-to-client reads arrive through WebSocket revision streams.
  - a note is split into a node (metadata) and a document (page body). The UI reads both from local SQLite; note writes are serialized as typed mutations to one workspace endpoint, while WebSocket sync distributes authoritative revisions back to clients.
- Reads normally do not call the server. The UI queries local SQLite directly

- The server maintains the authoritative accepted update history, validates permissions/content, allocates revisions, and handles database races.
  - Each client combines the confirmed server state with any local mutations that are still pending.
- Concurrent writes to the same Yjs map/scalar field resolve deterministically according to Yjs rules, not necessarily wall-clock last-write-wins.
- Deletion is different. The server deletes the node and creates a tombstone: apps/server/src/lib/nodes.ts:636. If deletion is accepted first, a later edit gets NOT_FOUND; if the edit is accepted first and deletion follows, deletion becomes the final state.
- The server does retain full materialized bodies in PostgreSQL; the missing piece is only a public/bulk HTTP read route.
  - The server does not expose a conventional HTTP API for retrieving all note contents.
  - documents.content column is PostgreSQL jsonb containing the complete DocumentContent
  - Whenever an update arrives, the server applies the Yjs history plus the incoming update and overwrites documents.content with the resulting full JSON

- When you open the webapp in a fresh browser, the local SQLite DB is empty and every sync cursor starts at '0'.
  - The client sets up three tiers of synchronizers: 2 workspace-wide streams — users and collaborations (one each, always on); 5 streams PER root the user collaborates on
  - A "root" is a top-level node (e.g. a Space) that the user has a collaboration row for.
- 👀 there is no "current state" stream
  - The client reconstructs the current state of every node by replaying the node_updates CRDT blobs through Yjs and merging into the local node_states table. 
  - The server's background node-updates-merge job collapses old updates so this history is bounded, not infinite.
- every accessible note is reconstructed even if unopened, but the Electron database does not retain all server history rows. It folds received history into a current JSON document, a current Yjs state, and a full-text search index; the local document_updates table is mainly for unsynced local edits.
  - all current note content in every accessible root is reconstructed locally during sync, even if you never open those notes. There is no per-note lazy-loading condition.
- The client persists each document in THREE forms, eagerly
  - documents.content: JSON of full current content, for ui render
  - document_states.state: Merged Yjs binary blob, for crdt edits
  - document_texts.text: Extracted plain text, for Offline full-text search
  - So even a note you never open is downloaded and stored 3× locally.
- After catch-up, the client normally does not retain all 2, 000 server deltas as 2, 000 local rows.  
  - the final database is not necessarily “full content multiplied by 2, 000 changes.” 
  - But each note is represented more than once: materialized JSON, Yjs state, and search-index overhead.

- Uploaded .md files and attachments are different: their node metadata is synchronized eagerly, but the actual file bytes are downloaded on demand.
  - Files use separate downloads / local_files tables with download_status

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
- 
- 
- 
- 

# frontend

# backend

# more
