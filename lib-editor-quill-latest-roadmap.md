---
title: lib-editor-quill-latest-roadmap
tags: [quill, roadmap]
created: 2023-11-27T20:19:34.667Z
modified: 2023-11-27T20:19:50.947Z
---

# lib-editor-quill-latest-roadmap

# guide

- changes
  - quill很久未更新了，v1.3.7和v2都最后更新在202004
# roadmap
- [The State of Quill and 2.0_201709](https://medium.com/@jhchen/the-state-of-quill-and-2-0-fb38db7a59b9)
  - Historically, major software releases have focused on technical developments and new features. Quill’s 2.0 release, however, will also prioritize supporting activities.
  - With early adopters proving out several uses cases and providing more confidence in Parchment’s API, we can move from making sure our aim is possible towards making them easy for the wider audience.
  - Tables are coming.
  - Quill has been designed with a modular architecture. Themes has also been underdeveloped
  - Adopting New Web Features. One example is using `event.key` to more easily add keyboard shortcuts
# changelog

## v2.0

- [v2.0.0_20240417](https://github.com/quilljs/quill/releases/tag/v2.0.0)
  - Quill is now a valid ESM package for better ecosystem (e.g. bundlers) and tree-shaking support
  - Migrated to TypeScript
  - Nested Quill support: adds the OT ability for table format and also supports nested scrolls
  - Improved IME and spell corrector using input event instead of MutationObserver
  - Auto detect scrolling container
  - Semantic cleanups for TEXT_CHANGE event to generate better delta diff
  - History: Record selection in history module
  - Clipboard: Improve support for pasting from Google Docs and Microsoft Word
  - 2.0 includes many performance optimizations, the most important of which is the improved rendering speed for large content

- [v2.0.0-beta.0_2023-12-08](https://github.com/quilljs/quill/releases/tag/v2.0.0-beta.0)
  - Quill has been significantly modernized. 
  - Leveraging the latest browser-supported APIs, Quill now delivers a more efficient and reliable editing experience.
  - Nested Quill support
  - Improved IME and spell corrector support
  - History: Record selection in history module
  - Auto detect scrolling container
  - Quill 2.0 includes many performance optimizations, the most important of which is the improved rendering speed for large content.

## v1.0

- v1.3.7_2019-09-09
  - Security related bug fixes.
# more

# discuss

- ## 

- ## 

- ## [is there any plan for quilljs2.0 _202004](https://github.com/zenoamaro/react-quill/issues/601)
- Chrome is going to stop supporting mutation events that are in quill 1.3.7 on July 30 2024
