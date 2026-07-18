---
title: lib-office-joplin-dev
tags: [joplin, note-taking]
created: 2024-01-28T20:51:43.532Z
modified: 2024-01-28T20:52:21.981Z
---

# lib-office-joplin-dev

# guide
- pros
  - MIT > AGPLv3
  - Note history (revisions)
  - Synchronisation with various services, including Nextcloud, Dropbox, WebDAV and OneDrive.
    - 还支持同步到本地文件夹
    - 由客户端polling拉取最新内容来实现同步
  - 客户端丰富，支持win/linux/mac/android/ios/cli, 还提供Web Clipper, 但不支持web
  - End To End Encryption (E2EE)
  - 支持plugins，并提供了插件市场网站
  - export支持导出 md+图片
  - 附件可配置下载策略 always/manual/auto
  - server db 存放最新内容快照, 方便提供api

- cons
  - 未实现web端
  - ~~基于文件，难以实现多页面的联动更新~~ 
  - client db全量存数据的架构在大量数据的场景对客户端设备要求高，scale不友好
    - ? 大量数据时首次同步时间长

- features
  - 支持本地文件管理?
  - Offline first, so the entire data is always available on the device even without an internet connection.
  - Support notes, to-dos, tags and notebooks.
  - Support for alarms (notifications) in mobile and desktop applications.
  - Markdown notes
  - Choice of both Markdown and Rich Text (WYSIWYG) editors.
  - File attachment support - images are displayed, other files are linked and can be opened in the relevant application.
  - Supports multiple languages.
# dev-xp
- 设置同步到本地filesystem后, 所有note会自动导出到本地作为.md文件, 
  - 但文件名是uuid, 内容是markdown原文，文件末尾是类似frontmatter的endmatter

- 社区提供了和obsidian类似的sync plugin, 支持同步到 Google Docs, supernote, ...
# codebase
- architecture
  - ui <> (local-file <>) local-sqlite <> remote-server <> remote-db

- Joplin uses a client-server sync architecture:
  - self-hosted-server, joplin cloud, onedrive, WebDAV
  - @joblin/lib (db, model, sync, encryption)
  - electron-desktop, react-native-mobile, cli(nodejs)
  - react-native-web
  - The mobile app (@joplin/app-mobile) can run as a web app using react-native-web
- The desktop app cannot run directly as a web app because:
  - It uses Electron-specific APIs (ipcMain, ipcRenderer, BrowserWindow, native menus, etc.)
  - It bundles Node.js modules that don't work in browsers
  - Different UI component library, not react-native-web
  - However, both share the same core library (@joplin/lib), so business logic, database, sync, and models are identical.

- SQLite Database is the Source of Truth
  - The SQLite database (joplin.sqlite or db-dev.sqlite) is the authoritative data store for all clients (Desktop, Mobile, CLI).
- File API: Abstract interface (file-api.ts) with drivers for each sync target
- Creates Real Files: Only during explicit export (File → Export or joplin export CLI)
  - Exports EVERYTHING as .md files with resources folder
  - CLI sync uses db, no files op
- Joplin is offline-first: both desktop and React Native download every current note body during synchronization, even if you never open the note. 
  - Opening a note later reads it from local SQLite and does not fetch its body from the server.
- The local database can be larger than the raw Markdown because Joplin also builds:
  - A normalized copy of note title/body.
  - An SQLite full-text-search index.
  - Sync metadata and retained note-history revisions.

- @joplin/server is a standalone Koa-based Node.js server
  - REST API for sync operations
  - User management, authentication (including SAML)
  - PostgreSQL or SQLite database
  - Docker deployment support
  - Admin UI (served via Mustache templates)
  - Can be self-hosted or use Joplin Cloud 🤔
- The server stores items in PostgreSQL (or SQLite for dev)
  - if updated_time > sync_time
- The server does expose authenticated CRUD-like endpoints, but they operate on generic sync items and serialized content rather than a note-domain resource such as POST /notes.
  - These APIs receive Joplin’s serialized item format. The server extracts fields such as item type, parent ID and timestamps, checks permissions and size limits, stores the item, and records a change event.
- The server itself mainly stores the submitted full snapshot and emits change records. It does not merge note bodies or implement a normal ETag/If-Match optimistic concurrency protocol. Consequently, there is still a narrow race if two clients both check the remote state and then upload simultaneously; this limitation is acknowledged in packages/ lib/Synchronizer.ts
- authenticated user can retrieve all current note contents by enumerating generic sync items and downloading each item’s serialized content.
  - With E2EE enabled, the server can return only encrypted note payloads, not plaintext titles or bodies.
- how the Joplin Server sync driver works: it obtains delta metadata, then performs individual content requests through its get() method. The synchronizer queues these downloads

- 🔄 Synchronizer.ts orchestrates bidirectional sync
  - Clients configure sync target as "Joplin Server" with URL + credentials
  - clients sync to various targets (Joplin Server, cloud services, filesystem)
  - sync with multiple backend drivers via FileApi interface
- How Local File Editing Syncs to DB (External Editor Feature)
  - When you use an external editor (VS Code, Typora, etc.), Joplin uses ExternalEditWatcher.ts with `chokidar` file watcher
- Joplin uses POLLING-based sync, NOT WebSocket/push
- Doc Sharing exists but is sync-based 而不是协作
  - ShareService.ts creates share records on server
  - Recipients sync normally → receive shared notebook on next sync
  - No real-time collaborative editing ( **no OT/CRDT, no live cursors** )
- UI Editing → SQLite DB (Source of Truth)
  - NO files are written to the filesystem when editing in the UI. The editor works entirely against the SQLite database.
  - The editor component (packages/app-desktop/gui/NoteEditor*.tsx) calls dispatch({ type: 'NOTE_SAVE', note }) which triggers Note.save() → SQLite.
  - **Serialize full note content** 
  - When the synchronizer finds a changed note, it calls serializeForSync(), which serializes all syncable fields, including the complete note body snapshot. It then uploads that serialized item with PUT, or includes it in a batch request
  - If you make 100 edits between sync runs, they normally become one upload of the latest snapshot.
- The server parses the serialized item, extracts searchable/routing metadata, and writes the remaining current content to its configured database, filesystem, or S3 storage. It replaces the stored content rather than reconstructing it from patches
  - server records a small CREATE, UPDATE, or DELETE event containing identifiers, filename, type, timestamps, and sharing information, but not the note body
- External Editor (VS Code, Obsidian) → SQLite DB
  - When you use "Open in External Editor", Joplin temporarily exports the note to a file, watches it, and syncs back on change.
  - writeNoteToFile_(note) → /tmp/edit-{noteId}.md 

- Joplin does not replicate SQLite tables or execute row/column changes against the server database. It synchronizes a small set of logical item types, while substantial client state remains local.
  - The local SQLite database has ~30 tables, but only 7 entity types are syncable. Everything else is local-only infrastructure.
  - NOT every column of synced tables is synced either
  - There are row-level exceptions too. For example, local conflict notes with is_conflict = 1 are excluded from upload
- A few selected global values are synchronized specially through info.json, including E2EE configuration, master keys, note-lock key, public/private key data, sync version, and note-history settings. That is a small explicit object, not synchronization of the settings table.
  - The attachment download behavior setting (Always, Auto, or Manual) is also device-local and stored in the local settings file
- The server database also has a different schema: it stores generic Joplin items, ownership records, change events, and current item content rather than mirroring the client’s notes, folders, and other tables.

- when i get a new pc and open joplin and set sync target to the self-hosted server, how is data synced to the new pc?
  - Check sync target version (info.json on server)
  - Run migrations if needed (lock dir, temp dir, schema updates)
  - Fetch remote sync info (fetchSyncInfo) - gets E2EE state, PPK, etc.
  - Merge with local sync info (mergeSyncInfos)
  - Start normal sync from cursor = null (full sync)
  - attachment/Resource/blob download (if any) 
  - The first sync is a full download (cursor = null), subsequent syncs are incremental.
  - it fetches ALL changes, but with pagination & optimizations
  - Pagination: 200 Changes Per Request
  - Change Compression Reduces Volume
  - ~~"Delta with Items" Optimization: each delta page includes full item content~~ 
    - Joplin Server uses delta pagination + separate content fetches, not "Delta with Items.
    - Since the local note now has that timestamp, the client skips another content download.
  - Parallel Downloads via TaskQueue
  - Re-downloads on resume?  yes, Cursor saved after each page.  Cursor persisted to sync.{targetId}.context setting
    - If sync interrupts: Next sync resumes from last saved cursor, not from zero.
  - Blocks UI?  No, Background sync with progress updates
  - Heavy on server? Moderate - changes table indexed by user_id, counter 
  - Heavy on client? Local SQLite writes batched in transaction  
- When the client uploads changes, it sends the full content, not deltas
  - only filesystem-based targets (local, WebDAV, S3) embed jopItem
  - PostgreSQL items table (full content) + changes table (metadata only)
  - The server always has the latest full content after each sync.
  - Content fetch: Separate GET per item via download queue
- The server still has to scan the change records, so an enormous change table can make initial synchronization slower on the database/API side. 
  - Updates older than 180 days are periodically compacted, retaining only the latest old update per item.
- Attachments are separate from note text. Resource metadata is synchronized as an item, while the binary is stored under .resource/resource-id and downloaded separately. 
  - Attachment metadata is eagerly synchronized, but binary attachment files have a configurable download policy
  - Setting attachment download behavior to Auto or Manual can greatly reduce a new device’s initial download, but there is no equivalent lazy-download setting for note bodies.
- a very large note collection can produce significant network, SQLite writes, search-indexing CPU, and disk usage, especially on mobile. 
- Downloads are paginated and use a bounded task queue, with five concurrent connections by default, so the entire collection is not held in memory at once.

- 
- 
- 
- 
- 
- 

- Conflict Resolution
  - conflicts are detected and handled by clients, not Joplin Server.
  - strategy: Remote Wins + Preserve Local as Conflict Note
  - Each client stores a sync_time representing when its local item was last synchronized. Before uploading a locally modified item, the synchronizer obtains the current remote version and essentially checks: remote.updated_time > local last sync time
  - Remote content becomes the "current" note in DB (overwrites local changes in main note)
  - Local changes are saved as a CONFLICT NOTE in "Conflicts" notebook 
  - Metadata stored in conflict_note_states table
  - User manually resolves via UI: Merges changes, Deletes conflict note when done
  - Joplin does not currently perform an automatic three-way text merge, although it stores base/local/remote context that could support better merging later
- For non-note items, the behavior varies:
  - Resource binary conflicts preserve the local resource through a conflict attachment note.
  - Metadata-only differences may simply accept the remote version.
  - Other generic items generally take the remote version.
  - Remote deletion generally deletes the local version, subject to safeguards such as folder-child handling.

- Note History is also separate. Revisions are sync items containing text patches, normally created no more often than every ten minutes and retained for 90 days by default. 
  - These patches are for history restoration; they are not used by the server to construct the current note

- 
- 
- 
- 
- 

- The CLI (packages/app-cli/app/) is a full-featured client using the same @joplin/lib
  - joplin cat
  - joplin edit
  - joplin import/export
  - joplin sync
  - The CLI is not a second-class citizen - it's a full peer to Desktop/Mobile using the exact same @joplin/lib core

- 
- 
- 
- 
- 
- 

# docs
- [Joplin synchronisation ](https://joplinapp.org/help/dev/spec/sync/)
  - each device uploads its notes, notebooks, tags, etc. to the server, and also downloads any notes they do not have, or any recent changes.
  - Each entry in sync_items is scoped to a sync target (sync_target property), so theoretically it's possible to sync the same items to multiple sync targets.
  - 技术上支持同步到多个target， 但产品上未实现
# not-yet

# faq

## The initial sync is very slow, how can I speed it up?

- [Workaround for slow initial bulk sync after evernote import? - Support - Joplin Forum _201810](https://discourse.joplinapp.org/t/workaround-for-slow-initial-bulk-sync-after-evernote-import/746/1)
# changelog
- v2.13_202312
  - New plugins APIs
    - Note list
    - Imaging list
  - Rich Text Editor improvements
  - New beta Markdown editor based on CodeMirror 6
  - Improved ENEX import

- [v2.12_202307](https://github.com/laurent22/joplin/releases/tag/v2.12.1)
  - Support for Apple Silicon
  - addressed various bugs in the Rich Text editor
  - customize the read and write permissions for the notebooks you share
  - Choose to resize an image or not

- [v2.11_202303](https://github.com/laurent22/joplin/releases/tag/v2.11.1)
  - Add support for plugin user data
  - Auto-detect language on startup

- v2.10_202212
  - New design for "New note" and "New to-do" buttons
  - Android app is available in the Play Store

- [v2.10.3_20221231](https://github.com/laurent22/joplin/releases/tag/v2.10.3)
  - Switch license to AGPL-3.0 

- [v2.9_20221216](https://joplinapp.org/news/20221216-release-2-9)
  - Both the desktop and mobile application now support proxies
  - New PDF viewer
  - New mobile text editor
# more
