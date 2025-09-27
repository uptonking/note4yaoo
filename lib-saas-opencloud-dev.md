---
title: lib-saas-opencloud-dev
tags: [cloud-drive, opencloud]
created: 2025-09-22T12:32:19.215Z
modified: 2025-09-22T12:32:49.473Z
---

# lib-saas-opencloud-dev

# guide

- pros
  - license: 
  - ⏳ File Versioning & Recovery: Roll back to previous file versions, trash bin
  - 🔌 Extension System: Add new features and third-party integrations.
  - Privacy-First Design: Zero-Knowledge principle ensures admins can't access user content.
  - Secure & Flexible File Sharing with granular roles, expiration dates, and password
  - On-Premise: Fully self-hosted deployment for maximum control.
  - Built-in File Preview

- cons
  - 未实现文件树
  - 在mac上进行源码开发不顺利

- features
  - Seamless File Synchronization: Access your files across all devices
    - Works on Windows, Mac, Linux, Android (soon), iOS (soon), and Web.
  - Spaces - Collaborative Team Folders: Ensure continuity even if team members leave
  - Real-Time Collaboration: Work on documents simultaneously with Collabora Web Office.
  - Use full-text search, tags, and filters for quick access.
  - Unlimited Storage & Uploads: No file size restrictions.

- who is using #opencloud
  - ?
# draft
- storage使用本地minio失败, 异常是 
  - http service dataprovider could not be started, : S3 configuration incomplete
  - reva server error

- 使用本地文件系统时，不支持collab mode, 异常是 
  - grpc service storageprovider could not be started, 
  - error: not supported: inotify watcher is not supported on this platform

- 💡 ideas
  - 一种产品设计思路, ai聊天作为一种文件保存在网盘，聊天列表使用一种特殊视图
# dev-xp

# devops
- build from srouce
  - default storage folder: ~/.opencloud/storage/users/users

```sh
make clean generate-dev

make -C opencloud build-debug

# ./opencloud/bin/opencloud-debug server

dotenvx run -- ./opencloud/bin/opencloud-debug server

```

```sh
# use local minio
minio server ~/Documents/runappdata/minioopencloud

# mc alias set <ALIAS> <YOUR-S3-ENDPOINT> <YOUR-ACCESS-KEY> <YOUR-SECRET-KEY> 
mc alias set opencloud http://localhost:9000 minioadmin minioadmin
```

- open https://localhost:9200/
  - 注意本地打开的地址必须是 `https://` 开头, 否则无法打开
  - user: admin
  - password: admin

- [[HOW-TO] Install Bare-metal opencloud version (without compilation)  _202506](https://github.com/orgs/opencloud-eu/discussions/1016)

- [External OpenID Connect Identity Provider | OpenCloud Docs](https://docs.opencloud.eu/docs/admin/configuration/authentication-and-user-management/external-idp/)
  - [Getting OpenCloud to work with External SSO/OIDC (Authentik) · opencloud-eu _202505](https://github.com/orgs/opencloud-eu/discussions/835)
  - 🌰 [[HOW-TO] Setup SSO (OIDC) with Authentik (web, desktop app, iOS app) ](https://github.com/orgs/opencloud-eu/discussions/1014)
# more
