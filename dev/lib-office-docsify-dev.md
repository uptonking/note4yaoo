---
title: lib-office-docsify-dev
tags: [docsify, lib, office]
created: 2020-12-16T11:17:26.623Z
modified: 2020-12-16T11:18:30.262Z
---

# lib-office-docsify-dev

- A magical documentation site generator.

# guide

- features
  - No statically built html files
  - Support SSR
  - Support embedded files
  - Smart full-text search plugin
  - Useful plugin API
  - Multiple themes

- usecase
  - md文档
  - libs

- who is using
  - https://shoelace.style/
  - https://imdone.io/docs/

- examples

- tips

# pieces

- docsify依赖marked、prismjs

# docs

- 不同于 GitBook、Hexo 的地方是它不会生成静态的 .html 文件，所有转换工作都是在运行时。
  - 无需构建，写完文档直接发布

- 全文搜索插件
  - 会根据当前页面上的超链接获取文档内容，在localStorage内建立文档索引。
  - 默认过期时间为一天
- 评论插件
  - Disqus、Gitalk

- 服务端渲染（SSR）
  - 你可以直接在你的 Node 服务器上执行 docsify start 
  - docsify start 其实是依赖了 docsify-server-renderer 模块，你完全可以用它自己实现一个 server，可以加入缓存等功能
