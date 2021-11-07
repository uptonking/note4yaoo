---
title: lib-editor-ckeditor5-docs-latest-changelog
tags: [changelog, ckeditor, docs]
created: '2021-10-29T16:09:08.817Z'
modified: '2021-10-29T16:09:36.091Z'
---

# lib-editor-ckeditor5-docs-latest-changelog

# guide

- [Collaboration features release notes](https://ckeditor.com/collaboration/changelog/)
# [changelog](https://github.com/ckeditor/ckeditor5/blob/master/CHANGELOG.md)

## v31.0.0__202110

- Introduce the `Command#affectsData` property to indicate whether a given command should stay enabled in editor modes with restricted write permissions. 
- The mentions feature has gained the ability to customize the max number of items in the list

- InsertHtmlEmbedCommand and UpdateHtmlEmbedCommand have been replaced by `HtmlEmbedCommand`

- New collaboration features samples are available:
  - For the React integration that will implement the context feature, as well as the watchdog.

## v30.0.0__202109

- Cut down the search time in the Find & replace feature
- config.toolbar.viewportTopOffset property was moved to `config.ui.viewportOffset` and it now accepts an object.
- toWidgetEditable() will now set highlight handling for the editable element.

## v29.0.0__202107

> Image plugin works as a glue for both the ImageBlock and ImageInline features now

- Support for inline images in the image feature, allowing to insert multiple images in a single content block.
- The find and replace feature.
- The source editing feature for classic editor with the ability to directly edit the HTML or Markdown content.
- Remembering the language when creating a new code block.

## v28.0.0__202105

- All the packages use multiple exports instead of one object in the src/index.js file. 
- add captions to tables
-  new `allowChildren` property for the data schema item definition.
- The export to PDF and export to Word features are now enabled in the read-only mode.

## v27.0.0__202103

- Support for drag and dropping of textual content and block objects (like images and tables) within the editor.
- Support for bubbling of view. Document events.

## v25.0.0__202101

- ui: Configuration passed to ToolbarView.fillFromConfig() will be stripped off of any leading, trailing, and duplicated separators ('|' and '-').

## v23.0.0__202009

- This release brings the new pagination feature.
- In order to use the "insert image via URL" feature you now need to load the `ImageInsert` instead of `imageUpload`

- v23.1.0
  - The new `data-cke-ignore-events` attribute in view element that prevents CKEditor from handling events fired in this element.
  - The new `triggerBy` option that triggers element re-render.

## v20.0.0__202006

> ckeditor5: Node >=12.0.0 is required now.

- Typing around widgets.
- Support for linking images.

## v17.0.0__202002

- introduces support for styling tables and table cells as well as a new special characters picker feature.
- added support for editor contexts
- introduced an extensible system for parsing and normalizing CSS properties which main goal was to make the editor better pick up certain style names in pasted/loaded content.

## v16.0.0__201912

- introduces one of the most community-requested features: code blocks. 
- We included a new restricted editing plugin, too.

## v15.0.0__201910

- introduces support for inserting horizontal lines, page breaks and SVG images into the WYSIWYG editor. 

- From other news, we changed the versioning policy. 
  - Now, all packages will have the same major version, hence, we needed to release this one as v15.0.0 
  - (we skipped versions 13.0.0 and 14.0.0). 

## v12.0.0__201902

- introduces a new editor (called "Balloon block editor"), the editor content placeholder and support for inline widgets

## v11.0.0__201807

- introduces two new plugins (autosave and block toolbar)

- v11.1.0 brings the long-awaited media embed feature, support for block content in tables, tables available in real-time collaboration

## v10.0.0__201804

> The first stable release of CKEditor 5

- We decided to skip version numbers lower than v5.0.0 to avoid collisions with CKEditor 3-4.
- The license under which CKEditor 5 is released has been changed from a triple GPL, LGPL and MPL license to a GPL2+ only. 

## v1.0.0-beta.4__201804

- two new plugins were introduced – ParagraphButtonUI and HeadingButtonsUI which make it possible to replace the headings dropdown with separate buttons for each heading level.
- The 1.0.0-beta.3 version number was skipped in order to align the project version number which diverged from builds version numbers

## v1.0.0-alpha.1__201710

- New packages: @ckeditor/ckeditor5-easy-image: v1.0.0-alpha.1

## v0.8.0__201703

- New packages: @ckeditor/ckeditor5-presets: v0.1.1
