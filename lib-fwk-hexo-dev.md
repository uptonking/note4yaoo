---
title: lib-fwk-hexo-dev
tags: [hexo, static-site-generator]
created: 2024-02-09T10:53:01.641Z
modified: 2024-02-09T10:53:39.813Z
---

# lib-fwk-hexo-dev

# guide
- pros
  - Hundreds of themes & plugins
  - 基于ssr/ssg，seo友好, 生成的产物是多页应用MPA，加载比SPA快
  - 不依赖前端框架如react

- cons
  - hexo(nodejs)比hugo(go)慢
  - 每次更新内容后需要全量rebuild
  - 对文件的目录结构有要求

- features
  - hexo generate的产物是多页app，而不是spa
  - Support for GitHub Flavored Markdown and most Octopress plugins
  - Powerful API for limitless extensibility
  - one command to deploy your site to GitHub Pages, Heroku or other platforms

- who is using #hexo
  - ?

- alternatives
  - hugo, jekyll
  - gitbook, mdBook-rust
  - vuepress, docusaurus, rspress, docsify

- tips
  - 用hexo作为ssg生成重展示型的网站，可替代部分cms
  - ❓ 默认ssr
# dev-xp
- ❓ hexo server能正常查看，但hexo build的产物index.html只有部分css，没有html内容
  - 肯能是版本太旧?
# more
