---
title: lib-editor-rich-outline-latest-roadmap
tags: [outline-wiki, roadmap]
created: 2021-09-09T18:31:22.314Z
modified: 2021-09-09T18:31:39.852Z
---

# lib-editor-rich-outline-latest-roadmap

# guide

# roadmap for outline
- 文章内容存储到数据库的格式是文本字符串，参考payloadcms保存json
# changelog for outline
- changes
  - [changelog](https://www.getoutline.com/changelog)

- [202003 - Adopt BSL 1.1 license](https://github.com/outline/outline/pull/1197)
  - v0.40.1_202002, BSD
  - v0.40.2_202002, NA202303
  - v0.43.0_202005, NA202305, ✨ 在20200523将编辑器迁移到v10-prosemirror，但未添加失效日期
  - v0.44.0_202007, NA202307, 在v0.45.0里面才添加失效日期
  - v0.47.1_202209, NA202309，将编辑器升级到v11，但变化不大
  - v0.48.1_202009, NA20230926, ✨ 集中修复bug， Added support for importing html and docx files
  - v0.49.0_202010, NA202310, Importing ".doc" files exported from Confluence is now supported，协作初步demo但不在源码
  - v0.50.0_202011, NA202311, [Sessions are now synced across browser tabs](https://github.com/outline/outline/releases/tag/v0.50.0)
  - v0.51.0_202012, NA202312, [the first community translation，git发版记录](https://github.com/outline/outline/tags?after=v0.57.0)
  - v0.55.0_202104, NA202404， pluggable authentication, Collection Permissions & Viewers
    - https://github.com/outline/outline/tree/v0.55.0/LICENSE
  - v0.59.0_202109, NA202509, Generic OIDC authentication provider; history侧边栏能显示修改、移动、删除
    - https://github.com/outline/outline/tree/v0.59.0/LICENSE
  - v0.60.0_202111, NA202511, ✨🔀 支持collab
  - v0.61.0_202111, NA202511, Move to Typescript
  - v0.62.1-202203, NA202603, Move editor into codebase
  - v0.63.0-202204, NA202604, editor now supports file attachments
    - added search to publicly shared documents
    - Empty documents are now cleaned up automatically 
  - v0.64.0-202205, NA202605, New TLDraw, Otter.ai, Gliffy, JSFiddle, and Scribe embed
    - improvements for large documents with collaborative editing enabled
  - v0.65.0-202207, NA202607, full support for outgoing Webhooks so you can integrate Outline with other tools
    - Mermaid diagrams in the editor
    - ability to setup multiple authentication providers
  - v0.66.0-202209, NA202609, possible to subscribe to a document without editing it
    - Added support for Grist embeds
    - Viewers can now be upgraded to editors on individual collections or groups
  - v0.67.0-202211, NA202611, As of this release all documents edits are sent through the collaborative process using websockets
    - Add HTML export 
    - Show diff when navigating revision history
  - v0.68.0-202302, NA202702, New document publish flow allows choosing a location after creating a draft 
    - Duplicated docs are now created as unpublished drafts 
    - Added import/export of documents as JSON
  - v0.69.0-202304, NA202704, Commenting and mentions
    - Database migrations are now run automatically
    - Image resize operations can now now be undone
  - v0.70.0-202307, NA202707, Allow embeds to be used inside tables
    - Commenting outside of edit mode is now possible
    - Use `umzug` to autorun migrations 
  - v0.71.0-202308, NA202708, Find and replace now available
    - Added support for rich hover cards for external links using Iframely
    - Added support self hosted Grist
  - v0.72.0-202310, NA202710, Local file system storage is now available as an alternative to Minio/S3
    - emoji picker
    - Embedding videos is now possible 
    - [File storage ](https://docs.getoutline.com/s/hosting/doc/file-storage-N4M0T6Ypu7)
      - If you would like to store file uploads on the same server that Outline is running from then you can do so using the local file system storage option.
  - v0.75.0-202402, NA202802, a rebuild of the internal permissions in order to support inviting users to individual documents, a complete redesign of the Share menu on documents
    - introduced AI Answers in cloud-hosted Outline
    - Embeds are now rendered within HTML and PDF exports
    - include drafts in search results
    - possible to replace a file attachment inline
  - v0.77.0-202404, NA202804, changes how documents are rendered, allowing the introduction of new editor functionality and attributes
    - big improvements to tables: Column resizing, Toggleable headers, scroll horizontally
  - v0.78.0-202409, NA202809, add groups directly to documents, all members of the group will receive access to the document
  - v0.82.0-202502, NA202902, Editor embeds are now vertically resizable
  - v1.0.0-202510, NA202910, 
    - https://github.com/outline/outline/releases/tag/v1.0.0
    - image lightbox has improved again with added support for zooming and panning of images.
    - A new display mode for URL's in documents, which shows a mention-style chip instead of a full URL preview. 
    - mention groups in documents and comments 
    - Permanent deletion of documents is now restricted to admins only

- 
- 
- 
- 
- 
- 

- 📕 202512 - [PDF embeds ](https://www.getoutline.com/changelog/pdf-embeds)

- 202511 - [Popular documents ](https://www.getoutline.com/changelog/popular-documents)

- 202509 - [New lightbox ](https://www.getoutline.com/changelog/new-lightbox)

- 202504 - [Collection subscriptions ](https://www.getoutline.com/changelog/collection-subscriptions)

- 🔗 202501 - [Document mentions _202501](https://www.getoutline.com/changelog/document-mentions)
  - mention documents using the @ trigger

- 202408 - [Comment resolving ](https://www.getoutline.com/changelog/comment-resolution)

- 202404 - [GitHub integration ](https://www.getoutline.com/changelog/github-integration)

- 👥  202402 - [Document sharing and permissions ](https://www.getoutline.com/changelog/document-permissions)

- 👾 202401 - [AI answers ](https://www.getoutline.com/changelog/ai-answers)

- 202310 - [Embedded videos ](https://www.getoutline.com/changelog/embedded-videos)

- 🔍 202308 - [Find and replace ](https://www.getoutline.com/changelog/find-and-replace)

- 202307 - [Link hover previews ](https://www.getoutline.com/changelog/link-previews)

- 202305 - [In app notifications ](https://www.getoutline.com/changelog/in-app-notifications)

- 💬 202303 - [Commenting ](https://www.getoutline.com/changelog/commenting)

- 202302 - [Windows Desktop App ](https://www.getoutline.com/changelog/windows-app)

- 202302 - [JSON Import / Export](https://www.getoutline.com/changelog/json-export)
  - useful for migrating data between Outline instances

- 📕 202301 - [PDF & HTML export ](https://www.getoutline.com/changelog/pdf-html-export)
  - [Improved PDF exports _202312](https://www.getoutline.com/changelog/exporting-improvements)
  - [New Images Layout ](https://www.getoutline.com/changelog/edge-to-edge-images): full-width
  - [A new publishing flow ](https://www.getoutline.com/changelog/publish-improvements): Before this update, you had to choose the location for a document before creating it. you can create a document first and then choose where it will live in your knowledge base.

- 🍎 202212 - macOS Desktop App

- 202210 - Multiple workspaces

- 202209 - Visualizing document history
  - [feat: Show diff when navigating revision history](https://github.com/outline/outline/pull/4069)
  - document update notifications without having to open it

- 20220531 - [May fixes and improvements ](https://www.getoutline.com/changelog/may-fixes)
  - Lots of backend performance improvements to improve loading speeds
  - When importing a document a revision is now written immediately so that it can be restored to the imported state
  - Links with in-page anchors are no longer broken when a document is renamed
  - Emoji's and embeds are now copied to the clipboard correctly when copying document text
  - Improved search indexing for publicy shared documents

- 202204 - embed support JSFiddle, Gliffy, Otter.ai, tldraw
  - Shared documents now include search

- 202203 - [file attachments in documents](https://www.getoutline.com/changelog/file-attachments)
  - Move editor into codebase

- ✏️ 202201 - [v0.62.1, Move editor into codebase](https://github.com/outline/outline/pull/2930)

- ⤴️ 202111 - [v0.61.0, Move to Typescript](https://github.com/outline/outline/pull/2783)

- 202111 - [v0.60.0, NA202511](https://github.com/outline/outline/releases/tag/v0.60.0)
  - We're excited to include the first beta of collaborative editing in this release.
  - [Store CRDT snapshots with revisions](https://github.com/outline/outline/pull/2698)

- 🔀 202109 - [Collaborative Editing Beta](https://www.getoutline.com/changelog/collaborative-editing)

- 202108 - [v0.58.0](https://github.com/outline/outline/releases/tag/v0.58.0)
  - Headings in editor are now collapsible
  - Added process concurrency (defaults to number of CPU cores)

- 202104 - [v0.55.0](https://github.com/outline/outline/releases/tag/v0.55.0)
  - Collection permissions now include the ability to make a collection read-only by default

- 🔒 202103 - [v0.54.0](https://github.com/outline/outline/releases/tag/v0.54.0)
  - converting authentication to a new pluggable system and a new database schema to support future changes.

- 202102 - brings PWA support to Outline, allowing you to install the app to your desktop

- 202101 - v0.52.0
  - Document delete confirmation now shows an option to archive 
  - Deleting a document no longer deletes it's attachments if they have been copied into other documents
  - Google Drive embeds are now supported

- 202012 - [year in Review](https://www.getoutline.com/changelog/2020-in-review)
  - a new editor, completely rewritten using prosemirror
  - dropping the initial download size of the entire application by more than 2Mb’s to ensure the app loads incredibly fast and documents load in milliseconds.
  - notice blocks, and rich embeds like Google Slides – plus a /slash menu for quickly performing actions with only the keyboard
  - Permissions + access
  - Shared templates

- 202011 - [v0.50.0, NA202311](https://github.com/outline/outline/releases/tag/v0.50.0)
  - Sessions are now synced across browser tabs, logging in or out in one tab will be reflected in others. 
  - Table of contents is now displayed on publicly shared docs by default
  - Awkward scroll behavior when caret is moved at the end of a header
  - [chore: Refactor backlinks and revisions_20201028](https://github.com/outline/outline/pull/1611)

- 202009 - Import from Microsoft Word, confluence
  - The last two weeks we've been focused on bug fixing, performance and reliability. 
  - the initial javascript bundle download size, which has now dropped from 2.8Mb to just 700Kb.

- 202008 - [Document templates are here](https://www.getoutline.com/changelog/document-templates)

- ✏️ 202005 - [v0.43.0 将编辑器迁移到v10](https://www.getoutline.com/changelog/v0.43.0)
  - a new editor, completely rewritten using prosemirror

## v0.0.x early-versions

- [feat: Backlinks__201907](https://github.com/outline/outline/pull/979)
  - Adds support for references/backlinks that will be displayed at the bottom of referenced documents.
  - New Backlink model, database table, and service
# changelog for rich-markdown-editor

## [v11.0.0__20200927](https://github.com/outline/rich-markdown-editor/releases/tag/v11.0.0)

- styled-components is now a peer dependency, make sure your host app has it included in package.json
- Pasting a url will now always auto link

## [v10.0.0__20200519](https://github.com/outline/rich-markdown-editor/releases/tag/v10.0.0)

- v10.0.0 is a complete rewrite of the editor. 
  - It is incompatible with v9.0.0 and moves from using Slate to Prosemirror
  - [Migrate to Prosemirror](https://github.com/outline/rich-markdown-editor/issues/134)

- [Convert from slate to Prosemirror_202005.v10.0.0](https://github.com/outline/rich-markdown-editor/pull/150)
