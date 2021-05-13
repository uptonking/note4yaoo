---
title: lib-notebook-starboard-dev
tags: [notebook, starboard]
created: '2021-05-06T09:41:49.951Z'
modified: '2021-05-06T09:44:07.629Z'
---

# lib-notebook-starboard-dev

# guide

- features
  - Browser-native
  - Portable
  - Hackable
  - Works on mobile devices

# Overview

- https://github.com/gzuidhof/starboard-notebook
  - https://unpkg.com/starboard-notebook/dist/index.html
  - https://starboard.gg/
  - /633Star/MPLv2/202005/ts
  - In-browser literal notebook runtime used in Starboard.

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
- Starboard allows you to define your own cell types at runtime, which is how the plugin adds `Observable` cell support. 
  - Observable cells are all about reactivity, try changing the sliders below.
- Starboard is a base notebook runtime that runs entirely in the browser sandbox which can be extended dynamically.
- This plugin wouldn't be possible without the unofficial-observablehq-compiler package. This package provides an alternative implementation for the closed source compiler. (MIT licensed)

# [Starboard – Fully in-browser literate notebooks like Jupyter Notebook](https://news.ycombinator.com/item?id=24029002)

- Cell-by-cell notebooks like Jupyter are great for prototyping, explaining and exploration, but their dependence on a Python server (with often undocumented dependencies) limits their ability to be shared and remixed. 
  - Now that browsers support dynamic imports, it has become possible to create a similar workflow entirely in the browser.
  - That motivated me to build Starboard Notebook, a tool I wished existed

* Run entirely in the browser, there is no server or setup, it's all static files.
* Web-native, so no widget system is necessary. There is nearly no magic, it's all web tech (HTML, CSS, JS).
* Stores as a plaintext file, it will play nicely with version control systems.
* Hackable: the sandbox that your code gets run in contains the editor itself, so you can metaprogram the editor itself (e.g. adding support for other languages such as Python through WASM).
* You can import any code that targets the browser directly (e.g. puts stuff on the window object), or that has exports in ES module format.

- discussion

- I worked on a similar project
  - It's half abandoned now. 
  - one issue of js based notebook is the missing of a file system. 
  - data scientists load huge data into notebooks, this is hard to do on the web. 
  - There is the new web filesystem api, but that only helps load local files.
- [我为什么要做Epiphany](https://epiphany.pub/@shi-yan/wo-wei-shen-me-yao-zuo-epiphany)
- 我们做了Epiphany，我们心目中未来的交互式内容平台。特点:
  - 用Markdown格式书写，支持数学公式。
  - 可以嵌入交互式程序。目前支持Javascript和Python。未来会支持更多语言。
  - 一套通用的API，可以绘制图像，打印输出和创建UI与读者互动。
  - 拥有类似Github的版本管理系统，可以合作内容。
  - 支持众筹式的出版。
- 最近的两个类似平台observable和iodide都不约而同地选择了利用web技术。
  - https://github.com/iodide-project/iodide
    - /inactive
- My vision is for this to be handled by things like remoteStorage, Solid, or (if you must) Google Drive. 
  - I find having control over your data and delegating access to various apps to be a nice flow when implemented well
  - It's not a silver bullet. For larger data you can't afford to download it every time. 

