---
title: lib-saas-overleaf-dev
tags: [latex, overleaf]
created: 2024-10-19T09:25:56.391Z
modified: 2024-10-19T09:26:35.210Z
---

# lib-saas-overleaf-dev

> A web-based collaborative LaTeX editor

# guide
- pros
  - 支持多种视图source/wysiwyg, 都基于codemirror实现

- cons 
  - license: AGPLv3
  - 支持ha/scaling的server pro需付费

- features
  - ?

- 依赖compile的系统实现参考
  - jupyter依赖kernel编译python/其他语言
  - overleaf依赖textlive编译latex
  - 网易tango低代码平台会先将用户搭建产生的react组件编译为ast再基于codesandbox在前端运行
# draft

# dev-xp

# changelog

## v5_2024-04-02

- Required database upgrade from MongoDB 4 to MongoDB 5
- Rebranding of filesystem paths from ShareLaTeX brand to Overleaf brand
- Rebranding of SHARELATEX_* to OVERLEAF_* environment variables

- Added support for using IAM credentials when using AWS S3 for project/history files

## v4_2023-05-30

- 📝 A new Source editor in addition to the Legacy editor will be available to users. 
  - The new Source editor provides better accessibility, and better support for non-latin text.
- Deleted projects and users can be automatically cleaned up after 90 days.
- MongoDB now needs to run as a Replica Set. 
- TeXLive 2023 is now the default version for instances not running Sandboxed Compiles.

- pro
  - Overleaf Git integration 
  - [Enhanced Rich Text functionality – Rich-text commenting and tracked changes. _202302](https://www.overleaf.com/blog/the-updated-rich-text-editor-simplifies-team-collaboration)
  - Support documentation for horizontal scaling, which allows for increased computing resources for large deployments

## v3_2021-10-05

- Symbol Palette
- This release requires updating Mongo version to 4.2
- TexLive 2021 is available for instances running Sandboxed Compiles.

## v2_2019-10-09

- A lot has changed in the last few years, with ShareLaTeX joining forces with Overleaf to create one incredible authoring platform. Now that the merge is complete it's time to release a new version of ShareLaTeX Overleaf Community Edition and Server Pro!

- A brand new user interface theme
- A new interface for creating (or uploading) files in a project
- Linked Files: import a file from another project.

- pro
  - Rich Text mode: write your document like a rich-text document, backed by nice clean LaTeX

- We've made some changes to the way the Sanboxed Compiles work. 
  - In previous versions, the administrators often needed to fiddle with user and group permissions on the docker socket to get Sibling Containers to work. 
  - In this release, we've changed all that so it's handled automatically inside the Server Pro container, so it should just work in the majority of cases.
  - From this release onwards we will no longer support the old "Docker-In-Docker" method of sandboxed compiles, as it has become more and more difficult to get this to work as time goes on. We strongly encourage admins to consider the newer Sibling Containers method as an alternative.

- You can now opt-in to a new version of TeX Live. The default is still TeX Live 2017, but you can find instructions on how to get TeX Live 2018 or later 

## v1_2018

- pro
  - Per-User Track Changes
  - Improved Autocomplete
  - Improved Spellcheck
  - A new auto-compile option, keep the pdf view in sync while you type
  - Use both 2016 and 2017 versions of texlive, for backward compatibility
# more
