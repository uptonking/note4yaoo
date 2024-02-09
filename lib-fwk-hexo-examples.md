---
title: lib-fwk-hexo-examples
tags: [examples, hexo, static-site-generator]
created: 2024-02-09T10:54:47.417Z
modified: 2024-02-09T10:55:03.085Z
---

# lib-fwk-hexo-examples

# guide

# popular
- https://github.com/jaredly/hexo-admin /201806/js/inactive
  - https://jaredforsyth.com/hexo-admin/admin/
  - An admin UI for the Hexo blog engine. Based off of the Ghost interface, with inspiration from svbtle and prose.io.
  - I haven't used Hexo in several years
  - 支持编辑

- https://github.com/Qexo/Qexo /GPLv3/202402/python
  - 一个快速、强大、漂亮的在线 Hexo 编辑器
  - 开放 API

- https://github.com/tajpure/hexo-editor /201808/js/inactive
  - https://github.com/tajpure/hexo-editor/wiki/Getting-Started
  - a web editor for hexo blog platform. You can use it to edit, generate and deploy posts over the web. 
  - This editor will auto save your post to the server by TextSync.
  - https://github.com/tajpure/TextSync /201606/js/inactive
    - Synchronize text from client to server based on the rsync algorithm

- https://github.com/wzpan/hexo-generator-search /MIT/202111/js/inactive
  - This plugin is used for generating a xml/json file from your Hexo blog that provides data for searching.
  - Generate search data for Hexo 3.x and 4.x. 
  - This plugin is used for generating a search index file, which contains all the necessary data of your articles that you can use to write a local search engine for your blog. Supports both XML and JSON format output.
  - If you don't want to write search engine by yourself, there are many themes that take use this plugin for local searching that works out of box.
# themes
- https://github.com/kaiiiz/hexo-theme-book /MIT/202010/js/inactive
  - https://kaiiiz.github.io/hexo-theme-book-demo/
  - book-like hexo theme with some useful features.
  - 效果类似docusaurus

- https://github.com/objchris/hexo-theme-bookcase /MIT/202001/js/inactive
  - https://objchris.com/hexo-theme-bookcase/
  - A clean, Gitbook style theme for HEXO.

- https://github.com/HiNinoJay/hexo-theme-A4 /MIT/202401/js
  - https://ninojay.top/
  - 模仿A4纸张的一个hexo极简主题。主打一个简洁，体积小，配置少。

- https://github.com/zalando-incubator/hexo-theme-doc /MIT/201903/js
  - https://zalando-incubator.github.io/hexo-theme-doc
  - A documentation theme for Hexo

- https://github.com/PhosphorW/hexo-theme-academia /MIT/202005/js
  - https://phosphorw.github.io/
  - light & simple & responsive page for academic websites on Hexo

- https://github.com/iTimeTraveler/hexo-theme-hipaper /MIT/202011/js
  - https://itimetraveler.github.io/hexo-theme-hipaper/
  - A fashional newspaper theme for Hexo

- https://github.com/iissnan/hexo-theme-next /MIT/201801/js
  - http://notes.iissnan.com/
  - Elegant theme for Hexo
- https://github.com/theme-next/hexo-theme-next /AGPLv3/202107/js
  - https://theme-next.org/
  - Elegant and powerful theme for Hexo
# examples

# plugins

- https://github.com/hexojs/hexo-renderer-marked /MIT/202312/js
  - This plugin uses marked as its render engine.
  - By default, this plugin contains a potential security issue: It is possible to inject Markdown containing Unsafe HTML that will not be sanitized
  - solution is to migrate to `hexo-renderer-markdown-it` which is safe by default and does not suffer from the same limitations
- https://github.com/hexojs/hexo-renderer-markdown-it /MIT/202401/js
  - This renderer plugin uses Markdown-it as a render engine on Hexo
  - Support for Markdown, GFM and CommonMark

- https://github.com/hexojs/hexo-math /MIT/202008/js
  - A hexo plugin that uses MathJax to render math equations.
  - Embed `KaTeX` and `MathJax` in Hexo post/page via tag plugins. 
  - Equations are rendered in Hexo (server-side), so browser-side javascript library is not needed and should be removed.
  - hexo-math uses tag plugin approach due to minor incompatibility between LaTeX and marked, the default markdown renderer of Hexo (via hexo-renderer-marked).
- https://github.com/next-theme/hexo-filter-mathjax /MIT/202211/js/inactive
  - Server side MathJax Renderer Plugin for Hexo.
# utils

# more
