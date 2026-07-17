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
  - 支持plugins，并提供了插件市场网站
  - 客户端丰富，支持win/linux/mac/android/ios/cli, 还提供Web Clipper
  - End To End Encryption (E2EE)
  - Note history (revisions)
  - Synchronisation with various services, including Nextcloud, Dropbox, WebDAV and OneDrive.
  - export支持导出 md+图片

- cons
  - 未实现web端
  - 同步基于文件，难以实现多页面的联动更新
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
# usage
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

- @joplin/server is a standalone Koa-based Node.js server
  - REST API for sync operations
  - User management, authentication (including SAML)
  - PostgreSQL or SQLite database
  - Docker deployment support
  - Admin UI (served via Mustache templates)
  - Can be self-hosted or use Joplin Cloud 🤔
- The server stores items in PostgreSQL (or SQLite for dev)
  - if updated_time > sync_time
- Conflict Resolution
  - strategy: Remote Wins + Preserve Local as Conflict Note
  - Remote content becomes the "current" note in DB (overwrites local changes in main note)
  - Local changes are saved as a CONFLICT NOTE in "Conflicts" notebook 
  - Metadata stored in conflict_note_states table
  - User manually resolves via UI: Merges changes, Deletes conflict note when done

- 🔄 Synchronizer.ts orchestrates bidirectional sync
  - Clients configure sync target as "Joplin Server" with URL + credentials
  - clients sync to various targets (Joplin Server, cloud services, filesystem)
  - Delta-sync with multiple backend drivers via FileApi interface
- How Local File Editing Syncs to DB (External Editor Feature)
  - When you use an external editor (VS Code, Typora, etc.), Joplin uses ExternalEditWatcher.ts with `chokidar` file watcher
- Joplin uses POLLING-based delta sync, NOT WebSocket/push
- Doc Sharing exists but is sync-based 而不是协作
  - ShareService.ts creates share records on server
  - Recipients sync normally → receive shared notebook on next delta sync
  - No real-time collaborative editing ( **no OT/CRDT, no live cursors** )
- UI Editing → SQLite DB (Source of Truth)
  - NO files are written to the filesystem when editing in the UI. The editor works entirely against the SQLite database.
  - The editor component (packages/app-desktop/gui/NoteEditor*.tsx) calls dispatch({ type: 'NOTE_SAVE', note }) which triggers Note.save() → SQLite.
- External Editor (VS Code, Obsidian) → SQLite DB
  - When you use "Open in External Editor", Joplin temporarily exports the note to a file, watches it, and syncs back on change.
  - writeNoteToFile_(note) → /tmp/edit-{noteId}.md 

- 
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
