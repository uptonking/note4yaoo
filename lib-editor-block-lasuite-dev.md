---
title: lib-editor-block-lasuite-dev
tags: [block-editor, lasuite-docs, notion-like]
created: 2025-07-17T14:38:58.722Z
modified: 2025-07-17T14:39:41.606Z
---

# lib-editor-block-lasuite-dev

# guide
- pros
  - license: MIT
  - collab by yjs is optional, 支持文档分享
  - version-history
  - subpage/sub-doc, 支持多层嵌套的subpage，折叠交互待优化
  - self-hostable 私有化部署方便，提供了docker/k8s等多种方式，还提供了很多环境变量可配置
  - export pdf/docx
  - 提供了 业务系统 与 帐户系统 基于OIDC实现SSO单点登录的示例
  - 支持ai能力，支持llama

- cons
  - 不支持个人所有文件的 FileTree, 可通过 subpage 缓解
  - database/table
  - editor
  - collab
  - 文件不支持添加tag
  - ~~本地开发的环境配置过于复杂~~ 

- features
  - 文档名在编辑器内容外，方便在名称和内容之间插入其他内容
  - pin docs
  - doc-toc
  - 产品设计未采用多tab

- editor-pros 🌹
  - slash-menu /
  - toggle list
- editor-cons 🐛
  - 编辑器标题按enter回车键时光标不会自动进入内容区
# draft
- 如何区分 自己的内容 和 外部的内容

- roadmap
  - prosemirror-multi-column: MIT plugin
  - export pdf/docx: MIT approach
  - lasuite-desktop, 使用类似colanode的架构实现pc版 ❓
    - pc版的架构还是vscode更合适，具备diff/timeline/fileTree/web等强大功能
  - open-chat for lasuite
  - doc-api-for-ai, 参考notion的实现方式
  - 参考切换chat的ux和逻辑，来优化切换docs的体验

- docs-editor  + image-gen
  - comfyui: text-to-image
  - svg图片

- ✅ 完全本地部署的架构

- 分析数据库的结构，文件编辑操作的结构

- collab的op、光标
  - websocket水平扩展时是否采用粘性会话

- search如何实现

- 文档分享的数据流

- ai-features
  - 实现方式是浮动工具条的下拉菜单
  - summarize, rephrase, beautify

- auth
  - ❓ 用authentik替换keycloak碰到问题, 打开nginx默认首页http://localhost:8083/会显示authentik主页, 但此时api请求为http://localhost/api/v3/core/users/me/, 而不是正常的 http://localhost:9000/api/v3/core/users/me/
  - 使用better-auth实现邮箱密码登录
  - 使用简化版的oidc替代keycloak
  - 🤔 使用django-auth代替keycloak
  - 接入更多登录

- 
- 
- 

- issues-maybe
  - ~~不同的浏览器打开时，存在数据不一致的情况~~ 

- codebased
  - version-history的原理: 基于s3 bucket 的versioning 实现

## ai-to 👾

- ai-edit
  - 采用全文替换，还是片段替换
  - 针对长文编辑的优化，还有考虑llm模型厂商的限制

- ai编辑文档考虑使用 fast-apply 的模型方案

- 参考markdown流式输出的方案实现文档的流式输出

- 
- 

# dev-xp
- 分析文档内容数据持久化在哪里了，`impress_document` 这张表似乎没有具体内容
  - 文档内容都存储在s3里

- 用户正常编辑文档时，没有http请求来持久化文档，而通过websocket通道`/collab/ws`来更新光标文档信息

- sharing-doc
  - share doc时，sub-doc 也会自动分享出去

## editor-dev

- 编辑器内图片url默认只有登录用户能访问，未登录用户不能访问
  - http://localhost:8083/media/2e7c9a29-06e5-4b4c-b9f8-7a9617db7d71/attachments/918abdac-b9f9-4d8b-b7f4-27e72808c954.png

## config-lasuite

- 登录失效的默认时间为
# bugs
- drag
  - 拖拽开始时，必须要停顿一下留出时间来显示原位置的拖拽指示线，否则会拖拽失败

- collab
  - 协作时，drag调整顺序会失效
  - 切换doc再切回来时，协作者光标的颜色会变化
# more

# lasuite-documentation
- [La Suite Docs – System & Requirements](https://github.com/suitenumerique/docs/blob/main/docs/system-requirements.md)
  - RAM – start at 8 GB dev / 16 GB staging / 32 GB prod. Postgres and Keycloak are the first to OOM; scale them first.
  - Frontend: Uses pre-built Next.js static assets served by Nginx (no Node.js runtime needed)
  - Object Storage: External services (S3, Azure Blob) or self-hosted solutions (MinIO) are both viable
  - Scaling: Horizontal scaling is recommended for Django API and Y-Provider services
