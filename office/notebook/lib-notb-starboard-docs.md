---
title: lib-notb-starboard-docs
tags: [docs, starboard]
created: 2021-05-13T04:11:12.966Z
modified: 2024-06-30T03:20:05.773Z
---

# lib-notb-starboard-docs

# guide

# overview
- Starboard Notebook /889Star/MPLv2/202206/ts
  - https://github.com/gzuidhof/starboard-notebook
  - https://unpkg.com/starboard-notebook/dist/index.html
  - https://starboard.gg/
  - In-browser literal notebook runtime used in Starboard.
  - 编辑器已分离，基于rich-markdown-editor和prosemirror
  - 前端基于lit
# [About Why Starboard is worth building](https://starboard.gg/about)
- Starboard's unique design decisions
  - Browser-native: 
    - there is no bridge required between the server and the browser like in Jupyter notebook as everything is in-browser. 
  - Zero-setup: 
    - there is zero setup and you don't need a server running to serve your notebook. 
    - Everything is a static file.
  - Portable: 
    - Starboard notebooks are stored on disk as plaintext files for maximum portability. 
  - Hackable: 
    - Different than any other notebook system the Starboard editor itself runs inside the sandbox. 
    - The code you write in the notebook can alter the notebook itself: 
    - you can dynamically create new cell types, change the CSS styles, or anything really.

- Starboard vs Starboard Notebook
  - Starboard Notebook is the actual notebook runtime with the editor (the code cells, outputs and buttons).
  - This website, Starboard, embeds this editor and allows you to save and share notebooks (allowing you to share by just a link) and will in the future have some social features (stars, upvotes, followers, ...). Think of it as a publishing platform for your notebooks.
  - A somewhat correct analogy: If Starboard was GitHub, Starboard Notebook would be Git.
# [An Open Source ObservableHQ notebook environment](https://starboard.gg/gz/open-source-observablehq-nfwK2VA)
- Large parts of Observable are open source, but not everything. 
  - In particular the editor and compiler are closed which means that you have to use the ObservableHQ web app to author notebooks. 
  - You can however embed the resulting notebook on your own website.
- Starboard is an open source in-browser notebook system. 
  - Think Jupyter Notebook but re-imagined for the browser.
- This notebook showcases a plugin for Starboard that allows you to use reactive cells just like you would in Observable.
- Starboard allows you to define your own cell types at runtime, which is how the plugin adds `Observable` cell support. 
- Starboard is by no means a replacement for everything that ObservableHQ has to offer, 
  - and it will never be, 
  - but being able to leverage its powerful reactive paradigm in a completely self-hosted setup can be really useful.
- Starboard is a base notebook runtime that runs entirely in the browser sandbox which can be extended dynamically.
- This plugin wouldn't be possible without the unofficial-observablehq-compiler package. 
  - This package provides an alternative implementation for the closed source compiler. (MIT licensed)
