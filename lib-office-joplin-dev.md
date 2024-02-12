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
  - 支持plugins
  - 客户端丰富，支持win/linux/mac/android/ios, 还提供Web Clipper
  - End To End Encryption (E2EE)
  - Note history (revisions)
  - Synchronisation with various services, including Nextcloud, Dropbox, WebDAV and OneDrive.

- cons
  - 未实现web端

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

# codebase

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
