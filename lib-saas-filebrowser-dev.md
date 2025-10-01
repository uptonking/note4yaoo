---
title: lib-saas-filebrowser-dev
tags: [cloud-drive, filebrowser]
created: 2025-09-30T08:57:29.693Z
modified: 2025-09-30T08:58:01.051Z
---

# lib-saas-filebrowser-dev

# guide
- pros
  - license: apache
  - Multiple sources support
  - Login support for OIDC, password + 2FA, and proxy
  - Directory-level access control that can be scoped to user or group
  - 存储层支持文件系统
  - rich media preview

- cons
  - 存储层不支持 S3/webdav/FTP
  - 未实现客户端本地文件夹和服务端文件夹的同步, 采用的是服务端为数据源而客户端仅查看的方案
  - 不支持预览markdown

- features
  - Multiple users
  - Single sign-on support
  - 在ui上操作文件会将操作同步到文件系统
  - Ultra-efficient indexing and real-time updates
    - Every file and directory in the source gets indexed (by default). This enables powerful features such as instant search,
  - Developer API support with long-lived API Tokens
  - 系统数据默认使用 ~~sqlite~~

- tips
  - ?
# draft

# devops

- api-swagger需登录查看: http://localhost:9200/swagger/doc.json

```sh
make setup
make dev
```

- 开发时默认使用的配置是 `test_config.yaml`, 而不是 `config.yaml`.
# dev-xp

- 
- 
- 

# more
