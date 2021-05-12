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

# [An Open Source ObservableHQ notebook environment](https://starboard.gg/gz/open-source-observablehq-nfwK2VA)

- Large parts of Observable are open source, but not everything. 
  - In particular the editor and compiler are closed which means that you have to use the ObservableHQ web app to author notebooks. 
  - You can however embed the resulting notebook on your own website.

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
