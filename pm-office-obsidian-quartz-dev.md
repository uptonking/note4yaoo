---
title: pm-office-obsidian-quartz-dev
tags: [obsidian, quartz, static-site-generator]
created: 2026-07-12T14:28:42.034Z
modified: 2026-07-12T14:41:02.051Z
---

# pm-office-obsidian-quartz-dev

> static-site generator that transforms Markdown content into fully functional websites. 

# guide
- pros
  - 支持 wikilinks/backlinks
  - 支持 bases
  - 支持 graph view
  - 支持 mermaid
  - 支持 plugins
  - Parallel processing — markdown parsing uses a worker pool across all CPU cores
  - Incremental rebuilds — watch mode only re-processes changed files

- cons
  - installed by git, not cli, 安装繁琐， 升级容易产生冲突
  - 不支持ssr, 支持spa/mpa
  - 偏重静态展示，bases动态操作数据的功能太弱
  - 虽然自身ui支持i18n, 但似乎不支持多语言版本的文档
  - 需要用户symlink/copy内容， 改变用户的习惯， 设计成用户无感更好
  - plugins installed via `git`

- features
  - bases formula计算的列能正常渲染

- 对bases的支持度很低
  - 页面内的properties默认不渲染
  - table/card/list 显示都是只读的，不能再次filter/sort
  - inline bases交互差
  - embed .base 文件有时未渲染， 因为相对路径解析失败了
  - bases的空内容渲染为 - 而不是空白, 很多cell的内容丢失了
  - table的group ux很糟糕
  - 会丢失sort排序， 但少数排序也可以正确展示
  - image(property) 不能正确显示图片

- links
  - 部分 wikilink 404， 因为相对路径解析失败了， 似乎只能解析同级文件夹下的

- editing/updating
  - page-render 默认是只读的mpa/spa
  - file > db 监控本地文件变化，然后更新db和pages
  - db > file 简单的编辑实现可考虑每次全量更新文件到db并导出本地
  - 如何 将cms的db设计 和 ssg的ux 结合
  - cli启动时，从db读取列表和内容， 编辑时更新db并更新本地文件， 本地文件更新时
# draft
- remote data source
  - docusaurus给出的方案是将加载内容放在 beforeLoadContent
  - [nextra remote](https://nextra.site/docs/advanced/remote) 
    - 直接在page组建内 await fetch
# dev-xp
- remote data source
- docusaurus给出的方案 [Extend existing content plugins (CMS integration, middleware, doc gen...) _202102](https://github.com/facebook/docusaurus/issues/4138)
    - You probably mean using Docusaurus as the UI of a headless CMS. It's nice to see work being done integrating Docusaurus with WordPress or any other CMS, afaik it's not something many have done so far.
    - What I understand is that your plugin downloads the files as MDX, writes then to the disc, and they are expected to be found by the official blog plugin. So basically the blog plugin would somehow need to wait for the completion of your plugin's loadContent
    - I don't think it's a good idea to introduce this plugin ordering logic. We really want plugins to work in isolation and not interfere with each other. This ordering logic is also something that was often requested on Gatsby and they pushed hard against implementing it.
    - My suggestion to this problem is that you should not actually write a new Docusaurus plugin for this, but instead enhance the existing blog plugin. If we created a blog plugin async beforeLoadContent() option, you would be able to write the MDX files here instead of trying to orchestrate a more complex workflow using multiple plugins.
    - here's a runnable example of extending the blog plugin to expose extra global data
# more

# roadmap

# changelog
- Quartz 5 is a ground-up rearchitecture of Quartz focused on extensibility, performance, and Obsidian compatibility.
  - The biggest change in v5 is the move to a community plugin ecosystem. 
    - Most plugins that were built into Quartz 4 are now standalone community plugins 
    - Plugins are now standalone packages maintained in the quartz-community GitHub organization and installed via `git`.
    - community plugins ship compiled dist/ directories, skipping build-from-source on install
  - Configuration moved from TypeScript (quartz.config.ts) to YAML (quartz.config.yaml)
  - The layout system is now declarative. 
    - Plugins declare their position (left, right, beforeBody, afterBody) and priority in the config
    - each plugin declares its own position and priority
  - Quartz 5 aims for full compatibility with Obsidian’s core features: Wikilinks, Callouts, Mermaid, Canvas
  - Quartz 5 introduces page types — plugins that define how different kinds of pages are rendered: Content, Folder, Tag, Bases, Canvas
  - Parallel processing — markdown parsing uses a worker pool across all CPU cores
  - Incremental rebuilds — watch mode only re-processes changed files
  - SPA routing — client-side navigation with micromorph for instant page transitions
