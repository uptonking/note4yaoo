---
title: lib-office-notable-docs
tags: [docs, notable]
created: 2024-01-29T23:07:25.687Z
modified: 2024-01-29T23:07:40.193Z
---

# lib-office-notable-docs

# guide

# [changelog](https://github.com/notable/notable/releases)
- v1.8.4_2020-01-22
  - Bundling OS-specific dependencies only when needed
  - Ensuring both creation date and modification date are updated when duplicating a note

- v1.8.0_2019-11-07
  - Upgraded Electron to v7
  - Rewritten “Select Data Directory...” window as a modal window

- v1.7.0_2019-08-10
  - Added support for adding image attachments via copy and paste
  - Added support for writing footnotes
  - Added support for importing HTML notes

- v1.6.0_2019-07-09
  - Added support for linking to search queries
  - Using natural sorting

- v1.5.0_2019-05-12
  - Added context menu actions for copying attachments/tags/notes names
  - Upgraded to Electron v5
  - Markdown: improved stripping of headers, emojis, images, links, wikilinks and todos

- v1.4.0_2019-03-15
  - 💰 Switched to the AGPL license
  - Added a “Toggle Sidebar” menu entry
  - Search: added a button for clearing the input
  - Replaced CodeMirror with Monaco

- v1.3.0_2019-01-31
  - Added Wiki-style links supports
  - Added support for linking to attachments from `source` elements

- v1.2.0_2019-01-25
  - Added “Undo” and “Redo” to the menu
  - Added basic support for range selection when holding shift key
  - Added a Split-View mode

- v1.1.0_2019-01-04
  - Added KaTeX support
  - Added support for double-click to collapse/expand tags
  - Search: searching notes contents (non fuzzly) too

- v1.0.1_2018-12-27
  - Multi-Editor: improved confirmation messages for adding/removing tags
  - Tagbox: ensuring their never share the same name
  - Tags: updating the tree instead of completely rebuilding it, O(n) -> O(1)
  - Ensuring the special “Tags” tag is collapsible too

- v1.0.0_2018-12-22
  - 支持win/linux/mac
# docs
- The data directory is where all your notes and attachments will be stored
  - You can edit your notes/attachments without even using Notable
  - you could also import a Markdown note simply by copying it into the `notes` directory.
- The sidebar is where all your notes are categorized.
  - All Notes: contains all notes
  - Favorites: fixed menu    
  - Tags: all notes tagged with any tag except the special ones: `Notebooks/*` and `Templates/*`
      - You can create sub-categories in the following sections: Notebooks, Tags and Templates by using nested tags. 
  - Untagged: notes that have no tags
  - Trash: notes that have been deleted. 
      - These notes won't be displayed in any other category.
  - Notebooks: notes tagged with the special `Notebooks/*` tag
  - Templates: notes tagged with the special `Templates/*` tag. 
      - These notes won't be displayed in any other category.
- The middlebar shows you all notes contained in the currently active category
  - title of notes is searched in fuzzily
  - content of notes is searched in full-match
  - order by title/modified
  - Pinned notes are displayed before the others.
- The mainbar is where you can preview and edit the currently active note
  - The toolbar contains buttons for triggering actions to the current note
- Edit the markdown notes with Monaco Editor
  - a button in the toolbar for opening the current note in the default Markdown editor
  - When 2 or more notes are selected a multi-note editor will be displayed in the mainbar
- Notes are written in GitHub-flavored Markdown
  - Notes can have some metadata: fav/tags
  - syntax features: GFM, KaTex, AsciiMath, mermaid
  - attachments: simply copied into `attachments` sub-directory
- Tags are useful for better categorization
  - Root tags don't contain any forward slash ( `/` )
  - Tags can also be nested like a path
  - tag starting with `Notebooks/` will show in Notebooks section
  - tag starting with `Templates/` will only show in Templates section
- Shortcuts
  - NoteApp/Editor/Nav/Other
- Importing
  - Markdown files: `md`/`mkd`/`mdwn`/`mdown` /`markdown`/`markdn`/`mdtxt`/`mdtext`/`txt`
  - Evernotes' exports with extension: `enex`
  - Alternatively you could also just put your Markdown notes into the `notes` sub-directory 
  - Newly imported tags will be tagged with a special `Import-XXXX` tag
- Multi-Note Editing
  - When 2 or more notes are selected a multi-note editor will be displayed in the mainbar
  - fav/pin/trash/tag/
- Linking Attachments/Notes/Tags
  - Attachments can be rendered inline, linked to, and linked to via a button
      - The `@attachment` token is used for this
  - Notes can be linked to, and linked to via a button. 
      - The `@note` token is used for this. 
      - Wiki-style links are supported too.
  - Tags can be linked to, and linked to via a button. 
      - The `@tag` token is used for this.
- Synchronization
  - third-party service will take care of the synchronization
- Mobile Editing
  - third-party apps for editing Markdown files
  - if you need to change some metadata or add an attachment, but it would be ok most of the times
- Collaborative Editing
  - not planned
- Version Control
  - not planned
- Encrypted Notes
  - third-party program will take care of the encryption
