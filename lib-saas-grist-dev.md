---
title: lib-saas-grist-dev
tags: [excel, grist, pivot-table]
created: 2024-02-04T20:53:54.264Z
modified: 2024-02-04T20:54:21.002Z
---

# lib-saas-grist-dev

# guide
- pros
  - license: apache2
  - 支持2种embed模式(readonly/edit), 还可以使用grist-static嵌入无后端的静态版

- cons
  - 不支持已有数据库，需要import data

- features
  - Python formulas
  - portable, self-contained format, based on SQLite
  - Can be displayed on a static website with grist-static – no special server needed.
  - Drag-and-drop dashboards
  - Access control options
  - Sandboxing options for untrusted documents
# draft
- roadmap
  - react frontend
# dev

# devops

- env

```sh
yarn install
yarn run build
yarn run install:python

# yarn start
dotenvx run -- yarn start
```

- webapp: http://localhost:8484
# codebase
- 用户在界面上创建表T1时，server会在主数据库会添加数据元信息记录，表T1的实际数据在本地`grist-core/docs`文件夹，用户创建的每个document对应一个sqlite格式的`.grist`文件，用户创建的每张表对应.grist数据库中的一张表，.grist数据库中还包含视图、权限、action等业务数据和元数据
# more
- [Questions about self-hosted grist and authentik with OIDC - Ask for Help - Grist Creators _202406](https://community.getgrist.com/t/questions-about-self-hosted-grist-and-authentik-with-oidc/5250)
  - [SAML configuration unclear (documentation update needed) · Issue · gristlabs/grist-core _202202](https://github.com/gristlabs/grist-core/issues/135)
