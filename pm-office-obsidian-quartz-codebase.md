---
title: pm-office-obsidian-quartz-codebase
tags: [codebase, quartz]
created: 2026-07-12T14:41:48.073Z
modified: 2026-07-12T14:41:57.129Z
---

# pm-office-obsidian-quartz-codebase

# guide

# overview

# markdown-pipeline

- what happens when running npx quartz build
  - ./quartz/bootstrap-cli.mjs parsing the command-line arguments using yargs
  - Transpiling and bundling the rest of Quartz (which is in Typescript) to regular JavaScript using esbuild
- Running the local preview server if --serve is set. 
  - starts a file watcher to detect source-code changes (e.g. anything that is .ts, .tsx, .scss, or packager files). On a change, we rebuild the module using esbuild’s rebuild API which drastically reduces the build times.
  - After transpiling the main Quartz build module (quartz/build.ts), we write it to a cache file .quartz-cache/transpiled-build.mjs and then dynamically import this using await import(cacheFile). 
  - In build.ts, we start processing content
  - Recursively glob all files in the content folder, respecting the .gitignore.
  - Quartz detects the number of threads available and chooses to spawn worker threads if there are >128 pieces of content to parse (rough heuristic) md files.
  - Each worker (or just the main thread if there is no concurrency) creates a unified parser based off of the plugins defined in the configuration.
  - Parsing has three steps: Read the file into a vfile, Applied plugin-defined text transformations over the content., Slugify the file path and store it in the data for the file. 
  - Markdown parsing using `remark-parse` (text to mdast).
  - Convert Markdown into HTML using remark-rehype (mdast to hast).
  - Apply plugin-defined HTML-to-HTML transformations.
  - Filter out unwanted content using plugins.
  - Emit files using plugins
  - hast-util-to-jsx-runtime with Preact
  - JSX is rendered to HTML using preact-render-to-string which statically renders the JSX to HTML 
  - CSS is minified and transformed using Lightning CSS
  - Scripts are split into beforeDOMLoaded and afterDOMLoaded and are inserted in the `<head> / <body>` respectively.
  - each emitter plugin is responsible for emitting and writing its own emitted files to disk.
- If the --serve flag was detected, we also set up another file watcher to detect content changes (only .md files). 
  - We keep a content map that tracks the parsed AST and plugin data for each slug and update this on file changes. Newly added or modified paths are rebuilt and added to the content map. 
  - Then, all the filters and emitters are run over the resulting content map. 
  - This file watcher is debounced with a threshold of 250ms. On success, we send a client refresh signal using the passed in callback function.
- Once the page is done loading, the page will then dispatch a custom synthetic browser event "nav". This is used so client-side scripts declared by components can ‘setup’ anything that requires access to the page DOM.
  - A separate "render" event can be dispatched when the DOM is updated in-place without a full navigation (e.g. after content decryption). 
  - Components that attach listeners to content elements should listen for both "nav" and "render".
# backend

# webapp
- Page frames control the inner HTML structure of each page. 
  - the frame determines how layout slots are arranged inside the page.
# plugins
- There are now four plugin categories:
  - Transformers: Map over content (parse frontmatter, generate descriptions, syntax highlighting)
  - Filters: Filter content (remove drafts, explicit publish)
  - Emitters: Reduce over content (generate RSS, sitemaps, alias redirects, OG images)
  - Page Types: Define how pages are rendered. Each page type handles a specific kind of page (content notes, folder listings, tag listings, 404). The PageTypeDispatcher emitter routes pages to the appropriate page type plugin based on the content.
  - Bases Views: Custom view renderers for the bases-page plugin’s database-like view system. Plugins can register new view types (e.g., timeline, kanban) via the ViewRegistry.  
- plugin types are not mutually exclusive — a single plugin can be a transformer AND provide components (e.g., obsidian-flavored-markdown), or be a page type AND provide custom frames (e.g., canvas-page).
# more
