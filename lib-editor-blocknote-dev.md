---
title: lib-editor-blocknote-dev
tags: [block-editor, blocknote, notion-like, prosemirror, tiptap-editor]
created: 2022-10-21T21:01:26.654Z
modified: 2023-02-05T19:03:27.729Z
---

# lib-editor-blocknote-dev

# guide

- pros-BlockNote

- cons-BlockNote

- pros-SuiteDocs
  - version-history
  - collab

- cons-SuiteDocs
  - 本地开发的环境配置过于复杂
  - 编辑器标题按enter回车键时光标不会自动进入内容区
# draft

# dev-xp

# more

# suite-docs

- features
  - pin docs
  - doc-toc

- editor
  - slash-menu /
# suite-docs-draft
- ❓
  - 分析文章内容数据持久化在哪里了，impress_document 这张表似乎没有具体内容
  - 不同的浏览器打开时，存在数据不一致的情况

- 使用简化版的oidc替代keycloak
# suite-docs-dev-xp

# suite-docs-codebase
- urls
  - webapp http://localhost:3000/
  - admin http://localhost:8071/admin
    - user: admin@example.com ,  pass: admin
# suite-docs-documentation

- [La Suite Docs – System & Requirements](https://github.com/suitenumerique/docs/blob/main/docs/system-requirements.md)
  - RAM – start at 8 GB dev / 16 GB staging / 32 GB prod. Postgres and Keycloak are the first to OOM; scale them first.
  - Frontend: Uses pre-built Next.js static assets served by Nginx (no Node.js runtime needed)
  - Object Storage: External services (S3, Azure Blob) or self-hosted solutions (MinIO) are both viable
  - Scaling: Horizontal scaling is recommended for Django API and Y-Provider services
# more-suite-docs
