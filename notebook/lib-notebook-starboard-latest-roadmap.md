---
title: lib-notebook-starboard-latest-roadmap
tags: [roadmap, starboard]
created: 2021-05-13T04:31:31.783Z
modified: 2021-05-13T04:32:00.516Z
---

# lib-notebook-starboard-latest-roadmap

# guide

# [changelog](https://github.com/gzuidhof/starboard-notebook/blob/master/CHANGELOG.md)

- 0.9.0-202105
  - The iframe now resizes to at least be able to show dropdown menus.
  - Update to Bootstrap version 5.0.0.
  - Update to Monaco version 0.23.0.
- 0.8.0-202103
  - Markdown cells now have their own WYSIWYG editor (as well as a plaintext editor for advanced users).
  - A newly inserted cell now defaults to Markdown instead of Javascript when no cells are present.
  - Clicking anywhere outside of a markdown cell stops its edit mode.
- 0.7.20-202103
  - Introduce ProseMirror as the default editor for Markdown content. 
    - Note that it isn't enabled yet for Markdown editors by default, it still needs some love (in particular it needs KaTeX support)
    - StarboardContentEditor element is exposed in the exports for plugins to use.
- 0.7.0-202011
  - This update features a large style rework - the notebook's actual content is now capped in width. 
  - The global styles are now more easily changed through CSS custom variables properties.
  - Added emoji support in Markdown
- 0.6.0-202010
  - update starboard-notebook switches to a new format which is more similar to Jupytext's formats.
  - The old format still works (but will be phased out) 
  - A cell's properties are now nested under cell.metadata.properties instead of cell.properties.
- 0.5.2-202010
  - CodeMirror is now the default editor which loads without user input.
  - The chosen editor is now persisted (in LocalStorage).
  - Enable Python support in standalone notebooks.
- 0.4.0-202008
  - A large refactor: 
    - Starboard Notebook is now built around a single Runtime that allows for metaprogramming and plugin support. 
    - This is a single source of truth for the state and functionality of a notebook. It is exposed as a global variable `runtime`.
- 0.2.2-202008
  - first post
