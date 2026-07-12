---
title: pm-office-obsidian-quartz-docs
tags: [docs, quartz]
created: 2026-07-12T14:41:05.923Z
modified: 2026-07-12T14:41:14.911Z
---

# pm-office-obsidian-quartz-docs

# guide

# overview

# docs
- Wikilink matching is case-insensitive to mirror Obsidian: [[My Note]], [[my note]], and [[MY NOTE]] all resolve to the same file. The generated URL is lowercased (e.g. my-note).
# deployment
- Self-Hosting
  - Copy the public directory to your web server and configure it to serve the files. 
  - You can use any web server to host your site. 
  - Since Quartz generates links that do not include the .html extension, you need to let your web server know how to deal with it.

- Quartz emits CSS and JS files with content hashes in their filenames (e.g. index-a3f2c1b.css, component-7d4e2f.css). 
  - Since the filename changes whenever the content changes, these files can be cached indefinitely. 
  - HTML files should not be cached long-term since they reference the hashed filenames and need to stay fresh.
# more
