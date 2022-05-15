---
title: lib-editor-slate-dev
tags: [lib, slate, text-editor]
created: '2022-05-15T18:41:00.527Z'
modified: '2022-05-15T18:41:17.192Z'
---

# lib-editor-slate-dev

> A completely customizable framework for building rich text editors.

# guide
- features
  - First-class plugins. 
    - The most important part of Slate is that plugins are first-class entities. 
    - That means you can completely customize the editing experience, to build complex editors like Medium's or Dropbox's, without having to fight against the library's assumptions.
  - Schema-less core. 
    - Slate's core logic assumes very little about the schema of the data you'll be editing
  - Nested document model. 
    - The document model used for Slate is a nested, recursive tree, just like the DOM itself. 
    - This means that creating complex components like tables or nested block quotes are possible for advanced use cases.
  - Parallel to the DOM. 
    - Slate's data model is based on the DOM—the document is a nested tree, it uses selections and ranges, and it exposes all the standard event handlers. 
    - This means that advanced behaviors like tables or nested block quotes are possible.
  - Intuitive commands. 
    - Slate documents are edited using "commands"
    - This greatly increases your ability to reason about your code.
  - Collaboration-ready data model. 
    - The data model Slate uses—specifically how operations are applied to the document—has been designed to allow for collaborative editing to be layered on top
  - Clear "core" boundaries. 
    - With a plugin-first architecture, and a schema-less core, it becomes a lot clearer where the boundary is between "core" and "custom", which means that the core experience doesn't get bogged down in edge cases.

- slate-resources
  - https://docs.slatejs.org/
  - https://www.slatejs.org/examples/richtext

- slate /18.6kStar/MIT/202009/ts
  - https://github.com/ianstormtaylor/slate
  - https://docs.slatejs.org/general/changelog
  - a completely customizable framework for building rich text editors.
  - since v0.50.0(201911), slate codebase has had a complete overhaul(彻底检修)
    - The data model is now comprised of simple JSON objects.(old: Immutable.js data structures)
    - Plugins are now plain functions that augment the Editor object they receive and return it again.
    - The codebase now uses TypeScript. 
