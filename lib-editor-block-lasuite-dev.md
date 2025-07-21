---
title: lib-editor-block-lasuite-dev
tags: [block-editor, lasuite-docs, notion-like]
created: 2025-07-17T14:38:58.722Z
modified: 2025-07-17T14:39:41.606Z
---

# lib-editor-block-lasuite-dev

# guide
- pros
  - version-history
  - collab
  - subpage/subdoc

- cons
  - 不支持 FileTree
  - 本地开发的环境配置过于复杂
  - 编辑器标题按enter回车键时光标不会自动进入内容区

- features
  - pin docs
  - doc-toc

- editor
  - slash-menu /
# draft
- 完全本地部署的架构

- 分析数据库的结构，文件编辑操作的结构

- 
- 
- 

- code-to ❓
  - 不同的浏览器打开时，存在数据不一致的情况

- 测试协作的op、光标

- 使用类似colanode的架构实现pc版

- 使用简化版的oidc替代keycloak
  - 接入更多登录

## ai-to

- ai编辑文档考虑使用 fast-apply 的模型方案
# dev-xp
- 分析文章内容数据持久化在哪里了，impress_document 这张表似乎没有具体内容
  - 内容都存储在s3里
# more

# lasuite-documentation
- [La Suite Docs – System & Requirements](https://github.com/suitenumerique/docs/blob/main/docs/system-requirements.md)
  - RAM – start at 8 GB dev / 16 GB staging / 32 GB prod. Postgres and Keycloak are the first to OOM; scale them first.
  - Frontend: Uses pre-built Next.js static assets served by Nginx (no Node.js runtime needed)
  - Object Storage: External services (S3, Azure Blob) or self-hosted solutions (MinIO) are both viable
  - Scaling: Horizontal scaling is recommended for Django API and Y-Provider services
