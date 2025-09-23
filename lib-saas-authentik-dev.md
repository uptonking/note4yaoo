---
title: lib-saas-authentik-dev
tags: [auth, authentik]
created: 2025-09-23T13:06:53.251Z
modified: 2025-09-23T13:07:14.156Z
---

# lib-saas-authentik-dev

# guide

- pros
  - ?

- cons
  - ?

- features
  - Read Replicas: You can configure additional read replica databases to distribute database load and improve performance.

- pros
  - ?
# draft
- authentic + lasuite-docs?

- ❓ how to register user on custom webapp?
# dev-xp
- authentik + gitea
  - gitea退出登陆后，无法切换用户登录，会以刚才的用户自动登录

- authentik + outline
  - outline退出后能跳转到authentik账户提示页，可以切换用户
# devops
- [Full development environment](https://docs.goauthentik.io/developer-docs/setup/full-dev-environment/)
-[Configuration | authentik](https://docs.goauthentik.io/install-config/configuration/)

```shell
# Install the required native dependencies 
brew install  libxmlsec1 libpq krb5 pkg-config  golangci-lint

make node-install
make core-install

# uv run scripts/generate_config.py
make gen-dev-config

# -- createdb testdb, createdb is a command line utility
CREATE DATABASE authentik;

make migrate
# Generate the required schema files and TypeScript client
make gen

make web-watch

go mod download

make run-server
make run-worker
```

# codebase

# more

- [immich SSO with Authentik - DEV Community _202404](https://dev.to/rzumbado/immich-sso-with-authentik-2gi9)
  - a quick tutorial to help setting up immich single sign on (SSO) with authentik.
  - for this tutorial I will only focus on integrating them both for your convenience AFTER they are up and running.
  - https://github.com/rzumbado/immich-authentik-sample

- [Authentik 教程系列：简介和安装配置 - ECWU's Notebook](https://ecwuuuuu.com/post/authentik-tutorial-1-introduction-and-install/)
  - 当我们这些自部署的服务越来越多，去访问每一个服务都需要单独的账号和密码；如果用户不止你一人，多账号管理也会成为一个麻烦的事情。
  - 一种可行的方案是部署一个统一登录服务（SSO）。我们可以将部署的各种应用进行接入。那么当用户需要使用时，不再是在应用内进行登录，而是会被跳转到这个统一登录服务中，进行登录和鉴权
  - 通过这个统一登陆服务，你就可以实现一个账号访问所有接入的应用。而且也可以很方便的去管理或者创建新的用户，去控制每一个用户具体的权限。
  - [Authentik 视频教程 - 合集 _202408](https://ecwuuuuu.com/post/authentik-tutorial-video/)

- [authentik: Authentication, SSO, User Management & Password Reset for Home Networks](https://helgeklein.com/blog/authentik-authentication-sso-user-management-password-reset-for-home-networks/)
